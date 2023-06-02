# Chapter 11: Intercanister calls. // 第11章：インターキャニスターコール
To achieve the vision of the Internet Computer, services (i.e canisters) needs to be able to call each other and run in an interoperable way. This capability is achieved through **inter-canister calls**. In this chapter, we will see how we can realize such calls and the potential issues to avoid.  
Internet Computer のビジョンを実現するためには、サービス（すなわちキャニスター）が互いに呼び出し可能で、相互運用可能な方法で実行される必要があります。この機能は、**インターキャニスターコール** によって実現されます。本章では、このような呼び出しをどのように実現するか、また、回避すべき潜在的な問題を確認します。

## A simple example / 簡単な例
To illustrate inter-canister calls we will use the following example, with 2 canisters:  
インターキャニスターコールを説明するために、２つのキャニスターを使用した下記の例を使用します：
1. Secret canister: This canister stores a secret password and this password should be divulgated only to users that paid. To verify payments, a mechanism of invoices is used.  
シークレットキャニスター： このキャニスターには秘密のパスワードが保存され、このパスワードは支払いを行ったユーザーだけに公開されます。支払いを確認するために、インボイスの仕組みが利用されています。
```motoko
actor Secret {
    getPassword : shared () -> async Result.Result<Text, Text>;
};
````
2. Invoice canister: This canister is responsible for creating, storing and checking the status of invoices.  
インボイスキャニスター： インボイス（請求書）の作成、保管、ステータスチェックを行うキャニスターです。
```motoko
actor Invoice {
    createInvoice : shared () -> async InvoiceId;
    checkStatus : shared (id : InvoiceId) -> async ?InvoiceStatus;
    payInvoice : shared (id : InvoiceId) -> async Result.Result<(), Text>;
};
```
Where invoices are defined as follows:  
インボイスは以下のように定義されている：
```motoko
public type InvoiceId = Nat;
public type InvoiceStatus = {
    #Paid;
    #Unpaid;
};
public type Invoice = {
    status : InvoiceStatus;
    id : InvoiceId;
};
```

> For the purpose of this lesson, this example is oversimplied.  If you are interested in how a real invoice canister looks like, check the [invoice canister from DFINITY](https://github.com/dfinity/invoice-canister).

> このレッスンの目的からすると、この例はオーバーな表現です。実際の請求書キャニスターがどのように見えるかに興味がある場合は、[invoice canister from DFINITY](https://github.com/dfinity/invoice-canister) を確認してください。

## Calling an actor by reference. / アクターを参照で呼び出す。
> For this section, check the source code in [ADD LINK].

> この部分については、[ADD LINK] でソースコードを確認してください。

The most straighforward way to call another canister it's **by reference**. This technique will always work, whether you are working locally or on mainnet but it requires two informations about the canister you want to call:  
他のキャニスターを呼び出す最も簡単な方法は、**by reference** です。この手法は、ローカルで作業していてもメインネットで作業していても常に機能しますが、呼び出したいキャニスターについて２つの情報が必要です： 
1. The canister id. / キャニスター ID。
2. The interface of the canister (at least partially). / キャニスターのインターフェイス（少なくとも部分的に）。

For the sake of this example, we will assume that the `Invoice` canister is deployed with the following canister id: `rrkah-fqaaa-aaaaa-aaaaq-cai`. To call this canister from the `Secret` canister we use the following syntax in `secret.mo`. Any type used in the interface needs to be imported or defined previously in `secret.mo`.  
この例では、`Invoice` キャニスターが次のキャニスター ID でデプロイされていると仮定します: `rrkah-fqaaa-aaaaaaq-cai`. このキャニスタを `Secret` キャニスタから呼び出すには、`secret.mo` で以下のシンタックスを使用します。インターフェイスで使用する型は、`secret.mo` で事前にインポートまたは定義しておく必要があります。
```motoko
let invoiceCanister = actor("rrkah-fqaaa-aaaaa-aaaaq-ca") : actor {
    createInvoice : shared () -> async InvoiceId;
    checkStatus : shared (id : InvoiceId) -> async ?InvoiceStatus;
    payInvoice : shared (id : InvoiceId) -> async Result.Result<(), Text>;
};
```
Once `invoiceCanister` is defined, any function can be called can be called. For instance that's how you would call `createInvoice`.  
`invoiceCanister` が定義されると、どんな関数でも呼び出すことができるようになります。例えば、`createInvoice` を呼び出す方法はこうです。
```motoko
let invoiceId = await invoiceCanister.createInvoice();
```
When you import an actor by reference, you only need to specify the interface that you plan to use. For instance, if you take a look at `secret.mo` we never use the `payInvoice` function. That's why we could simplify the actor declaration.  
アクターを参照でインポートする場合、使用する予定のインターフェイスを指定するだけでよいです。例えば、`secret.mo` を見てみると、`payInvoice` 関数を使うことはありません。そのため、アクターの宣言を簡略化できるのです。
```motoko
let invoiceCanister = actor("rrkah-fqaaa-aaaaa-aaaaq-ca") : actor {
    createInvoice : shared () -> async InvoiceId;
    checkStatus : shared (id : InvoiceId) -> async ?InvoiceStatus;
};
```
## Importing locally / ローカルにインポート
> For this section, check the source code in [ADD LINK].
When you a working locally, assuming that you canister is defined in `dfx.json` as follows.

> この部分については、[ADD LINK] にあるソースコードを確認してください。
ローカルで作業する場合、キャニスターは `dfx.json` で以下のように定義されていると仮定してください。

```json
{
    "canisters": {
        "invoice": {
          "main": "invoice.mo",
          "type": "motoko"
        },
        "secret": {
            "main": "secret.mo",
            "type": "motoko"
        }
      }
}
```
You can  the following syntax at the top of your main file.  
メインファイルの先頭には、以下の構文があります。
```motoko
import invoiceCanister "canister:invoice"
actor Secret  {

    let invoiceId = await invoiceCanister.createInvoice(); 

};
```
Generally, to import a canister locally, you use the following syntax at the top of your main motoko file:  
一般的に、キャニスターをローカルにインポートするには、メインのmotokoファイルの先頭で次の構文を使用します：
```motoko
import Y "canister:X"
```
`X` is the name given in `dfx.json` to the canister you are tring to import. `Y` is how you want to reference the import in the following code.  
`X` は、インポートしようとしているキャニスターの `dfx.json` で指定された名前です。`Y` は、下記のコードでインポートを参照する方法です。
## Importing on the mainnet / メインネットでの取り込み
> This syntax is currently not available due to tooling limitations but will be available at some point.

> この構文は、現在ツールの制限により利用できませんが、いずれは利用できるようになる予定です。

## Finding the interface of a canister / キャニスターのインターフェイスを探す
Before calling another canisters, you might want to check its interface. To find the interface of any canister, you can use the [Internet Computer Dashboard](https://dashboard.internetcomputer.org/).  
他のキャニスターを呼び出す前に、そのキャニスターのインターフェイスを確認したい場合があります。任意のキャニスターのインターフェイスを調べるには、[Internet Computer Dashboard](https://dashboard.internetcomputer.org/) を使用します。

1. Navigate to the [the dashboard](https://dashboard.internetcomputer.org/). / [the dashboard](https://dashboard.internetcomputer.org/) に移動します。
<p align="center"> <img src="./assets/main-dashboard.png" width="500px" style="border: 1px solid black;"/> </p>

2. In the search bar, enter the ID of the canister you want to examine. / 検索バーで、調べたいキャニスターのIDを入力します。
<p align="center"> <img src="./assets/ledger-dashboard.png" width="500px" style="border: 1px solid black;"/> </p>

3. Scroll down through the list of methods until you reach the **Canister Interface** section. / メソッドのリストをスクロールダウンして **Canister Interface** セクションに到達します。
<p align="center"> <img src="./assets/canister-interface.png" width="500px" style="border: 1px solid black;"/> </p>

4. Here, you can view a list of all public types used and the interface of the service, that list all public methods. / ここでは、使用されているすべてのパブリックタイプのリストと、すべてのパブリックメソッドをリストしたサービスのインターフェイスを表示できます。
<p align="center"> <img src="./assets/service-interface.png" width="500px" style="border: 1px solid black;"/> </p>

5. You can use the different tabs to see the interface in different languages (**Candid**, **Motoko**, **Rust**, **JavaScript**, **Typescript**). / 異なるタブを使って、異なる言語（**Candid**, **Motoko**, **Rust**, **JavaScript**, **Typescript**）でインターフェースを確認できます。

<p align="center"> <img src="./assets/motoko-interface.png" width="500px" style="border: 1px solid black;"/> </p>

## Async values. / Async の値
A canister processes its messages sequentially (one at-a-time), with each message representing a call to a public function.  
キャニスターは、メッセージを順次（一度に１つずつ）処理し、各メッセージはパブリック関数への呼び出しを表します。

Suppose you are **canister A** and you are calling **canister B**. The following sequence of events occurs:  
あなたが **キャニスター A** で、**キャニスター B** に電話をかけているとします。このとき、次のような流れになります：
- **Canister A** receives a message, which triggers a function. This function then initiates an inter-canister call which result in canister A sending a message to **canister B**.
- **キャニスター A** がメッセージを受信し、それが関数をトリガーします。この関数は次にインターキャニスターコールを開始し、その結果キャニスターAは **キャニスター B** にメッセージを送信します。
- Canister B already has a queue of 2 messages, so the new message is added to the end of the queue.
- キャニスター B にはすでに２つのメッセージのキューがあるので、新しいメッセージはキューの最後に追加されます。
- Canister A continues to receive and process additional messages, while canister B processes it's messages one-at-a time.
- キャニスター A は追加のメッセージを受信して処理し続け、キャニスター B はメッセージを１つずつ処理します。
- Canister B eventually sends a response to canister A. The message is added to the queue of canister A.
- キャニスター B は、最終的にキャニスター A に応答を送信します。そのメッセージは、キャニスター A のキューに追加されます。

<p align="center"> <img src="./assets/inter-canister-example.gif" width="500px" style="border: 1px solid black;"/> </p>

As you can see, between the instant you call a canister and the moment you receive a response, various events can happen, such as a user calling a function, an answer from a previous message returning, or another canister calling one of the public functions. These events can result in the internal state of the canister being significantly different from what you initially anticipated. **Always keep that in mind!**  
このように、キャニスターを呼び出してから応答を受け取るまでの間に、ユーザが関数を呼び出したり、以前のメッセージからの応答が返ってきたり、別のキャニスターがパブリック関数のいずれかを呼び出したりするなど、さまざまなイベントが発生する可能性があります。これらのイベントにより、キャニスターの内部ステートが、最初に予想したものと大きく異なることがあります。**常に心に留めておいてください！**

## Intra-Subnet vs Inter-Subnet イントラサブネット vs インターサブネット
### Intra-Subnet / イントラサブネット
When canister A and canister B belong to the same subnet, consensus is not required for inter-canister calls. This is because the inter-canister call results from a message being processed has already been agreed upon during the previous consensus round. There is an upper limit to the amount of computation that can be handled within a single consensus round; however, assuming this limit is not surpassed, **canister A will** receive its response in the same round.  
キャニスター A と キャニスター B が同じサブネットに属する場合、、インターキャニスターコールにコンセンサスは必要ありません。これは、処理されるメッセージのキャニスター間呼び出し結果が、前のコンセンサスラウンドですでに合意されているためです。1回のコンセンサス・ラウンドで処理できる計算量には上限がありますが、この上限を超えないと仮定すると、**キャニスターAは同じラウンドで応答を受け取ります**。
### Inter-Subnet / インターサブネット
When **canister A** and **canister B** are located in different subnet, the situation is more complex.  
**キャニスター A** と **キャニスター B** が異なるサブネットに配置されている場合、状況はより複雑になります。<br/>
The message needs to go through the **XNet messaging system**, which is a protocol of messages for cross-subnet interactions.  
メッセージは、サブネット間の相互作用のためのメッセージのプロトコルである **XNetメッセージングシステム** を経由する必要があります。<br/>
The XNet messaging system is composed of **subnet streams**. For instance assuming **canister A** is located in **subnet A** and sends a message to **canister B** located in **subnet B**, the message will go through the **subnet stream** of **subnet A** destinated to **subnet B**. This subnet stream is certified by the subnet every round, so that the other subnet can take a look at it and check the authenticity of messages (this is possible because **subnet B** knows the public key of **subnet A** and can verify the signature on the certification).  
XNet メッセージングシステムは **サブネットストリーム** で構成されています。たとえば、**キャニスターA** が **サブネットA** に位置し、**サブネットB** に位置する **キャニスターB** にメッセージを送信すると仮定すると、メッセージは **サブネットA** の **サブネットストリーム** を経由して **サブネットB** に宛先されます。このサブネットストリームはラウンドごとにサブネットによって認証され、他のサブネットがそれを見てメッセージの真正性をチェックできるようになっています（これは、**サブネットB** が **サブネットA** の公開鍵を知っていて、認証の署名を検証できるため可能です）。

This will lead to the following scenario:  
そうすると、次のようなシナリオになります：
1. A message is sent to a user to **canister A**, this message needs one round of consensus to be processed by the subnet. / あるユーザーに対して、**キャニスターA**というメッセージが送られる。このメッセージは、サブネットで処理されるために1ラウンドのコンセンサスを必要とする。
2. This message is processed by **canister A**, this message triggers an inter-canister call. This inteer-canister call triggers a message in the subnet steam of **subnet A** dedicated to **subnet B**. This stream needs to be certified by the subnet, which is done at the end of the execution cycle. / このメッセージは**キャニスターA**で処理され、このメッセージはキャニスター間通話をトリガーします。このキャニスター間通話は、**サブネットB**専用の**サブネットA**のサブネットストリームでメッセージをトリガーします。このストリームはサブネットによって認証される必要があり、これは実行サイクルの終了時に行われる。
3. **Subnet B** receives the message as part of the subnet stream coming from **Subnet A**, checks the authencitiy and add the message into a block to process it. / **サブネットB** は、**サブネットA** から来るサブネットストリームの一部としてメッセージを受信し、その正当性をチェックし、メッセージを処理するブロックに追加します。
4. 
## Message delivery failure
WIP / 制作途中
## Commit point and rollbacks
WIP / 制作途中
## Composite queries.
WIP / 制作途中