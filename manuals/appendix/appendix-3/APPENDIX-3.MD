# Appendix 3: A new chapter in digital identity: Internet Identity. / 付録3：デジタル ID の新章： Internet Identity
## The end of username & passwords. / ユーザー名とパスワードの終焉。
Identity is at the core of our digital lives. In the rapidly evolving world of the internet, it has become more important than ever to have secure and trustworthy methods of accessing our personal accounts and spaces.  
ID は、私たちのデジタルライフの核となるものです。急速に進化するインターネットの世界では、個人のアカウントやスペースにアクセスするための安全で信頼できる方法を持つことが、これまで以上に重要になってきています。<br/>
For years, the traditional way of logging into websites has been with passwords & usernames.  
長年、ウェブサイトへのログインは、パスワードとユーザー名で行うのが伝統的な方法でした。

<p align="center"> <img src="assets/password_username.jpeg" width="400px" style="border: 2px solid black;"></p>
<p align="center"> You are probably familiar with that type of interface.</p>
<p align="center"> そのようなインターフェースは、皆さんもよくご存じでしょう。</p>

To create effective and secure passwords, one should:  
効果的で安全なパスワードを作成するには、下記が必要です：
- Select a long and randomly generated password.
- 長く、ランダムに生成されるパスワードを選択する。
- Avoid using the same password across multiple websites.
- 複数の Web サイトで同じパスワードを使用することは避ける。

However, even when respecting basic security rules, this method of login has fundamental issues:  
しかし、基本的なセキュリティルールを尊重しても、このログイン方法には根本的な問題があります：
1. The server that grants authentication must store the username and password combination to verify the login and grant access. Although the password is often stored as a  hash, data breaches and leaks are still common. / 認証を付与するサーバーは、ログインを検証してアクセスを許可するために、ユーザー名とパスワードの組み合わせを保存する必要があります。パスワードはハッシュとして保存されることが多いが、データ侵害や漏洩が後を絶ちません。
2. Remembering and keeping track of passwords is a challenge, as most people have multiple accounts on various platforms, making it difficult to recall all of them. This is why the use of password managers and logging in through big tech companies (Apple, Facebook, Google, Microsoft) has become more prevalent. / パスワードを覚えて管理するのは大変なことです。ほとんどの人がさまざまなプラットフォームで複数のアカウントを持っているため、すべてのパスワードを思い出すのは困難です。そのため、パスワードマネージャーの使用や、大手テック企業（Apple、Facebook、Google、Microsoft）を通じたログインが普及しているのです。
3. Using passwords on a decentralized infrastucture like the Internet Computer is a bad idea. We are evolving in a world where we assume that some nodes can be malicious. If we need to send the password to all nodes, then it might leak at this point. / Internet Computer のような分散型インフラストラクチャでパスワードを使用するのは悪い考えです。私たちは、一部のノードが悪意を持っている可能性があることを前提とした世界で進化しているのです。もし、すべてのノードにパスワードを送る必要があるなら、この時点でパスワードが漏れてしまうかもしれません。  

## Login with BigTech / BigTech でログイン
As a result, the use of password managers and logging in through big tech companies like Apple, Facebook, Google, or Microsoft has become more prevalent. However, this method of login has its drawbacks as well. It requires people to trust these big tech companies with their personal information and access to other websites.  
その結果、パスワードマネージャーを使用したり、Apple、Facebook、Google、Microsoft などの大手テック企業を通じてログインすることが一般的になってきました。しかし、このようなログイン方法には欠点もあります。それは、個人情報や他のウェブサイトへのアクセスについて、これらの大手テック企業を信頼する必要があることです。

<p align="center"> <img src="./assets/login_bigtech.png" width="300px" style="border: 2px solid black;"> </p>

With the increasing number of information we put online, do we really want to trust a  handful of private companies?  
ネットに流す情報が増えている中、一握りの民間企業を本当に信頼できるのでしょうか。

<p align="center"> <img src="./assets/facebook_meme.jpeg" width="300px" style="border: 2px solid black;"> </p>

## Digital signatures / デジタル署名
Digital signatures are a more secure alternative to traditional username and password authentication. Digital signatures use a cryptographic technique to verify the authenticity of a message or document, ensuring that it has not been tampered with and that it comes from a verified sender. They are widely used in electronic transactions, such as online banking and e-commerce, as they provide a higher level of security and protection against fraud.  
デジタル署名は、従来のユーザー名とパスワードによる認証に代わる、より安全な方法です。デジタル署名は、暗号化技術を使用してメッセージや文書の真正性を検証し、改ざんされていないこと、検証された送信者からのものであることを確認します。より高度なセキュリティと不正行為からの保護を実現するため、オンラインバンキングや電子商取引などの電子取引で広く使用されています。

