# Homework diary 📔 / 宿題日記 📔
On the second day at school, you and your classmates find yourselves diving into your first collaborative assignment. Though working together is stimulating, the challenge of managing responsibilities and progress for each team member becomes quickly apparent... 😩  
入学して２日目、あなたはクラスメートと一緒に初めての共同作業に取り掛かることになりました。共同作業は刺激的だが、各メンバーの責任と進捗を管理することの難しさがすぐにわかります...。😩<br/>

During a lunch break, your group brainstorms solutions for a better system to organize the tasks and assignments.  
昼休みに、あなたのグループは、タスクや課題を整理するためのより良いシステムの解決策をブレインストーミングします。<br/>

One of your classmates proposes the idea of creating a homework diary on the famous **Joogle Cloud**, where each member can update tasks and monitor progress. The group quickly agrees and starts building the diary. As you observe the project taking shape, you notice a sly smile forming on the face of one student. 😼  
クラスメートの一人が、有名な **Google Cloud** 上に宿題日記を作成し、メンバーそれぞれがタスクを更新して進捗状況を確認するというアイデアを提案します。そこで、各メンバーはタスクを更新し、進捗状況を確認することができます。グループ全員がすぐに同意し、日記を作り始めました。あなたは、プロジェクトが形になっていくのを見ながら、ある生徒の顔に はにかんだ笑み が浮かんでいることに気づきます。😼<br/>

The next day, you discover that this cunning student has exploited their access to the API keys, altering the diary to mark all their homework as completed. 🫢  
翌日、この狡猾な生徒が API キーへのアクセスを悪用し、日記を改ざんして宿題をすべて完了したことにしていることが判明しました。🫢<br/>

Shocked and disappointment spread through the group, and you realize that the centralized solution has failed to provide the transparency and security you all craved for.  
衝撃と失望がグループ全体に広がり、中央集中型ソリューションが、皆さんが切望していた透明性と安全性を提供できていないことに気づきます。

