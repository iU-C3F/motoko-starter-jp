## Appendix 4: Network Nervous System (NNS) / 付録4 Network Nervous System (NNS)
<p align="center"> <img src="assets/nns_home.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> Home page of the NNS</p>
<p align="center">NNSのホームページ</p>

The most developed DAO operating on the IC (so far!) is the one that manages the network itself. This DAO is called the **Network Nervous System** and it is responsible for making decisions about the future of the network, coordinating various parties, and arranging the network's structure.  
IC 上で最も発達した（今のところ！）DAO は、ネットワークそのものを管理するものです。この DAO は **Network Nervous System** と呼ばれ、ネットワークの将来についての意思決定、様々な関係者の調整、ネットワークの構造のアレンジなどを行う役割を担っています。

Typically, when a blockchain needs to be upgraded, it takes a few weeks or months to complete the process. This requires node operators to upgrade their software. If some node operators refuse to upgrade or if a group of them install a different version, it can result in a "fork," where the blockchain splits into two separate chains - creating two completely different network of lower sizes.  
通常、ブロックチェーンのアップグレードが必要な場合、数週間から数ヶ月の期間を要します。そのため、ノードオペレータがソフトウェアをアップグレードする必要があります。一部のノードオペレータがアップグレードを拒否したり、オペレータのグループが異なるバージョンをインストールしたりすると、ブロックチェーンが２つのチェーンに分割される「フォーク」が発生し、規模の小さい全く異なる2つのネットワークが形成される可能性があります。

<p align="center"> <img src="assets/hard_fork.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> The 2017 Bitcoin fork split the community, with some advocating for increased block size, leading to the creation of two versions: the original Bitcoin and Bitcoin Cash with new rules</p>
<p align="center">2017年のビットコインフォークでは、ブロックサイズの拡大を主張する人もいてコミュニティが分裂し、オリジナルのビットコインと新しいルールのビットコインキャッシュの2種類が誕生することになりました</p>

On the Internet Computer, upgrades are voted on by the **Network Nervous System** (NNS). If the upgrades are accepted, the software of the nodes is directly upgraded, which mitigates the possibility of a fork.  
Internet Computer では、アップグレードは **Network Nervous System** (NNS) によって投票されます。アップグレードが受け入れられると、ノードのソフトウェアが直接アップグレードされるため、フォークの可能性が緩和されます。
<br/>
The NNS is governed by a liquid democracy, in which ICP holders stake their ICPs to create neurons.  
NNS は、ICP ホルダーが ICP をステーキングしてニューロンを作るというリキッド・デモクラシーで運営されています。  
The voting power of these neurons is based on :  
これらのニューロンの投票権は下記に基づくものです：
- The amount of staked ICPs.
- ICPのステーキング量。
- The duration of the staking.
- ステーキングの持続時間。
- The age of the neuron.
- ニューロンの年齢。

<p align="center"> <img src="assets/neuron_recap.png" width="800px" style="border: 2px solid black;"> </p>

The proposals that can be voted on by the **NNS** (**Network Nervous System**) are grouped into different categories, such as:  
**NNS**（**Network Nervous System**）で投票できる　提案は、以下のようにさまざまなカテゴリーに分類されています：
- 💸 Network economics: proposals related to determining the rewards paid to node operators.
- 💸 ネットワーク経済：ノードオペレータに支払われる報酬の決定に関連する提案。
- 👨‍💼 Node administration: proposals related to administering node machines, including upgrading or configuring the operating system, virtual machine framework, or node replica software.
- 👨‍💼 ノード管理：オペレーティングシステム、仮想マシンフレームワーク、ノードレプリカソフトウェアのアップグレードや設定など、ノードマシンの管理に関連するプロポーザル。
- 🌏 Subnet management: proposals related to administering network subnets, such as creating new subnets, adding and removing subnet nodes, or splitting subnets.
- 🌏 サブネット管理：新しいサブネットの作成、サブネットノードの追加と削除、サブネットの分割など、ネットワークのサブネットの管理に関する提案。
- 🧑‍⚖️ Governance: proposals related to administering governance, such as motions and configuring certain parameters.
- 🧑‍⚖️ ガバナンス：特定のパラメータの動作や設定など、ガバナンスの管理に関する提案。