As the Internet Computer is built on a lot of cryptography, you won't be surprised to learn that they are used as a authentication mechanism for messages.  
Internet Computer は多くの暗号技術の上に成り立っているので、メッセージの認証メカニズムとして使われていることに驚くことはないでしょう。

A digital signature scheme relies on 3 algorithms:  
デジタル署名の仕組みは、3つのアルゴリズムに依存しています： 
1. **Key generation**: This algorithm is used to generate a public key and a private key. The public key is used to verify the digital signature, while the private key is used to create the digital signature. / **鍵の生成**： このアルゴリズムは、公開鍵と秘密鍵を生成するために使用されます。公開鍵は電子署名の検証に使用され、秘密鍵は電子署名の作成に使用されます。

2. **Signature**: This algorithm is used to create the digital signature using the private key. It applies a mathematical formula to the data that needs to be signed and the private key to generate a unique digital signature. / **署名**： 秘密鍵を使って電子署名を作成するためのアルゴリズムです。署名が必要なデータと秘密鍵に数式を適用し、一意のデジタル署名を生成します。

3. **Verification**: This algorithm is used to verify the digital signature using the public key. It applies a mathematical formula to the signed data, the digital signature, and the public key. If the output of the formula matches the original data, the digital signature is considered valid and the data is considered authentic. / **検証**： このアルゴリズムは、公開鍵を使用したデジタル署名の検証に使用される。署名されたデータ、電子署名、公開鍵に数式を適用する。数式の出力が元のデータと一致した場合、デジタル署名は有効であり、データは本物であるとみなされる。

<p align="center"> <img src="./assets/digital_signatures.png" width="800px" style="border: 2px solid black;"></p>

