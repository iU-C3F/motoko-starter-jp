# Chapter 3: Primitive Types in Motoko. / 第3章 Motoko おけるプリミティブ型
Primitive types are fundamental core data types that are not composed of more fundamental types. <br/>

プリミティブ型は、より基本的な型から構成されない基本的なコアデータ型である。<br/>

Primitive types are all the types that do not need to be imported before they can be used in type annotation.  
プリミティブ型は、型アノテーションで使用する前にインポートする必要のないすべての型です。
<p align="center"> <img src="./assets/motoko_primitives_types.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> A few primitive types in Motoko</p>
<p align="center">Motoko の数少ないプリミティブタイプ</p>

## 🔢 Nat
`Nat` is used for **unbounded** natural numbers (1,2,3,4,...♾️). By default all positive whole numbers are casted to `Nat`.  
`Nat` は **無限の** 自然数 (1,2,3,4,...♾️) に対して使用されます。デフォルトでは、すべての正の整数が `Nat` にキャストされます。

```motoko
let n : Nat = 1;
```
Is equivalent to  
は、下記と同等です。

```motoko
let n = 1; // Will be casted to Nat automatically 自動的にNatにキャストされます
```
**Unbounded** means that value of type `Nat` will never [overflow](https://www.youtube.com/watch?v=WN8i5cwjkSE). The memory representation used will grow to accommodate any finite number. Motoko also has the concept of **bounded** natural numbers (`Nat8`, `Nat16`, `Nat32`, `Nat64`) that we will cover later. If you try to assign a negative number to a `Nat` the program will trap.  
**Unbounded** は `Nat` 型の値が決して [オーバーフロー](https://www.youtube.com/watch?v=WN8i5cwjkSE) しないことを意味します。使用されるメモリ表現は、どんな有限の数にも対応できるように成長します。また、Motoko には、後で取り上げる **bounded** 自然数 (`Nat8`, `Nat16`, `Nat32`, `Nat64`) という概念もあります。もし `Nat` に負の数を代入しようとすると、プログラムはトラップします。

```motoko
let n : Nat = -1;
```
This line will return an error: `literal of type Int does not have expected type Nat`.  
この行はエラーを返します：`literal of type Int does not have expected type Nat`.

`Nat` supports usual operations:  
`Nat`は通常の演算に対応しています：
- Addition: you can add two numbers using the addition operator `+`
- 加算：加算演算子 `+` を使って2つの数値を加算できます。

```motoko
let a : Nat = 1 + 1;    // 2
```
- Subtraction: you can subtract two numbers using the subtraction operator `-`
- 減算：減算演算子 `-` を使って、2つの数値を引き算できます。
```motoko
let a : Nat = 10 - 2;   // 8
```
> Be careful with substractions. `Nat` only plays with the positive numbers. If the result of the subtraction is less than zero, it won't fit. The value will no longer be of the `Nat` type and that could cause trouble if your program is expecting a value of the `Nat` type. 

> 減算に注意してください。`Nat` は正の数しか扱えません。引き算の結果が 0 よりも小さいと、適合しません。その値はもはや `Nat` 型ではなくなるので、プログラムが `Nat` 型の値を期待している場合、トラブルの原因になる可能性があります。

- Multiplication: you can multiply two numbers using the multiplication operator `*`
- 乗算：乗算演算子 `*` を使って、2つの数値を掛け合わせることができます。
```motoko
let a : Nat = 10 * 10;  // 100
```
- Division and modulo: to divide two numbers, you can use the division operator `/` and to find the remainder of a divided by b, you can use the modulo operator `%`
- 除算と剰余：2つの数を割るには除算演算子 `/` を、a を b で割った余りを求めるには剰余演算子 `%` を使用できます。
```motoko
let a : Nat = 10 / 2;   // 5
let b : Nat = 3 % 2;    // 1
```
## ➖ Int.
Integers represents whole numbers that can be positive or negative. The same mathematical operations seen earlier (addition, multiplication, subtraction, division, and modulo) can be performed on both `Int` and `Nat`.  
整数は正負のある整数を表します。先に見たのと同じ数学的操作（加算、乗算、減算、除算、剰余）は `Int` と `Nat` の両方に対して行うことができます。

```motoko
let i : Int = -3; 
let j : Int = 5;
```

> Since `Int` includes positive and negative whole numbers it includes all value of type `Nat`. We say that `Nat` is a subtype of `Ìnt`.
`Ìnt` is also an unbounded type and has bounded equivalents that we will cover later (`Int8`, `Int16`, `Int32`, `Int64`).

> `Int` は正負の整数を含むので、 `Nat` 型の値はすべて含まれます。`Nat` は `Ìnt` の部分型です。
また、`Ìnt` は unbounded 型であり、後で取り上げる bounded 型の等価物（`Int8`, `Int16`, `Int32`, `Int64`）があります。

## 🚦 Bool.
A `Bool` is either `true` or `false`. `Bool` stands for boolean and this data type only contains two values.  
`Bool` は `true` か `false` のどちらかです。`Bool`はbooleanの略で、このデータ型は2つの値しか持ちません。
```motoko
let light_on : Bool = true;
let door_open : Bool = false;
````

Booleans can be used and combined with logical operators:  
Boolean は、論理演算子と組み合わせて使用できます：

- `and`
```motoko
let result = false and false;   //false
```
```motoko
let result = true and false;    //false
```
```motoko
let result = false and true;    //false
```
```motoko
let result = true and true;     //true
```
- `or`
```motoko
let result = false or false;   //false
```
```motoko
let result = true or false;    //true
```
```motoko
let result = false or true;    //true
```
```motoko
let result = true or true;     //true
```
- `not`

```motoko
let result = not true;      //false
```
```motoko
let result = not false;     //true
```

`Nat` and `Int` supports comparison operators, which compare two integers and returns a `Bool`:  
`Nat` と `Int` は比較演算子をサポートしており、2つの整数を比較して `Bool` を返します： 
- The `==` (equality) operator which indicates if two values are equal.
- 2つの値が等しいかどうかを示す `==` (等号) 演算子です。
- The `!=` (not equal) operator which indicates if two values are different.
- 2つの値が異なるかどうかを示す`!=`（not equal）演算子。
- The `<` (less than) and `>` (more than) operators.
- 演算子 `<` (less than) と `>` (more than) です。
- The `<=` (less than or equal to) and `>=` (more than or equal to) operators.
- `<=`（以下）、`>=`（以上）の演算子です。

```motoko
3 < 5   // true
1 >= 1  // true
1 != 1  // false
2 == 10/5   // true
```
> The `==` operator is very different from the `=` operator. The first will test if two values are equal while the later will asign a value to a variable.

> 演算子 `==` は `=` 演算子と大きく異なります。前者は2つの値が等しいかどうかを調べるもので、後者は値を変数に代入するものです。

## 💬 Text
In Motoko, strings can be written surrounded by double quotes `"`  
Motokoでは、文字列をダブルクォート `"` で囲んで記述できます。
```motoko
"Hello Motoko Bootcamp!"
```
The type for string is `Text`.  
文字列の型は `Text` です。
```motoko
let welcomePhrase : Text = "Hello Motoko Bootcamp!";
```
We can use the concatenation operator `#` to join two `Text` together.  
連結演算子 `#` を使って、2つの `Text` を連結できます。
```motoko
let firstName : Text = "Motoko";
let surname : Text = "Bootcamp";
let completeName : Text = firstName # surname;
```

We can access the size of a `Text` by calling the `.size()` method.  
`.size()`メソッドを呼び出すことで、`Text`のサイズにアクセスできます。
```motoko
let name : Text = "Motoko";
let size = name.size()  // 6
```
## 🔤 Char
A value of type `Text` is actually composed of values from another type: `Char`. A `Text` is the concatenation of multiple characters. Characters are single-quote delimited `'`  
`Text`型の値は、実際には別の型の値で構成されています： `Char`です。`Text` は複数の character が連結したものです。character はシングルクォートで区切られた `'` です。
```motoko
let character_1 : Char = 'c';
let character_2 : Char = '8';
let character_3 : Char = '∏';
```
`Char` are represented by their [Unicode code points](https://deliciousbrains.com/how-unicode-works/). We can use the `Char` module from the Base library to check the unicode value.  
`Char` はその[Unicode code points](https://deliciousbrains.com/how-unicode-works/)で表されます。Unicodeの値を調べるには、Baseライブラリの `Char` モジュールを使用します。

```motoko
import Char "mo:base/Char";
import Debug "mo:base/Debug";
actor {
    let a : Char = 'a';
    Debug.print(debug_show(Char.toNat32(a)));   // 97
}
```
We can easily iterate over all the characters in a `Text`, by calling the `chars()` method. We can then use this iterator to create a `for` loop.  
`chars()`メソッドを呼び出すことで、簡単に `Text` に含まれるすべての文字を反復処理できます。そして、このイテレータを使用して `for` ループを作成できます。
```motoko
import Debug "mo:base/Debug";
import Char "mo:base/Char";
actor {
    let name : Text = "Motoko";
    for (letter in name.chars()){
        Debug.print(Char.toText(letter));
    };
};
```
> Notice how when we iterate `letter` is a `Char` and we need to convert it back to `Text` to use `Debug.print`.
The `Char` module also contains a few functions that can be used to test properties of characters:

> `letter` が `Char` であり、`Debug.print` を使用するために `Text` に変換する必要があることに注意してください。
`Char`モジュールには、文字のプロパティをテストするために使用できるいくつかの関数も含まれています：

- `isDigit`
```motoko
Char.isDigit('9');  // true
```
- `isWhitespace`
```motoko
Char.isWhitespace('a'); // false
```
- `isLowercase`
```motoko
Char.isLowercase('c');  //  true
```
- `isUppercase`
```motoko
Char.isUppercase('D');  // true
```
- `isAlphabetic`
```motoko
Char.isAlphabetic('|'); // false
```
## 💥 Float.
`Float` are numbers that have a decimal part.  
`Float`は小数部を持つ数値です。
```motoko
let pi = 3.14;
let e = 2.71;
```
If you want to use `Float` for whole numbers, you need to add the type descriptor otherwise they would automatically be casted to `Ìnt` or `Nat`.  
整数値に対して `Float` を使用したい場合、型記述子を追加しなければ、自動的に `Ìnt` や `Nat` にキャストされてしまいます。
```motoko
let f : Float = 2;
let n = 2;  // Automatically casted to type Nat
```

`Float` are implemented on 64-bits folowing the [IEEE 754 representation](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/). Due to the limited precision, operations may result in numerical errors.  
`Float` は [IEEE 754 representation](https://www.geeksforgeeks.org/ieee-standard-754-floating-point-numbers/) に従い、64ビットで実装されています。精度が低いため、演算によっては数値誤差が生じることがあります。

```motoko
0.1 + 0.1 + 0.1 == 0.3 // => false
```
```motoko
1e16 + 1.0 != 1e16 // => false
```
## 🎛️ Bounded types / Bounded 型
Motoko provides support for bounded types which are integer types with fixed precision. These bounded types can be useful for several reasons:  
Motokoは，固定精度の整数型である有界型をサポートしています。これらの境界付き型は、いくつかの理由で有用です：
- Memory efficiency: Bounded types allow you to know exactly how much memory your data will occupy.
- メモリ効率が良い： メモリ効率：バウンド型は、データが占有するメモリ量を正確に把握できます。
- Exact sizing: When you know that an API returns an exact number, you can use bounded types to ensure that the - returned number is represented accurately.
- 正確なサイジング： APIが正確な数値を返すことが分かっている場合、境界型を使って、返された数値が正確に表現されていることを確認できます。
- Execution efficiency: If you know that your numbers require 64-bit arithmetic, using `Nat64` is more efficient than using `Nat`.
- 実行効率： 数値が64ビット演算を必要とすることが分かっている場合、`Nat`を使うよりも`Nat64`を使う方が効率的です。
- Bitwise arithmetic: Bounded types make it easier to perform bitwise operations such as `<<` or `XOR` on binary data.
- ビット単位の演算： 境界型は、バイナリデータに対して `<<` や `XOR` などのビット演算を簡単に実行できるようにします。

### Nat8, Nat16, Nat32 and Nat64 / Nat8, Nat16, Nat32 と Nat64
There are four natural types supported in Motoko: `Nat8`, `Nat16`, `Nat32`, and `Nat64`.  
Motokoでサポートされている自然型は、`Nat8`, `Nat16`, `Nat32`, `Nat64`の4種類です。

The number in the type name specifies the number of bits in the type representation. For example, `Nat32` represents a 32-bit natural number.
型名に含まれる数値は、型表現のビット数を指定します。例えば、`Nat32`は32ビットの自然数を表します。

To declare a bounded variable, you must specify the type explicitly to avoid it being automatically cast to a regular `Nat`:  
境界付き変数を宣言するには、通常の `Nat` に自動的にキャストされるのを避けるために、明示的に型を指定する必要があります：
```motoko
let n : Nat32 = 1;
```
In contrast, if you declare a variable without specifying its type, it will default to a regular `Nat`  
一方、型を指定せずに変数を宣言した場合は、デフォルトで通常の `Nat` になります。
```motoko
let n = 1; // Will be casted to Nat automatically / 自動的に Nat にキャストされます 
```
### Int8, Int16, Int32, and Int64 / Int8, Int16, Int32, と Int64
Motoko also supports integer types, including `Int8`, `Int16`, `Int32`, and `Int64`. Bounded integer types behave similarly to bounded natural types, except they support negative values. The number in the type name specifies the number of bits in the type representation. For example, `Int32` represents a 32-bit integer:  
Motoko は `Int8`, `Int16`, `Int32`, `Int64` などの整数型もサポートしています。境界付き整数型は、負の値をサポートすることを除いて、境界付き自然型と同様の動作をします。型名に含まれる数値は、型表現のビット数を指定します。例えば、`Int32` は32ビット整数を表します：
```motoko
let i : Int32 = -1;
```

## 🤖 Blob.
`Blob` stands for Binary Large Object. The `Blob` type represents an immutable sequence of bytes: they are immutable, iterable, but not indexable and can be empty. <br/>
`Blob`は Binary Large Object の略です。`Blob`型は、バイト列を表します。イミュータブルで反復可能であるが、indexable ではなく、空であることもあります。<br/>

Byte sequences are also often represented as `[Nat8]`, i.e. an array of bytes, but this representation is currently much less compact than `Blob`, taking 4 physical bytes to represent each logical byte in the sequence.  
バイト列は `[Nat8]` つまりバイトの配列として表現されることも多いが、この表現は `Blob` よりもはるかにコンパクトではなく、配列の各論理バイトを表現するのに4バイトの物理バイトが必要である。

If you would like to manipulate Blobs, it is recommended that you convert `Blobs` to `[var Nat8]` or `Buffer<Nat8>`, do the manipulation, then convert back.  
Blob を操作したい場合は、`Blobs` を `[var Nat8]` または `Buffer<Nat8>` に変換して操作を行い、それから元に戻すことをお勧めします。

## 🫙 Unit type / Unit 型
The last type we will mention in this chapter is the unit type `()`. This type is also called the empty tuple type. It's useful in several places, for example in functions to indicate that a function does not return any specific type.  
この章で最後に紹介するのは、unit 型 `()` です。この型は空タプル型とも呼ばれます。この型はいくつかの場所で有用であり，例えば，関数の中で，ある関数が特定の型を返さないことを示すのに使われます。
```motoko
import Debug "mo:base/Debug";
actor {
    public func printMessage(message : Text) : async () {
        Debug.print(message);
        return();
    };
}
```
