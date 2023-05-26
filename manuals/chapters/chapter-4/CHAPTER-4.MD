# Chapter 4: Candid the language of the Internet Computer. / 第4章 Internet Computer の 言語 Candid 
## Why do we need Candid? なぜ Candid が必要なのか？
Let's imagine the following situation:  
次のような状況を想像してみましょう：

- We are writing a canister in **Motoko** and we have defined a value `n` of type Nat.
- **Motoko** でキャニスターを書いていて、Nat型の値`n`を定義しています。
```motoko
let n : Nat = 5;
```
- We know  another canister that exposes a public function `square` that returns the `square` of the number provided - this canister is written in **Rust**.
- 私たちは、与えられた数の `２乗` を返すパブリック関数 `square` を公開している別のキャニスターを知っています - このキャニスターは **Rust** で書かれています。

We want to compute the square of our value `n`, but we are very lazy and we don't want to implement the `square` function in the **Motoko** canister, instead we want to make use of the already existing function in the **Rust** canister. That's possible and it will make use of **intercanister-calls** (a more advanced concept that we will see in more details in another lesson).

私たちは値 `n` の二乗を計算したいのですが、私たちはとても怠け者なので、**Motoko** キャニスターに `square` 関数を実装せず、代わりに **Rust** キャニスターに既に存在する関数を利用したいと思います。これは可能で、**intercanister-calls**（別のレッスンで詳しく説明する、より高度な概念）を利用することになります。

The problem is the following: `n` is of type `Nat` and the `square` function only accepts value of type `u128`. But, in **Motoko**, the type `u128` doesn't exist! It it is like trying to communicate in Spanish with someone that speaks Chinese.

問題は以下の通りです： `n` は `Nat` 型であり、`square` 関数は `u128` 型の値しか受け付けない。しかし、**Motoko**では `u128` という型は存在しない！これは、中国語を話す人とスペイン語でコミュニケーションをとろうとするようなものです。

<p align="center"> <img src="./assets/rust_motoko_situation.png" width="600px" style="border: 2px solid black;"> </p>
<p align="center"> Communication can be hard sometimes...</p>
<p align="center">コミュニケーションは時に難しいものです...</p>

> Composing services (i.e canisters) written in different languages is central to the vision of the **Internet Computer**. How do we solve this fundamental communication issue between canisters?

> 異なる言語で書かれたサービス（＝キャニスター）を組み合わせることは、**Internet Computer** のビジョンの中心です。このキャニスター間の根本的な通信の問題をどのように解決するのでしょうか？

## What is an IDL? / IDLとは？
We need to introduce an **Interface Description Language (IDL)**. An interface description language (**IDL**) is a generic term for a language that lets a program written in one language communicate with another program written in another unknown language.

**インターフェイス記述言語（IDL）** を導入する必要があります。インターフェース記述言語(**IDL**)とは、ある言語で書かれたプログラムが、別の未知の言語で書かれたプログラムと通信するための言語の総称である。

**Candid** is an **IDL** describing the public services deployed in canisters on the **Internet Computer**. The Candid interface allows inter-operation between services, and between services and frontends, independently of the programming language used. <br/>

**Candid** は、**Internet Computer** 上のキャニスターに展開されるパブリックサービスを記述する **IDL** です。Candid インターフェースは、使用するプログラミング言語に依存せず、サービス間、およびサービスとフロントエンド間の相互運用を可能にします。<br/>

Candid solves the problem we raised earlier by enabling a mapping between types in different languages.  
Candidは、異なる言語の型間のマッピングを可能にすることで、先に提起した問題を解決します。

<p align="center"> <img src="./assets/candid_mapping.png" width="600px" style="border: 2px solid black;"> </p>

## Candid file (.did)
A **Candid** file is a file with the .did extension - we can define the interface of the `square` canister with the following .did file:  
**Candid** ファイルは、拡張子が .did のファイルです。以下の .did ファイルで、`square`キャニスターのインターフェースを定義できます：
```candid
service : {
  square: (nat) -> (nat) query;
}
```

In this case, our service has a unique function named `square`. This function takes a `nat` and returns a `nat`. Notice that we also used the keyword `query`.  
このケースでは、我々のサービスには `square` というユニークな関数があります。この関数は `nat` を受け取り、`nat` を返します。キーワード `query` も使っていることに注意してください。

<p align="center"> <img src="./assets/candid_solved.png" width="600px" style="border: 2px solid black;"> </p>
<p align="center"> Candid is the common ground for all canisters to solve their misunderstanding!</p>
<p align="center">Candid は、すべてのキャニスターが誤解を解くための共通の土台となるものです！</p>