To learn more about the incredible power of the NNS, check out the [Internet Computer Wiki](https://wiki.internetcomputer.org/wiki/Network_Nervous_System).  
NNS の驚くべきパワーについては、[Internet Computer Wiki](https://wiki.internetcomputer.org/wiki/Network_Nervous_System) でご確認ください。

The NNS is constitued of **different canisters**. Each canister is deployed on the same subnet which is also called the [NNS subnet](https://dashboard.internetcomputer.org/subnet/tdb26-jop6k-aogll-7ltgs-eruif-6kk7m-qpktf-gdiqx-mxtrf-vb5e6-eqe).  
NNS は **異なるキャニスター** で構成されています。各キャニスターは、[NNS サブネット](https://dashboard.internetcomputer.org/subnet/tdb26-jop6k-aogll-7ltgs-eruif-6kk7m-qpktf-gdiqx-mxtrf-vb5e6-eqe) とも呼ばれる同一のサブネットに配備されています。

<p align="center"> <img src="assets/nns_recap.png" width="800px" style="border: 2px solid black;"> </p>
<p align="center"> Overview of the canisters running the NNS</p>
<p align="center">NNSを動かすキャニスターの概要</p>

-  🏦 [Ledger](https://icscan.io/canister/ryjl3-tyaaa-aaaaa-aaaba-cai): This canister is responsible for controlling the balance of ICPs for all users, processing transactions, minting & burning ICPs.
- 🏦 [Ledger](https://icscan.io/canister/ryjl3-tyaaa-aaaaa-aaaba-cai)： 全ユーザーの ICP の残高管理、取引処理、ICP の発行・焼却を行うキャニスターです。
- 🏛️ [Governance](https://icscan.io/canister/rrkah-fqaaa-aaaaa-aaaaq-cai): This canister is responsible for keeping track of neurons, proposals & votes and ultimately taking actions when the proposals are accepted or rejected.
- 🏛️ [Governance](https://icscan.io/canister/rrkah-fqaaa-aaaaa-aaaaq-cai)： このキャニスターは、ニューロン、提案、投票を追跡し、最終的に提案が受け入れられたり拒否されたりしたときにアクションを起こす役割を果たします。
- 🏭[Registry](https://icscan.io/canister/rwlgt-iiaaa-aaaaa-aaaaa-cai): This canister is responsible for storing and modifying the configuration of the Internet Computer (Adding or removing nodes, adding or removing subnets, storing public keys of subnets, assign nodes to subnets, storing canister ids and which subnet they belong to....)
- 🏭[Registry](https://icscan.io/canister/rwlgt-iiaaa-aaaaa-aaaaa-cai)：このキャニスターは、Internet Computer の構成を保存し、変更する役割を果たします（ノードの追加と削除、サブネットの追加と削除、サブネットの公開鍵の保存、ノードのサブネットへの割り当て、キャニスターIDの保存とどのサブネットに属しているか...）。
- 🪟 [NNS-UI](https://icscan.io/canister/qoctq-giaaa-aaaaa-aaaea-cai): This canister is responsible for storing the official interface that gives users a way to interact with the 3 others canisters. 
- 🪟 [NNS-UI](https://icscan.io/canister/qoctq-giaaa-aaaaa-aaaea-cai)：このキャニスターは、ユーザーが他の3つのキャニスターと対話する方法を提供する公式インターフェイスを格納する役割を担っています。

> **NNS-UI** is the main interface for interacting with the **NNS**, but other user-friendly interfaces can be created. The community has already created an [interface that allows proposal creation without using a terminal](https://nnsproposal.icp.xyz/), a missing feature in the main **NNS-UI**.

> **NNS-UI** は **NNS** と対話するための主要なインターフェイスですが、他のユーザーフレンドリーなインターフェイスを作ることができます。すでにコミュニティでは、メインの **NNS-UI** に欠けている機能である [ターミナルを使わずにプロポーザルを作成できるインタフェース](https://nnsproposal.icp.xyz/) を作成しています。

As we seen with the example of the **NNS** - building a **DAO** can involve deploying and managing multiple canisters.  
**NNS** の例で見たように、**DAO** を構築するには、複数のキャニスターを配備し管理する必要があります。