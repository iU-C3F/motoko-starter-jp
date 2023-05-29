# Chapter 6: Storing data in data structures. / 第6章 データ構造でデータを保存
## 🗃️ Array / 配列
In Motoko, an array of type `Array` is a group of **similar** elements (i.e same type) that are stored together. To create an array, one must specify the types of elements that the array will contain. 
For instance, here is how to create an array that will hold `Nat`.  
Motoko では、`Array`型の配列は、一緒に保存される **類似** 要素（すなわち同じ型）のグループである。配列を作成するには、その配列に含まれる要素の種類を指定する必要があります。
例えば、`Nat`を格納する配列を作成する方法を以下に示します。

```motoko
let ages : [Nat] = [16, 32, 25, 8, 89];
```
An array that will hold values of type `Text`.
```motoko
let words : [Text] = ["Motoko", "is", "the", "best", "language"];
```
Contrary to other programming languages which might be more flexible in that regard, in Motoko we can't mix elements of different types in the same array.  
他のプログラミング言語ではもっと柔軟に対応できるかもしれませんが、Motoko では同じ配列の中に異なる型の要素を混在させることはできません。<br/>
The following code will throw an error: `literal of type Text does not have expected type Nat`.  
下記のコードではエラーが発生します：`literal of type Text does not have expected type Nat`。
```motoko
let array : [Nat] = [14, 16, 32, 25, "Motoko"];
```
<p align="center"> <img src="assets/array.png" width="600px" style="border: 2px solid black;"></p>
To access a specific element within an array, we use its index. Keep in mind that arrays in Motoko are zero-indexed, which means that the first element is at position 0, the second element is at position 1, and so on. For example, to access the first element of an array named `myArray`, we would use `myArray[0]`, and to access the second element, we would use `myArray[1]`.

配列の中の特定の要素にアクセスするには、そのインデックスを使用します。Motoko の配列はゼロインデックスであることに留意してください。つまり、最初の要素は 0 番、2 番目の要素は 1 番、といった具合になります。例えば、`myArray` という名前の配列の最初の要素にアクセスするには、`myArray[0]` を使い、2番目の要素にアクセスするには、`myArray[1]` を使うことになるでしょう。
```motoko
let myArray : [Nat] = [23, 16, 32, 25];
let a = myArray[0]  // 23
let b = myArray[3]  // 25
```
We can access the size of an array using the `.size()` method.  
配列のサイズにアクセスするには、`.size()` メソッドを使用します。

```motoko
let names : [Text] = ["Emma Smith", "Olivia Johnson", "Ava Brown", "Isabella Davis"];
let size = names.size();    // 4
```

To loop over an array we can use the `.vals()` iterator. Here is an example that would gave us the sum of an array.  
配列をループするためには、`.vals()` イテレータを使用します。以下は、配列の和を求める例です。
```motoko
actor {
    let array : [Nat] = [1, 2, 3, 4, 5];
    var sum : Nat = 0;

    public func somme_array() : async Nat {
        for (value in array.vals()){
          sum := sum + value;
        };
       return sum; 
    };
};
```

In Motoko, arrays have a fixed size that is determined when the array is created. This means that the size cannot be increased later on. To add a new element to an array, a new array must be created and all of the existing elements must be transferred to the new array manually. This makes `Array` not really adapted for datastructures that needs be constantly updated.  
Motoko では、配列のサイズは作成時に固定で決定されます。つまり、後からサイズを大きくすることはできません。配列に新しい要素を追加するには、新しい配列を作成し、既存の要素をすべて手動で新しい配列に移さなければならない。このため、`Array`は常に更新する必要があるデータ構造にはあまり適していません。

