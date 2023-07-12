# The Verifier 👨‍🏫 / 検証者 👨‍🏫
## Introduction / はじめに
Imagine that you are now an instructor at [Motoko School](https://twitter.com/MotokoSchool), where you are currently overseeing a cohort of more than 200 dedicated students!  🤯  
あなたは今、[Motoko School](https://twitter.com/MotokoSchool) の講師として、200人を超える熱心な生徒を指導していると想像してください！ 🤯<br/>
As part of the program, you have assigned these ambitious learners to tackle 4 distinct projects, each designed to challenge their skills and knowledge. Upon completion, it falls on your shoulders to meticulously review and evaluate their work, ultimately determining whether they have met the criteria for [graduation](../../../README.MD#🎓-graduation).  
このプログラムの一環として、あなたは意欲的な学習者に4つのプロジェクトを課し、それぞれのスキルと知識に挑戦させました。修了後は、彼らの作品を丹念にレビューし、評価し、最終的に [卒業](../../../README.MD#🎓-graduation) の基準を満たしたかどうかを判断するのがあなたの役目です。 <br/>
Fortunately, as an adept Motoko developer yourself, you possess the expertise and confidence to streamline this verification process by leveraging automation. This innovative approach will not only save you valuable time but also pave the way for the future of **Motoko Bootcamp**.  
幸いなことに、Motoko の開発者であるあなたには、自動化を活用してこの検証プロセスを合理化する専門知識と自信があります。この革新的なアプローチは、あなたの貴重な時間を節約するだけでなく、**Motoko Bootcamp** の未来への道を開くことになるでしょう。
## 🧑‍🏫 Requirements / 前提条件
Your task is to create the code for an **instructor**, which is implemented as a canister. The idea is for the student to input his canister id and get automatically verified by the canister. If the canister id submitted fulfill the requirements then the students will automatically graduate; just imagine the HOURS of work you will save!  
あなたの仕事は、キャニスターとして実装された **インストラクター** のコードを作成することです。生徒が自分のキャニスター ID を入力し、キャニスターによって自動的に認証されるようにすることです。提出されたキャニスター ID が要件を満たしていれば、学生は自動的に卒業できます！<br/>

> For the purpose of this Bootcamp, we will not attempt to build a verifier that test all 4 previous projects. We will only attempts to verify a simple version of the calculator you've implemented during Day 1. The code for this simple calculator has already been implemented for you, and can be found [here](../project/calculator/calculator.mo).  

> この Bootcamp では、過去に実施した４つのプロジェクトすべてをテストする検証機を作ろうとはしません。１日目に実装した電卓のシンプルなバージョンの検証のみを試みます。このシンプルな電卓のコードはすでに実装されており、[ここ](../project/calculator/calculator.mo)で見つけることができます。

## Part 1: Storing the students information. / 第１回：学生情報を保存する。
The idea in this section is to build the code for storing informations about students.  
このセクションでは、学生に関する情報を保存するためのコードを構築することです。

### Step-by-step / ステップバイステップ
A student profile is defined as follows:  
学生プロファイルは、以下のように定義されます：
```motoko
public type StudentProfile = {
    name : Text;
    team : Text;
    graduate : Bool;
};
```
1. Define a variable named `studentProfileStore`, which is a `HashMap` for storing student profile. The keys in this map are of type `Principal` and represent the identity of students, while the values are of type `StudentProfile`.  
`studentProfileStore` という名前の変数を定義しなさい。これは学生のプロファイルを格納するための `HashMap` です。このマップのキーは `Principal` 型で、学生のIDを表し、値は `StudentProfile` 型です。
2. Implement the `addMyProfile` function which accepts a `profile` of type `StudentProfile` and adds it into the `studentProfileStore`. This function assumes that the `caller` is the student corresponding to the profile.  
型 `StudentProfile` の `profile` を受け取り、それを `studentProfileStore` に追加する `addMyProfile` 関数を実装しなさい。この関数は、`caller` がプロファイルに対応する学生であると仮定しています。
```motoko
addMyProfile: shared (profile : StudentProfile) -> async Result.Result<(), Text>;
```
3. Implement the `seeAProfile` query function, which accepts a principal `p` of type `Principal` and returns the optional corresponding student profile.  
`seeAProfile` クエリー関数を実装しなさい。この関数は `Principal` 型の principal `p` を受け取り、principal に対応する optional な学生プロファイルを返します。
```motoko
seeAProfile : query (p : Principal) -> async Result.Result<StudentProfile, Text>;
```
4. Implement the `updateMyProfile` function which allows a student to perform a modification on its student profile. If everything works, and the profile is updated the function should return a simple unit value wrapped in an `Ok` result. If the `caller` doesn't have a student profile the function should return an error message wrapped in an `Err` result.  
学生が学生プロファイルを変更できる `updateMyProfile` 関数を実装しなさい。すべてがうまくいき、プロフィールが更新された場合、関数は `Ok` result にラップされた単純な unit 値を返す必要があります。もし `caller` が学生プロファイルを持っていない場合、この関数は `Err` result にラップされたエラーメッセージを返す必要があります。
```motoko
updateMyProfile : shared (profile : StudentProfile) -> async Result.Result<(), Text>;
```
5. Implement the `deleteMyProfile` function which allows a student to delete its student profile. If everything works, and the profile is deleted the function should return a simple unit value wrapped in an `Ok` result. If the `caller` doesn't have a student profile the function should return an error message wrapped in an `Err` result.  
学生が学生プロファイルを削除できる `deleteMyProfile` 関数を実装しなさい。すべてがうまくいき、プロフィールが削除された場合、関数は `Ok` 結果にラップされた単純な unit 値を返す必要があります。もし `caller` が学生プロファイルを持っていない場合、この関数は `Err` result にラップされたエラーメッセージを返す必要があります。
```motoko
deleteMyProfile : shared () -> async Result.Result<(), Text>;
```
## Part 2: Testing of the simple calculator. / 第2部：簡易電卓のテスト。
The goal of this section is to write the code for testing the functionality of the simple calculator (you don't need to write the code for this one! I've already done it). We will will test threee functions:  
このセクションの目標は、シンプルな電卓の機能をテストするためのコードを書くことです（このコードは書く必要はありません！私はすでにやっています）。私たちは、３つの関数をテストします：
- The `reset` function.
- The `add` function.
- The `sub` function.

If these three functions are correctly implemented, it indicates a successful test, validating the canister. During the calculator testing, we will perform inter-canister calls, considering three different scenarios:  
これら3つの関数が正しく実装されていれば、テストが成功したことを示し、キャニスターを検証できます。電卓テストでは、3つのシナリオを想定して、インターキャニスターコールを行います：

- Scenario 1: The calls to the calculator are executed correctly, but the returned results are not as expected. For example, if calling reset followed by add(1) returns 2 instead of the expected result.
- シナリオ1：電卓の呼び出しは正しく実行されるが、返される結果が期待通りでない。例えば、resetの後にadd(1)を呼び出すと、期待通りの結果ではなく、2が返される場合。
- Scenario 2: The calls to the calculator are executed correctly, and the returned results match our expectations.
- シナリオ2：電卓の呼び出しは正しく実行され、返された結果は期待に沿うものである。
- Scenario 3: The calls to the calculator fail. This could be due to reasons such as the calculator not implementing the add function, not being deployed on the network, or running out of computation cycles.
- シナリオ3：電卓の呼び出しに失敗する。これは、電卓が加算関数を実装していない、ネットワーク上に配置されていない、計算サイクルが不足しているなどの理由によるものです。

To handle the different scenario, we define the `TestResult` type as follows:  
異なるシナリオに対応するために、`TestResult` 型を以下のように定義します：
```motoko
public type TestResult = Result.Result<(), TestError>;
public type TestError = {
    #UnexpectedValue : Text;
    #UnexpectedError : Text;
};
```
1. Implement the `test` function that takes a `canisterId` of type `Principal` and returns the result of the test of type `TestResult`. Make sure to distringuish between the two types of errors.  
`Principal` 型の `canisterId` を受け取り、`TestResult` 型のテスト結果を返す `test` 関数を実装しなさい。2種類のエラーを区別することを確認します。
- UnexpectedValue should be returned whenever the calculator returns a wrong value. For instance, if a call to `reset` followed by `add(1)` returns 2.
- 電卓が間違った値を返すときは常に UnexpectedValue を返すようにします。例えば、`reset` の後に `add(1)` を呼び出すと、2が返される場合です。
- UnexpectedError should be returned for all other types of errors. For instance, if the function `add` is not even implemented as part of the canister's interface.
- その他のタイプのエラーには UnexpectedError を返す必要があります。例えば、関数 `add` がキャニスタのインターフェイスの一部として実装されていない場合などです。
```motoko
test: shared (canisterId : Principal) -> async TestResult;
```
## Part 3: Verifying the controller of the calculator. / 第3回：電卓のコントローラーを検証。
In this section we want to make sure that the owner of the verified canister is actually the student that registered it. Otherwise, a student could use the canister of another one.  
このセクションでは、検証されたキャニスターの所有者が、実際にそれを登録した学生であることを確認したいと思います。そうでなければ、ある学生が他の学生のキャニスターを使用できます。
### Step-by-step / ステップバイステップ
Implement the `verifyOwnership` function that takes a `canisterId` of type `Principal` and a `principalId` of type `Principal` and returns a boolean indicating if the `principalId` is among the controllers of the canister corresponding to the `canisterId` provided.  
`Principal` 型の `canisterId` と `Principal` 型の `principalId` を受け取り、指定された `canisterId` に対応するキャニスターのコントローラーの中に `principalId` があるかどうかを示すブール値を返す関数 `verifyOwnership` を実装しなさい。
```motoko
verifyOwnership : shared (Principal, Principal) -> async Bool;
```

> Tip: To implement step 3, you'll need to make an intercanister call to the management canister by using the `canister_status` method, which will return information on the canister among which are the list of controllers. The management canister is defined in the [ic.mo](./verifier/ic.mo). However, currently, the `canister_status` method can only be accessed when the calling canister is also the controller of the canister whose status you want to check. To overcome this limitation, you'll need to use a `try/catch` block to catch the error returned by the management, access the error message with `Error.message(e)` and then parse the message using the `parseControllersFromCanisterStatusErrorIfCallerNotController` method. I recommend reading the [dedicated topic on the forum](https://forum.dfinity.org/t/getting-a-canisters-controller-on-chain/7531/15)

> ヒント：このメソッドはキャニスターの情報を返し、その中にはコントローラーのリストも含まれています。管理キャニスタは [ic.mo](./verifier/ic.mo) で定義されています。しかし、現在、`canister_status` メソッドにアクセスできるのは、呼び出し元のキャニスターが、ステータスを確認したいキャニスターのコントローラでもある場合のみです。この制限を克服するには、`try/catch` ブロックを使用して、マネージメントが返すエラーをキャッチし、エラーメッセージに `Error.message(e)` でアクセスし、`parseControllersFromCanisterStatusErrorIfCallerNotController` メソッドを使用してメッセージをパースする必要があるでしょう。[フォーラムの専用トピック](https://forum.dfinity.org/t/getting-a-canisters-controller-on-chain/7531/15) を読むことをお勧めします。

```motoko
func parseControllersFromCanisterStatusErrorIfCallerNotController(errorMessage : Text) : [Principal] {
    let lines = Iter.toArray(Text.split(errorMessage, #text("\n")));
    let words = Iter.toArray(Text.split(lines[1], #text(" ")));
    var i = 2;
    let controllers = Buffer.Buffer<Principal>(0);
    while (i < words.size()) {
      controllers.add(Principal.fromText(words[i]));
      i += 1;
    };
    Buffer.toArray<Principal>(controllers);
  };
```
## Part 4: Graduation! 🎓 / 第4部：卒業式 🎓
In this sections the idea is to let students submit their work and automatically verify the canister. If the tests are passed then the `graduation` field of the student is automatically changed.  
このセクションでは、学生に作品を提出させ、自動的にキャニスターを検証することを考えます。もしテストに合格すれば、その学生の `graduation` フィールドは自動的に変更されます。

### Step-by-step / ステップバイステップ
Implement the `verifyWork` function that takes a `canisterId` of type `Principal` and a `principalId` of type `Principal` that corresponds to the identity of the student and perfoms the necessary verifications on the canister. If all the criteria for graduations are validated; then the `graduation` field of the student is updated accordingly. This function will returns  a `Ok` result indicating if the submitted project has been successfuly verified. This function will return a text message wrapped in an `Err` message in case the verification fails or something unexpected happens.  
学生の ID に対応する `Principal` 型の `canisterId` と `PrincipalId` を受け取り、キャニスターに対して必要な検証を行う `verifyWork` 関数を実装しなさい。卒業のためのすべての基準が検証された場合、学生の `graduation` フィールドはそれに応じて更新されます。この関数は、提出されたプロジェクトが正常に検証されたかどうかを示す `Ok` result を返します。この関数は、検証に失敗した場合や予期せぬことが起こった場合には、`Err`メッセージにラップされたテキストメッセージを返します。

```motoko
verifyWork: shared (canisterId : Principal, principalId: Principal) -> async Result.Result<(), Text>;
```

## 📺 Interface / インターフェイス
> At the end of the project your canister should implement the following interface:

> プロジェクトの終了時には、キャニスターは以下のインターフェイスを実装している必要があります：

```motoko
actor Verifier {
    // Part 1
    addMyProfile : shared StudentProfile -> async Result.Result<(),Text>;
    updateMyProfile : shared StudentProfile -> async Result.Result<(),Text>;
    deleteMyProfile : shared () -> async Result.Result<(),Text>;
    seeAProfile : shared Principal -> async Result.Result<StudentProfile, Text>;

    //Part 2
    test : shared Principal -> async TestResult;

    //Part 3
    verifyOwnership : shared (Principal, Principal) -> async Bool;

    //Part 4
    verifyWork : shared (Principal, Principal) -> async Result.Result<(), Text>;
};
```

## 最後に
「最後に」は、C3F の ICP 開発者コミュニティにて、Motoko Bootcamp を進めている方に向けてのものです。
当課題を消化できたところで、C3F の Discord のチャンネル \"#【c3f開発コミュニティ】\" へその旨を報告しましょう！もしくは、消化が難しい場合は、質問しましょう！