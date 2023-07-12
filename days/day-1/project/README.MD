# Calculator 電卓 ➕✖️➖➗
On your first day of class, you enter the halls, eager to embark on the journey of a lifetime. Little do you know that you have forgotten to bring one essential tool to class — a **calculator**. 😳  
授業初日、あなたは一生に一度の旅に出ようと意気込んで会場に足を踏み入れます。しかし、あなたは授業に必要な道具を一つ忘れていることに気づかない - それは **電卓** です。😳<br/> 

Your professor, a renowned expert in the community, begins the day's lesson by presenting a series of complex mathematical problems that require the use of a calculator. The students around you huddle together, pulling out their calculators to tackle the challenge. 💪  
その日の授業は、地域の有名な専門家である教授が、電卓を使わなければならない複雑な数学の問題を次々と提示することから始まります。あなたの周りの生徒たちは、この課題に取り組むために電卓を取り出し、身を寄せ合っています。💪<br/>

As you search your bag in vain for your calculator, you realize that you have inadvertently left it behind. Instead of panicking or admitting defeat, your resourceful nature kicks in. You decide to rely on your intelligence and aptitude in Motoko to create your own calculator. 🧑‍💻  
バッグの中から電卓を探し出すと、うっかり忘れてしまったことに気づきます。慌てず、負けず、機転を利かせます。あなたは、自分の知能と Motoko への適性を頼りに、自分だけの電卓を作ることにしました。🧑‍💻

## 🧑‍🏫 Requirements / 必要条件
Your task is to create the code for a **calculator**, which is implemented as a canister.  
あなたの課題は、キャニスターとして実装されている**電卓**のコードを作成することです。
<br/>
The canister should have a public interface that allows users to perform calculations. The canister has a memory variable called `counter` which represents the result of the most recent calculation.  
キャニスターは、ユーザが計算を実行できるようなパブリックなインタフェースを持つ必要がある。キャニスタは `counter` というメモリ変数を持ち、これは最も新しい計算結果を表します。

## 📒 Steps ステップ
1. Define a mutable variable called `counter` of type `Float` to store the result of the most recent calculation. / 最新の計算結果を格納するために、`Float`型の `counter` というミュータブル変数を定義しなさい。
2. Implement the `add` function, which accepts a value `x` of type `Float`, increments the counter, and returns its new value. / `Float`型の値`x`を受け取り、カウンタをインクリメントして新しい値を返す `add` 関数を実装しなさい。
```motoko
add : shared(x : Float) -> async Float;
```
3. Implement the `sub` function, which accepts a value `x` of type `Float`, decrements the counter, and returns its new value. / `Float`型の値 `x` を受け取り、カウンタをデクリメントして新しい値を返す `sub` 関数を実装しなさい。
```motoko
sub : shared(x : Float) -> async Float;
```
4. Implement the `mul` function, which accepts a value `x` of type `Float`, multiplies it with the counter, and returns the new value of the counter. / `mul`関数を実装しなさい。この関数は `Float` 型の値 `x` を受け取り、カウンタと掛け合わせ、新しいカウンタの値を返します。
```motoko
mul : shared(x : Float) -> async Float;
```
5. Implement the `div` function, which accepts a value `x` of type `Float`, divides the counter by `x`, and returns the new value of the counter. Ensure to guard against division by zero. / この関数は `Float` 型の値 `x` を受け取り、カウンタを `x` で割り、新しいカウンタの値を返します。ゼロによる除算に対して確実にガードしなさい。
```motoko
div : shared(x : Float) -> async ?Float;
```
6. Implement the `reset` function, which sets the value of counter to zero, effectively resetting it. / カウンターの値をゼロにし、事実上リセットする `reset` 関数を実装しなさい。
```motoko
reset: shared () -> async ();
```
7. Implement the `see` function, which serves as a query and returns the current value of counter. / クエリーとして機能し、カウンターの現在値を返す `see` 関数を実装しなさい。
```motoko
see: shared query () -> async Float;
```
8. Implement the `power` function, which accepts a value `x` of type `Float`, raises the counter to the power of `x`, and returns the new value of the counter. / 関数 `power` を実装しなさい。この関数は `Float` 型の値 `x` を受け取り、カウンタを `x` のべき乗に引き上げ、カウンタの新しい値を返します。
```motoko
power: shared (x : Float) -> async Float;
```
9. Implement the `sqrt` function, which calculates the square root of the counter and returns the new value of the counter. / カウンターの平方根を計算し、カウンターの新しい値を返す `sqrt` 関数を実装する。
```motoko
sqrt: shared () -> async Float;
```
10. Implement the `floor` function, which returns the largest integer less than or equal to the counter. / カウンター以下の最大の整数を返す `floor` 関数を実装しなさい。
```motoko
floor: shared () -> async Int;
```
11. Deploy the `Calculator` on the Internet Computer. / Internet Computer 上に `Calculator` をデプロイしなさい。

## 📺 Interface
> At the end of the project, your canister should implement the following interface.

> プロジェクト終了時には、キャニスターは以下のインターフェイスを実装している必要があります。

```motoko
actor {
    add : shared(x : Float) -> async Float;
    sub : shared(x : Float) -> async Float;
    mul : shared(x : Float) -> async Float;
    div : shared(x : Float) -> async ?Float;
    reset: shared () -> async ();
    see: shared query () -> async Float;
    power: shared (x : Float) -> async Float;
    sqrt: shared () -> async Float;
    floor: shared () -> async Int;
};
```

## 最後に
「最後に」は、C3F の ICP 開発者コミュニティにて、Motoko Bootcamp を進めている方に向けてのものです。
当課題を消化できたところで、C3F の Discord のチャンネル \"#【c3f開発コミュニティ】\" へその旨を報告しましょう！もしくは、消化が難しい場合は、質問しましょう！