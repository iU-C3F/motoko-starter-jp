# Chapter 8: Advanced Types.　/ 第8章：高度な型
## ❓ Optional types / Optional 型
In Motoko, as in many other programming languages, there is a special value called `null` used to represent the absence of a result. This is helpful when indicating that a function returns nothing. The value `null` is of type `Null`, which only contains one value: `null`.  
Motoko では、他の多くのプログラミング言語と同様に、結果がないことを表すために`null`と呼ばれる特別な値が存在します。これは、関数が何も返さないことを示すときに便利です。値 `null` は `Null` 型であり、`null` という１つの値のみを含みます。

Consider an array of names called `names` and a function called `find_name` that takes a list of names as input and returns the index of the first occurrence of the name in the array. If the name is not found, the function should return `null` instead of an index. This way, the function indicates that it did not find the name without producing an error.  
`names`という名前の配列と、名前のリストを入力として受け取り、配列の中で名前が最初に出現するインデックスを返す `find_name` という関数があるとします。名前が見つからなかった場合、この関数はインデックスの代わりに `null` を返さなければなりません。このようにすると、関数はエラーを出さずに名前が見つからなかったことを示します。

The following code is not valid in Motoko:  
以下のコードは、Motoko では無効です：
```motoko
let names : [Text] = ["Motoko", "Rust", "JavaScript", "TypeScript"];
public func find_name(name : Text) : async Nat {
    var index : Nat = 0;
    for(language in names.vals()){
        if (language == name){
            return index;
        };
        index +=1;
    };
    return null; // We haven't found any match so we return null. / 一致するものが見つからなかったので、null を返します。
};
````
Motoko throws an error because `null` is not of type `Nat`. To indicate that a function may return either a `Nat` value or `null`, we need a way to express that the function's return type can be one of two possibilities. The specific return value of the function depends on the input, which is unknown in advance, so we cannot predict if the function will return a `Nat` or `null` until it is executed.  
Motoko は `null` が `Nat` 型でないため、エラーを投げます。関数が `Nat` 値か `null` のどちらかを返す可能性があることを示すには、関数の戻り値の型が２つの可能性のどちらかであることを表現する方法が必要です。関数の具体的な戻り値は入力に依存し，それは事前に分からないので，関数が `Nat` を返すか `null` を返すかは実行されるまで予測できません。

We can use an optional type, `?T`, to express this. In our case, we would use `?Nat`. We can rewrite our code using this notation:  
これを表現するために、Optional 型である `?T` を使用できます。私たちの場合は、`?Nat`を使用します。この記法でコードを書き直すことができます：
```motoko
let names : [Text] = ["Motoko", "Rust", "JavaScript", "TypeScript"];
public func find_name(name : Text) : async ?Nat {
    var index : Nat = 0;
    for(language in names.vals()){
        if (language == name){
            return ?index;
        };
        index +=1;
    };
    return null; // We haven't found any match so we return null. / 一致するものが見つからなかったので、null を返します。
};
```

The optional type, indicated by `?`, can be used with any other type, such as `?Text`, `?Int`, `?Bool`, and more.  
`?` で示されるオプション型は、`?Text`、`?Int`、`?Bool`など、他のどの型でも使えます。

Also, the optional type is often used with the `switch/case` pattern in Motoko. This pattern allows you to handle an optional value and execute different parts of your code depending on whether the input value is `null` or not. You can use the `switch/case` pattern to check if an optional value is present and perform different actions based on that, resulting in more elegant and safer code.  
また、optional 型は Motoko の `switch/case` パターンと一緒に使われることが多いです。このパターンでは、オプショナル値を扱い、入力値が `null` かどうかに応じてコードの異なる部分を実行できます。`switch/case` パターンを使って optional 値が存在するかどうかをチェックし、それに基づいて異なるアクションを実行することで、よりエレガントで安全なコードを実現できます。
```motoko
public func handle_null_value(n : ?Nat) : async Text {
    switch(n) {
        // Check if n is null 
        case(null){
            return ("The argument is null"); 
        };
        case(? something){
            return ("The argument is : " # Nat.toText(something));
        };
    };
};
```
Lastly, the Base library provides an **Option** module for operating on optional values. For example, you can use the `Option.get()` function to unwrap an optional value with a default value:  
最後に、Base ライブラリは、optional 値を操作するための **Option** モジュールを提供します。例えば、`Option.get()` 関数を使って、デフォルト値を持つオプショナル値をアンラップできます：
```motoko
import Option "mo:base/Option";
actor {
    public func always_return_a_nat(n : ?Nat) : async Nat {
        return(Option.get(n, 0))
    };
}
```
This function takes a `?Nat` as input and returns a `Nat`. If you provide a `Nat` as input, it will return the same value. However, if you provide `null`, it will return the default value, set to 0.  
この関数は `?Nat` を入力として受け取り、`Nat` を返す。入力として `Nat` を指定した場合は、同じ値を返します。しかし、`null`を入力した場合は、デフォルトの値である 0 を返します。
## 👤 Generic Type / Generic 型
A generic type, usually written as `T`, allows you to write functions and code that can adapt to different types. When we talk about `T`, it refers to **whatever type you want**. This means that you can create a single function or class that can handle multiple types of inputs or data, without having to write separate code for each type.  
通常 `T` と書かれる generic 型は、異なる型に適応できる関数やコードを書くことを可能にします。`T` について話すとき、それは **あなたが望むどんな型でも** を指します。つまり、それぞれの型に対して別々のコードを書かなくても、複数の入力やデータを扱える関数やクラスを１つ作ることができます。

Let's imagine that we have a task at hand - to determine if the size of an array is even or not. We're going to write a function called `isArrayEven` that takes an array as an input and returns a `Bool` value indicating whether the size of that array is even or not.  
ある配列のサイズが偶数かどうかを判断する、というタスクがあるとします。ここでは、配列を入力として受け取り、その配列のサイズが偶数かどうかを示す `Bool` 値を返す `isArrayEven` という関数を作成することにします。
```motoko
public func isArrayEven(array : [Nat]) : async Bool {
    let size = array.size();
    if(size % 2 == 0){
        return true;
    } else {
        return false;
    };
};
```
This function works as intended, but is limited to arrays filled with `Nat`. So, what if we want to check the size of an array filled with `Text` or `Int`?  
この関数は意図したとおりに動作しますが、`Nat`で埋められた配列に限定されます。では、`Text`や`Int`で埋められた配列のサイズを確認したい場合はどうすればよいでしょうか。<br>
One approach would be to create a separate function for each possible type:  
一つの方法として、可能性のあるタイプごとに別の関数を作成することが考えられます：
- `isArrayEvenNat`
- `isArrayEvenText`
- `isArrayEvenInt` 

As you can imagine, this quickly becomes hard to manage and maintain. A better solution is to utilize the power of generics. With generics, we can write a single function that works for any type of array. It's a more elegant and efficient way to solve the problem. So, let's embrace our new friend - generics - and make our code more dynamic and flexible!  
想像できるように、これはすぐに管理と維持が難しくなります。そこで、generics　の力を活用するのがよいでしょう。generics を使えば、どんなタイプの配列にも対応する関数を１つ書くことができます。これは、よりエレガントで効率的な問題解決方法です。それでは、新しい友人である generics を受け入れて、コードをよりダイナミックで柔軟なものにしましょう！
```motoko
func isArrayEven<T>(array : [T]) : Bool {
    let size = array.size();
    if(size % 2 == 0){
        return true;
    } else {
        return false;
    };
};
```
Notice `<T>` following the name of the function. It means that this function now depends on the type of `T`. We need to specify the type of `T` when we want to use the function.  
関数名の後に続く `<T>` に注目してください。これは、この関数が `T` の型に依存することを意味しています。この関数を使用する際には、`T` の型を指定する必要があります。
```motoko
let array : [Nat] = [1,2,3,4];
let bool : Boolean = isArrayEvent<Nat>(array); // Replace T with the actual type when you use the function. 
```

We've  already used generics when playing with `Buffer` & `Array` without talking about it.  
私たちはすでに `Buffer` と `Array` を扱うときに generics を話題にすることなく使用しています。
- The type `Buffer<T>` is a generic class and we need to provide a type when creating a new buffer.
- `Buffer<T>` 型は generics クラスであり、新規にバッファを作成する際には型を指定する必要があります。
    ```motoko
    let b = Buffer.Buffer<Nat>(2);
    ```

- `Array.append<T>` is a generic function and we need to provide the type of the elements of the arrays we are concatening.
- `Array.append<T>` は generics 関数であり、連結する配列の要素の型を指定する必要があります。
    ```motoko
    let array1 = [1, 2, 3];
    let array2 = [4, 5, 6];
    Array.append<Nat>(array1, array2) // [1, 2, 3, 4, 5, 6];
    ```
## 🤫 Shared types / Shared 型
When information is sent to or received from an `actor` in Motoko, it uses specific data types called **shared types**. These **shared types** are used in `public` functions that can be accessed by other actors. So, **shared types** are the kinds of data that can be used as input or output for these public functions, allowing different actors to communicate with each other.  
Motoko の `actor` に情報を送ったり受け取ったりするとき、**shared 型** と呼ばれる特定のデータ型が使われます。この **shared 型** は、他の actor がアクセスできる`public` 関数で使用されます。つまり、**shared 型** は、これらの public 関数の入力または出力として使用できるデータの種類であり、異なるアクターが互いに通信することを可能にします。<br/>

If we try to deploy [the following actor](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=2185064550):  
[下記の actor](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=2185064550) を配置しようとすると:
```motoko
actor {
  var mutableArray : [var Nat] = [var 1, 3, 5, 7]; 

  public func showArray() : async [var Nat] {
    return mutableArray
  };
}
```
We will encounter the following error: `Error in file Main.mo:3:28 shared function has non-shared return type [var Nat] type [var Nat] is or contains non-shared type var Nat`.  
次のエラーが発生します： `Error in file Main.mo:3:28 shared function has non-shared return type [var Nat] type [var Nat] is or contains non-shared type var Nat`.

A very important rule to remember: **every mutable state is always private to an actor.**  
覚えておくべき非常に重要なルールです： **ミュータブルなステートは、常に actor の private なステートです。**

To put it short - anything that you can modify in your the state of your canister should be consider private and you won't be able to share it with other actors.  
簡単に言うと、キャニスターのステートを変更できるものはすべてプライベートなものと考え、他のアクターと共有することはできません。<br/>

<p align="center"> <img src="./assets/mutable_state_actor.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> If it's a var your can't share it outside!</p>
<p align="center">var の場合、外で共有することはできません！</p>

> For a complete overview of all the shared types, [refer to the Motoko Book](https://web3.motoko-book.dev/internet-computer-programming-concepts/async-data/shared-types.html?highlight=Shared%20types#shared-types).

> 全 shared 型の概要については、[Motoko Book](https://web3.motoko-book.dev/internet-computer-programming-concepts/async-data/shared-types.html?highlight=Shared%20types#shared-types) をご参照ください。

## 🔃 Recursive types / Recursive 型
Read [this section](https://web3.motoko-book.dev/advanced-types/recursive-types.html) of the Motoko Book.  
Motoko Book の [このセクション](https://web3.motoko-book.dev/advanced-types/recursive-types.html) をお読みください。