The `nat` used here is not the same as the `Nat` type in **Motoko**, or any type in **Rust**. If the `square` canister was written in Motoko the Candid interface would be exactly the same. The description of the service is independent of the language it was written in - this is key!

ここで使われている `nat` は **Motoko** の `Nat` 型や、**Rust** のどの型とも同じではありません。もし`square`キャニスターが Motoko で書かれていたとしても、Candid のインターフェースは全く同じになります。サービスの記述は、それが書かれた言語に依存しない - これが重要なポイントです！

Candid solves the problem we've raised earlier by enabling a mapping between types in different languages.

Candid は、異なる言語の型間のマッピングを可能にすることで、先に提起した問題を解決します。

<p align="center"> <img src="./assets/candid_mapping.png" width="600px" style="border: 2px solid black;"> </p>

The type `u128` will be converted to `nat` which is then converted to `Nat` in the **Motoko** canister. This makes it possible to write the following code:

タイプ `u128` は `nat` に変換され、**Motoko** キャニスターで `Nat` に変換されます。これにより、以下のようなコードを書くことが可能になる：

```motoko
actor {
    let n : Nat = 5;

    // We define the other canister in our own code.
    // もう一つのキャニスターは自分たちのコードで定義します。
    let rustActor : actor = {
        square : Nat -> Nat;    // We use Motoko types here ここでは、Motoko の型を使用しています  
    };

    public func getSquareOfN() : async Nat {
        await rustActor.square(n);  // This is how you can call another canister - pretty cool, right?! こうして別のキャニスターを呼び出すことができるのですが、なかなかかっこいいでしょう？
    };

};
```
> Candid is sometimes called "**the language of the Internet Computer**" as it how canisters communicate with each other. You will rarely have to write Candid but it's important to understand why Candid was created, how to read it, and how it works since you'll encounter Candid files in the projects you will work on. 

> Candid は、キャニスター同士が通信するための言語で、"**Internet Computer の言語**" と呼ばれることがあります。Candid を書くことはほとんどありませんが、プロジェクトで Candid ファイルに出会うことが多いので、Candid がなぜ作られたのか、どう読むのか、どう動くのかを理解することは重要です。

## Interacting with a canister キャニスターとの対話
To follow along this part, it is strongly recommended that you deploy locally the sample greet application that is shipped with `dfx`.  
このパートに沿って、`dfx`に同梱されているサンプル greet アプリケーションをローカルにデプロイすることを強く推奨します。
1. Generate the code for this project by running / 実行して、このプロジェクトのコードを生成します。
```bash
$ dfx new greet
```
2. Start your local replica. / ローカルレプリカを起動します。
```bash
$ dfx start --clean
```
3. Open another terminal tab & deploy the project. / 別のターミナルタブを開き、プロジェクトをデプロイします。
```bash
$ dfx deploy 
```
The Candid interface is automatically generated when building a Motoko project, but it can also be written manually. In its simplest form, the Candid DID file contains a service description. When the project is deployed, the `greet.did` file will contain the following service description:  
Candidのインターフェースは、Motokoプロジェクトのビルド時に自動的に生成されますが、手動で記述することも可能です。最も単純な形として、Candid の DID ファイルにはサービスの説明が含まれています。プロジェクトがデプロイされると、`greet.did`ファイルには以下のようなサービス説明が含まれることになります：
```candid
service : {
  greet: (text) -> (text) query;
}
```
> You can find the .did file under .dfx/local/canisters/greet_backend. If you don't see it make sure that you have built & deployed the project.

> .didファイルは、.dfx/local/canisters/greet_backend の下にあります。もし見つからない場合は、プロジェクトをビルド＆デプロイしたことを確認してください。

The greet dApp has one public function: `greet(text)`. From the service description we can see, that the greet() function takes a text and returns another text, and the service is a query function (faster execution). 

greet dApp は１つの public 関数を持っています: `greet(text)`。 サービスの説明から、greet() 関数はテキストを受け取り、別のテキストを返すこと、そしてサービスはクエリー関数であることがわかります（より高速な実行）。

