# Appendix 1: Deploying and managing a canister. / 付録1：キャニスターのデプロイと管理
In this appendix, we will deploy, interact and mange a canister. To illustrate all those interactions we will deploy a canister called `Counter` and experiment with it.You just need to follow along and copy the code!  
この付録では、キャニスターのデプロイ、対話、管理を行います。これらすべての相互作用を説明するために、`Counter`というキャニスターをデプロイし、それを使って実験します！
## Prequesites 前提条件
Make sure that you have  `dfx` installed.  
`dfx` がインストールされていることを確認します。
```motoko
$ dfx --version
dfx 0.12.0
```
> Your version can be different, as long as it is above 0.12.0. If not, run `dfx upgrade`. 

> 0.12.0 以上であれば、バージョンは異なっていてもかまいません。もし違うなら、`dfx upgrade` を実行してください。

## Generating the project / プロジェクトを生成する
We first need to deploy a canister. Follow the instructions:  
まず、キャニスターを展開する必要があります。説明書に従ってください：
1. Generate a new folder called `first_project`. / `first_project`という新しいフォルダを生成します。
```bash
$ mkdir first_project
```
2. Move into your newly generated folder. / 新しく生成したフォルダーに移動します。
```bash
$ cd first_project
```
3. Create two files `dfx.json` & `main.mo` / dfx.json`と`main.mo`の2つのファイルを作成する。
```bash
$ touch dfx.json && touch main.mo
```
4. Copy & paste the following code in your `dfx.json` file / 以下のコードをコピーして、`dfx.json` ファイルに貼り付けます。
```json
{
    "canisters": {
      "Counter": {
        "main": "main.mo",
        "type": "motoko"
      }
    }
  }
