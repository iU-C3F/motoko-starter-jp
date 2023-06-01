# Day 3️⃣
Welcome to **Day 3** of the Motoko Bootcamp. As we near the middle of the week, we hope you're all advancing, acquiring new skills, and enjoying the journey.  
Motoko Bootcamp の **Day 3** へようこそ。今週も中盤に差し掛かりましたが、皆さんは前進し、新しいスキルを身につけ、旅を楽しんでいることでしょう。<br/>

Today, we'll address the essential building blocks for creating an application on the Internet Computer: CRUD operations and authentication.  
今日は、Internet Computer 上でアプリケーションを作成するために不可欠なビルディング・ブロックを取り上げます： CRUD 操作と認証。<br/>

It's vital to master the topics we'll explore today. If you need assistance, don't hesitate to reach out to your teammates or mentors. Remember, we're all here to learn, share a laugh, and support one another. 😉  
今日取り上げるトピックをマスターすることが肝心です。サポートが必要な場合は、遠慮なくチームメイトやメンターに声をかけてください。私たちは皆、学び、笑い、支え合うためにここにいることを忘れないでください。

## 🍿 Lectures & events 講演とイベント
> Be sure to consult the calendar for the precise schedule of each lecture.

> 各講演の正確なスケジュールは、必ずカレンダーでご確認ください。

| Title | Mentor |  Description |
|-----------------|-----------------|-----------------|
 Motoko: HashMap & CRUD | <a href="https://twitter.com/CapuzR" target="_blank"> Ricardo </a> | This lecture covers CRUD operations on canisters, which involve managing data through **Create**, **Read**, **Update**, and **Delete** operations. / キャニスターの CRUD 操作について、**Create**, **Read**, **Update**, **Delete**操作によるデータ管理について説明します。
| Frontend, authentication and Internet Identity | <a href="https://twitter.com/kylpeacock" target="_blank"> Kyle  </a> | In this lecture you'll understand how to connect your canister to a frontend using the JavaScript agent. / この講義では、JavaScriptエージェントを使用して、キャニスターをフロントエンドに接続する方法について理解します。
##  🧭 Tasks of the day / 本日のタスク
> **When starting your day** use this list as a guide, it contains all the material that you need to read and the challenges you need to tackle.

> **一日の始まりに**。このリストには、読むべき資料や必要な課題がすべて含まれているので、ガイドとして活用してください。

- Read 読みましょう [Chapter 3: Primitive Types](../../manuals/chapters/chapter-3/CHAPTER-3.MD)
    - [Float](../../manuals/chapters/chapter-3/CHAPTER-3.MD#-float)
    - [Blob](../../manuals/chapters/chapter-3/CHAPTER-3.MD#-blob)
    - [Bounded types](../../manuals/chapters/chapter-3/CHAPTER-3.MD#%EF%B8%8F-bounded-types)
- Read 読みましょう [Chapter 6: Storing data in data structures](../../manuals/chapters/chapter-6/CHAPTER-6.MD) 
    - [HashMap & TrieMap](../../manuals/chapters/chapter-6/CHAPTER-6.MD#-hashmap--triemap)
- Read 読みましょう [Chapter 7: Non-primitives types](../../manuals/chapters/chapter-7/CHAPTER-7.MD).
    - [Variants](../../manuals/chapters/chapter-7/CHAPTER-7.MD#-variants).
    - [Array](../../manuals/chapters/chapter-7/CHAPTER-7.MD#-arrays)
    - [Mutable arrays](../../manuals/chapters/chapter-7/CHAPTER-7.MD#-mutable-arrays)
    - [Iterators](../../manuals/chapters/chapter-7/CHAPTER-7.MD#-iterators)
- Read 読みましょう [Chapter 8: Advanced types](../../manuals/chapters/chapter-8/CHAPTER-8.MD)
    - [Recursive types](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-recursive-types)
    - [Shared types](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-shared-types)
- Read 読みましょう [Chapter 9: Handling errors](../../manuals/chapters/chapter-9/CHAPTER-9.MD)
    - [The Result type](../../manuals/chapters/chapter-9/CHAPTER-9.MD#-the-result-type)
- Read 読みましょう [Chapter 10: Identity on the Internet Computer](../../manuals/chapters/chapter-10/CHAPTER-10.MD) in full.
- Read 読みましょう [Appendix 3: A new chapter in digital identity: Internet Identity](../../manuals/appendix/appendix-3/APPENDIX-3.MD#internet-identity)
- Complete the [project of the day](./project/README.MD). / [project of the day](./project/README.MD) を完成させてください。
## 🎯 Learning objectives / 学習目標
> **Before finishing your day**, review the following list and ensure that you have addressed each item on it. It's important that you have a clear understanding of all these concepts. <i> Why not try explaining them to one of your teammate to gauge your level of understanding? </i>

>**一日を終える前に**、以下のリストを見直し、各項目に対応できているかどうかを確認してください。これらの概念をすべて明確に理解することが重要です。<i>チームメイトに説明してみて、自分の理解度を測ってみてはいかがでしょうか。</i>

- Understanding that mutable state cannot be shared between actors. 
- ミュータブルステートはアクター間で共有できないことを理解する。
- Getting familiar with more [advanced types](../../manuals/chapters/chapter-8/CHAPTER-8.MD) such: [Optional](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-optional-types) & [Generic types](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-optional-types).
- より [高度な型](../../manuals/chapters/chapter-8/CHAPTER-8.MD) などに慣れる： [Optional](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-optional-types) と [Generic types](../../manuals/chapters/chapter-8/CHAPTER-8.MD#-optional-types) など。
- Getting familiar with using data structures such as: [HashMap and TrieMap](../../manuals/chapters/chapter-6/CHAPTER-6.MD#-hashmap--triemap).
- [HashMap と TrieMap](../../manuals/chapters/chapter-6/CHAPTER-6.MD#-hashmap--triemap) などのデータ構造に慣れる。
- Understanding what is a [Principal](../../manuals/chapters/chapter-10/CHAPTER-10.MD#the-concept-of-principal), how it's used on the Internet Computer and being able to [manipulate the primitive type `Principal` in Motoko](../../manuals/chapters/chapter-10/CHAPTER-10.MD#accessing-the-user-principal).
- [Principal](../../manuals/chapters/chapter-10/CHAPTER-10.MD#the-concept-of-principal) とは何か、インターネットコンピュータでどのように使われているかを理解し、[Motoko のプリミティブ型 `Principal` を操作](../../manuals/chapters/chapter-10/CHAPTER-10.MD#accessing-the-user-principal) できるようになる。
- Understanding how to interact with a canister using the **JavaScript** agent.
- **JavaScript** エージェントを使用したキャニスターとの対話方法を理解する。
- Understanding how to use [Internet Identity](../../manuals/appendix/appendix-3/APPENDIX-3.MD#internet-identity) as an authentication service and how it works.
- 認証サービスとしての [Internet Identity](../../manuals/appendix/appendix-3/APPENDIX-3.MD#internet-identity) の利用方法とその仕組みを理解する。

> The Internet Computer reached 1 Billion blocks within 14 months of it's launch. It would take 18,0000 years for **Bitcoin** to get there. 

> Internet Computer は、ローンチから14ヶ月で10億ブロックに到達しました。**Bitcoin** がそこに到達するには、18,000年かかる。

Good luck 🍀  
幸運を祈ります 🍀