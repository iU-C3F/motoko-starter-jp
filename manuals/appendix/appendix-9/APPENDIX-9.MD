# Appendix 9: HTTP Request to access a canister through a browser. / 付録9：ブラウザからキャニスターにアクセスするためのHTTPリクエスト。
## Difference between HTTP request & HTTP outcalls. / HTTP リクエストと HTTP アウトコールの違い。
In this chapter, we will cover how canisters can be accessed through HTTP requests. This is a separate topic from **HTTP Outcalls**:  
この章では、キャニスターを HTTP リクエストでアクセスする方法について説明します。これは **HTTP Outcalls** とは別のトピックです：

- HTTP Request: Canisters can handle incoming requests and serve web pages.  
- HTTP リクエスト： キャニスターは、受信したリクエストを処理し、ウェブページを提供できます。
- HTTP Outcalls: Canisters can send requests and communicate with the Web 2.0 world. This can be used for various use cases, such as querying an exchange for token prices, getting the latest weather information, and sending notifications to users.
- HTTP アウトコール： キャニスターはリクエストを送信し、Web 2.0 ワールドと通信できます。トークンの価格を取引所に問い合わせたり、最新の気象情報を取得したり、ユーザーに通知を送ったりと、さまざまなユースケースに利用できます。

Whenever you [access a canister](https://wujxq-qqaaa-aaaaj-qazca-cai.raw.ic0.app/) through your browser there are a few steps involved. Let's go through all of them.
You will notice that URLs on the Internet Computer are of the following form: <CANISTER_ID>.ic0.app The .ic0.app indicates that you are reaching out to [boundary nodes]().  
ブラウザから [キャニスターにアクセス](https://wujxq-qqaaa-aaaaj-qazca-cai.raw.ic0.app/) する場合、必ずいくつかの手順があります。ここでは、そのすべてを説明します。
Internet Computer のURLは、次のような形になっていることにお気づきでしょうか： <CANISTER_ID>.ic0.app .ic0.appは、あなたが[バウンダリーノード]()に到達していることを示します。

## What are boundary nodes? / バウンダリーノードとは何ですか？
Canisters are hosted and executed by nodes that participate in the IC consensus However, those nodes are not directly accessible by end users.
To protect the consensus nodes & improve performance there is a layer of boundary nodes which serve different useful purposes:  
キャニスターは、IC コンセンサスに参加するノードによってホストされ実行されます。しかし、これらのノードはエンドユーザーが直接アクセスできるわけではありません。コンセンサスノードを保護し、パフォーマンスを向上させるために、異なる有用な目的を持つバウンダリーノードの層が存在します：

- Translate the HTTP request of the user's browser to canister call. This part is called the HTTP Gateway protocol. When canisters send their response the gateway will convert it back to an HTTP request.
- ユーザーのブラウザの HTTP リクエストをキャニスターコールに変換します。この部分を HTTP ゲートウェイプロトコルと呼びます。キャニスターが応答を送信すると、ゲートウェイはそれを HTTP リクエストに変換します。
- Route the calls to the correct subnet running the canister. To properly route those calls the boundary nodes have to keep track of the entire configuration of the Internet Computer:
- 呼び出しを、キャニスターを実行している正しいサブネットにルーティングします。これらの呼び出しを適切にルーティングするために、バウンダリーノードは Internet Computer の全構成を把握しておく必要があります：
    - List of subnets.
    - サブネットのリスト。
    - List of nodes and which subnet they belong to.
    - ノードのリストと、それらがどのサブネットに属しているか。
    - The canisters run by each subnet.
    - 各サブネットで実行されるキャニスター。
- Load balancing among the subnet's replica nodes (i.e if a replica is lagging behind and has already a lot of work on its plate - boundary nodes will send the request to another replica).
- サブネットのレプリカノード間のロードバランシング（あるレプリカが遅れていて、すでに多くの仕事を抱えている場合、バウンダリーノードは別のレプリカにリクエストを送ります）。
- Protect subnets from DDoS attacks.
- DDoS 攻撃からサブネットを保護します。

<p align="center"> <img src="./img/http_gateway.png" width="800px" style="border: 2px solid black;"> </p>

> Currently, boundary nodes are run by the DFINITY Foundation. However, the objective ([as part of the roadmap](https://forum.dfinity.org/t/boundary-node-roadmap/15562)) is to have anyone able to set up and run a boundary nodes. This will make interaction with the Internet Computer more reactive for end users and this will make the platform more robust to censorship.

> 現在、バウンダリーノードは DFINITY Foundation によって運営されています。しかし、目標（[ロードマップの一部として](https://forum.dfinity.org/t/boundary-node-roadmap/15562)）は、誰でもバウンダリーノードをセットアップして実行できるようにすることです。これにより、エンドユーザーにとって Internet Computer との相互作用が状況の変化により対応できるようになり、検閲に対してより強固なプラットフォームとなることでしょう。

## Asset canister / アセットキャニスター
To serve web content on the Internet Computer, a canister should have a method that can handle an `http_request`, which includes the URL, HTTP method, and headers, and produce an HTTP response, consisting of a status, headers, and body. There are two ways to go about that:  
Internet Computer 上に Web コンテンツを提供するために、キャニスターは URL、HTTP メソッド、ヘッダーを含む `http_request` を処理し、ステータス、ヘッダー、ボディからなる HTTP レスポンスを生成できるメソッドを持つ必要があります。それには、２つの方法があリます：

- Implement the http_request method and all associated logic yourself.  
- http_request メソッドと関連するすべてのロジックを自分で実装する。 
- Use the provided **asset** canister: this is a special canister whose code has been already implemented by DFINITY. You need to specify the type of this canister in `dfx.json` & add the source folder of your web app. Once the asset canister is deployed on the Internet Computer the website can be accessed at `http://<canister id>.ic0.app` and `http://<canister id>.raw.ic0.app`. The frontend canister that is shipped when you deploy a project with `dfx new <project>` is an asset canister (as you can confirm by looking at `dfx.json`).
- 提供された **asset** キャニスターを使用する: これは、DFINITY によってコードが既に実装されている特別なキャニスターです。このキャニスターの種類を `dfx.json` で指定し、Web アプリのソースフォルダに追加する必要があります。アセットキャニスターが Internet Computer 上に配置されると、ウェブサイトは `http://<canister id>.ic0.app` と `http://<canister id>.raw.ic0.app` でアクセスできるようになります。`dfx new <project>` を使用してプロジェクトをデプロイする時に同梱されるフロントエンドキャニスターはアセットキャニスターです（`dfx.json` を見れば確認できます）。

> You can access [the source code for this canister written in Rust](https://github.com/dfinity/sdk/tree/master/src/canisters/frontend/ic-frontend-canister) under the [DFINITY organization](https://github.com/dfinity).  

> [Rustで書かれたこのキャニスターのソースコード](https://github.com/dfinity/sdk/tree/master/src/canisters/frontend/ic-frontend-canister) は、[DFINITY Foundation](https://github.com/dfinity) の下でアクセスできます。 

## Difference between ic0.app & raw.ic0.app / ic0.app と raw.ic0.app の相違点
As we've said earlier there are two ways to access a canister:  
先に述べたように、キャニスターにアクセスする方法は２つあります：
- raw.ic0.app: the raw URL raw URL will simply return the request as it is so serves the asset files (HTML, CSS, Javascript).
- raw.ic0.app: raw URL はリクエストをそのまま返すだけなので、アセットファイル（HTML、CSS、Javascript）を提供します。
- ic0.app: uses a service worker to verify the content served by the boundary node. The service worker is loaded and then handles requests, verifying the signature of the assets served by the canister using the public key on the Internet Computer.
- ic0.app：バウンダリーノードが提供するコンテンツを確認するために、サービスワーカーを使用します。サービスワーカーはロードされた後、リクエストを処理し、Internet Computer 上の公開鍵を使用してキャニスターが提供するアセットの署名を検証します。

<p align="center"> <img src="./img/service_worker.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> Loading the service worker...</p>

When accessing a webpage, speed is a key factor. This is why we use query calls to handle http_request. However, it's important to note that query calls do not go through a consensus process and cannot create signatures. To address this issue, we use certified variables. This means that the content must be certified prior to the call being made. In some cases, this certification process may not be possible and if you are accessing a website under ic0.app, you may encounter an error page as a result.

ウェブページにアクセスするとき、スピードは重要な要素です。そのため、http_request の処理にクエリーコールを使用しています。ただし、クエリーコールは合意形成プロセスを経ないため、署名を作成できないことに注意が必要です。この問題に対処するため、私たちは認証済み変数を使用しています。つまり、呼び出しが行われる前に、コンテンツの認証が必要なのです。場合によっては、この認証プロセスができないこともあり、ic0.app の下でウェブサイトにアクセスする場合、結果としてエラーページが表示されることがあります。

<p align="center"> <img src="./img/body_no_verification.png" width="800px" style="border: 2px solid black;"> </p>

<p align="center" > In that case you should access under raw.ic0.app to avoid the issue.  
その場合、raw.ic0.app でアクセスすることで問題を回避できます。</p>

> It's worth noting that the service worker received when accessing ic0.app could potentially be altered by the boundary node to certify incorrect responses. This is a potential issue since most users won't take the time to verify the authenticity of the service worker. To mitigate this risk, it would be ideal to have the public key of the Internet Computer directly integrated into the hardware or browser! This would provide an expectional level of security and be a convenient option, giving users peace of mind and the confidence to trust the authenticity of the content they are accessing!"

> ic0.app にアクセスしたときに受け取ったサービスワーカーが、バウンダリーノードによって不正な応答を証明するために変更される可能性があることは注目に値します。これは、ほとんどのユーザーがサービスワーカーの信頼性を確認する時間を取らないため、潜在的な問題です。このリスクを軽減するためには、Internet Computer の公開鍵をハードウェアやブラウザに直接組み込むことが理想的です！これにより、期待されるレベルのセキュリティが提供され、便利なオプションとなり、ユーザーに安心感を与え、アクセスしているコンテンツの真正性を信頼する自信を与えることができます！"

## 🤙 Contacting the canister / 🤙 キャニスターにコンタクト
Once the boundary node has received the request. It will encode it into Candid and automatically call the http_request method of the canister. reachable by browsers, you need to implement an `http_request` method as part of the public interface of your  actor.  
バウンダリーノードがリクエストを受信すると、それを Candid にエンコードして、キャニスターの http_request メソッドを自動的に呼び出します。ブラウザからアクセスできるようにするには、アクターのパブリックインターフェースの一部として`http_request`メソッドを実装する必要があります。<br/>

This is the minimum code needed to return a simple page that prints **Hello world**.  
これは、**Hello world** をプリントするシンプルなページを返すために必要な最小限のコードです。
```motoko 
import Text "mo:base/Text";
import Http "http";
actor {
    public type HttpRequest = Http.HttpRequest;
    public type HttpResponse = Http.HttpResponse;

    public query func http_request(req : HttpRequest) : async HttpResponse {
        return({
            body = Text.encodeUtf8("Hello World");
            headers = [];
            status_code = 200;
            streaming_strategy = null;
        });
    };
};
```
Here is the content of the `HTTP` module, the file name is `http.mo`.  
以下は `HTTP` モジュールの内容であり、ファイル名は `http.mo` です。
```motoko
module Http {
    public type HeaderField = (Text, Text);

    public type HttpRequest = {
        body: Blob;
        headers: [HeaderField];
        method: Text;
        url: Text;
    };

    public type HttpResponse = {
        body: Blob;
        headers: [HeaderField];
        status_code: Nat16;
        streaming_strategy: ?StreamingStrategy;
    };

    public type StreamingStrategy = {
        #Callback: {
            callback : StreamingCallback;
            token    : StreamingCallbackToken;
        };
    };

    public type StreamingCallback = query (StreamingCallbackToken) -> async (StreamingCallbackResponse);

    public type StreamingCallbackToken =  {
        content_encoding : Text;
        index            : Nat;
        key              : Text;
    };

    public type StreamingCallbackResponse = {
        body  : Blob;
        token : ?StreamingCallbackToken;
    };
}
```