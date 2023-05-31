# Chapter 9: Handling errors. / 第9章 エラーのハンドリング
In Motoko, when something doesn't work as expected, there are various ways to show that an error has occurred. Some methods include:  
Motoko では、何かが期待通りに動かないとき、エラーが発生したことを示すさまざまな方法があります。いくつかの方法を紹介します：
- Using the `Result` type.  
- `Result`型を使用する。 
- Throwing error with the `throw` keyword or the `Error` library.
- `throw` キーワードまたは `Error` ライブラリを使用して、エラーをスローする。
- Trapping the program. 
- プログラムをトラップする。

In this section we will see different options and learn when to use each one for managing errors effectively.  
このセクションでは、さまざまなオプションを見て、エラーを効果的に管理するためにそれぞれのオプションを使用するタイミングを学びます。
## 🚥 The `Result` type. / `Result` 型
The `Result` type is extremly useful in Motoko to handle errors, it is defined as a variant type.  
`Result` 型は、Motoko ではエラーを処理するのに非常に便利で、バリアント型として定義されています。
```motoko
type Result<Ok, Err> = {#ok : Ok; #err : Err}
```
With `Ok` and `Err`, you can specify the types to return based on success or failure. For example, when creating a Result type for student graduation:  
`Ok`と`Err`では、成功または失敗に基づいて返す型を指定することができます。例えば、学生の卒業を表す Result 型を作成する場合：

```motoko
type Score = Nat; // The score of a student. / 生徒の点数。
type ExamFailed = {
    #ScoreTooLow : Nat;     //  The score of the student.  / 生徒の点数。
    #Absent;    //  One reason for not passing an exam. / 試験に合格できない理由の一つ。
    #Cheated;   //  Another reason for not passing an exam. / 試験に合格できないもう一つの理由。
};
```
- If a student graduates, their score is returned. The score is of type `Score`, which is an alias for `Nat`.
- 学生が卒業した場合、そのスコアが返されます。スコアは `Score` 型であり、これは `Nat` のエイリアスです。
- If a student fails, a variant indicating the reason for failure is returned. The variant is of type `ExamFailed`.
- 学生が不合格だった場合、不合格の理由を示す variant が返されます。variant は `ExamFailed` 型です。

Now we can use those new types to replace `Ok` and `Err`.  
これで、これらの新しい型を使って `Ok` と `Err` を置き換えることができるようになりました。
```motoko
type ExamResult = Result.Result<Score, ExamFailed>;
```
In cases like our example, using a variant type for `Err` is quite common. It allows for better management of different error types and makes pattern matching easier. This means anyone reviewing the error can better understand its specific cause!  
この例のような場合、`Err` にバリアントタイプを使用することは非常に一般的です。これは、異なるエラータイプをよりよく管理し、パターンマッチをより簡単にするためです。これは、エラーをレビューする人が、その特定の原因をよりよく理解できることを意味します！
```motoko
func sendMessageToStudent(result : ExamResult) : Text {
    switch(result) {
        case(#ok(score)){
            return ("Congrats 🎉 - you have graduated with a score of : " # Nat.toText(score));
        };
        case(#err(failure)){
            switch(failure){
                (#ScoreTooLow(score)){
                    return ("Unfortunately your score is below requirements. Next time you'll graduate! You had a score of : " # Nat.toText(score));
                };
                case(#Absent){
                    return ("You were absent at the exam. Please schedule another time.");
                };
                case(#Cheated){
                    return("Cheating is a short-term gain that leads to long-term pain");
                };
            };
        };
    };
};
```
### When should I use the Result type? / Result タイプはどのような場合に使用すればよいですか？
Using `Result` to report errors in your API offers a significant benefit: it allows other developers and programs to handle errors predictably. That's why `Result` is often used for expected errors in your program when you want to return a value. `Result` will not impact the normal behavior of the program.  
API でエラーを報告するために `Result` を使用すると、他の開発者やプログラムがエラーを予測可能に処理できるようになるという大きなメリットがあります。そのため、プログラム内で予想されるエラーに対して、値を返したいときに `Result` がよく使われます。`Result` がプログラムの正常な動作に影響を与えることはありません。

