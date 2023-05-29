# Appendix 2: Unlocking the power of DAOs with canisters. / 付録2： キャニスターで DAO の力を引き出す。
## 🧩 What is DAO? / DAO とは？
> During this week you will have the opportunity to build a prototype for a Decentralized Autonomous Organization (DAO). This is why we want to answer an important question: **What is a DAO?**

> この１週間で、皆さんは分散型自律組織（DAO）のプロトタイプを作る機会を得ます。そのため、重要な質問に答えたいと思います： **DAOとは何なのか？**

## 🏛️ Decentralized Autonomous Organization: a new model of governance? / 分散型自律組織：新しいガバナンスのモデル？

<p align="center"> <img src="./assets/dao_icon.png" width="300px" style="border: 2px solid black;"> </p>

Throughout history, humans have find different creative ways to organize in social groups and structures. They have done so different reasons such as safety, support, social identity, work, power or even economic. A few common groups include: family unit, tribes, clans, states, guilds, secrect societies, political parties...  
歴史上、人類は社会集団や社会構造の中に、さまざまな創造的な組織化の方法を見出してきました。その理由は、安全、支援、社会的アイデンティティ、仕事、権力、あるいは経済的なものなど、さまざまです。一般的なグループには、家族単位、部族、氏族、国家、ギルド、世襲制社会、政党などがあります。

With the advent of the Internet, social networks, cryptocurriencies & smart contracts many believe that a new type of organization is about to start a new chapter of human history: **DAO**.  
インターネット、ソーシャルネットワーク、暗号化技術、スマートコントラクトの出現により、新しいタイプの組織が人類の歴史の新しい章を始めようとしていると多くの人が信じています： **DAO** です。

A Decentralized Autonomous Organization (DAO) is a digital organization that is composed of members living all around the world, and is governend and organized by smart contracts.  
DAO（Decentralized Autonomous Organization）とは、世界中に住むメンバーで構成され、スマートコントラクトによって統治・組織化されたデジタル組織です。

Because smart contracts execute automatically, are decentralized, transparent, can't be censored or modified by any individual the same applies to **DAOs** in the sense that they are not controlled by any single individual or entity, they rather operate based on the collective decision-making of their members.  
スマートコントラクトは自動的に実行され、分散化され、透明性が高く、いかなる個人によっても検閲や修正ができないため、**DAOs** も同様に、単一の個人または団体によって制御されず、むしろメンバーの集団意思決定に基づいて運営されることになります。

A few usecases for DAOs include:  
DAO の使用例としては、以下のようなものがあります：

