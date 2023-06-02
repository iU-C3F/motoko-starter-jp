# MotoCoin 🪙
As your first week at the prestigious [Motoko School](https://twitter.com/MotokoSchool) comes to an end, you're in awe of the wealth of knowledge and collaborative spirit that surrounds you. The school is a hub of innovation and creativity, drawing the brightest minds from around the world to master the art of building on the Internet Computer.  🏗️  
名門 [Motoko スクール](https://twitter.com/MotokoSchool) での最初１週間が終わろうとしているとき、あなたは自分の周りにある豊富な知識と協力的な精神に畏敬の念を抱くでしょう。この学校はイノベーションとクリエイティビティの拠点であり、世界中から優秀な人材が集まり、Internet Computer の構築技術を習得しています。 🏗️

One evening, while exploring the school's virtual library, you stumble upon a hidden section filled with stories of the school's successful alumni. You're fascinated by their accomplishments, yet you notice a common theme: many have built incredible wealth, but only a few have given back to the school. 🫢  
ある晩、あなたは学校のバーチャル図書館で、成功した卒業生たちのエピソードが書かれた隠しページを見つけました。多くの人が信じられないほどの富を築いたが、学校に貢献した人はごくわずかだったのです。🫢

At the same time, you overhear a conversation about the school's financial struggles and its inability to provide adequate resources for students in need. This revelation weighs heavily on your mind, and you feel compelled to find a solution that bridges the gap between the school's prosperous alumni and its underfunded programs. 💸  
その頃、あなたは学校の財政難と、必要な学生に十分なリソースを提供できていないという会話を耳にします。この事実はあなたの心に重くのしかかり、あなたは学校の豊かな卒業生と資金不足のプログラムとの間のギャップを埋める解決策を見つけなければならないと感じるのです。💸

Inspired by the alumni stories, you envision a digital token that connects the past, present, and future of the **Motoko School** – the **MotoCoin**. This token would allow alumni and other investors to invest in the school's future while supporting its present needs. 🌱  
卒業生のストーリーに触発され、あなたは **Motoko School** の過去、現在、未来をつなぐデジタルトークンである **MotoCoin** を構想しています。このトークンによって、卒業生や他の投資家は、学校の現在のニーズをサポートしながら、学校の未来に投資できるようになります。🌱

You share your idea with a group of enthusiastic students, and together, you begin working tirelessly to bring **MotoCoin** to life. Built on the Internet Computer, the **MotoCoin** would enable investors, students, contributors to participate to the school's growth and success. 🚀  
あなたは自分のアイデアを熱心な学生たちと共有し、一緒に **MotoCoin** を実現するために精力的に活動を開始します。Internet Computer 上に構築された**MotoCoin** は、投資家、学生、貢献者が学校の成長と成功に参加することを可能にします。🚀

## 🧑‍🏫 Requirements / 前提条件
Your task is to create a ledger for a token that can be used as a currency for the school. The ledger is implemented as a canister.  
あなたの課題は、学校の通貨として使用できるトークンの台帳を作成することです。台帳はキャニスターとして実装されています。

## 📺 Interface
We define the following types:  
以下のタイプを定義します：
```motoko
type Subaccount = Blob;
type Account = {
    owner : Principal;
    subaccount : ?Subaccount;
};
```
Your canister should implement the following interface:  
キャニスターは、以下のインターフェイスを実装する必要があります：
```motoko
actor {
    // Returns the name of the token 
    name : shared query () -> async Text;

    // Returns the symbol of the token 
    symbol : shared query () -> async Text;

    // Returns the the total number of tokens on all accounts
    totalSupply : shared query () -> async Nat;

    // Returns the balance of the account
    balanceOf : shared query (account : Account) -> async (Nat);

    // Transfer tokens to another account
    transfer : shared (from: Account, to : Account, amount : Nat) -> async Result.Result<(), Text>;

    // Airdrop 100 MotoCoin to any student that is part of the Bootcamp.
    airdrop : shared () -> async Result.Result<(),Text>;
}
```
## 📒 Steps / ステップ
1. Define a variable called `ledger`, which is a `TrieMap`. In this datastructure, the keys are of type `Account` and the values are of type `Nat` and represent the balance of each account. You can use the helper functions in `account.mo` to help you.  
`TrieMap`である `ledger` という変数を定義しなさい。このデータ構造では、キーは `Account` 型、値は `Nat` 型で、各アカウントの残高を表しています。このとき、`account.mo`にあるヘルパー関数を利用できます。
2. Implement `name` which returns the name of the token as a `Text`. The name of the token is `MotoCoin`.  
トークンの名前を `Text` として返す `name` を実装しなさい。トークンの名前は `MotoCoin` です。
3. Implement `symbol` which returns the symbol of the token as a `Text`. The symbol of the token is `MOC`.  
トークンのシンボルを `Text` として返す `symbol` を実装しなさい。トークンのシンボルは `MOC` です。
4. Implement `totalSupply` which returns the total number of `MOC` token in circulation.  
MOCトークンの流通総数を返す `totalSupply` を実装しなさい。
5. Implement `balanceOf` which takes an `account` and returns the balance of this account. If the account has never interacted with the ledger before, you will return 0.  
`account` を受け取り、その account の残高を返す `balanceOf` を実装しなさい。この勘定科目がこれまで一度も元帳とやりとりしたことがない場合は、0 を返すことになります。
6. Implement `transfer` that accepts three parameters: an `Account` object for the sender (`from`), an `Account` object for the recipient (`to`), and a `Nat` value for the amount to be transferred. This function should transfer the specified amount of tokens from the sender's account to the recipient's account. This function should return an error message wrapped in an `Err` result if the caller has not enough token in it's main account.  
送信者の `Account` オブジェクト (`from`) と受信者の `Account` オブジェクト (`to`) 、そして転送量を表す `Nat` 値の 3 つのパラメータを受け取る `transfer` を実装しなさい。この関数は、指定された量のトークンを送信者のアカウントから受信者のアカウントに転送する必要があります。この関数は、呼び出し元のメインアカウントに十分なトークンがない場合、 `Err` 結果でラップされたエラーメッセージを返す必要があります。
7. Implement `airdrop` which adds 100 MotoCoin to the main account of all students participating in the Bootcamp.  
Bootcampに参加する生徒全員のメインアカウントに100MotoCoinを追加する`airdrop`を実装しなさい。

To implement airdrop - use the function `getAllStudentsPrincipal` on the canister with id `rww3b-zqaaa-aaaam-abioa-cai`, this returns the list of all principals of the students participating in the Bootcamp.  
エアドロップを実装するには - id `rww3b-zqaaa-aaaam-abioa-cai` のキャニスターで関数 `getAllStudentsPrincipal` を使用し、Bootcamp に参加する学生のすべての principal のリストを返します。
```motoko
getAllStudentsPrincipal : shared () -> async [Principal];
```

