# Chapter 1: Fundamental concepts. / 第1章：基本的な考え方
##  What is a canister? / キャニスターとは？
There is one word you absolutely need to master from this entire week. Are you ready for it? 
It's... 🥁... **CANISTER**!  
この一週間から絶対にマスターしなければならない言葉があります。その準備はできていますか？
それは ...🥁... **キャニスター** です！

The Internet Computer is a platform that hosts a large number of applications, all of those applications run smoothly within special containers called **canisters**.  
Internet Computer は、多数のアプリケーションをホストするプラットフォームであり、それらのアプリケーションはすべて **キャニスター** と呼ばれる特別なコンテナの中でスムーズに動作します。

- The Internet Computer is responsible for smoothly and safely run all the canisters deployed on the platform in parallel.
- Internet Computer は、プラットフォーム上に展開されたすべてのキャニスターを並行して円滑かつ安全に動かす役割を担っています。
- Developers build applications by writing the source code for those canisters. An application can be built into one or several canisters depending on the architecture.
- 開発者は、それらのキャニスターのソースコードを書くことで、アプリケーションを構築します。アプリケーションは、アーキテクチャに応じて、1つまたは複数のキャニスターに構築することができます。
- Users will interact with applications by sending messages to canisters. This happens whenever you use an application on the Internet Computer and interact with it - a few examples of such interactions are:
- ユーザーはキャニスターにメッセージを送ることで、アプリケーションと対話することになります。これは、Internet Computer 上でアプリケーションを使用し、そのアプリケーションと対話するたびに起こります。このような対話のいくつかの例を挙げます：
    - When you post on a social network.
    - ソーシャルネットワークに投稿したとき。
    - When you send a token to another address.
    - トークンを他のアドレスに送信するとき。
    - When you buy or sell an NFT.
    - NFTを購入または売却するとき。
    - When you read content on a website hosted on the Internet Computer.
    - Internet Computer 上でホストされているウェブサイトのコンテンツを読むとき。
    - And way more...
    - その他にも...

<p align="center"> <img src="./assets/oc_message.png" height="600px" style="border: 1px solid black;"/> </p>
<p align="center"> OpenChat is a decentralized messaging application built on the Internet Computer. </p>
<p align="center"> OpenChat は、Internet Computer 上で構築された分散型メッセージング・アプリケーションです。 </p>

## WebAssembly
Before we move on to Motoko - we actually need to explain another term: **WebAssembly**.
Motokoの話に移る前に、実はもう1つ用語を説明する必要があるんです： **WebAssembly** です。

<p align="center"> <img src="./assets/canister_overview.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> Overview of a canister.</p>
<p align="center"> キャニスターの概要</p>

If we zoom inside, a canister is composed of:  
中を拡大すると、キャニスターが構成されています：
- A **WebAssembly module** which is a piece of compiled code from languages such as Rust or Motoko. This is the code that is installed in the canister and is ultimately running. 
- Rust や Motoko などの言語からコンパイルされたコードである **WebAssemblyモジュール** です。これは、キャニスターにインストールされ、最終的に実行されるコードです。
- A **WebAssembly memory** - also called memory pages. This is where the state of the canister is stored and files are stored (photos, videos, tokens...). Code runs by the WebAssembly module will modify the memory.
- **WebAssembly memory** - メモリページとも呼ばれます。キャニスターのステートが保存され、ファイル（写真、ビデオ、トークン...）が保存される場所です。WebAssemblyモジュールによって実行されるコードは、このメモリを変更します。

<p align="center"> <img src="./assets/webassembly.png" width="600px" style="border: 2px solid black;"> </p>

<p align="center"> What is <b> WebAssembly </b>? <p>
<p align="center"><b>WebAssembly</b> とは何ですか？<p>
WebAssembly is a low-level binary format for executing code in multiples environments (browsers, cloud platform, smart devices, virtual machine..). The main benefits of using WebAssembly are, 

WebAssemblyは、複数の環境（ブラウザ、クラウドプラットフォーム、スマートデバイス、仮想マシン...）でコードを実行するための低レベルのバイナリーフォーマットです。WebAssemblyを使用する主な利点は以下の通りです、 

- **WebAssembly** supports code written in multiple languages (C, C++, Rust, Motoko) making it a versatile solution for developers.
- **WebAssembly** は、複数の言語（C、C++、Rust、Motoko）で書かれたコードをサポートしており、開発者にとって多用途なソリューションとなっています。
- **WebAssembly** code is portable and can run on almost any device. You write it once and you can run it everywhere!
- **WebAssembly** のコードはポータブルで、ほとんどすべてのデバイスで実行することができます。一度書いたら、どこでも実行できます！
<p align="center"> <img src="./assets/webassembly_stack.png" width="500px" style="border: 1px solid black;"/> </p>
<p align="center"> Write once and deploy on any platform. </p>
<p align="center"> 一度書けば、どんなプラットフォームでも展開できます。</p>

