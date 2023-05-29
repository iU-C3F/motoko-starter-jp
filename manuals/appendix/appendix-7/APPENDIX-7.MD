# Appendix 7: Debugging and testing with Motoko. / 付録7：Motoko でデバッグとテスト
## Debugging / デバッグ
**Debug** is a module that provides utility functions for debugging and printing informations. 
[See the documentation page](https://internetcomputer.org/docs/current/motoko/main/base/Debug).  
**Debug** は、デバッグや情報印刷のためのユーティリティ関数を提供するモジュールです。
[ドキュメントページをご覧ください](https://internetcomputer.org/docs/current/motoko/main/base/Debug)。

### Print
```motoko
func print(text : Text)
```
`Debug.print()` will print text to the output stream (i.e your terminal).  
`Debug.print()` は、出力ストリーム（つまりターミナル）にテキストを出力します。
```motoko
import Debug "mo:base/Debug";
actor {
    Debug.print("Hello!");
};
```
<p align="center"> <img src="./assets/debug_print.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> The text will be printed in the same tab that is running your replica. Make sure to check out the correct place!</p>
<p align="center">テキストは、あなたのレプリカを実行している同じタブでプリントされます。正しい場所にチェックアウトするようにしてください！</p>

> Unfortunately, `print` can only be used locally. On the mainnet or when using Motoko Playground there is no concept of output stream so `Debug.print` has no effect.

> 残念ながら、`print`はローカルでしか使えません。メインネットや Motoko Playground を使用する場合、出力ストリームの概念がないため、`Debug.print` は何の効果もありません。

`Debug.print()` only accepts a value of type `Text` as input. If you have any  object, you can use the `debug_show` command to automatically convert it to `Text`.  
`Debug.print()` は入力として `Text` 型の値しか受け付けません。任意のオブジェクトがある場合、`debug_show`コマンドを使用すると、自動的に `Text` に変換することができます。
```motoko
let array : [Nat] = [19, 8, 2, 5];
Debug.print(debug_show(array));
```
You can also use convertion functions  
変換機能を利用することもできます
```motoko
import Nat "mo:base/Nat";
import Debug "mo:base/Debug";
actor {
    let n : Nat = 5;
    Debug.print(Nat.toText(n));
}
```
### Trap / トラップ
```motoko
func trap(errorMessage : Text) : None
```
`Debug.trap()` will stop the execution and return an error message with it.  
`Debug.trap()` は実行を停止し、それとともにエラーメッセージを返します。
```motoko
import Debug "mo:base/Debug";
actor {
    Debug.trap({errorMessage = "Unexpected reach"});
};
```

This could be useful as the error message will be visible in the return of the canister call, and not on a separate terminal. Also the behavior will be the same either in Local or Mainnet.  
これは、エラーメッセージが別の端末ではなく、キャニスター呼び出しのリターンで表示されるため、便利です。また、ローカルでもメインネットでも動作は同じになります。

You can use it with debug_show() to output any variable you might deem relevant.  
debug_show() と併用することで、関連すると思われる変数を出力できます。

<p align="center"> <img src="./assets/debug_trap.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> In this example the variable is printed in the same tab as you made the call.</p>
<p align="center">この例では、呼び出しを行ったのと同じタブに変数が出力されます。</p>