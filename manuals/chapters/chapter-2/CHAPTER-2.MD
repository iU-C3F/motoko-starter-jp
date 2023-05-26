# Chapter 2: Common programming concepts. / 第2章：一般的なプログラミングの概念
## 📦 Variables / 変数
A variable is a value that has an arbitrary name, defined by a declaration. <br/>
変数とは、宣言によって定義された、任意の名前を持つ値のことです。<br/>
In Motoko, variables can be declared using either the `let` or `var` keyword, followed by the assignment operator `=`
Motoko では、変数は `let` または `var` キーワードで宣言し、その後に代入演算子 `=` を使用できます。

- Variables declared with `let` are immutable, meaning that their value cannot be changed once they are assigned. 
- `let`で宣言された変数は、一度代入されるとその値を変更することができないイミュータブルなものです。
```motoko
let n = 1;
```
- Variables declared with `var` are mutable, their value can be reassigned to a new value at any time using the reassignment operator `:=`.
- `var`で宣言された変数はミュータブルであり、その値は再割り当て演算子 `:=` を用いていつでも新しい値に再割り当てすることができます。

```motoko
var n = 1;
n := 2;
```

The syntax convention is to use `lowerCamelCase` for variable names and to use spaces around the `=` sign. Also, a variable declaration ends with a semicolon `;` Whenever you declare a variable don't forget to end the declaration with `;` otherwise Motoko will complain.

構文の決まりは、変数名には `lowerCamelCase` を使い、`=` 記号の周りにはスペースを使うことです。また、変数の宣言はセミコロン `;` で終わります。変数を宣言するときは、必ず `;` で終わらせることを忘れないでください。

If we try the following code:  
試しに次のようなコードを書いてみると：
```motoko
let n = 1;
n := 2;
```

An attempt is made to reassign a value to an immutable variable - that's why an error will occur. The specific error message will be `type error [M0073], expected mutable assignment target`. This  message indicates that the variable being reassigned is immutable and cannot be changed.

不変の変数に値を再代入しようとしたため、エラーが発生します。具体的なエラーメッセージは `type error [M0073], expected mutable assignment target` です。このメッセージは、再代入される変数が不変であり、変更できないことを示しています。

## 🍎 Types / 型
The **Motoko** language places a strong emphasis on types and is more strict in enforcing them compared to other general-purpose languages like **JavaScript** or **Python**. This strictness serves a purpose, as it helps prevent errors and issues. 

**Motoko** 言語は、**JavaScript** や **Python** のような他の汎用言語と比較して、型を重視し、その強制をより厳格に行っています。この厳密さは、エラーや問題を防ぐという目的もあります。

**Motoko** has static types, this means that each variable is assigned a specific type, which is determined before the program runs. The compiler checks each use of the variable to avoid errors that may occur during runtime. <br/>

**Motoko** は静的な型を持っています。これは、各変数に特定の型が割り当てられており、プログラムが実行される前に決定されることを意味します。コンパイラは、実行時に発生する可能性のあるエラーを回避するために、変数の各使用をチェックします。<br/>

To assign a type to a variable we use the `:` symbol, this is called **type annotation**.  
変数に型を割り当てるには、`:`という記号を使いますが、これを**型アノテーション**と呼びます。
```motoko
let age : Nat = 20;
let message : Text = "Of all the acts, the most complete is that of building";
let open : Bool = false;
```

You can generally omit the type declaration - the **Motoko** compiler will automatically guess the type to the variable based on the first value that you provide this is called **type inference**.

一般に、型宣言を省略できます。**Motoko** コンパイラは、最初に指定された値に基づいて、変数の型を自動的に推測します。これを**型推論**と呼びます。

```
let age = 20;   // Will be assigned type Nat / 型 Nat が割り当てられるでしょう。
```
> For the duration of the Bootcamp it is recommended to keep all type declarations to make things clearer, especially if you are new to typed languages.

> 特に型付き言語に慣れていない人は、物事を明確にするために、Bootcamp の期間中、すべての型宣言を保持することが推奨されます。

## 💬 Comments. / コメント
A one-line comment is written by starting the line with `//`.  
一行コメントは、行頭を `//` で始めることで記述します。
```motoko
// Hello! It is recommended to use comments to make your code more readable.
```

A comment can span into multiple lines, in that case you'll need to add `//` on each line.  
コメントは複数行にまたがることがありますが、その場合は各行に `//` を追加する必要があります。
```motoko
//  Sometimes you'll have a lot to say
//  In those cases 
//  You can use more than one line
```

