# Day 2️⃣
Welcome back for **Day 2!**  
おかえりなさい！**Day 2！**<br/>
We're thrilled to see you again and congrats on completing the first day. We hope you've had the opportunity to connect with your teammates and enjoyed the networking session.  
またお会いできたことに感激しています。初日を終えられたこと、おめでとうございます。チームメイトとつながり、ネットワーキングセッションを楽しんでいただけたでしょうか。<br/>
Today, we'll delve deeper into the Motoko language with two specialized lectures and a new project. Let's dive in!  
今日は、2つの専門講義と新企画で、Motoko 言語を深く掘り下げます。さあ、飛び込もう！
## 🍿 Lectures & events / 講演とイベント
> Be sure to consult the calendar for the precise schedule of each lecture.

> 各講演の正確なスケジュールは、必ずカレンダーでご確認ください。

| Title | Mentor |  Description |
|-----------------|-----------------|-----------------|
 Motoko: Array, List & Buffer | <a href="https://twitter.com/mariano_stoll" target="_blank"> Stoll </a> | This lectures covers the datastructures `Array`, `List` & `Buffer` and how to use them. / この講義では、データ構造である`Array`, `List` と `Buffer` とその使用方法について説明します。
| Motoko: Char, Text & Iter | <a href="https://twitter.com/seb_icp" target="_blank"> Seb  </a> | This lecture covers the types `Char` and `Text` in Motoko and explains how those are linked through the type `Iter`.　/ 本講義では、Motokoにおける `Char` 型と `Text` 型を取り上げ、それらが `Iter` 型を介してどのように連携しているかを説明します。

##  🧭 Tasks of the day / 本日のタスク
> Use this list as a guide for your day, it contains all the material that you need to read and the challenges you need to tackle.

> このリストには、読むべき資料と取り組むべき課題がすべて含まれています。
- Read 読みましょう [Chapter 2: Common programming concepts](../../manuals/chapters/chapter-2/CHAPTER-2.MD).
    - [Control flow](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-2/CHAPTER-2.MD#%EF%B8%8F-control-flow)
- Read 読みましょう [Chapter 3: Primitive Types in Motoko](../../manuals/chapters/chapter-3/CHAPTER-3.MD).
    - [Text](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-3/CHAPTER-3.MD#-text)
    - [Char](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-3/CHAPTER-3.MD#-char)
    - [Unit type](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-3/CHAPTER-3.MD#-unit-type)
- Read 読みましょう [Chapter 5: Modules and the Base library](../../manuals/chapters/chapter-5/CHAPTER-5.MD)  in full.
- Read 読みましょう [Chapter 6: Storing data in data structures](../../manuals/chapters/chapter-6/CHAPTER-6.MD)
    - [Array](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#%EF%B8%8F-array)
    - [Buffer](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-buffer)
    - [List](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-list)
- Read 読みましょう [Chapter 7: Non-primitives types](../../manuals/chapters/chapter-7/CHAPTER-7.MD).
    - [Tuples](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-tuples)
    - [Objects](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-objects)
- Read 読みましょう [Appendix 2: Unlocking the power of DAOs with canister](../../manuals/appendix/appendix-2/APPENDIX-2.MD) in full.
- Read 読みましょう [Appendix 4: Overview of the NNS](../../manuals/appendix/appendix-4/APPENDIX-4.MD) in full.
- Read 読みましょう [Appendix 7: Debugging and testing with Motoko](../../manuals/appendix/appendix-7/APPENDIX-7.MD)
    - [Debugging](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/appendix/appendix-7/APPENDIX-7.MD#debugging)
- Complete the [project of the day](./project/README.MD). / [project of the day](./project/README.MD) を完成させてください。
## 🎯 Learning objectives 学習目標
> **Before you finish your day**, review the following list and ensure that you have addressed each item on it. It's important that you have a clear understanding of all these concepts. <br/> <i> Why not try explaining them to one of your teammate to gauge your level of understanding? </i>

> **一日を終える前に**、以下のリストを確認し、各項目に対応できていることを確認してください。これらの概念をすべて明確に理解することが重要です。<br/> <i> チームメイトに説明してみて、理解度を測ってみてはいかがでしょうか。 </i>

- Understand what is a [module](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#-modules).
- [module](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#-modules) とは何かを理解する。
- Understand what is the [base library](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#-the-base-library), [how to use it](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#importing-from-the-base-library) and where to find the [source code](https://github.com/dfinity/motoko-base). 
- [base library](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#-the-base-library) とは何か、[how to use it](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-5/CHAPTER-5.MD#importing-from-the-base-library)、[source code](https://github.com/dfinity/motoko-base) はどこにあるのかを理解する。
- Understand how to use the [Debug module](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/appendix/appendix-7/APPENDIX-7.MD#debugging) to test your code locally.
- [Debug module](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/appendix/appendix-7/APPENDIX-7.MD#debugging) を使って、コードをローカルでテストする方法を理解する。
- Understand how to manipulate [control flow operators](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-2/CHAPTER-2.MD#%EF%B8%8F-control-flow) in Motoko: `if`, `else`, `for`, `while`, `switch/case`
- Motoko の [control flow operators](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-2/CHAPTER-2.MD#%EF%B8%8F-control-flow) の操作方法を理解する：`if`, `else`, `for`, `while`, `switch/case`
- Getting familiar with more primitive types in Motoko: `Text`, `Char` & the unit type.
- Motoko でよりプリミティブな型に慣れる：`Text`、`Char`、ユニット型。
- Getting familiar with simple data structures in Motoko: [Array](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#%EF%B8%8F-array) , [List](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-list) & [Buffer](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-buffer).
- Motokoの簡単なデータ構造に慣れる： [Array](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#%EF%B8%8F-array) , [List](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-list) & [Buffer](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-6/CHAPTER-6.MD#-buffer)
- Getting familiar with more advanced types: [Tuples](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-tuples) and [Objects](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-objects).
- より高度な型に慣れ親しむ： [Tuples](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-tuples) と [Objects](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/chapters/chapter-7/CHAPTER-7.MD#-objects)
- Understanding [what is DAO](../../manuals/appendix/appendix-2/APPENDIX-2.MD), how it can be used and how the Internet Computer enables new innovative usecases for those organisations.
- [what is DAO](../../manuals/appendix/appendix-2/APPENDIX-2.MD)、その利用方法、Internet Computer がそれらの組織にとって新しい革新的利用事例をいかに可能にするかを理解する。
- Becoming familiar with an important DAO on the Internet Computer: the [Network Nervous System](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/appendix/appendix-4/APPENDIX-4.MD).
- インターネット・コンピュータの重要な DAO である [Network Nervous System](https://github.com/motoko-bootcamp/motoko-starter/blob/main/manuals/appendix/appendix-4/APPENDIX-4.MD) に精通する。

> Before deciding to call it **Motoko**, the language developed by **DFINITY** was actually called **ActorScript**. 

> **DFINITY** が開発した言語は、**Motoko** という名前になる前は、実は **ActorScript** という名前でした。

Good luck 🍀  
幸運を祈ります 🍀