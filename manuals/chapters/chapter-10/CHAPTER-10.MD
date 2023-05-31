# Chapter 10: Identity on the Internet Computer. / 第10章：Internet Computer 上のID 
## Your keys = Your identity / あなたの鍵 ＝ あなたの ID

Whether you are interacting with the Internet Computer using [Internet Identity](https://internetcomputer.org/docs/current/tokenomics/identity-auth/what-is-ic-identity), `dfx`, or even [Plug wallet](https://plugwallet.ooo/), your identity is represented by a key pair consisting of:  
[Internet Identity](https://internetcomputer.org/docs/current/tokenomics/identity-auth/what-is-ic-identity)、`dfx`、あるいは [Plug wallet](https://plugwallet.ooo/) を使って Internet Computer とやりとりする場合でも、あなたの ID は、以下のものからなる鍵ペアで表現されます：

<p align="center"> <img src="./assets/identity_recap.png" width="600px" style="border: 2px solid black;"> </p>

- A **private key**, which grants you access to all the ICPs you own, allows you to manage canisters, and enables you to access your identity across various applications.
- **秘密鍵** は、所有するすべての ICP へのアクセスを許可し、キャニスターを管理し、さまざまなアプリケーションで自分の ID にアクセスできるようにするものです。
- A **public key**, from which your **principal** is derived.
- **公開鍵**。ここからあなたの **Principal** が導き出されます。

## Managing identities with dfx / dfx によるID の管理
We can use `dfx` to create, delete and manage our identities, those identities are used to deploy, manage and interact with the canisters we deploy.  
私たちは `dfx` を使って ID を作成、削除、管理することができます。これらの ID は、私たちが配備したキャニスターを配備、管理、対話するために使われます。

### Creating an identity / ID の作成
To generate a new identity you can run the following command  
新しい ID を生成するには、次のコマンドを実行します。
```bash
$ dfx new identity <NAME>
```
> You can include the --disable-encryption flag when executing the command to prevent encryption of the file containing your private key. Otherwise, the file will be encrypted, and you will be prompted for a password every time a command requiring a signature is used.

> 秘密鍵を含むファイルの暗号化を防ぐために、コマンド実行時に --disable-encryption フラグを含めることができます。そうでない場合は、ファイルは暗号化され、署名を必要とするコマンドを使用するたびにパスワードの入力を求められるようになります。

The private key generated for this identity will be automatically saved in the `.config/dfx/identity/<NAME> directory`. This private key is stored as a PEM file, a specific format used for storing keys. The file may be encrypted or unencrypted, based on the flag you choose.  
この ID のために生成された秘密鍵は、自動的に`.config/dfx/identity/<NAME>ディレクトリ`に保存されます。この秘密鍵は、鍵を保存するために使用される特定のフォーマットである PEM ファイルとして保存されます。このファイルは、選択したフラグによって暗号化されたり非暗号化されたりすることがあります。  

For example, the PEM file corresponding to the `default` identity, which is an identity automatically created when you install `dfx`, has a private key stored within that resembles the following:  
例えば、`dfx`をインストールしたときに自動的に作成される ID である `default` に対応する PEM ファイルには、次のような秘密鍵が格納されている：
```
-----BEGIN EC PRIVATE KEY-----
MHQCAQEEIPkmcU+rvYCcvylnVClTrleDyWqmelhQmigzMvq8zFC3oAcGBSuBBAAK
oUQDQgAE5knNEHs+kzvCteeu4e650NzqGvLhlzoWXXKupjCreV1dhuH5oIHIVyoM
ldnRBAE39QwyGwkQoxWhmo+Sl9F4zA==
-----END EC PRIVATE KEY-----
```  

### Switching between identities / ID の切り替え
To check the current used identity, execute:  
現在使用されている ID を確認するには、下記を実行します：
```bash
$ dfx identity whoamis 
```
（訳注：誤字。whoamis ではなく whoami）

To view other available identities, run:  
その他の利用可能なIDを表示するには、下記を実行します：
```bash
$ dfx identity list
```
Finally, switch the active identity using:  
最後に、アクティブIDを使用して切り替えます：
```bash
$ dfx identity use <NAME> 
```

## From Public Key to Principal / 公開鍵からPrincipal へ
With `dfx`, you can access a unique identifier for each identity called **principal**:  
`dfx`では、**principal** と呼ばれる各 ID に固有の識別子にアクセスできます：
```motoko
$ dfx identity get-principal
2ujkt-fujau-bunuv-gt4b6-2s27j-cv5qi-kddkp-jl7m4-wdj3e-bqdrt-qqe
```
A principal identifies entities interacting with the Internet Computer and is directly derived from the public key. These entities can be users or canisters. Different types of principals include:  
Principal は、Internet Computer と相互作用するエンティティを識別し、公開鍵から直接導出されます。これらのエンティティは、ユーザまたはキャニスターです。異なるタイプの Principal は以下の通り：

A principal is a public identifier used to identify entities that can interact with the Internet Computer. The principal is derived directly from the public key. These entities are either users or canisters. We distinguish different types of principals:  
Principal は、Internet Computer と相互作用できるエンティティを識別するために使用される公開識別子です。Principal は、公開鍵から直接導かれます。これらのエンティティは、ユーザまたはキャニスターのいずれかです。私達は、異なるタイプの Principal を区別します：
- **Self-authenticating IDs** (User): Derived directly from a user's public key, such as your dfx identity's principal. These principals are 29 bytes long.
- **自己認証 ID**（ユーザー）： dfx ID の Principal など、ユーザーの公開鍵から直接導出されます。これらの Principal は 29 バイト長です。
- **Opaque IDs** (Canister): A canister's principal is its canister ID, determined automatically based on its subnet and the number of deployed canisters.
- **不透明な ID**（キャニスタ）： キャニスターの Principal はキャニスター ID で、サブネットと配備されたキャニスターの数に基づいて自動的に決定されます。
- **Anonymous ID** (Anonymous): The default caller when an unauthenticated user calls functions, such as fetching information from a canister before logging in. The canister recognizes the caller as the Anonymous ID since the user's principal is unknown until login.
- **Anonymous ID**（アノニマス）： 認証されていないユーザが、ログイン前にキャニスターから情報を取得するなどの機能を呼び出す際のデフォルトの呼び出し元です。ログインするまでユーザの Principal は不明であるため、キャニスターは呼び出し元をアノニマス ID として認識します。

> Two [additional principal types](https://internetcomputer.org/docs/current/references/ic-interface-spec#id-classes) exist but are rarely encountered. They are used internally by the protocol or reserved for future use.

> ２つの [追加の Principal 型](https://internetcomputer.org/docs/current/references/ic-interface-spec#id-classes) が存在するが、めったに遭遇することはありません。これらはプロトコルの内部で使用されるか、将来の使用のために予約されています。

## Principal in Motoko / Motoko の Principal 
In Motoko, principals are a primitive type called `Principal`.  
Motokoでは、Principal は`Principal`というプリミティブな型です。<br/>
Within an actor, access the principal of a function caller using the `shared (message)` syntax placed between the `public` and `func` keywords. This enables message inspection, where `message.caller` represents the principal of the calling entity (user or canister).  
アクター内で、`public` と `func` キーワードの間に置かれた `shared (message)` 構文を使って、関数呼び出し元の Principal にアクセスします。これにより、メッセージの検査が可能になり、`message.caller` は呼び出し側のエンティティ（ユーザーまたはキャニスター）の Principal を表します。

```motoko
actor {
    public shared (message) func whoIsCalling() : async Principal {
        let p = message.caller;
        return p;
    };
};
```
> Message is a special object that is available to all `public shared functions`. As of today, it is only used for accessing the `caller` property but it might have other use cases in the future.  
> message は、すべての `public shared functions` で利用可能な特別なオブジェクトです。現在のところ、`caller`プロパティにアクセスするためにのみ使用されていますが、将来的には他のユースケースがあるかもしれません。

Use object destructuring to access the caller directly for shorter syntax:  
オブジェクトのデストラクチャリングを使用して呼び出し元に直接アクセスすることで、より短いシンタックスを実現します：
```motoko
actor {
    public shared ({ caller }) func returnCallerPrincipal() : async Principal {
        return caller;
    };
};
```
Use `Principal.toText()` and `Principal.fromText()` from the [Principal module](https://7po3j-syaaa-aaaal-qbqea-cai.ic0.app/base-library/primitive-types/principal.html?highlight=Principal#principal) to convert between `Principal` and its textual representation.  
`Principal`とそのテキスト表現との変換には、[Principal モジュール](https://7po3j-syaaa-aaaal-qbqea-cai.ic0.app/base-library/primitive-types/principal.html?highlight=Principal#principal)の `Principal.toText()` と `Principal.fromText()` を使用します。

```motoko
let p : Principal = message.caller;
let textualRepresentation : Text = Principal.toText(p); // => "un4fu-tqaaa-aaaab-qadjq-cai"
let standardRepresentation : Principal = Principal.fromText(textualRepresentation); 
```

## The Anonymous identity / アノニマスの ID 
As mentioned earlier, the anonymous identity is associated with a specific principal and is used for unauthenticated calls to the Internet Computer. To determine if a caller is authenticated, use the `Principal.isAnonymous()` function, which returns a `Bool` indicating the user's anonymity.  
先に述べたように、アノニマス ID は特定の Principal に関連付けられ、Internet Computer への認証されていない呼び出しに使用されます。呼び出し元が認証されているかどうかを判断するには、 `Principal.isAnonymous()` 関数を使用します。この関数は、ユーザーのアノニマス性を示す `Bool` 値を返します。
```motoko
let p : Principal = message.caller;
let isAnonymous : Bool = Principal.isAnonymous(p);
if(isAnonymous){
    return ("Sorry only authenticated users can access this app!");
};
```

> The textual representation of the anonymous principal is `2vxsx-fae`. Make sure to remember it as you will often come accross it.

> アノニマスPrincipal のテキスト表現は `2vxsx-fae` です。よく目にするので、必ず覚えておいてください。