## ⚙️ Functions / 関数
This section focuses solely on functions that are defined within the body of an actor using the `actor {}` syntax. Any function that is outside the `actor {}` syntax will be covered in future chapters.

このセクションでは、`actor {}` 構文を使用してアクターの本体内で定義される関数にのみ焦点を当てます。`actor {}` 構文の外側にある関数は、今後の章でカバーします。

### A simple example / 簡単な例
To introduce functions - let's look at an example: here is an actor that is responsible to keep track of a  counter. 

関数を紹介するために、例を見てみましょう。あるカウンターを記録する役割を持つアクターがいます。

```motoko
actor Counter {
    var count : Nat = 0;

    public func setCount(n : Nat) : async Nat {
        count := n;
        return count;
    };

};
```

The keyword `func` is used to declare functions, followed by the name given to the function, in that case `increaseCount`. As for variables, the syntax convention is to use `lowerCamelCase` for function names.  <br/>

関数を宣言するには、キーワード `func` を使用し、その後に関数名（この場合は `increaseCount` ）を指定します。変数と同様に、関数名には `lowerCamelCase` を使用するのが構文上の規則です。<br/>

### Function type / 関数型
When defining a function in Motoko, the typed arguments and return type are used to determine the type of the function as a whole. For example, the function setCount has the following type:  
Motoko で関数を定義する場合、型付き引数と戻り値の型から、関数全体の型が決定されます。例えば、関数 setCount は次のような型を持っています：
```motoko
setCount : (n : Nat) -> async Nat;
```
To declare a function in Motoko, you must specify the types of the arguments and return values. Function arguments are enclosed in parentheses `()`, and in this case, the function takes an argument `n` of type `Nat`. After the function arguments, the return type is specified : `async Nat`.  
Motokoで関数を宣言するには、引数と戻り値の型を指定する必要があります。関数の引数は括弧 `()` で囲まれ、この場合、関数は `Nat` 型の引数 `n` を受け取ります。関数の引数の後には、戻り値の型が指定されています : `async Nat`

> You might be wondering why the return type for the `setCount` function is `async Nat` instead of simply `Nat`? <br/> The term `async` stands for asynchronous, which means that in the **Actor model** we discussed earlier, canisters or actors communicate with each other asynchronously. When one canister sends a request to another (or when a user calls a function), there will be a brief waiting period before the caller receives a response. <br/> 
Asynchronous programming allows you to run your code in a non-blocking manner. The `async Nat` return type for the `setCount` function indicates that the caller must wait for a few moments before receiving the return value. Eventually, the response will be a value of type `Nat`, but with a delay due to the asynchronous nature of the communication between canisters. **All public functions declared in the body of an actor must be of return type `async`**. 

> `setCount` 関数の戻り値が単なる `Nat` ではなく `async Nat` になっていることを不思議に思っているかもしれません。`async` という用語は asynchronous の略で、先ほど説明した **Actorモデル** では、キャニスターまたはアクターは互いに非同期で通信することを意味します。あるキャニスターが別のキャニスターにリクエストを送信するとき（またはユーザーが関数を呼び出すとき）、呼び出し元がレスポンスを受け取るまでに短い待ち時間が発生します。 <br/>非同期プログラミングでは、コードをノンブロッキングで実行することができます。`setCount`関数の `async Nat` 戻り値の型は、呼び出し側が戻り値を受け取るまでしばらく待たなければならないことを示します。最終的に、応答は `Nat` 型の値となりますが、キャニスター間の通信が非同期であるため、遅延が発生します。 **アクター本体で宣言されるすべてのパブリック関数は、戻り値の型が `async`** である必要があります。

### Body and return / Body と return
- The curly brackets `{}` are used for the function body. The body of the function is a set of instructions executed when the function is being called.
In our example, for `setCount` we have 2 instructions:
1. Assign the value of `count` to the value of `n`. 
2. Return the current value of `count`.

- 中括弧 `{}` は関数本体に使用されます。関数本体は、関数が呼び出されたときに実行される命令の集合です。
この例では、`setCount`に対して、2つの命令を用意しています：
1. `count`の値を`n`の値へ代入する。
2. 現在の `count` の値を返す。

Motoko allows to omit the `return` at the end of the body of the function, because a block always evaluates to its last expression. Which means, we could rewrite the code in the following way and it would still be valid:  
Motoko では、ブロックは常に最後の式で評価されるため、関数本体の最後にある `return` を省略することができます。つまり、次のようにコードを書き換えても有効ということです：

