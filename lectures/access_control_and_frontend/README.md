# Access Control / アクセス制御

This project demonstrates a simple example of how to implement access control in a web application using Motoko and JS. The application tracks the number of times different users have clicked a button. We demonstrate two different strategies for authentication: using a secret key and authenticating with Internet Identity using the `@dfinity/ii-login-button` web component.  
このプロジェクトでは、Motoko と JS を使用して Web アプリケーションにアクセス制御を実装する方法の簡単な例を示しています。このアプリケーションは、異なるユーザーがボタンをクリックした回数を追跡します。秘密鍵の使用と、`@dfinity/ii-login-button` ウェブコンポーネントを使用した Internet Identity による認証 の２つの異なる戦略を実演しています。

## Demo / デモ

You can try out the demo [here](https://qizwk-hqaaa-aaaab-qaida-cai.icp0.io/).  
デモは [こちら](https://qizwk-hqaaa-aaaab-qaida-cai.icp0.io/) で試せます。

## How to run locally / ローカルで実行する方法

### Prerequisites / 前提条件

- [Node.js](https://nodejs.org/en/download/) >= 12.0.0
- [DFINITY Canister SDK](https://internetcomputer.org/docs/current/tutorials/deploy_sample_app)

### Steps / ステップ

1. Clone this repo and install dependencies:  
このレポをクローンして、依存関係をインストールします：

```bash
git clone git@github.com:krpeacock/access-control-tutorial.git
cd access-control-tutorial
npm install
```

2. Start the local internet computer emulator:  
ローカルの Internet Computer エミュレーターを起動します：
```bash
dfx start --background --clean --host "127.0.0.1:4943"
```

3. Deploy the canisters:  
キャニスターをデプロイします：

```bash
dfx deploy
```

You can open the app there in your browser, or you can run the vite dev server:  
ここでアプリをブラウザで開いてもいいし、vite dev server を起動してもいいです：

```bash
npm run dev
```

## How it works / 仕組みについて

In the backend, the canister stores a map of counts with the principal as the key. The canister has three methods:  
バックエンドでは、キャニスターは Principal をキーとするカウントのマップを保存します。キャニスターは、3つのメソッドを備えています：

- increment
- getCount
- getCounts

The `increment` method increments the count for the principal that calls it. The `getCount` method returns the count for the principal that calls it. The `getCounts` method returns the counts for all principals.  
`increment` メソッドは、それを呼び出した Principal のカウントを増加させます。`getCount` メソッドは、それを呼び出した Principal のカウントを返します。`getCounts` メソッドは、すべてのプリンシパルのカウントを返します。

The frontend has a single page. It includes an input that converts the string into an `Ed25519KeyIdentity`. It displays the principal that you will be calling with, and then anytime you click the button, it will update the count for that principal and display the new count.  
フロントエンドには１つのページがあります。このページには、文字列を `Ed25519KeyIdentity` に変換する入力があります。ボタンをクリックすると、そのプリンシパルのカウントが更新され、新しいカウントが表示されます。

There is also a button to log in with Internet Identity. This will open a popup that will prompt you to log in with Internet Identity. Once you log in, it will display your principal and you can click the button to increment your count.  
また、Internet Identity でログインするボタンもあります。これは、Internet Identity でログインするよう促すポップアップを開きます。ログインすると、Principal が表示され、ボタンをクリックすると、カウントが増加します。

Finally, there is a table of all the identities that have been used with the site.  
最後に、このサイトで使用されたすべての identity の表があります。