Concatenating two arrays to an `Array` can be done using `Array.append()` - a function from the [Array](https://internetcomputer.org/docs/current/motoko/main/base/Array) module.  
[Array](https://internetcomputer.org/docs/current/motoko/main/base/Array) モジュールの関数である `Array.append()` を使って、2つの配列を1つの `Array` に連結できます。
```motoko
let array1 = [1, 2, 3];
let array2 = [4, 5, 6];
Array.append<Nat>(array1, array2) // [1, 2, 3, 4, 5, 6];
```
However, this function is **depreceated**. It is recommended to avoid it in production code. That's because as we've said before it is impossible to simply add elements to an array. Under the hood, `Array.append()` will create a new array and copy the values of the two existing arrays which is not efficient.  
ただし、この機能は **非推奨** です。本番のコードでは避けることが推奨されます。それは、先に述べたように、配列に要素を単純に追加することは不可能だからです。Array.append()`は、新しい配列を作成し、既存の2つの配列の値をコピーしますが、これは効率的ではありません。

## 🥞 Buffer / バッファー
A more adapted structure to dynamically add new elements is the type `Buffer`. 
A `Buffer` can be instantiated using the [Buffer](https://internetcomputer.org/docs/current/motoko/main/base/Buffer) library. 
One needs to provide the types of elements stored inside and the initial capacity. 
The initial capacity represents the length of the underyling array that backs this list. In most cases, you will not have to worry about the `capacity` since the Buffer will automatically grow or resize the underlying array that holds the elements.

新しい要素を動的に追加するために、より適合した構造は `Buffer` 型です。
`Buffer`は、[Buffer](https://internetcomputer.org/docs/current/motoko/main/base/Buffer) ライブラリを使用してインスタンス化できます。
内部に格納される要素の種類と初期容量を指定する必要があります。
初期容量は、このリストをバックアップする基礎配列の長さを表します。ほとんどの場合、Buffer は自動的に要素を保持する配列のサイズを大きくしたり小さくしたりするので、`容量`を気にする必要はありません。
```motoko
import Buffer "mo:base/Buffer";
actor {
    let b = Buffer.Buffer<Nat>(2);
}
```
In this case, the types of elements in the buffer is `Nat` and the initial capacity of the buffer is `2`.  
この場合，バッファの要素の種類は `Nat` で，バッファの初期容量は `2` となります．

To add an element use the `.add()` method.  
要素を追加するには、`.add()` メソッドを使用します。
```motoko
b.add(0);   // add 0 to buffer / バッファに 0 を追加する
b.add(10);   // add 10 to buffer / バッファに 10 を追加する
b.add(100)    // causes underlying arrray to increase in capacity since the capacity was set to 2 / 容量が 2 に設定されているため、基礎となる配列の容量が増える
```
To get the number of elements in the buffer use the `.size()` method. The `size` is different than the capacity we've mentionned earlier since it represents the number of elements that are actually stored in the buffer.  
バッファ内の要素数を取得するには、`.size()` メソッドを使用します。`size`は、先に述べた容量とは異なり、実際にバッファに格納されている要素の数を表します。
```motoko
let b = Buffer.Buffer<Nat>(2);
b.add(0);   
b.add(10);   
b.add(100);  
b.size();   // 3
```
To access an elements in the buffer, use the `.get()` method and provides the index. Traps if `index` >= `size`. Indexing is zero-based like with `Array`.  
バッファ内の要素にアクセスするには、`.get()`メソッドを使用し、インデックスを指定します。index` >= `size` の場合はトラップする。インデックスは `Array` と同様にゼロベースである。
```motoko
let b = Buffer.Buffer<Nat>(2);
b.add(0);   
b.add(10);   
b.add(100);  
b.get(2);   // 100
```

A buffer can easily be converted to an array using the `toArray()` function from the [Buffer library](https://internetcomputer.org/docs/current/motoko/main/base/Buffer#function-toarray-1).  
Buffer は [Buffer library](https://internetcomputer.org/docs/current/motoko/main/base/Buffer#function-toarray-1) の `toArray()` 関数を用いて簡単に配列に変換できます。
```motoko
let b = Buffer.Buffer<Nat>(2);
b.add(0);   
b.add(10);   
Buffer.toArray<Nat>(b); // [0, 10];
```
## 🔗 List
Purely-functional, singly-linked lists. A list of type List<T> is either null or an optional pair of a value of type T and a tail, itself of type List<T>.  
純粋に機能的な、単一リンクのリスト。List<T> 型のリストは，null か，T 型の値と List<T> 型の末尾のオプションのペアであるかのいずれかです。

[List library](https://internetcomputer.org/docs/current/motoko/main/base/List/)
```motoko
type List<T> = ?(T, List<T>);
```
"The difference between a list and an array is that an array is stored as one contiguous block of bytes in memory and a list is 'scattered' around without the elements having to be adjacent to each other. The advantage is that we can use memory more efficiently by filling the memory more flexibly. The downside is that for operations on the whole list, we have to visit each element one by one which may be computationally expensive."
[source](https://web3.motoko-book.dev/base-library/data-structures/list.html)  
"リスト "と "配列 "の違いは、配列はメモリ上に1つの連続したバイトのブロックとして格納され、リストは要素が隣接していなくても「散在」していることです。利点は、より柔軟にメモリを埋めることで、より効率的にメモリを使用できることです。欠点は、リスト全体に対する操作の場合、各要素を1つずつ訪問しなければならず、計算コストが高くなる可能性があることです。"
[ソース](https://web3.motoko-book.dev/base-library/data-structures/list.html)

Read about Lists and Recursive types [here](https://web3.motoko-book.dev/advanced-types/recursive-types.html).  
リストと再帰型については[こちら](https://web3.motoko-book.dev/advanced-types/recursive-types.html)をご覧ください。

Here is an example of a function that retrieves the last element of a particular list.  
ここでは、あるリストの最後の要素を取得する関数の例を紹介します。
```motoko
func last<T>(l : List<T>) : ?T {
    switch l {
        case null { null };
        case (?(x, null)) { ?x };
        case (?(_, t)) { last<T>(t) };
    };
};
```

## 💿 HashMap & TrieMap
In Motoko, [HashMap](https://internetcomputer.org/docs/current/references/motoko-ref/HashMap) and [TrieMap](https://internetcomputer.org/docs/current/references/motoko-ref/TrieMap) are both implemented as a Class and have the same interface. The only difference is that `TrieMap` is represented internaly by a `Trie` while `HashMap` is using `AssocList`. All examples that will follow use `HashMap` but it would be similar for `TrieMap`.  
Motoko では、[HashMap](https://internetcomputer.org/docs/current/references/motoko-ref/HashMap) と [TrieMap](https://internetcomputer.org/docs/current/references/motoko-ref/TrieMap) は、どちらもClassとして実装されており、同じインターフェイスを持っています。唯一の違いは、`HashMap` が `AssocList` を使っているのに対し、`TrieMap` は内部的に `Trie` で表現されていることです。この後の例では `HashMap` を使用するが、`TrieMap` でも同様です。

- K is the type of the key (`Nat`, `Text`, `Principal`...)
- Kは キーの型（`Nat`, `Text`, `Principal`...）です。
- V is type of the value that will be stored (User data, Token balance...)
- V は保存される値の型（ユーザーデータ、トークン残高...）です。

```motoko
class HashMap<K, V>(initCapacity : Nat, keyEq : (K, K) -> Bool, keyHash : K -> Hash.Hash)
```

To instantiate a value from the class, we need to provide:  
クラスから値をインスタンス化するために、以下を提供する必要があります：
1. An initial capacity of type `Nat`. / `Nat`型の初期容量
    ```motoko
    initCapacity : Nat
    ```
2. A function that can be used for testing equality of the keys. / キーの等質性をテストするために使用できる関数
    ```motoko
    keyEq : (K, K) -> Bool
    ```
3. A function that can be used for hashing the keys. / キーのハッシュ化に使用できる関数
    ```motoko
    keyHash : K -> Hash.Hash
    ```

Let's imagine that we want to store a `Student` associated with his `Principal`. Where `Student` is defined as  
例えば、`Student` をその `Principal` と関連付けて保存したいとします。ここで、`Student`は以下のように定義される。
```motoko
type Student = {
    name : Text;
    age : Nat;
    favoriteLanguage : Text;
    graduate : Bool;
};
```

In that case:  
その場合は
- K is of type `Principal` and represents the key of the HashMap.
- Kは `Principal` 型であり、HashMap のキーを表す。
- V is of type `User` and represents the stored value. 
- V は `User` 型であり、保存された値を表す。（訳注：おそらく誤字。`User` ではなく `Student`）

To initiate our `HashMap`  
`HashMap` を初期化するには
```motoko
import HashMap "mo:base/HashMap";
import Principal "mo:base/Principal";
actor {
    type Student = {
        name : Text;
        age : Nat;
        favoriteLanguage : Text;
        graduate : Bool;
    };

    let map = HashMap.HashMap<Principal, Student>(1, Principal.equal, Principal.hash);
}
```
To add a new entry to the `map` we can use the `.put()` method.  
新しいエントリを `map` に追加するには、`.put()` メソッドを使用できます。
```motoko
map.put(principal, student);
```
This will insert the value `student` with key `principal` and overwrites any previous value. We can use this method to create a `register` function that students would need to call and provide all their relevant informations.  
これにより、キー `principal` を持つ値 `student` が挿入され、以前の値はすべて上書きされます。このメソッドを使用して、学生が呼び出す必要がある `register` 関数を作成し、関連するすべての情報を提供できます。

```motoko
public shared ({ caller }) func register(name : Text, age : Nat, favoriteLanguage : Text) : async () {
    if(Principal.isAnonymous(caller)){
        // We don't want to register the anonymous identity
        return;
    };
    let student : Student = {
        name;
        age;
        favoriteLanguage;
        graduate = false;  
    };
    map.put(caller, student);
};
```

Once a value has been inserted in the `map`, we can access it using the `.get()` method.  
値を `map` に挿入したら、`.get()` メソッドを使ってその値にアクセスすることができます。
```motoko
map.get(principal);
```
This will return an optional value `?Student` associated with the provided principal. We can use this method to create a `getStudent` `query` function that would return information on students.  
これは、指定された校長に関連付けられた optional な値 `?Student` を返します。このメソッドを使用して、生徒の情報を返す `getStudent` `query` 関数を作成できます。
```motoko
public query func getStudent(p : Principal) : async ?Student {
map.get(p);
};
```
We can delete a value from the `map` by using the `.delete()` or `remove()` methods.  
`.delete()` または `remove()` メソッドを使用すると、`map` から値を削除することができます。
```motoko
map.delete(principal);   // Delete but doesn't return the value / 削除はするが、値は返さない
let oldValue = map.remove(principal);   // Delete but returns the value / 削除するが、値を返す
```
It is possible to iterate over the map:  
マップを繰り返し表示することが可能です：
- You can iterate over the keys with `.keys()`.
- .keys()`でキーを反復処理できます。
- You can iterate over the values with `.vals()`.
- .vals()`で値を反復処理できます。
- You can iterate over both with `.entries()`.
- .entries()`を使えば、両方を繰り返し処理できます。