- **WebAssembly** is fast. It's a language that is very close to machine language and has been optimised for speed and performance. You can use it for creating complex and intensive applications (Games, simulations, graphic)!
- **WebAssembly** は速いです。機械語に非常に近い言語であり、スピードとパフォーマンスのために最適化されています。複雑で集中的なアプリケーション（ゲーム、シミュレーション、グラフィック）の作成に使用できます！
- **WebAssembly** provides a secure execution environment, by putting the code in a special area called a sandbox. The sandbox makes sure that the program is only able to do things and access resources that have been granted access to and doesn't allow it to access sensitive informaiton. This helps a lot when trying to write secure code or for users to make sure they won't get harmed by the code running on their machine!
- **WebAssembly** は、サンドボックスと呼ばれる特別な領域にコードを置くことで、安全な実行環境を提供します。サンドボックスは、プログラムがアクセス権を与えられたリソースにしかアクセスできないことを確認し、機密情報へのアクセスを許可しません。これは、安全なコードを書こうとするときや、ユーザーが自分のマシン上で実行されているコードによって害を受けないことを確認するときに、大いに役立ちます！

The only problem with **WebAssembly** is that it's a low-level language and it provides very little abstraction, making it difficult to use for writing complex applications like dApps (decentralized applications). 

**WebAssembly** の唯一の問題は、低レベルの言語であり、抽象化をほとんど行わないため、dApps（分散型アプリケーション）のような複雑なアプリケーションを書くのに使いにくいということです。

## The Motoko language / Motoko言語
<p align="center"> <img src="./assets/motoko_banner.png" width="600px" style="border: 1px solid black;"/> </p>

That's why the [DFINITY Foundation](https://dfinity.org/) has introduced a new language called **Motoko**, which is a programming language specifically designed for creating decentralized applications (dApps) on the Internet Computer. Since Motoko code can directly be compiled into **WebAssembly**, it is an incredible language to build on the Internet Computer. Motoko is a high-level language, that is easy to use. You write in Motoko and then it compiles for you in WebAssembly.