Of course, digital signatures have been already used intensively in the world of crypto! Everyone should know the famous saying: [Not your keys not your crypto](https://www.ledger.com/academy/not-your-keys-not-your-coins-why-it-matters). 
Users owning and mangaging their keys is great for security & decentralization, however it's not that easy.  
もちろん、デジタル署名は暗号の世界ではすでに盛んに使われています！誰もが有名なことわざを知っているはずです： [Not your keys not your crypto](https://www.ledger.com/academy/not-your-keys-not-your-coins-why-it-matters) 。
ユーザーが自分の鍵を所有し管理することは、セキュリティと分散化のために素晴らしいことですが、しかし、それはそれほど簡単なことではありません。<br/> The main problem is keeping them secure & accessible.  
主な問題は、それらを安全に保ち、アクセスできるようにすることです。

<p align="center"> <img src="./assets/lost_bitcoins.jpeg" width="800px" style="border: 2px solid black;"></p>
<p align="center"> If you loose your keys, there is no backup! </p>
<p align="center">鍵を紛失しても、バックアップがない！</p>

If we want to manage our entire digital identities using cryptographic keys while onboarding millions of people into Web3, it seems that there is a challenging project to solve here! How do we keep the benefits of digital signatures while making it easier to use for everyone?  
何百万人もの人々を Web3 に取り込みながら、暗号鍵を使ってデジタル ID 全体を管理したいのであれば、ここには解決すべき困難なプロジェクトがあるように思われます！デジタル署名の利点を維持しつつ、誰もが使いやすいものにするにはどうしたらいいのでしょうか？

## Web Authentication / ウェブ認証
[WebAuthentication](https://webauthn.guide/), also known as WebAuth, is a web standard that attempts to solve the issues raised earlier and standardize logins using public-key cryptography.  
[WebAuthentication](https://webauthn.guide/) は、WebAuth とも呼ばれ、先に挙げた問題を解決し、公開鍵暗号を用いたログインを標準化しようとする Web 標準です。

- When a user first register to a WebAuthn-enabled service: 
- WebAuthn 対応サービスにユーザーが初めて登録するとき： 
    1. A key pair is generated for you. / キーペアが生成されます。
    2. The private key is stored securely on your device. / 秘密鍵は、お客様の端末に安全に保管されます。
    3. The public key is sent to the service and associate it with the user's account. / 公開鍵はサービスに送信され、ユーザーのアカウントと関連付けられます。

<p align="center"> <img src="./assets/webAuthn_registration.png" width="400px" style="border: 2px solid black;"></p>


- When the same user wants to login again:
- 同じユーザーが再度ログインを希望する時：
    1. A challenge is generated by the service. / 1. サービスによりチャレンジが生成されます。
    2. The device attemps to verify your identity through authentication factors (FaceID, TouchID, YubiKey, Windows Hello...) / デバイスは認証要素（FaceID、TouchID、YubiKey、Windows Hello...）を通じて本人確認を試みます。
    3. If the verification is correct, the device will sign the challenge and send it back to the service. / 認証が正しい場合、デバイスはチャレンジに署名してサービスに送り返します。
    4. If the signature is correct, the service will grant access. / 署名が正しい場合、サービスはアクセスを許可します。

<p align="center"> <img src="./assets/webAuthn_signature.png" width="400px" style="border: 2px solid black;"></p>

The device usually integrates a secure chip that stores the private key. Those chips are designed to **never leak the private key**, they are only able to create signature when requested.  
デバイスは通常、秘密鍵を格納する安全なチップを内蔵しています。これらのチップは、秘密鍵を絶対に漏らさないように設計されており、要求されたときだけ署名を作成できます。

WebAuthentication is both secure & convenient.  
WebAuthenticationは、安全性と利便性を兼ね備えています。

## Messages on the Internet Computer / Internet Computer 上のメッセージ
As we mentionned on  day 1, all requests sent to the Internet Computer are passed through messages. All those messages are signted.  
１日目に述べたように、Internet Computer に送られるすべてのリクエストは、メッセージを通して渡されます。そのメッセージはすべて署名されています。

<p align="center"> <img src="./assets/message_authenticated.png" width="800px" style="border: 2px solid black;"></p>

A message contains the following information:  
メッセージには、以下の情報が含まれます：
- ID of the target canister.
- 対象のキャニスターの ID。
- Function called on this canister.
- このキャニスターで呼び出された関数。
- Arguments provided for this functions. 
- この関数に提供される引数。
- A nonce that can be used to distinguish other two similar messages.
- 他の２つの類似したメッセージを区別するために使用できる nonce。

But more importantly, the message contains a signature! We can use this signature to verify the identity of the caller.  
しかし、もっと重要なのは、メッセージに署名が含まれていることです！この署名を使って、発信者の身元を確認することができるのです。

> There is an identity which is called the **Anonymous** identity, and allows communication with the Internet Computer in a completely anonymous manner. The textual representation of principal associated with this identity is **2vxsx-fae**. You can try the `whoami` method yourself from the [Candid UI](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/?id=sm7ch-cyaaa-aaaaj-qaz3q-cai) - when interacting from the Candid UI you are not authenticated so you should see the anonymous principal.

> Internet Computer との通信を完全に匿名で行うことができる、**Anonymous** と呼ばれる ID が存在します。この ID に関連する Principal のテキスト表現は、**2vxsx-fae** です。[Candid UI](https://a4gq6-oaaaa-aaaab-qaa4q-cai.raw.ic0.app/?id=sm7ch-cyaaa-aaaaj-qaz3q-cai) から `whoami` メソッドを試すことができます。Candid UI から対話する場合、あなたは認証されていないので、匿名プリンシパルが表示されるはずです。

## Delegations / デリゲーション
With WebAuthentication, whenever the user creates a signature his identity will be verified through the authentication factors that've mentionned before, usually asking the user for confirmation.  
WebAuthentication を使用すると、ユーザーが署名を作成するたびに、先に述べた認証要素によって身元が確認され、通常はユーザーに確認を求めることができます。  
Let's imagine that our user wants to do the 3 following actions:  
ユーザーが次の3つのアクションを行いたい場合を考えてみましょう：
1. Log in into DSCVR. / DSCVRにログインします。
2. Update his user profile. / 彼のユーザープロフィールを更新する。
3. Post a message. / メッセージを投稿する。

<p align="center"> <img src="./assets/withoutII_hell.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> Every single interaction with the network would require an user validation  🤦‍♂️ / ネットワークとのやりとりのたびに、ユーザー認証が必要になる 🤦‍♂️</p>

Since all messages are signed on the Internet Computer it would mean that we have to confirm our identity everytime that we interact with any canister! That would quickly be annoying for users.  
すべてのメッセージは Internet Computer 上で署名されるため、キャニスターとやりとりするたびに、自分の身元を確認しなければならないことになります！これでは、ユーザーにとって迷惑な話です。<br/>

The solution? **Delegation**!  
その解決策は？**デリゲーション**（委任） です！  
A delegation is a short-term pair of keys, that we create when an user log in. This pair of keys is stored locally and can be used for performing any number of actions, during a specific timeframe.  
デリゲーションとは、ユーザーがログインする際に作成される、短期間の鍵のペアです。この鍵のペアはローカルに保存され、特定の時間枠の中で、任意の数のアクションを実行するために使用できます。  
The document that grants delegation is signed by the master pair of keys.  
デリゲーションを許可するドキュメントは、マスター鍵ペアによって署名されます。

## Canister signature / キャニスターの署名
Each subnet is able to create a signature that certifies a piece of data coming from the Internet Computer. A canister can request the subnet it is hosted in to create a signature on a specific data; this mechanism is called [certified variables](https://internetcomputer.org/how-it-works/response-certification/).  
各サブネットは、Internet Computer から来るデータの一部を証明する署名を作成することができます。キャニスターは、ホストされているサブネットに特定のデータに対する署名を作成するよう要求できます。このメカニズムは、[certified variables](https://internetcomputer.org/how-it-works/response-certification/) と呼ばれています。

Building upon this mechanism, canisters are able to create signatures.  
この仕組みをベースに、キャニスターは署名を作ることができるのです。
> If you want to know more about certified variables, check out this video & this repository.
[TODO: ADD MORE IMAGE OR TEXT]

> 認証変数についてもっと知りたい方は、このビデオとこのリポジトリをチェックしてください。
[TODO: ADD MORE IMAGE OR TEXT]

Making use of WebAuthn, delegations & canister signatures, DFINITY has designed an identity solution called **Internet Identity**.  
DFINITY は、WebAuthn、デリゲーション、キャニスター署名を活用し、**Internet Identity** という ID ソリューションを設計しました。<br/>
Internet Identity allows users to create sessions with Web3 services and dapps, and sign traditional blockchain transactions.  
Internet Identity により、Web3 サービスや Dapps とのセッションを作成したり、従来のブロックチェーントランザクションに署名できます。
## Internet Identity
Internet Identity is a canister that manages your pair of keys and allows you to create short-term delegations top log in into other canisters. It does not store the private keys are those are securely stored on your device(s). 
Whenever you try to log in to a service through Internet Identity: a session key pair will be created on your device and stored locally, then once you've confirmed the log in you'll request the Internet Identity to create a signature and grant a delegation to your short 

Internet Identity は、鍵のペアを管理するキャニスターであり、他のキャニスターにログインするための短期委任を作成できます。秘密鍵はデバイスに安全に保存されるため、Internet Identity は秘密鍵を保存しません。
Internet Identity を通じてサービスにログインしようとするたびに、セッション鍵ペアがデバイスに作成され、ローカルに保存されます。ログインが確認されると、Internet Identity に署名の作成 と 短期間の委任を付与するよう 要求します。

1. Creation of an anchor: this is your identity to which you'll be able to add devices. / アンカーを作成：これは、デバイスを追加できるあなたの ID です。

2. Registration of device(s) to your anchor. / デバイスをアンカーに登録。
- You can register multiple devices to your identity. All registered devices have access to your identity.
- ID には、複数のデバイスを登録することができます。登録されたすべてのデバイスは、あなたの ID にアクセスできます。
- You need to have at least one registered device at any time - otherwise you'll not be able to access your identity and you'll have to use one the backup mechanisms that you've (hopefully) put in place.
- 常に少なくとも１台のデバイスを登録する必要があります。そうしないと、自分の ID にアクセスできなくなり、(できれば) 用意されているバックアップメカニズムを使用する必要があります。
- You can remove registered devices whenever you need. 
- 登録したデバイスは、必要なときにいつでも削除できます。

3. Connect to a dApp / dAppに接続する
    1. You are visiting your favorite application and want to log in using Internet Identity. / お気に入りのアプリケーションにアクセスし、Internet Identity を使用してログインしたい。
    2. Your identity is verified (Biometric authentication / USB security keys) / 本人確認（生体認証/USBセキュリティキー）を行います。
    3. A local short-term key pair is created. / ローカルの短期キーペアが作成されます。
    4. A **signed** message from your master key pair is sent to the Internet Identity canister, asking the canister to create a delegation for your local key pair. / マスターキーペアの **signed** メッセージが Internet Identity キャニスターに送信され、キャニスターにローカル キーペアのデリゲーションを作成するよう依頼する。
    5. The delegation is sent back to your device and stored. / デリゲーションはデバイスに送り返され、保存されます。
    6. You can now use the application with your local key pair and send along the delegation. You don't have to request a signature using WebAuthn for each message that you send. / これで、ローカル鍵ペアでアプリケーションを使用し、デリゲーションに沿って送信できます。送信するメッセージごとに WebAuthn を使って署名を要求する必要はありません。

[TODO : ADD ILLUSTRATIONS]