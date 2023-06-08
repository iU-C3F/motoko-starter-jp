# Chapters / 各章の内容
## Introduction / はじめに
- Installation & prerequesites.
- インストール＆プレリクエスト。
- Motoko Playground.
- Motoko 遊び場
## Chapter 1: Fundamental Concepts / 第1章：基本的なコンセプト
- What is a canister?
- キャニスターとは？
- WebAssembly and why do we need Motoko?
- WebAssembly と、なぜMotokoが必要なのか？
- The actor model.
- アクターモデル。
- Update vs Query.
- アップデート vs クエリー。
- Fuel on the Internet Computer: cycles.
- Internet Computer 上の燃料：cycle。
## Chapter 2: Common programming concepts. (MB) / 第2章 プログラミングの共通概念 (MB)
- Variables & Mutability.
- 変数とミュータビリティ。
- Types.
- 型。
- Functions.
- 関数。
- Comments.
- コメント。
- Control flow.
- コントロールフロー。
## Chapter 3: Primitive Types in Motoko. (MB) / 第3章 Motoko のプリミティブ型 (MB)
- `Nat`.
- `Int`.
- `Bool`.
- `Text`.
- `Char`.
- `Float`.
- `Blob`.
- `Nat8`, `Nat16`, `Nat32`, `Nat64`, `Int8`, `Int16`, `Int32`, `Int64`.
## Chapter 4: Candid the language of the Internet Computer. / 第4章 Internet Computer の言語 Candid
- Why do we need Candid? 
- なぜ Candid が必要なのか？
- What is an IDL?
- IDL とは？
- The Candid file (`.did`).
- Candid ファイル (`.did`) 。
## Chapter 5: Modules and the Base library (MB) / 第5章 モジュールとベースライブラリ(MB)
## Chapter 6: Storing data in our first data structures. (MB) / 第6章 初めてのデータ構造でデータを保存する (MB)
- `Array`.
- `Buffer`.
- `List`.
- `HashMap`.
- `TrieMap`.
## Chapter 7: Non-primitives Types. (MB) / 第7章 ノンプリミティブタイプ (MB)
- Tuples.
- タプル。
- Records.
- レコード。
- Variants.
- バリアント。
- Arrays.
- 配列。
- Mutable Arrays.
- ミュータブルな配列
- Iterators.
- イテレーター。
## Chapter 8: Advanced Types. (MB) / 第8章：高度な型 (MB)
- Optional types.
- オプショナル型
- Generic types.
- ジェネリック型
- Recursive types.
- 再帰型。
- Shared types.
- Shared 型。
## Chapter 9: Handling errors. / 第9章 エラーのハンドリング
- The `Result` type.
- `Result` 型
- The `Error` type.
- `Error` 型
- Trap. 
- Trap。
- Try/Catch.
- Try/Catch。
## Chapter 10: Identity on the Internet Computer. / 第10章： Internet Computer 上の ID
- Digital signatures.
- 電子署名。
- Messages.
- メッセージ。
- The concept of Principal.
- Principal のコンセプト
- PEM File.
- PEM ファイル。
- Accessing the message & the caller.
- メッセージと caller へのアクセス。
- The `Principal` type in Motoko.
- Motoko における `Principal` 型
- The Anonymous principal.
- アノニマスな Principal。
## Chapter 11: Intercanister calls. / 第11章：インターキャニスターコール
- Calling an actor by reference.
- 参照でアクターを呼び出し。
- Importing from another canister 
- 他のキャニスターからのインポート 
    - Locally
    - ローカル
    - Mainnet
    - メインネット
- Async values.
- Async の値。
- Atomicity & commit point.
- 原子性とコミットポイント
## Chapter 12: Upgrading a canister. / 第12章：キャニスターのアップグレード。
- Stable memory vs Heap memory.
- ステーブルメモリ vs ヒープメモリ。
- Stable variables.
- ステーブル変数。
- Stable types.
- ステーブル型。
- Interface changes.
- インターフェイスの変更。
- Data structure changes.
- データ構造の変更。
- Stable type signature.
- ステーブルタイプのシグネチャー。
- Metadata section.
- メタデータ部。
- Verifying upgrade compatibility.
- アップグレードの互換性の確認。
## Chapter 13: Playing with time. / 第13章 時間と遊ぶ
- `Time`
- `Timer` 
- `Heartbeat`
## Chapter 14: Mastering randomnes. / 第14章 ランダムネスを使いこなす。
- The issue when dealing with randomness in a deterministic system.
- 決定論的なシステムでランダム性を扱う場合の問題点。
- The `Random` library in Motoko and how to use it.
- Motokoの `Random` ライブラリとその使用方法。
## Chapter 15: Managing multiple canisters with actor classes. / 第15章 アクタークラスで複数のキャニスターを管理する。
- Actor classes.
- The management canister.
- Creating a canister factory.
- アクタークラス。
- マネージメントキャニスター。
- キャニスターファクトリーの作成。
## Chapter 16: Binary operations in Motoko. / 第16章 Motoko におけるバイナリ演算。
- Binary operations.
- バイナリの演算。