You can see more advanced uses of Candid in the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/candid/candid-concepts) or in other examples [Motoko examples](https://github.com/dfinity/examples/tree/master/motoko).

Candid のより高度な使い方は、[documentation](https://internetcomputer.org/docs/current/developer-docs/build/candid/candid-concepts) または他の例 [Motoko examples](https://github.com/dfinity/examples/tree/master/motoko) で見ることができます。

The Candid interface, as previously mentioned, allows inter-operation between services, and between services and frontends. Candid is also very useful for calling the canisters from different places:  
前述したように Candid インターフェースは、サービス間、サービスとフロントエンド間の相互運用を可能にします。また、Candid は、異なる場所からキャニスターを呼び出す際にも非常に便利です：
- Using the terminal with `dfx`. 
- `dfx`でターミナルを使用する。
- Using the Candid UI. 
- Candid UIを使う。
- Using a frontend (webpage) with the JavaScript Agent.  
- JavaScript Agentでフロントエンド（ウェブページ）を使う。 

<b> Let's take a look at those different methods! </b>  
<b> では、そのさまざまな方法について見ていきましょう！ </b>

## <a id="using-the-terminal"> 📺 Using the terminal (dfx) </a>
The Candid interface allows you to call backend services or functions from the command line. This is useful for administrative tasks that do not require a front end or for testing the back end. In the example of the Greet dApp, you can call the greet() method by running the command:  
Candid インターフェイスでは、コマンドラインからバックエンドのサービスや関数を呼び出すことができます。これは、フロントエンドを必要としない管理作業や、バックエンドのテストに便利です。Greet dApp の例では、コマンドを実行することで、greet() メソッドを呼び出すことができます：
```bash
$ dfx canister call greet_backend greet '("motoko")'
("Hello, motoko!")
```
The general structure for calling any method from any canister is as follows:  
任意のキャニスターから任意のメソッドを呼び出すための一般的な構造は、以下のとおりです：
```bash
$ dfx canister call <CANISTER_NAME OR CANISTER_ID> <METHOD_NAME> '(ARGUMENT)'
```
If you want to call a canister on the main net, you need to add the --network ic flag:  
メインネット上のキャニスターを呼び出したい場合は、--network ic フラグを追加する必要があります：
```bash
$ dfx canister --network ic call <CANISTER_NAME OR CANISTER_ID> <METHOD_NAME> '(ARGUMENT)'
```
> Note that when using dfx you should always put your arguments between "**()**". The format for the arguments is the Candid format. 

> dfx を使用する際は、引数を常に "**()**" で挟む必要があることに注意してください。引数の形式は Candid 形式です。

For more information about how to call canisters from the command-line, see the [documentation](https://internetcomputer.org/docs/current/references/cli-reference/dfx-canister).

コマンドラインからキャニスターを呼び出す方法については、[documentation](https://internetcomputer.org/docs/current/references/cli-reference/dfx-canister) を参照してください。

## <a id="candid-ui"> 📲 Candid UI </a>
While the command-line can be very practical, there's also an easier way to call the backend services, and that's by using the Candid UI. When a project is deployed, besides the Candid interfaces, an asset canister running the Candid UI is also deployed. The built process will show the URL in the console, but the URL can also be found in `greet/.dfx/local/canister_ids.json`:

コマンドラインは非常に実用的ですが、バックエンドサービスを呼び出すにはもっと簡単な方法があり、それは Candid UI を使用することです。プロジェクトがデプロイされると、Candid のインターフェースの他に、Candid UI を実行するアセットキャニスターもデプロイされます。ビルドされたプロセスでは、コンソールにURLが表示されますが、URL は `greet/.dfx/local/canister_ids.json` にも記載されています：

```json
{
  "__Candid_UI": {
    "local": "r7inp-6aaaa-aaaaa-aaabq-cai"
  },
  "greet_backend": {
    "local": "rrkah-fqaaa-aaaaa-aaaaq-cai"
  },
  "greet_frontend": {
    "local": "ryjl3-tyaaa-aaaaa-aaaba-cai"
  }
}
```
In this case the URL to the Candid UI is http://127.0.0.1:4943/?canisterId=r7inp-6aaaa-aaaaa-aaabq-cai&id=rrkah-fqaaa-aaaaa-aaaaq-cai  
この場合、Candid UIへのURLは http://127.0.0.1:4943/?canisterId=r7inp-6aaaa-aaaaa-aaabq-cai&id=rrkah-fqaaa-aaaaa-aaaaq-cai です。

> It's possible that the URL for the Candid UI may be different on your machine. Make sure to adjust the URL accordingly based on the canister IDs in your own file.

> あなたのマシンでは、Candid UI の URL が異なっている可能性があります。自分のファイルのキャニスター ID に基づいて、それに応じて URL を調整するようにしてください。

Simply click the **Query** buttons, and see the response in the Output Log.  
**Query** ボタンをクリックするだけで、出力ログに応答が表示されます。
<p align="center"> <img src="assets/candid_ui_local.png" width="600px" style="border: 2px solid black;"> </p>

<b> Local or Live? / ローカル または 本番？</b> <br/>
One important confusion to avoid is the difference between the local & live Candid UIs:  
Candid のUIは、ローカルと本番の違いも重要なポイントです：

- The [live Candid UI](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/) is unique for the entire Internet Computer - you can access the interface of any dApp (assuming that the candid file has been shipped). By using the live Candid UI you can directly modify the state of a canister. 
- [本番 Candid UI](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/) は、Internet Computer 全体にとってユニークなものです。（Candid ファイルが出荷されていると仮定して）どの dApp のインターフェースにもアクセスできます。Candid UI を使用することで、キャニスターのステートを直接変更できます。

- The local Candid UI that we tried earlier is only deployed on your local replica. It can only give you access to the canister that you've deployed locally.

- 先ほど試したローカルの Candid UI は、ローカルレプリカにしかデプロイされません。ローカルにデプロイしたキャニスターにしかアクセスできないのです。

> By the way - the Candid UI (live or local) is also deployed in a canister.

> ところで - Candid UI（本番またはローカル）も、キャニスターへデプロイされています。

## <a id="using-the-frontend"> 📑 Using Candid in the frontend / フロントエンドで Candid を使う</a>
The greet dApp has both a backend and a frontend, and the frontend accesses the backend services through the Candid interface. The project's source code is organized in the following three folders:  
greet dApp はバックエンドとフロントエンドの両方を持ち、フロントエンドは Candid インターフェイスを通じてバックエンドのサービスにアクセスします。このプロジェクトのソースコードは、以下の3つのフォルダにまとめられています：
- declarations
- greet_backend 
- greet_frontend

Let's take a look at the frontend's JavaScript file located at `src/greet_frontend/src/index.js`. This file is responsible for handling the front-end logic of the greet dApp. The front-end and back-end are connected using the Candid interface which allows the front-end to access the back-end services.

`src/greet_frontend/src/index.js`にあるフロントエンドの JavaScript ファイルを見てみましょう。このファイルは、greet dApp のフロントエンドのロジックを処理する責任を負っています。フロントエンドとバックエンドは Candid インターフェイスを使って接続されており、フロントエンドがバックエンドのサービスにアクセスできます。

```javascript
import { greet_backend } from "../../declarations/greet_backend";

document.querySelector("form").addEventListener("submit", async (e) => {
  e.preventDefault();
  const button = e.target.querySelector("button");

  const name = document.getElementById("name").value.toString();

  button.setAttribute("disabled", true);

  // Interact with foo actor, calling the greet method
  // foo actor と対話し、greet メソッドを呼び出します。
  const greeting = await greet_backend.greet(name);

  button.removeAttribute("disabled");

  document.getElementById("greeting").innerText = greeting;

  return false;
});
```
Two lines of code in this file are worth paying attention to. The first line is where the Candid service description is imported, and in this case, it's not the greet.did file but the index.js file. The Candid index.js is automatically generated when the project is built and imports the Motoko backend's services.  
このファイルでは２行のコードに注目する必要があります。１行目は Candid のサービス記述がインポートされる場所ですが、この場合は greet.didフ ァイルではなく、index.js ファイルをインポートしています。Candid の index.js は、プロジェクトのビルド時に自動生成され、Motoko バックエンドのサービスをインポートしています。

```javascript
import {greet_backend } from "../../declarations/greet_backend";
```
After importing the Candid interface we can now use the public backend service, which is illustrated in this line:  
Candid インターフェイスをインポートした後、この行で示されているパブリックバックエンドサービスを使用できます：

```javascript
const greeting = await greet_backend.greet(name);
```
The update function `greet()` is called with the name as a parameter, which will return the greeting message. The call is asynchronous so an **await** is added so the front end is waiting for a response before moving on.  
name をパラメータとしてアップデート関数 `greet()` を呼び出すと、挨拶メッセージが返されます。この呼び出しは非同期なので、**await** を追加して、フロントエンドが応答を待ってから次の処理に移るようにしています。

Several agents are developed by both DFINITY and the community to easily integrate the Candid interface in different programming languages. See the [documentation](https://internetcomputer.org/docs/current/developer-docs/build/agents/) for a list of the available agents.  
DFINITY とコミュニティの両方によって、異なるプログラミング言語で Candid インターフェースを簡単に統合するためのエージェントがいくつか開発されています。利用可能なエージェントの一覧は [documentation](https://internetcomputer.org/docs/current/developer-docs/build/agents/) を参照してください。