```
`dfx.json` is a configuration file used by `dfx` to gather information about your project. Each project has one dfx.json file, even if it contains multiple canisters.  
`dfx.json` は `dfx` がプロジェクトに関する情報を収集するために使用する設定ファイルです。複数のキャニスターを含む場合でも、各プロジェクトは1つの dfx.json ファイルを持ちます。<br/>

Within the `dfx.json` file, you can specify the list of canisters using the keyword "canisters" followed by a curly brace `{`. Each canister in the list is separated by a comma `,` .  
`dfx.json`ファイルの中では、キーワード "canisters" の後に中括弧 `{` を付けて、キャニスターのリストを指定できます。リスト内の各キャニスターはコンマ `,` で区切られます。

In the provided example, there is only one canister named `Counter`. It is of type `motoko` and the main file is located in the same folder with the name `main.mo`. The main file always contains the `actor{}` definition.  
この例では、`Counter`という名前のキャニスターが1つだけ存在します。これは `motoko` というタイプで、メインファイルは同じフォルダにあり、名前は `main.mo` です。メインファイルには常に `actor{}` の定義が含まれています。<br/>

> One `main.mo` file = One actor = One canister.

> `main.mo`ファイル１つ = アクター１つ = キャニスター1つ。

6. Copy & paste the following code in your `main.mo` file / 以下のコードを `main.mo` ファイルにコピー＆ペーストしてください。
```motoko
actor Counter {
    var i : Int = 0;

    public func add(j : Int) : async Int {
        i := i + j;
        i;
    };

    public func div(j : Int) : async Int {
        i := i / j;
        i;
    };

    public func reset() : async () {
        i := 0;
    };

    public query func show() : async Int {
        i;
    };
};
```

7. Start your local replica / ローカルレプリカを起動する
```bash
$ dfx start
Running dfx start for version 0.12.0
Using the default definition for the 'local' shared network because /Users/seb/.config/dfx/networks.json does not exist.
Dashboard: http://localhost:57765/_/dashboard
```

> You can click and access the dashboard. It will give you information about your local replica (replica version, canisters deployed, number of consensus rounds since start..)

> クリックしてダッシュボードにアクセスできます。ローカルレプリカに関する情報（レプリカのバージョン、デプロイされたキャニスター、開始からのコンセンサスラウンド数...）が表示されます。

8. Create an empty canister for `Counter`. /  `Counter`用の空のキャニスターを作成します。
```bash
$ dfx canister create Counter
Creating a wallet canister on the local network.
The wallet canister on the "local" network for user "seb" is "rwlgt-iiaaa-aaaaa-aaaaa-cai"
Creating canister Counter...
Counter canister created with canister id: rrkah-fqaaa-aaaaa-aaaaq-cai
```
`dfx` will automatically create a wallet for your `identity`. A wallet is necessary to hold cycles, which are necessary to create canisters. Only canisters can hold cycles and not your identity - that's why you need this wallet which acts as a proxy when you create and deploy canisters.
`dfx` は自動的にあなたの `identity` のためのウォレットを作成します。ウォレットは Cycle を保持するために必要で、キャニスターを作成するために必要です。キャニスターだけが Cycle を保持することができ、あなたの ID は保持することができません。

9. Compile your code into WASM. / 作成したコードをWASMにコンパイルします。
```bash
$ dfx build Counter
Building canisters...
Shrink WASM module size.
``` 
After this step, your Motoko file is compiled into a WebAssembly module, which size is optimised. You can find the module under `.dfx/canister/Counter/Counter.wasm`  
このステップの後、Motoko ファイルは WebAssembly モジュールにコンパイルされ、そのサイズは最適化されます。このモジュールは `.dfx/canister/Counter/Counter.wasm` の下で見つけることができます。

> If you wanna know what is actually inside the module. You can [convert your WASM to the WAT format](https://webassembly.github.io/wabt/demo/wasm2wat/), it's a textual representation for the WASM binary.

> モジュールの中身を知りたいなら [WASMをWAT形式に変換する](https://webassembly.github.io/wabt/demo/wasm2wat/) ことができます。これはWASMのバイナリをテキストで表現したものです。

10. Install the WASM inside the canister. / WASM をキャニスター内に設置します。
```bash
$ dfx canister install Counter
Creating UI canister on the local network.
The UI canister on the "local" network is "ryjl3-tyaaa-aaaaa-aaaba-cai"
Installing code for canister Counter, with canister ID rrkah-fqaaa-aaaaa-aaaaq-cai
```
**Congratulations! Your canister in now deployed.**

**おめでとうございます！あなたのキャニスターは今、デプロイされました**

The **Candid** interface, allows inter-operation between services, and between services and frontends. **Candid** is also very useful for calling the canisters from different places:  
**Candid** インターフェースは、サービス間、サービスとフロントエンド間の相互運用を可能にします。また、**Candid** は、異なる場所からキャニスターを呼び出すのに非常に便利です：

- Using the terminal with `dfx`.
- `dfx`でターミナルを使用する。
- Using the **Candid UI**.
- **Candid UI** を使う。
- Using a frontend (webpage) with the **JavaScript Agent**.
- **JavaScript Agent** でフロントエンド（Webページ）を使用する。

## Using the terminal ターミナルを使用
The Candid interface allows you to call backend services or functions from the command line. This is useful for administrative tasks that do not require a front end or for testing the back end. In the example of the `Counter` dApp, you can call the `add` method by running the following command:  
Candid インターフェイスでは、コマンドラインからバックエンドのサービスや関数を呼び出すことができます。これは、フロントエンドを必要としない管理作業や、バックエンドのテストに便利です。`Counter` dAppの例では、以下のコマンドを実行することで、`add` メソッドを呼び出すことができます：

```bash
$ dfx canister call Counter add '(3)'
(3 : int) 
```
As you can probably guess from the previous example, the format for calling canisters using `dfx` is the following:  
前の例から推測できるように、`dfx`を使ってキャニスターを呼び出すときの形式は以下の通りです：
```bash
dfx canister call NAME_OF_CANISTER NAME_OF_FUNCTION '(ARGUMENTS)'
```
Notice that you should put your arguments betwen `'()'` and the format for arguments is the **Candid** syntax, the returned type is `int` and not `Int` like in Motoko. This distinction will matter more when we will deal with complex arguments (object, tuples, arrays..).  
引数を `'()'` の間に置くこと、引数のフォーマットは **Candid** 構文であること、返される型は `int` であり Motoko のように `Int` ではないことに注目してください。この違いは、複雑な引数（オブジェクト、タプル、配列...）を扱うときに、より重要になるでしょう。

If you want to call a canister on the main net, you need to add the `--network ic` flag:  
メインネット上のキャニスターを呼び出したい場合は、`--network ic`フラグを追加する必要があります：
```bash
dfx canister --network ic call NAME_OF_CANISTER NAME_OF_FUNCTION '(ARGUMENTS)'
```

As we've seen before, we can **trap** the canister if we try to divide by 0.  
以前見たように、0 で割ろうとすれば、キャニスターを **トラップ** できます。
```bash
$ dfx canister call Counter div '(0)'
Error: Failed update call.
Caused by: Failed update call.
  The Replica returned an error: code 5, message: "Canister rrkah-fqaaa-aaaaa-aaaaq-cai trapped: integer division by 0"
```
An important thing to note, is that the canister persits it's state by default. If we send another command:  
注意すべき重要な点は、キャニスターはデフォルトでそのステートを保持することです。もし、別のコマンドを送ったら

```bash
$ dfx canister call Counter add '(5)'
(8 : int)
```
We can see that the value of `counter` is 8 - which corresponds to the two commands we've run so far.   
`counter`の値が 8 であることがわかります。これは、これまで実行した2つのコマンドに対応します。  
This property is called **orthogonal persistence**. Orthogonal persistence creates an illusion that a program runs forever without crashing or losing state. If you don't send command to your canister, it will kept the value of `counter` to 8 forever.   
この性質は、**直交永続化** と呼ばれています。直交持続性は、プログラムがクラッシュしたりステートを失ったりすることなく永遠に実行されるような錯覚を起こさせます。キャニスターにコマンドを送らないと、キャニスターは `counter` の値を永遠に 8 で保持します。

> The term "**orthogonal persistence**" may sound complex, but in practice, it simply means that you can focus on writing code without the need to build a database to store the state. The state is automatically persisted by 
default, eliminating the need for additional storage infrastructure.

> "**直交永続化**" という言葉は複雑に聞こえるかもしれませんが、実際には、ステートを保存するためのデータベースを構築する必要がなく、コードを書くことに集中できることを簡単に意味します。ステートは、デフォルトで自動的に永続化されます。
デフォルトで自動的に永続化されるため、ストレージのインフラを追加する必要がありません。

11. Copy & paste the following code in your `main.mo` file / 以下のコードを `main.mo` ファイルにコピー＆ペーストしてください。
```motoko
actor Counter {
    var i : Int = 0;

    public func add(j : Int) : async Int {
        i := i + j;
        i;
    };

    public func sub(j : Int) : async Int {
        i := i - j;
        i;
    };

    public func mult(j : Int) : async Int {
        i := i * j;
        i;
    };

    public func div(j : Int) : async Int {
        i := i / j;
        i;
    };

    public func reset() : async () {
        i := 0;
    };

    public query func show() : async Int {
        i;
    };
};
```

12. Recompile the code / コードの再コンパイル 
```motoko
$ dfx build Counter
```

13. Upgrade the canister with the new module / 新モジュールでキャニスターをアップグレードします
```motoko
$ dfx canister install Counter --mode upgrade
```

Now that we have upgraded our canister, if we look at the value of `counter` (  
さて、キャニスターをアップグレードしたところで、`counter`の値を見てみると、(
```motoko
$ dfx canister call Counter show 
(0 : int)
```

Yes, orthogonal persistence has limitations!  
そう、直交永続化には限界があるのです！<br/> 
Whenever we upgrade our canister, the state is wiped out and we start from 0 again. We will see in a future chapter that we can solve this issue, by using **stable memory** which is a memory that persists between upgrades.  
キャニスターをアップグレードするたびに、ステートは消去され、再び 0 からスタートします。この問題を解決するには、アップグレードの間も持続するメモリである **ステーブルメモリ** を使用する必要があります。

In the meantime, or more information about how to call canisters from the command-line, you can read the [documentation](https://internetcomputer.org/docs/current/references/cli-reference/dfx-canister) or simply run:  
一方、コマンドラインからキャニスターを呼び出す方法の詳細については、[documentation](https://internetcomputer.org/docs/current/references/cli-reference/dfx-canister) を読むか、単に実行できます：  
```bash
$ dfx canister --help
```
## Using the Candid UI / Candid UIを使用
While the command-line can be very practical, there's also an easier way to call the backend services, and that's by using the Candid UI. When a project is deployed, besides the Candid interfaces, an asset canister running the Candid UI is also deployed. The built process will show the URL in the console, but the URL can also be found in `/.dfx/local/canister_ids.json`:  
コマンドラインは非常に実用的ですが、バックエンドサービスを呼び出すにはもっと簡単な方法があり、それは Candid UI を使用することです。プロジェクトがデプロイされると、Candid のインターフェースの他に、Candid UI を実行するアセットキャニスターもデプロイされます。ビルドされたプロセスではコンソールに URL が表示されますが、URL は `/.dfx/local/canister_ids.json` に記載されていることもあります：
```json
{
  "Counter": {
    "local": "rrkah-fqaaa-aaaaa-aaaaq-cai"
  },
  "__Candid_UI": {
    "local": "ryjl3-tyaaa-aaaaa-aaaba-cai"
  }
}
```
In this case the URL to the Candid UI is http://127.0.0.1:4943/?canisterId=ryjl3-tyaaa-aaaaa-aaaba-cai&id=rrkah-fqaaa-aaaaa-aaaaq-cai  
この場合、Candid UIへのURLは http://127.0.0.1:4943/?canisterId=ryjl3-tyaaa-aaaaa-aaaba-cai&id=rrkah-fqaaa-aaaaa-aaaaq-cai です。

> It's possible that the URL for the Candid UI may be different on your machine. Make sure to adjust the URL accordingly based on the canister IDs in your own file.

> あなたのマシンでは、Candid UI の URL が異なっている可能性があります。自分のファイルのキャニスター ID に基づいて、それに応じて URL を調整するようにしてください。

Simply click the **Query** button, and see the response in the 
**Output Log**.

**Query** ボタンをクリックするだけで、**出力ログ** に応答が表示されます。
**出力ログ** で確認できます。

**Local or Live?** / **ローカル または 本番？**  
One important confusion to avoid is the difference between the local & live Candid UIs:  
避けるべき重要な混乱の一つは、ローカルと本番の Candid UIの違いです：
- The live Candid UI is unique for the entire Internet Computer - you can access the interface of any dApp (assuming that the candid file has been shipped). By using the live Candid UI you can directly modify the state of a canister. 
- Candid UI は Internet Computer 全体にとってユニークなもので、どんな dApp のインターフェースにもアクセスできます（Candid ファイルが同梱されていることが前提です）。Candid UI を使用することで、キャニスターのステートを直接変更できます。
- The local Candid UI that we tried earlier is only deployed on your local replica. It can only give you access to the canister that you've deployed locally.
- 先ほど試したローカルの Candid UI は、ローカルレプリカにのみデプロイされます。ローカルにデプロイしたキャニスターにしかアクセスできません。

> The CandidUI (live or local) is running in a canister.

> CandidUI（本番またはローカル）は、キャニスターで稼働しています。