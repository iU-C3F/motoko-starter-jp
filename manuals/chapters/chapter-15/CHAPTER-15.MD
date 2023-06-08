# Chapter 15: Managing multiple canisters with actor classes. / 第15章 アクタークラスで複数のキャニスターを管理する。
## Actor classes. / アクタークラス
## The management canister 👨‍💼 / マネージメントキャニスター
The management canister is used on the IC to perform the following operations:  
マネージメントキャニスターは、IC 上で以下の動作を行うために使用されます：
- Create canisters from another canister.
- 別のキャニスターからキャニスターを作成する。
- Install code inside other canisters (that you have control over!).
- 他のキャニスターの中にコードをインストールする（あなたがコントロールできるもの！）。
- Get informations on canister such as:
- 以下など、キャニスターに関する情報を得ます：
    - The status of a canister (running, stopping, stopped).
    - キャニスタのステータス (実行中、停止中、停止中)。
    - A SHA256 hash of the module installed on the canister.
    - キャニスタにインストールされたモジュールの SHA256 ハッシュ。
    - The controllers of the canister.
    - キャニスターのコントローラ。
    - The memory size taken by the canister.
    - キャニスターが使用するメモリ・サイズ。
    - The cycle balance of the canister.
    - キャニスターの Cycle の残高。
- Create [ECDSA](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-sign_with_ecdsa) signatures derived from the canister.
- キャニスターに由来する [ECDSA](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-sign_with_ecdsa) 署名を作成します。
- Create [http_request](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-sign_with_ecdsa)
- [http_request](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-sign_with_ecdsa) を作成します。 
- Interact with [the Bitcoin API](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-bitcoin-api)
- [Bitcoin API](https://internetcomputer.org/docs/current/references/ic-interface-spec#ic-bitcoin-api) と連動します。
- And way more! 
- そして、もっともっと！

> The IC management canister doesn't actually exists as a "canister". It doesn't contain a wasm module or memory 

> IC マネージメントキャニスターは、実際には「キャニスター」として存在しません。WASM モジュールまたはメモリにも入っていません。

- it's only an interface to make it easier to communicate with a management API on the IC. The IC management canister address is aaaaa-aa.  
- それは、IC 上の管理 API との通信を容易にするためのインターフェースに過ぎません。IC のマネージメントキャニスターのアドレスは aaaaa-aa です。 


Here is an example of how to use the managament canister inside an other actor.  
ここでは、マネージメントキャニスターを他のアクターの中で使用する例を紹介します。
```motoko
actor {
    let managementCanister = actor {
        create_canister : {} -> async {canister_id : Principal};
        stop_canister : { canister_id : Principal } -> async ();
        delete_canister : { canister_id : Principal } -> async ();
    };

// Create - Stop - Burn 🥲
    public func createStopBurn() : async () {
        let cid = await mangagementCanister.create_canister;
        await IC.stop(cid);
        await IC.delete_canister(cid) 
    };
};
```

Once you've created other canisters from within your canister you can install a wasm module inside of them. This requires that the module is already loaded inside your main canister. This pattern is used by a lot of applications on the IC to create multicanister dApps (OpenChat...)!  
キャニスターの中から他のキャニスターを作成したら、その中に wasm モジュールをインストールできます。この場合、メインキャニスターの中にモジュールが既にロードされている必要があります。このパターンは IC 上の多くのアプリケーションでマルチキャニスターの dApps （OpenChat...）を作成するために使用されています！

## Creating a canister factory. / キャニスターファクトリーの作成
（訳註：原文はまだ作成中だと思われる ）