Determined to find a better way, the group gathers once more, and you share the idea of building the collaborative homework diary on the **Internet Computer**.  
もっといい方法があるはずだと、もう一度集まり、あなたは  **Internet Computer** に共同宿題日記を作るというアイデアを共有しました。<br/>
Your classmates' eyes light up as they understand the potential of a decentralized platform to foster transparency, unity, and trust among your classmates. 🫂  
クラスメイトの透明性、結束、信頼を育む分散型プラットフォームの可能性を理解し、クラスメイトの目が輝きます。 🫂
## 🧑‍🏫 Requirements 前提条件 
Your task is to create a collaborative homework diary, implement as a canister. The homework diary will allow students to create, edit, delete, and view their homework tasks.  
あなたの課題は、キャニスターとして実装される共同作業用の宿題日記を作成することです。宿題日記では、生徒が宿題のタスクを作成、編集、削除、閲覧できます。
## 📒 Steps / ステップ
0. Import the type `Time` for the `Time` library. / `Time` ライブラリの `Time` 型をインポートしなさい。
1. Define a record type `Homework` that represents a homework task. A Homework has a title field of type `Text`, a description field of type `Text`, a dueDate field of type `Time`, and a completed field of type `Bool`. / 宿題を表すレコードタイプ `Homework` を定義しなさい。宿題は `Text` 型の title フィールド、`Text` 型の description フィールド、`Time` 型の dueDate フィールド、および `Bool` 型の completed フィールドを持ちます。
2. Define a variable called `homeworkDiary` that will be used to store the homework tasks. Use a suitable data structure (such as `Buffer` or `Array`) for this variable. / 宿題を格納するための `homeworkDiary` という変数を定義しなさい。この変数には、適切なデータ構造（`Buffer` や `Array` など）を使用します。
3. Implement `addHomework`, which accepts a homework of type `Homework`, adds the homework to the `homeworkDiary`, and returns the id of the homework. The id should correspond to the index of the homework in `homeworkDiary`. / `homework` 型の宿題を受け取り、その宿題を `homeworkDiary` に追加し、その宿題の id を返す `addHomework` を実装しなさい。id は `homeworkDiary` 内の宿題のインデックスに対応する必要があります。
```motoko
addHomework: shared (homework: Homework) -> async Nat;
```
4. Implement `getHomework`, which accepts a homeworkId of type `Nat`, and returns the corresponding homework wrapped in an Ok result. 
If the homeworkId is invalid, the function should return an error message wrapped in an `Err` result. / `Nat` 型の homeworkId を受け取り、対応する宿題を Ok 結果に包んで返す `getHomework` を実装しなさい。
homeworkId が無効な場合は、エラーメッセージを `Err` 結果で包んで返す必要があります。
```motoko
getHomework: shared query (id: Nat) -> async Result.Result<Homework, Text>;
```
5. Implement `updateHomework`, which accepts a homeworkId of type `Nat` and a homework of type `Homework`, updates the corresponding homework in `homeworkDiary`, and returns a unit value wrapped in an `Ok` result. If the homeworkId is invalid, the function should return an error message wrapped in an `Err` result. / `Nat` 型の homeworkId と `Homework` 型の宿題を受け取り、`homeworkDiary` の対応する宿題を更新し、`Ok` 結果にラップした単位値を返す `updateHomework` を実装しなさい。homeworkId が無効な場合、この関数は `Err` 結果でラップされたエラーメッセージを返す必要があります。
```motoko
updateHomework: shared (id: Nat, homework: Homework) -> async Result.Result<(), Text>;
```
6. Implement `markAsComplete`, which accepts a homeworkId of type `Nat` and updates the completed field of the corresponding homework to `true`, and returns a unit value wrapped in an `Ok` result. If the `homeworkId` is invalid, the function should return an error message wrapped in an `Err` result. / `Nat`型の homeworkId を受け取り、対応する宿題の completed フィールドを `true` に更新し、`Ok` 結果にラップされたユニット値を返す `markAsComplete` を実装しなさい。`homeworkId` が無効な場合は、エラーメッセージを `Err` でラップして返す必要がある。
```motoko
markAsCompleted: shared (id: Nat) -> async Result.Result<(), Text>;
```
7. Implement `deleteHomework`, which accepts a `homeworkId` of type `Nat`, removes the corresponding homework from the `homeworkDiary`, and returns a unit value wrapped in an `Ok` result. If the `homeworkId` is invalid, the function should return an error message wrapped in an `Err` result. / `deleteHomework`を実装しなさい。この関数は `Nat` 型の `homeworkId` を受け取り、`homeworkDiary` から該当する宿題を削除し、`Ok` 結果にラップされた Unit 値を返す。もし `homeworkId` が無効であれば、この関数は `Err` 結果で包まれたエラーメッセージを返すべきです。
```motoko
deleteHomework: shared (id: Nat) -> async Result.Result<(), Text>;
```
8. Implement `getAllHomework`, which returns the list of all homework tasks in `homeworkDiary`. / `homeworkDiary`に含まれるすべての宿題のリストを返す `getAllHomework` を実装しなさい。
```motoko
getAllHomework: shared query () -> async [Homework];
```
9. Implement `getPendingHomework` which returns the list of all uncompleted homework tasks in `homeworkDiary`. / `homeworkDiary` の未完了の宿題のリストを返す `getPendingHomework` を実装しなさい。
```motoko
getPendingHomework: shared query () -> async [Homework];
```
10. Implement a `searchHomework` query function that accepts a `searchTerm` of type `Text` and returns a list of homework tasks that have the given `searchTerm` in their title or description. / `text` 型の `searchTerm` を受け取り、与えられた `searchTerm` をタイトルまたは説明に含む宿題のリストを返す `searchHomework` クエリ関数を実装しなさい。
```motoko
searchHomework: shared query (searchTerm: Text) -> async [Homework];
```
11. Deploy the howework diary on the Internet Computer. / Internet Computer に howework diary をデプロイしなさい。
## 📺 Interface / インターフェイス
> At the end of the project, your canister should implement the following interface.

> プロジェクト終了時には、キャニスターは以下のインターフェイスを実装している必要があります。

```motoko
actor {
    // Add a new homework task / 新しい宿題を追加する
    addHomework: shared (homework: Homework) -> async Nat;

    // Get a specific homework task by id / IDで特定の宿題のタスクを取得する
    getHomework: shared query (id: Nat) -> async Result.Result<Homework, Text>;

    // Update a homework task's title, description, and/or due date / 宿題のタイトル、説明、期限を更新する。
    updateHomework: shared (id: Nat, homework: Homework) -> async Result.Result<(), Text>;

    // Mark a homework task as completed / 宿題を完了したことにする
    markAsCompleted: shared (id: Nat) -> async Result.Result<(), Text>;

    // Delete a homework task by id / 宿題のタスクをidで削除する
    deleteHomework: shared (id: Nat) -> async Result.Result<(), Text>;

    // Get the list of all homework tasks / すべての宿題のリストを取得する
    getAllHomework: shared query () -> async [Homework];

    // Get the list of pending (not completed) homework tasks / 保留（未完了）になっている宿題のリストを取得する
    getPendingHomework: shared query () -> async [Homework];

    // Search for homework tasks based on a search terms / 検索条件をもとに宿題を検索することができる
    searchHomework: shared query (searchTerm: Text) -> async [Homework];
}
```