## 🪤 Trap & assertions / トラップ と アサーション
A **trap** is a type of error that occurs during the execution of a message and cannot be resolved. The most common causes of traps are:  
**トラップ** とは、メッセージの実行中に発生し、解決できないエラーの一種です。トラップの原因として最も一般的なものは、以下の通りです：
- Division by zero.
- ゼロによる除算。
```motoko
let a : Nat = 5;
let b : Nat = 0;
let c = a / b;
```
- Index is out of bounds. 
- インデックスが圏外になった。
```motoko
let names : [Text] = [];
```
- Assertion failure
```motoko
assert(false);
```
In some situations, it can be useful to trap on purpose, with a defined message.  
状況によっては、メッセージを明確にした上で、意図的にトラップをかけることが有効な場合もあります。

The best way to do so if to use the `Debug.trap()` method from the [Debug library](https://internetcomputer.org/docs/current/motoko/main/base/Debug) which allows you to pass an error message along the `trap`.  
そのためには、[Debug library](https://internetcomputer.org/docs/current/motoko/main/base/Debug) の `Debug.trap()` メソッドを使用するのが一番です。このメソッドは、`trap` に沿ってエラーメッセージを渡すことができます。
```motoko
func trap(errorMessage : Text) : None
```
### Assertions / アサーション
Using the `assert` keyword to construct assertions lets you check if a certain condition is met. If the condition inside `assert()` is `false`, the program will stop running. If it's `true`, the program will continue as normal.  
`assert` キーワードを使ってアサーションを構築すると、ある条件が満たされているかどうかをチェックできます。`assert()` の中の条件が `false` であれば、プログラムの実行は停止します。もし `true` ならば、プログラムは通常通り続行されます。
```motoko
assert(2 == 1);  // always traps / 常時トラップ
```
```motoko
assert n % 2 == 0; // traps only when n not even / n が偶数でない場合にのみトラップ
```
```motoko
assert(true) // never traps 決してトラップされない
```

### When should I use a Trap? / トラップはどのような場合に使用するのですか？
Traps immediately stop the current task (i.e message) being executed by a canister, but they don't prevent the canister from handling future requests. Traps should be used for unexpected situations. For example, the `unwrap` function below:  
トラップは、キャニスターによって実行されている現在のタスク（メッセージなど）を直ちに停止しますが、キャニスターが今後の要求を処理するのを妨げることはありません。トラップは予期せぬ事態に使用する必要があります。例えば、以下の `unwrap` 関数がそうです：
```motoko
/// Unwraps the value of the option.
public func unwrap<T>(option : ?T) : T {
    switch option {
        case (?value)
            value;
        case null
            Debug.trap("Value is null - impossible to unwrap")
    }
};
```
> Traps have a very useful feature: if a function traps, the canister's state will be reverted. This will be discussed further in the context of [inter-canister calls](../chapter-11/CHAPTER-11.MD#commit-point-and-rollbacks).

> トラップには非常に便利な機能があり、関数がトラップした場合、キャニスターのステートは元に戻ります。これについては、[inter-canister calls](../chapter-11/CHAPTER-11.MD#commit-point-and-rollbacks) の文脈でさらに説明する予定です。

## 🔀 Handling asynchronous errors with the `Error` type and try/catch. / 非同期エラーを `Error` 型と try/catch でハンドリング。
> In this section the term **error** refers specifically to any value of type `Error`.

In Motoko, error handling can be a bit confusing, especially if you are used to error handling in other programming languages. Here are some key points to keep in mind:  
Motoko では、特に他のプログラミング言語でのエラー処理に慣れている場合、エラー処理が少し混乱することがあります。ここでは、留意すべきポイントをいくつか紹介します：

- Errors can be thrown using the `throw` keyword.
- Errors can be handled using the `try/catch` pattern.
- An error is of type `Error`, which can also be manipulated using the Error library.
- エラーは `throw` キーワードを使用して投げることができる。
- エラーは `try/catch` パターンを用いてハンドリングできる。
- エラーは `Error` 型であり、Error ライブラリを使用して操作できる。

However, error handling in Motoko can only be done in an asynchronous context. This means that you can only throw or catch errors in the body of a shared function.
In this example, we define an actor that contains two functions: `throwErrorSync` and `throwErrorAsync`.  
しかし、Motoko のエラー処理は、非同期コンテキストでしか行えません。つまり、共有関数のボディ内でしかエラーをスローしたりキャッチしたりできないのです。
この例では、2つの関数を含むアクターを定義しています： `throwErrorSync` と `throwErrorAsync` です。
```motoko
import Error "mo:base/Error";
actor {
  // Misplaced throw / 投げ間違え
  func throwErrorSync() : () {
    throw Error.reject("This will not work")
  };

  // Can throw an error in a shared/public function - this error will be consumed by another canister/user calling this function.
  // shared/public 関数でエラーを投げることができます。このエラーは、この関数を呼び出す別のキャニスター/ユーザによって消費されます。
  public func throwErrorAsync() : async () {
    throw Error.reject("This will not work")
  };
}
```
> You can see this example [in the Motoko Playground](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=907568632) - note the `misplaced throw` message in the body of `throwErrorSync`.

> この例は [Motoko Playground](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=907568632) で見ることができます - `throwErrorSync` のボディにある `misplaced throw` メッセージに注目してください。

The `try/catch` pattern in Motoko is particularly useful when you are attempting to call another canister and want to handle any possible errors that may occur during the call. This can include situations such as:  
Motoko の `try/catch` パターンは、他のキャニスターを呼び出そうとしているときに、呼び出し中に発生する可能性のあるエラーを処理したい場合に特に便利です。これには、次のような状況が含まれます：

- The target canister is not live or cannot be reached.
- 対象のキャニスターが生きていない、または到達できない。
- The function being called does not exist on the target canister.
- 呼び出された関数がターゲット・キャニスターに存在しない。
- The function being called traps, either due to a programming error or because it has run out of resources.
- 呼び出された関数が、プログラミング・エラーまたはリソースを使い果たしたために、トラップした。
- The function being called throws an error that needs to be handled.
- 呼び出された関数が、処理する必要のあるエラーをスローしている。

Assuming this is our canister A - deployed with canister id:  
これがキャニスター A であると仮定すると、キャニスター ID でデプロイされることになります： 
```motoko
actor {
    public func foo() : async Text {
        return "foo"
    };   
}
```
Assuming this is our canister B  
これが私たちのキャニスター B であると仮定すると
```motoko
actor {

    let canisterA = actor("xxx") : actor {
        foo : shared () -> async Text;
    };

    public func fooFromCanisterA() : async Text {
        try {
            let foo = await canisterA.foo()
            return foo;
        } catch (e) {
            return "An error occured when calling canister A".
        };
    };   
}
```
In the provided example, we have two canisters: **Canister A** and **Canister B**.  
この例では、2つのキャニスターがあります： **キャニスターA**と**キャニスターB**です。
- **Canister A** has a single public function `foo` that returns the text "foo". 
- **キャニスターA**には、テキスト "foo "を返す単一のパブリック関数`foo`があります。
- **Canister B** has a public function `fooFromCanisterA` that attempts to call the `foo` function on **Canister A** using the `try/catch` pattern. If the call to `canisterA.foo()` is successful, the function returns the value of `foo`. If an error occurs during the call, it is caught by the catch block, and the function returns the text `"An error occurred when calling canister A"`.
- **キャニスターB** はパブリック関数 `fooFromCanisterA` を持っており、`try/catch` パターンを使用して **キャニスターA** の `foo` 関数を呼び出そうとします。`canisterA.foo()` の呼び出しに成功すると、この関数は `foo` の値を返します。呼び出し中にエラーが発生した場合、それは catch ブロックによって捕捉され、関数は `"An error occurred when calling canister A"` というテキストを返します。

This example illustrates how the `try/catch` pattern can be used to handle errors when calling functions on other canisters, ensuring that your program continues to execute gracefully even if an error occurs during the call.  
この例では、`try/catch`パターンを使用して、他のキャニスターの関数を呼び出す際のエラーを処理し、呼び出し中にエラーが発生した場合でもプログラムが優雅に実行され続けることを保証する方法を説明しています。

## 🤔 Final words / 最後の言葉
Dealing with all these different situations and ways of handling unexpected issues can be confusing at first, especially when it comes to the `actor` model and asynchronous contexts. But don't stress if you don't get it all right away. The best way to understand it is to get some practice and as you'll encounter different situations your understanding will strengthen!  
これらの異なる状況や予期せぬ問題を処理する方法を扱うことは、特に `actor` モデルや非同期コンテキストに関しては、最初は混乱することでしょう。しかし、すぐにすべてを理解できなくてもストレスを感じる必要はありません。理解するための最良の方法は、練習を重ねることであり、様々な状況に遭遇することで理解が深まります！