```motoko
public func setCount(n : Nat) : async Nat {
    count := n;
    count;
};
```
### Public vs Private
So far we've only seen `public` functions. However, in Motoko you can also define `private` functions.  
ここまでは、`public` 関数だけを見てきました。しかし、Motokoでは `private` 関数も定義することができます。

```motoko
private func add(n : Nat, m : Nat) : Nat {
    return (n + m)
};
```
The function is now marked `private`, this means that it can only be used by the actor himself and cannot be called directly by users or external canisters.  
この関数は現在`private`とマークされており、これはアクター自身のみが使用でき、ユーザーまたは外部キャニスターから直接呼び出すことができないことを意味します。

Usually `private` functions are used as helpers in other functions, that are generally defined as `public`. For instance we could write the following.  
通常、`private`関数は、一般的に`public`として定義されている他の関数のヘルパーとして使用されます。例えば、次のように書くことができます。

```motoko
actor {
    var count : Nat = 0;

    private func add(n : Nat, m : Nat) : Nat {
        return (n + m)
    };

    public func addCount(n : Nat) : async Nat {
        let newCount = add(count,n);
        count := newCount;
        return count;
    };
}
```

> We can remove the `private` keyword , a function declaration defaults to a private function in Motoko unless declared otherwise (i.e unless declared `public`).

> `private` キーワードを削除すれば、Motoko の関数宣言は、そうでない場合（つまり、`public`と宣言されていない場合）、デフォルトで private 関数となります。


## 🕹️ Control flow. / 制御フロー
Control flow refers to the order in which a program is executed and the order that it follows. It decides which statements, instructions or function calls are executed and in what order, based on conditions or decisions made during the run time. <br/>
制御フローとは、プログラムの実行順序とそれに従う順序のことです。実行時の条件や判断に基づき、どの文や命令、関数呼び出しがどのような順序で実行されるかを決定するものです。<br/>

We discuss three common control flow constructs in Motoko: `if else` expressions, `loops` expressions and `switch` expressions.

ここでは、Motokoでよく使われる3つの制御フロー構成要素、`if else`式、`loop`式、`switch`式について説明します。

### If/else
The `if` statement allows the program to make a decision and execute a certain block of code only if a specific condition is met. The optional `else` statement provides an alternative if the condition is not met.  
`if` 文は、特定の条件が満たされた場合にのみ、プログラムが判断を下し、特定のコードブロックを実行することを可能にします。オプションの `else` 文は、条件が満たされない場合の代替案を提供します。
```motoko
    func isEven(n : Nat) : Bool {
        if(n % 2 == 0){
            return true
        } else {
            return false
        };
    };
```
In this case, the condition `n % 2` will be tested at runtime and depending on the value of `n` will returns `true` or `false`.  
この場合、実行時に `n % 2` という条件がテストされ、`n` の値に応じて `true` または `false` が返されます。 
In many cases the `else` block can be removed without modyfing the behavior of the code block.  
多くの場合、`else`ブロックはコードブロックの動作を変更することなく削除できます。
```motoko
    func isEven(n : Nat) : Bool {
        if(n % 2 == 0){
            return true;
        };
        return false;
    };
```
In other cases, you can add `else if` blocks to check additional conditions.  
その他の場合は、`else if` ブロックを追加して、追加の条件をチェックできます。
```motoko
    func checkNumber(i : Int) : Text {
        if(n < 0) {
            return ("The number is negative.");
        } else if (n == 0) {
            return("The number is zero.");
        } else if (n < 10) {
            return("The number is one digits.");
        } else if (n < 100) {
            return("The number is two digits.");
        } else {
            return ("The number is three or more digits.");
        }
    };
```
Note that `else if` statements are used after the initial `if` statement to check additional conditions, and only the code block associated with the first condition that evaluates to true will be executed.  
最初の `if` ステートメントの後に `else if` ステートメントを使用して追加の条件をチェックし、true と評価された最初の条件に関連するコードブロックのみが実行されることに注意してください。
### Loops / ループ
Loops enable the repeated execution of a code block until a specific condition is fulfilled. There are various types of loops, such as `for` loops and `while` loops:  
ループは、特定の条件が満たされるまで、コードブロックを繰り返し実行することを可能にします。ループには、`for`ループや`while`ループなど、さまざまな種類がある：
- `for` loops in Motoko use an iterator of the `Iter` type. We will delve into the `Iter` type in a later chapter, but to summarize, `Iter` objects facilitate looping through collections of data.
- Motoko の `for` ループは `Iter` 型のイテレータを使用します。`Iter` 型については後の章で詳しく説明しますが、要約すると、`Iter` オブジェクトはデータのコレクションをループすることを容易にします。