- **Decentralized venture capital**: DAOs can be used to enable decentralized venture capital funds, in which members can propose and vote on investments in projects. [The DAO](https://en.wikipedia.org/wiki/The_DAO_(organization)) was one of the first DAOs to be created and was designed to be a decentralized venture capital fund, although it was controversial and ultimately failed due to a hack.
- **Decentralized venture capital**： DAOは、メンバーがプロジェクトへの投資を提案し投票することができる、分散型ベンチャーキャピタルファンドを実現するために使用できます。[The DAO](https://en.wikipedia.org/wiki/The_DAO_(organization)) は最初に作られた DAO の一つで、分散型ベンチャーキャピタルファンドとして設計されたが、物議を醸し、最終的にはハッキングにより失敗しました。
- **Decision-making**: DAOs can be used to enable members to make decisions about the direction of a project or organization. For example, MakerDAO is a decentralized finance (DeFi) platform that is built on the Ethereum blockchain and is governed by a DAO, in which members can vote on proposals to change the parameters of the MakerDAO system, such as the interest rates on loans.
- **Decision-making**： DAO は、メンバーがプロジェクトや組織の方向性について意思決定を行えるようにするために使用できます。例えば、MakerDAO は Ethereum ブロックチェーン上に構築された分散型金融（DeFi）プラットフォームで、DAO によって統治されており、メンバーはローンの金利など MakerDAO システムのパラメータを変更する提案に投票できます。

## 🙁 Limitations of DAOs / DAO の限界
As we've said DAOs are formed through smart contracts. However, smart-contracts are pretty limited:  
これまで述べてきたように、DAO はスマートコントラクトによって形成されます。しかし、スマートコントラクトはかなり限定的です：
- They can't store any meaningful amount of data (photos, videos, files...). [The cost of storing 1GB of data in the Ethereum blockchain has been estimated at around $5.5M](https://steemit.com/ethereum/@suryanshkumr/you-need-usd5-5m-to-save-1gb-data-in-ethereum-blockchain-d)
- 意味のある量のデータ（写真、ビデオ、ファイル...）を保存することができないのです。[Ethereum ブロックチェーンに 1GB のデータを保存するコストは約 5.5M と見積もられている](https://steemit.com/ethereum/@suryanshkumr/you-need-usd5-5m-to-save-1gb-data-in-ethereum-blockchain-d)
- It is not possible to interact with a smart contracts directly from a browser. A wallet needs to be installed and acts as relay.
- ブラウザから直接スマートコントラクトとやり取りすることはできません。ウォレットをインストールし、リレーとして機能させる必要があります。
- Smart contracts rely on oracles to gather information from the external world and facilitate communication with it, as they are unable to interact with anything outside of the blockchain on their own. 
- スマートコントラクトは、自力でブロックチェーン外のものと対話することができないため、オラクルに依存して外界からの情報を収集し、外界とのコミュニケーションを円滑にします。
- Smart contracts are limited in term of computational  power they have access to. 
- スマートコントラクトは、アクセスできる計算能力が制限されています。

Those technical limitations results in concrete actions that a DAO would be unable to do:  
その技術的な制約から、DAO ができない具体的なアクションが生まれます： 
- 🌳 **Interact with the physical world**: DAOs are limited to the digital world and cannot interact with the physical world. A DAO could not plant a tree, turn on a light switch, or deliver a physical letter.
- 🌳 **物理的な世界と相互作用する**： DAO はデジタル世界に限定され、物理的な世界と相互作用することはできません。DAO は木を植えたり、電気のスイッチを入れたり、物理的な手紙を届けたりすることはできません。
- 📲 **Access external data sources**: For example, a DAO could not retrieve the current temperature from a weather website, or the current stock price from a financial website.
- 📲 **外部データソースにアクセスする**： 例えば、DAO は天気予報のウェブサイトから現在の気温を取得したり、金融のウェブサイトから現在の株価を取得できません。
- 🔮 **Use advanced computational power**: For example, a DAO could not run simulations to predict the outcome of a complex system, such as the spread of a pandemic or the performance of a financial portfolio.
- 🔮 **高度な計算能力**を使用する： 例えば、パンデミックの広がりや金融ポートフォリオのパフォーマンスなど、複雑なシステムの結果を予測するためのシミュレーションを DAO が実行できません。
- 🗂️ **Handle large amounts of data**: For example, a DAO could not store and process the complete medical records of millions of patients.
- 🗂️ **大量のデータを扱う**： 例えば、DAO は数百万人の患者の完全な医療記録を保存して処理できません。

Those important limitations are preventing DAOs to have a meaningful impact in the world.  
そういった重要な制約が、DAO が世の中に意味のあるインパクトを与えることを妨げているのです。

## 🚀 From smart-contracts to canisters / スマートコントラクトからキャニスターまで
Imagine that smart-contracts could:  
スマートコントラクトができることを想像してください：
- Store unlimited amount of data & run any computation.
- 無制限にデータを保存し、あらゆる計算を実行できる。
- Be accessible directly from any browser.
- ブラウザから直接アクセスできる。
- Communicate with the external world trough HTTP requests.
- HTTP リクエストで外部と通信する。
- Create and sign transactions on any blockchain (Bitcoin, Ethereum...).
- あらゆるブロックチェーン（Bitcoin、Ethereum...）上のトランザクションを作成し、署名する。
- Being upgradable to constantly add new features & fix potential bugs.
- 常に新機能を追加し、潜在的なバグを修正するためにアップグレード可能であること。
- Remove fees and enable anyone to interact with them. 
- 手数料を取り除き、誰でもやり取りできるようにする。

Does it sound interesting? Welcome to the fabulous world of **canisters**!  
面白そうですか？ようこそ、**キャニスター**の素晴らしい世界へ！<br/>

<p align="center"> <img src="assets/canister.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> Imagine what DAOs will be able to achieve using canisters!</p>
<p align="center">DAO がキャニスターを使って何を実現するのか、想像してください！</p>
By using canisters, DAOs are now able to control entire web applications.

キャニスターを使うことで、DAOはWebアプリケーション全体をコントロールできるようになりました。

This means that future web services (social network, search engine, games, mail client, messaging application...) can run entirely on a set of canisters, where the governance of those canisters is ensured through a tokenized public governance canister.  
つまり、将来のウェブサービス（ソーシャルネットワーク、検索エンジン、ゲーム、メールクライアント、メッセージングアプリケーション...）は、完全にキャニスターのセットで実行でき、それらのキャニスターのガバナンスは、トークン化されたパブリックガバナンスキャニスターによって保証されます。<br/>

<p align="center"> <img src="assets/ois.png" width="800px" style="border: 2px solid black;"> </p>

This concept is called Open Internet Services. The aim is to end the current monopoly of BigTech companies (Facebook, Google, Apple, Twitter, Microsoft, Tiktok... ) that profits from the centralized aspect of the Internet. By aligning incentivizes between investors, users, and developers, those services are expected to operate in a more transparent, privacy-friendly and cooperative manner.  
このコンセプトは、「オープン・インターネット・サービス」と呼ばれています。その目的は、インターネットの中央集権的な側面から利益を得ている現在のビッグテック企業（Facebook、Google、Apple、Twitter、Microsoft、Tiktok...）の独占を終わらせることにあります。投資家、ユーザー、開発者の間でインセンティブを調整することで、これらのサービスは、より透明性が高く、プライバシーに配慮した、協力的な方法で運営されることが期待されます。

<p align="center"> <img src="assets/web2_web3.jpeg" width="400px" style="border: 2px solid black;"> </p>

> **A prediction?** <br/> Open Internet Services are powerful and won't stop with social networks or messaging apps. They are here to revolutionize the way we work and live together. With unprecedented scalability of collaborative work enabled by the combined power of DAOs and OISs, the sky's the limit! Imagine the positive impact on humanity with projects like environmental conservation, medical research, and education all being amplified by this new level of coordination and collaboration. And this is just the tip of the iceberg, as this new technology could open the door to even more innovative solutions to some of the world's most pressing problems. This is an opportunity to make real progress and change the world in ways we never thought possible before. **Get ready, the future is here!**

> **予言？**  <br/> オープンなインターネットサービスは強力で、ソーシャルネットワークやメッセージングアプリにとどまることはありません。オープン・インターネット・サービスは、私たちの働き方や暮らし方に革命を起こすものです。DAOとOISの力を結集して実現した前例のないスケーラビリティのある共同作業で、空は無限に広がっています！環境保護、医療研究、教育などのプロジェクトが、この新しいレベルの調整とコラボレーションによって増幅され、人類にポジティブな影響を与えることを想像してください。そして、これは氷山の一角に過ぎません。この新しいテクノロジーは、世界で最も差し迫った問題のいくつかに、さらに革新的な解決策をもたらす扉を開く可能性があります。これは、私たちがこれまで考えもしなかったような方法で、真の進歩を遂げ、世界を変えるチャンスなのです。**準備はいいか、未来はここにある！**