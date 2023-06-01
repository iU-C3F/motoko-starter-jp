# Student wall 🎨 / 生徒用ウォール 🎨
It was your third day at Motoko School, and you were determined to start making some good friends.  
Motoko スクールに入学して３日目のあなたは、そろそろいい友達を作ろうと思っていました。<br/>
Being a big fan of music, you thought organizing a little music concert could be a great way to meet other like-minded students. 🎶  
音楽が大好きなあなたは、小さな音楽会を企画することで、同じ志を持つ生徒たちと知り合うことができると考えました。🎶

As you wandered the halls during lunchtime, you overheard two students discussing how they wished there was a better way to stay informed about school events and activities. They complained about how they had missed out on attending the previous year's [ICP Community Conference](https://twitter.com/icp_cc) because they weren't aware of it in time, and how they were determined not to let that happen again this year. 💪  
昼休みに廊下を歩いていると、２人の生徒が「学校のイベントや活動についてもっと情報を得る方法があればいいのに」と話しているのを耳にしました。彼らは、前年度の [ICP Community Conference](https://twitter.com/icp_cc) に気づかず参加できなかったことを訴え、今年も同じことが起こらないようにしようと決意していました。💪


This sparked an idea in your mind.  
これが、あなたの心にあるアイデアを呼び起こしました。<br/>

What if you could create a digital platform where students share upcoming events and activities. It would be the perfect way to advertise your music concert and help other students stay informed about everything happening on campus. 📅  
もし、生徒が今後のイベントや活動を共有するデジタルプラットフォームを作ることができたらどうでしょう。音楽コンサートを宣伝したり、他の生徒がキャンパスで起こっているすべてのことを知るのに最適な方法です。📅

You quickly shared your idea with the two students and they loved it. They introduced you to a few others who were also interested in the idea, and before you knew it, you had a group of motivated students ready to bring your idea to life. 🚀  
あなたは早速、そのアイデアを２人の生徒に伝えました。そして、そのアイデアを実現しようとする意欲的な生徒たちが、いつの間にか集まってきたのです。🚀

You all gathered in the computer lab and began brainstorming the features of your student wall. You wanted it to be more than just a bulletin board, so you came up with the idea to include images and surveys as well. You divided the work and got started coding.  
皆さんはコンピュータ室に集まり、生徒用ウォールの特徴を考え始めました。単なる掲示板にとどまらず、画像やアンケートも取り入れることを思いついたのです。作業を分担して、コーディングを開始しました。

## 🧑‍🏫 Requirements 前提条件
Your task is to develop the code for a student wall, implemented as a canister - a digital platform that will revolutionize how students communicate and stay informed about events, clubs, and activities in the community. Imagine a dynamic and interactive space where students can share their thoughts, ideas, and upcoming events with each other. 
This wall will be the go-to destination for students looking to get the latest scoop on what's happening in the school. 

あなたの仕事は、キャニスターとして実装される生徒ウォールのコードを開発することです。このデジタルプラットフォームは、生徒がイベントやクラブ、コミュニティでの活動についてコミュニケーションをとり、情報を得る方法に革命をもたらすでしょう。生徒が自分の考えやアイデア、今後のイベントなどを共有できる、ダイナミックでインタラクティブな空間を想像してください。
この壁は、学校で起こっていることの最新スクープを得たい生徒にとって、最も重要な場所となるでしょう。

## 📒 Steps / ステップ
We define a variant type called `Content` that represents the type of content of the messages that can be published on the wall.  
ウォールに公開できるメッセージの内容の種類を表す `Content` というバリアントタイプを定義します。
```motoko
public type Content = {
    #Text: Text;
    #Image: Blob;
    #Video: Blob;
};
```
1. Define a new type called `Message` which consists of three fields: `vote` of type `Int`, `content` of type `Content`, and `creator` of type `Principal`. / 3つのフィールドから構成される `Message` という新しい型を定義しなさい： この型は、 `Int` 型の `vote` 、 `Content` 型の `content` 、 `Principal` 型の `creator` の 3 つのフィールドから構成されます。

2. Declare a variable named `messageId` to serve as a continuously increasing counter, keeping track of the total number of messages posted. / 投稿されたメッセージの総数を追跡し、継続的に増加するカウンターとして機能する `messageId` という名前の変数を宣言します。

3. Create a variable called `wall`, which is a HashMap designed to store messages. The keys in the wall are of type `Nat` and represent message IDs, while the values are of type `Message`. / メッセージを格納するための HashMap である `wall` という変数を作成しなさい。wall のキーは `Nat` 型でメッセージ ID を表し、値は `Message` 型です。

4. Implement the `writeMessage` function, which accepts a content `c` of type `Content`, creates a new message from the content, adds the message to the wall, and returns the ID of the message.  
`Content`型のコンテンツ `c` を受け取り、そのコンテンツから新しいメッセージを作成し、メッセージを wall に追加して、そのメッセージの ID を返す `writeMessage` 関数を実装しなさい。
```motoko
writeMessage: shared (c : Content) -> async Nat;
```
5. Implement the `getMessage` function, which accepts a `messageId` of type `Nat` and returns the corresponding message wrapped in an `Ok` result. If the `messageId` is invalid, the function should return an error message wrapped in an `Err` result.  
`Nat`型の `messageId` を受け取り、対応するメッセージを `Ok` result で包んで返す `getMessage` 関数を実装しなさい。`messageId` が無効な場合、この関数は `Err` result でラップされたエラーメッセージを返すべきです。 
```motoko
getMessage: shared query (messageId: Nat) -> async Result.Result<Message, Text>;
```
6. Implement the `updateMessage` function, which accepts a `messageId` of type `Nat` and a content `c` of type `Content`. This function updates the content of the corresponding message only if the caller is the creator of the message. If the `messageId` is invalid or the `caller` is not the creator, the function should return an error message wrapped in an `Err` result. If the update is successful, the function should return a unit value wrapped in an `Ok` result.  
`Nat` 型の `messageId` と `Content` 型のコンテンツ `c` を受け取る `updateMessage` 関数を実装しなさい。この関数は、呼び出し元がメッセージの作成者である場合にのみ、対応するメッセージの内容を更新します。`messageId` が無効な場合、または `caller` が作成者でない場合、この関数は `Err` result に包まれたエラーメッセージを返す必要があります。更新が成功した場合、この関数は `Ok` result に包まれたユニット値を返す必要があります。 
```motoko
updateMessage: shared (messageId : Nat, c : Content) -> async Result.Result<(), Text>;
```
7. Implement the `deleteMessage` function, which accepts a `messageId` of type `Nat`, removes the corresponding message from the wall, and returns a unit value wrapped in an `Ok` result. If the `messageId` is invalid, the function should return an error message wrapped in an `Err` result.  
`deleteMessage`関数を実装しなさい。この関数は `Nat` 型の `messageId` を受け取り、対応するメッセージをウォールから削除し、`Ok` result に包まれた unit 値を返します。もし `messageId` が無効であれば、この関数は `Err` result に包まれたエラーメッセージを返さなければなりません。
```motoko
deleteMessage: shared (messageId : Nat) -> async Result.Result<(), Text>;
```
8. Implement the `upVote` function, which accepts a `messageId` of type `Nat`, increments the vote count of the corresponding message by one, and returns a unit value wrapped in an `Ok` result. If the `messageId` is invalid, the function should return an error message wrapped in an `Err` result.  

`Nat`型の `messageId` を受け取り、対応するメッセージの投票数を1つ増やし、`Ok` result に包まれた unit 値を返す `upVote` 関数を実装しなさい。`messageId` が無効な場合、この関数は `Err` result でラップされたエラーメッセージを返すべきです。 
```motoko
upVote: shared (messageId  : Nat) -> async Result.Result<(), Text>;
```
9. Implement the `downVote` function, which accepts a `messageId` of type `Nat`, decrements the vote count of the corresponding message by one, and returns a unit value wrapped in an `Ok` result. If the `messageId` is invalid, the function should return an error message wrapped in an `Err` result.  
この関数は `Nat` 型の `messageId` を受け取り、対応するメッセージの投票数を 1 つ減らし、`Ok` result に包まれた unit 値を返します。もし `messageId` が無効であれば、この関数は `Err` result に包まれたエラーメッセージを返す必要があります。
```motoko
downVote: shared (messageId  : Nat) -> async Result.Result<(), Text>;
```
10. Implement the query function `getAllMessages`, which returns a list of all messages stored in the wall.  
ウォールに保存されているすべてのメッセージのリストを返すクエリー関数 `getAllMessages` を実装しなさい。
```motoko
getAllMessages : query () -> async [Message];
```
11. Implement the query function `getAllMessagesRanked`, which returns a list of all messages from the wall, ordered by the number of votes in descending order.  
クエリー関数 `getAllMessagesRanked` を実装しなさい。この関数は、ウォールからのすべてのメッセージのリストを投票数の降順で返します。
```motoko
getAllMessagesRanked : query () -> async [Message];
```
12. Deploy the student wall on the Internet Computer. / Internet Computer に生徒用ウォールをデプロイしなさい。

## 📺 Interface / インターフェイス
Your canister should implement the following interface:  
キャニスターは、以下のインターフェイスを実装する必要があります：
```motoko
actor {
   
    // Add a new message to the wall
    writeMessage: shared (c : Content) -> async Nat;

    //Get a specific message by ID
    getMessage: shared query (messageId : Nat) -> async Result.Result<Message, Text>;

    // Update the content for a specific message by ID
    updateMessage: shared (messageId : Nat, c : Content) -> async Result.Result<(), Text>;

    //Delete a specific message by ID
    deleteMessage: shared (messageId : Nat) -> async Result.Result<(), Text>;

    // Voting
    upVote: shared (messageId  : Nat) -> async Result.Result<(), Text>;
    downVote: shared (messageId  : Nat) -> async Result.Result<(), Text>;

    //Get all messages
    getAllMessages : query () -> async [Message];

    //Get all messages
    getAllMessagesRanked : query () -> async [Message];
};
```