```motoko
var count : Nat = 0;
for (x in Iter.range(0, 10)) {
    count += 1;
};
```
In this example, `Iter.range(0, 10)` iterates through all natural numbers between 0 and 10, inclusive of both boundaries.  
この例では、`Iter.range(0, 10)` は、0から10までのすべての自然数（両端を含む）を反復処理します。

Alternatively, you can use `while` loops, which executes as long as the specified conditions remains true.  
また、`while`ループを使えば、指定した条件が真である限り実行することができます。

```motoko
var count : Nat = 0;
while (count < 10) {
    count += 1;
};
```
Here, the loop will continue to execute until the `count` variable is no longer less than 10.  
ここでは、変数 `count` が10より小さくなくなるまで、ループを実行し続けます。

### Switch/case
The `switch` expression in Motoko is a control flow construct that matches patterns based on its input. It begins with the `switch` keyword, followed by the input expression enclosed in parentheses `()`, and a code block enclosed in curly braces `{}`.  
Motokoの `switch` 式は、入力に基づいてパターンをマッチングする制御フロー構成体です。キーワード `switch` で始まり、入力式を括弧 `()` で囲み、中括弧 `{}` で囲んだコードブロックが続きます。
```motoko
let x = 3;
switch(x) {
    //
};
```
Within the code block, the `case` keyword is used to define patterns and expressions enclosed in curly braces `{}`. The input is compared to the patterns specified in each case, and if a match is found, the expression within the corresponding `case` block is executed.  
コードブロック内では、中括弧 `{}` で囲まれたパターンや式を定義するために `case` キーワードが使用されます。入力はそれぞれのケースで指定されたパターンと比較され、一致するものがあれば、対応する `case` ブロック内の式が実行されます。
```motoko
let x = 3;
switch(x) {
    case(0) {
        // This corresponds to the case x == 0
        return ("x is equal to 0");
    };
    case (1) {
        // This corresponds to the case x == 1
        return ("x is equal to 1");
    };
    case (2) {
        // This corresponds to the case x == 2
        return ("x is equal to 2");
    };
    case (_) {
        // This corresponds to all other cases
        return ("x is above 2");
    };
};
```
In Motoko, it is mandatory to include a `case(_)` statement for every possible input value in a `switch` expression. This is why the case(`_`) pattern is sometimes used as a catch-all case to handle any input value that did not match any of the other cases. The underscore symbol (`_`) is a wildcard that matches any value, so the `case(_)` pattern will match any input value.  
Motoko では、`switch`式に含まれるすべての可能な入力値に対して `case(_)` 文を含めることが義務付けられています。そのため、case(`_`)パターンは、他のどのケースにもマッチしなかった入力値を処理するためのキャッチオールケースとして使われることがあります。アンダースコア記号 (`_`) はどんな値にもマッチするワイルドカードなので、`case(_)` パターンはどんな入力値にもマッチします。

The `switch/case` expression is best used with variants.  
`switch/case`表現はバリアントと一緒に使うのがベストです。

```motoko
type Day = {
    #Monday;
    #Tuesday;
    #Wednesday;
    #Thursday;
    #Friday;
    #Saturday;
    #Sunday;
};
let day = #Monday;

switch(day) {
    case(#Monday){
        return ("Today is Monday");
    };
    case(#Tuesday){
        return ("Today is Tuesday");
    };
    case(#Wednesday){
        return ("Today is Wednesday");
    };
    case(#Thursday){
        return ("Today is Thursday");
    };
    case(#Friday){
        return ("Today is Friday");
    };
    case(#Saturday){
        return ("Today is Saturday");
    };
    case(#Sunday){
        return ("Enjoy your Sunday");
    };
};
```
In this example, we defined a variant type `Day`, declared a variable `day` with that type, and then used it as input in our `switch` expression. The switch expression is a powerful control flow construct that allows for pattern matching, providing a concise and readable way to handle multiple cases based on the input value.  
この例では、バリアントタイプ `Day` を定義し、そのタイプを持つ変数 `day` を宣言し、それを `switch` 式の入力として使用します。スイッチ式は、パターンマッチを可能にする強力なコントロールフロー構造で、入力値に基づいて複数のケースを処理する簡潔で読みやすい方法を提供します。