そこで、[DFINITY Foundation](https://dfinity.org/) は、Internet Computer 上で分散型アプリケーション（dApps）を作成するために特別に設計されたプログラミング言語である **Motoko** という新しい言語を発表しました。Motoko のコードは直接 **WebAssembly** にコンパイルすることができるので、Internet Computer上で構築するには信じられないような言語なのです。Motoko は高レベルの言語であり、使い方は簡単です。Motokoで書くと、WebAssembly にコンパイルしてくれます。

<p align="center"> <img src="./assets/motoko_to_wasm.png" width="600px" style="border: 1px solid black;"/> </p>
<p align="center"> In Motoko the code is spun, Into WebAssembly it does run.</p>
<p align="center"> Motoko でコードが書かれて、WebAssemblyで実行されます。</p>

> It's worth noting that WebAssembly, was co-designed by [Andreas Rossberg](https://github.com/rossberg), who joined the DFINITY Foundation early in 2017 to work on its canister smart contract execution environment and is also the original designer of the Motoko language. The standard is maintained by the [World Wide Web Consortium](https://www.w3.org/). 

> WebAssembly は2017年の初めに DFINITY Foundation に参加してそのキャニスタースマートコントラクト実行環境に取り組む [Andreas Rossberg](https://github.com/rossberg) が共同設計し、また Motoko 言語のオリジナル設計者であることは注目に値する。この標準は、[World Wide Web Consortium](https://www.w3.org/) によって維持されています。

In the following example, here is a `factorial` function, illustrated in **Motoko** and **WebAssembly**.  
以下の例では、**Motoko** と **WebAssembly** で説明されている `factorial` 関数を紹介します。
Don't stress out if you don't understand anything - that's normal:
わからないことがあってもストレスをためないように。それが普通です：

<table align="center">
  <tr>
    <th> Motoko </th>
    <th>WebAssembly (Binary)</th>
  </tr>
<td><pre>
func factorial(n : Nat) : Nat {
    if(n == 0) {
        return 1
    } else {
        return factorial(n - 1);
    }
};
</pre></td>

<td><pre>
20 00
42 00
51
04 7e
42 01
05
20 00
20 00
42 01
7d
10 00
7e
0b
</pre></td>
</tr>
</table>
<p align="center"> What do you think? Does writing this function seem easier with <b> Motoko </b>?</p>
<p align="center"> どうでしょう？この機能を書くのは、<b>Motoko</b> がいると楽そうですか？</p>

A Motoko file is a file with the extension `.mo`.  
Motoko ファイルとは、拡張子が`.mo`のファイルのことです。

<p align="center"> <img src="./assets/mo_extension.png" width="300px" style="border: 2px solid black;"> </p>

**Motoko** is a high-level language such as **JavaScript** or **Python**. It is generally considered easier to learn than a lower level language like **Rust** or **C**.  
**Motoko** は、**JavaScript** や **Python** のような高級言語です。一般に、**Rust** や **C** のような低レベルの言語よりも習得しやすいとされています。

---
<i> Motoko has a cool mascot that has been intensively used and modified in the community, for all sort of purposes!
So not only will you be able to build cutting-edge decentralized applications with Motoko, but you'll also have the coolest logo in the game. Don't believe us? Just check out the [Motoko NFT market](https://entrepot.app/marketplace/motoko) and see for yourself. </i>  
<i>Motoko にはクールなマスコットがあり、コミュニティではあらゆる目的で集中的に使用され、修正されてきました！
ですから、Motoko を使って最先端の分散型アプリケーションを構築できるだけでなく、このゲームで最もクールなロゴを手に入れることができるのです。信じられませんか？ [Motoko NFT market](https://entrepot.app/marketplace/motoko) を見て、ご自分の目で確かめてください。</i>

## The actor model. / actor モデル
If you open a Motoko file, there is a high probability that the first word that you will read is `actor`:  
Motoko のファイルを開くと、最初に読む単語は高い確率で`actor`です：
```
actor {

    /// CODE

};
````
An **actor** is how a canister is represented and abstracted in **Motoko**. This terms comes from the [Actor model](https://en.wikipedia.org/wiki/Actor_model) which is a way to write computer programs that can handle many tasks at the same time. It does this by treating **actors** as the basic building blocks of a program. <br/>
**actor** とは、**Motoko** においてキャニスターがどのように表現され、抽象化されるかを示すものです。この用語は [Actor model](https://en.wikipedia.org/wiki/Actor_model) に由来します。これは、同時に多くのタスクを処理できるコンピュータプログラムを書く方法です。これは、**actor** をプログラムの基本的な構成要素として扱うことで実現されています。 <br/>
An actor is a small computer program that can receive messages, do some work and then send messages to other actors. Actors can also create new actors and control them. All the actors talk to each other by sending messages. Since all interaction between actors is done via message passing, this allows for very high levels of concurrency and parallelism, making it well-suited for distributed systems. In that regards, **the Internet Computer is a distributed computer where each program is a canister !**  
actor とは、メッセージを受け取り、何らかの作業を行い、他のactor にメッセージを送ることができる小さなコンピュータプログラムのことです。actor は、新しいactor を作成し、それらを制御することもできます。すべてのactor は、メッセージを送信することで互いに会話します。actor 間のやり取りはすべてメッセージパッシングで行われるため、非常に高いレベルの並行性と並列性を実現でき、分散システムに適しています。その点で、**Internet Computer は、各プログラムがキャニスターである分散型コンピュータです！**

Since canisters have been implemented to follow the actor model - you won't be surprised to learn that canisters:  
キャニスターは actor モデルに準拠して実装されているため、キャニスターの存在を知っても驚くことはないでしょう：

- Have a private state (memory) & can run computations.
- プライベートなステート（メモリ）を持ち、計算を実行することができる。
- Receive messages from users or other canisters.
- ユーザーや他のキャニスターからメッセージを受け取ることができる。
- Can send messages to users or other canisters.
- ユーザーまたは他のキャニスターにメッセージを送ることができる。
- Can create other canisters.
- 他のキャニスターを作成することができる。

<p align="center"> <img src="./assets/actor_model.gif" width="800px" style="border: 2px solid black;"></p>
<p align="center">A canister receives a message, execute it, and possibilty send other messages to other canisters (or even create new ones) in response. </p>
<p align="center">キャニスターはメッセージを受け取り、それを実行し、それに応じて他のキャニスターに他のメッセージを送る（あるいは新しいものを作る）可能性があります。</p>

Let's now consider the following actor:  
ここで、次のような actor を考えてみましょう：
```motoko
actor {
    var message : Text = "Hello Motoko Bootcamp!";

    public func changeMessage(t : Text) : async () {
        message := t;
    };

    public query func readMessage() : async Text {
        return message;
    };
};
```
We can see that this actor has:  
この actor は下記であることがわかります：
- One variable called `message`, that is initialized to a value `Hello Motoko Bootcamp`.
- `message` という変数が1つあり、値 `Hello Motoko Bootcamp` に初期化されています。
- Two public functions:
    - `changeMessage` which updates the value of `message` to whatever is provided as argument.
    - `readMessage` which shows the value of `message` without modifying it. 
- 2つのパブリック関数があります：
    - `changeMessage` は `message` の値を引数として与えられたものに更新します。
    - `readMessage` は `message` の値を変更せずに表示します。


The `public` keyword indicates that both functions can be called from the outside by users or other canisters. The `public` functions of an actor represents the [API](https://en.wikipedia.org/wiki/API) of the canister. 

`public`キーワードは、両方の関数がユーザーや他のキャニスターによって外部から呼び出されることができることを示します。actor の `public` 関数は、キャニスターの [API](https://en.wikipedia.org/wiki/API) を表します。

## Update vs Query
Have you noticed the `query` keyword in the previous example?  
先ほどの例で、`query` というキーワードがあることにお気づきでしょうか？
<br/> When an user calls a canister, it is important to distinguish two types of calls:  
ユーザーがキャニスターを呼び出す場合、2種類の呼び出しを区別することが重要です：

### Update calls
Update calls are used when the user wants to modify the state of a canister. To ensure the integrity of the Internet Computer, these calls must be processed through consensus and by all nodes, which results in a delay of around 1-2 seconds. An update call would be used in the following situations:  
アップデートコールは、ユーザがキャニスタのステートを変更したいときに使用されます。Internet Computer の完全性を確保するために、これらの呼び出しはコンセンサスを通じて、すべてのノードによって処理されなければならず、その結果、約1～2秒の遅延が発生します。アップデートコールは、次のような状況で使用されます：

- Posting on a social media, such as [DSCVR](https://dscvr.one/).
- [DSCVR](https://dscvr.one/) などのソーシャルメディアに投稿する。
- Sending a message on a messaging application, such as [OpenChat](https://oc.app/).
- [OpenChat](https://oc.app/) などのメッセージングアプリケーションでメッセージを送信できます。
- Liking or sharing a content on [Distrikt](https://az5sd-cqaaa-aaaae-aaarq-cai.ic0.app/).
- [Distrikt](https://az5sd-cqaaa-aaaae-aaarq-cai.ic0.app/) のコンテンツに「いいね！」または「シェア」する。
- Buying a NFT on [Entrepot](https://entrepot.app/).
- [Entrepot](https://entrepot.app/) で NFT を購入する。

<p align="center"> <img src="./assets/update_call_gif.gif" width="800px" style="border: 2px solid black;"></p>

### Query calls クエリーコール
This type of call is used when a user wants to read data without modifying the state. These calls can be answered by a single node, making them very fast (at around 200ms). The downside is that **query** calls are less secure as a malicious node could potentially provide false information. A query call would be used in the following situations:  
このタイプの呼び出しは、ユーザーがステートを変更せずにデータを読みたいときに使用されます。このタイプの呼び出しは、1つのノードで応答できるため、非常に高速です（約200ミリ秒）。欠点は、悪意のあるノードが偽の情報を提供する可能性があるため、**クエリー**コールは安全性が低いことです。クエリコールは次のような状況で使用されます：

- Reading an article on [Nuance](https://nuance.xyz/).
- [Nuance](https://nuance.xyz/) の記事を読む。
- Checking your user profile picture on 
- ユーザープロフィール画像を確認する 
- Loading a video or a picture on any platform.
- 任意のプラットフォームで動画や画像を読み込む。

<p align="center"> <img src="./assets/query_call_gif.gif" width="800px" style="border: 2px solid black;"></p>

> Since a query call bypasses consensus and relies on a single node, it's less secure than an update call.

> クエリーコールはコンセンサスをバイパスして1つのノードに依存するため、アップデートコールよりも安全性に欠ける。

|  | Update call | Query call |
|-----------------|-----------------|-----------------|
Response Time | 2-5 seconds 🐢  | 200-400 ms ⚡️  |
Consensus| Yes | No |  
Read | Yes | Yes |
Write| Yes | No |
Cost | Cost cycles | Free (for now)


Let's go back to our previous actor  
前回の actor に戻りましょう
```motoko
actor {
    var message : Text = "Hello Motoko Bootcamp!";

    public func changeMessage(t : Text) : async () {
        message := t;
    };

    public query func readMessage() : async Text {
        return message;
    };
};
```

The `query` keyword tells us that `readMessage` function is only for reading information. On the other hand, `changeMessage` can update the state (we don't need to add the `update` keyword as it is assumed by default).  
`query` キーワードは、`readMessage`関数が情報を読み取るためだけの関数であることを物語っています。一方、`changeMessage`はステートを更新できます（デフォルトで想定されているため、`update`キーワードを追加する必要はない）。


> We have deployed the previous actor on the Internet Computer - and you can access <a href="https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/?id=rhjue-eaaaa-aaaaj-qazra-cai" target="_blank"> his API. </a> Try the interface and test the speed difference between `changeMessage` & `readMessage`. Have fun and leave a kind message for the next student.

> 私たちは、前の actor を åInternet Computer 上に配置しました。そして、あなたは <a href="https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/?id=rhjue-eaaaa-aaaaj-qazra-cai" target="_blank"> 彼の API</a> にアクセスすることができます。インターフェイスを試して、`changeMessage`と`readMessage`の速度差をテストしてください。楽しんで、次の生徒のために親切なメッセージを残してください。

## Fuel on the Internet Computer: cycles. / Internet Computer 上の燃料： cycle
To pay for computation & storage costs canisters have to be loaded with **cycles**.
Each canister has it’s own **cycle** balance - this can be thought of as the battery life of a **canister**. 
**Cycles** can be obtained by burning **ICPs**.

計算とストレージのコストを支払うために、キャニスターに **cycle** をチャージする必要があります。
各キャニスターにはそれぞれ **cycle** の残高があり、これは **キャニスター** の電池寿命と考えることができます。
 **cycle** は **ICP** を燃焼させることで得ることができます。

<p align="center"> <img src="./assets/cycles_burned.gif" width="600px" style="border: 2px solid black;"> </p>
<p align="center"> When processing a new message, cycles are deducted from the canister's balance and burned.</p>
<p align="center"> 新しいメッセージを処理する際、キャニスターの残高から cycle が差し引かれ、燃やされます。</p>

Unlike **gas** on **Ethereum**, **cycles** on the **Internet Computer** are not paid by the user. This means you can interact with canisters and browse websites without paying anything. This is known as the **reverse-gas model** and is a major improvement for the user's experience as it eliminates the need for creating wallets, holding tokens, and paying high fees.  
**Ethereum** の **ガス** とは異なり、**Internet Computer** の **Cycle** は、ユーザーによって支払われることはありません。つまり、何も支払わずにキャニスターと対話し、ウェブサイトを閲覧することができます。これは **逆ガスモデル** として知られており、ウォレットの作成、トークンの保持、高額な手数料の支払いが不要になるため、ユーザーの体験にとって大きな改善となります。

Cycles are measured in trillions (T), which is equivalent to 1,000,000,000,000 or 10^12. One trillion cycles always cost 1 XDR, which is a currency based on market exchange rates that represents a basket of major currencies. As of now, 1 XDR is equal to $1.34. The price of cycles is not affected by the price of ICP tokens. Instead, the conversion rate of ICP tokens to cycles is constantly adjusted by monitoring the price of ICP.

Cycle は、1,000,000,000 または 10^12 に相当するトリリオン（T）単位で測定されます。1兆 Cycle は常に1XDRで、これは主要通貨バスケットを表す市場為替レートに基づく通貨です。現在のところ、1XDRは1.34ドルに相当します。Cycle の価格は、ICPトークンの価格には影響されません。その代わり、ICPトークンから Cycle への変換レートは、ICPの価格を監視することで常に調整されます。

Each operation perfomed on the network has a cost attached to it:  
ネットワーク上で実行される各操作には、コストが付加されています：
- Creating a canister.
- キャニスターを作成する。
- Executing an update message.
- 更新メッセージの実行。
- Executing an inter-canister call.
- キャニスタ間コールを実行する。
- Storing data.
- データを保存する。
- Performing an HTTPS outcall.
- HTTPS Outcallを実行する。
- Computing a threshold ECDSA signature.
- 閾値ECDSA署名を計算する。

The cost of those operations also depends on the subnet in which they are performed and the **replication factor** of this subnet. The replication factor corresponds to the number of nodes in a subnet, which can range from 13 to 40.

これらの操作のコストは、それが実行されるサブネットと、このサブネットの **レプリケーション係数** にも依存します。レプリケーション係数は、サブネット内のノード数に対応し、13から40の範囲で設定できます。