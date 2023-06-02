# Chapter 12: Upgrading a canister. / 第12章 キャニスターをアップグレード
Upgrading a canister is a common task. However, there are a few things to consider before doing so, notably:  
キャニスターのアップグレードは、一般的な作業です。しかし、その前に考慮しなければならないことがいくつかあります：
- Could the upgrade cause data loss?
- アップグレードによってデータ損失が発生する可能性はありますか？
- Could the upgrade break the dApp due to interface changes?
- アップグレードにより、インターフェースの変更により、dApp が壊れる可能性はありますか？
## Stable memory vs Heap memory / ステーブルメモリ と ヒープメモリ の比較
A canister has access to two types of memories:  
キャニスターは２種類のメモリにアクセスできます：
1. A wasm heap which is constrained to 4 GiB because currently the runtime of canisters [wasmtime](https://github.com/bytecodealliance/wasmtime) has only 32 bit addressing. This limit will be increased when [wasm64](https://github.com/WebAssembly/memory64) is supported by the runtime. The heap is a “pile" of memory, it is space available to the canister to allocate and de-allocate as needed. The heap is wiped during upgrades. The heap is the fastest memory available to the canister.  
キャニスターのランタイム [wasmtime](https://github.com/bytecodealliance/wasmtime) は現在３２ビットアドレッシングしか持たないため、4 GiB に制限された wasm ヒープ。この制限は、[wasm64](https://github.com/WebAssembly/memory64) がランタイムでサポートされたときに増える予定です。ヒープはメモリの "山" であり、キャニスターが必要に応じて割り当てたり解除したりできるスペースです。ヒープはアップグレードの際に消去されます。ヒープは、キャニスターが利用できる最速のメモリーです。

2. A [stable memory](https://internetcomputer.org/docs/current/references/ic-interface-spec#system-api-stable-memory) that can currently store up to 48GiB of storage. Everything in stable memory will survive upgrades. Accessing data in stable memory is slower compared to accessing memory in the heap because stable memory is not directly accessible within the runtime environment. Instead, accessing stable memory requires calling an external API.  
現在 48 GiB まで保存できる [ステーブルメモリ](https://internetcomputer.org/docs/current/references/ic-interface-spec#system-api-stable-memory) 。ステーブルメモリにあるものはすべてアップグレードに耐えられます。ステーブルメモリ内のデータへのアクセスは、ヒープ内のメモリへのアクセスに比べて遅くなります。これは、ステーブルメモリがランタイム環境内で直接アクセスできないからです。その代わりに、ステーブルメモリにアクセスするには、外部の API を呼び出す必要があります。

> Developers who are new to the IC often ask the question: which memory should I use? Unfortunately, there is no one-size-fits-all answer to this question. The optimal choice depends on the requirements of your application (safety during upgrade over performances) and the amount of memory you'll need. If you are interested, [read & join the discussion over this topic that is constantly evolving](https://forum.dfinity.org/t/motoko-stable-memory-in-2022/10433). 

> IC を初めて使う開発者は、どのメモリーを使えばいいのか、という質問をよくします。残念ながら、この質問に対する画一的な答えは存在しません。最適な選択は、アプリケーションの要件（性能よりもアップグレード時の安全性）と必要なメモリー量に依存します。もしご興味があれば、[常に進化しているこのトピックに関するディスカッションを読んで、参加してみてください](https://forum.dfinity.org/t/motoko-stable-memory-in-2022/10433)。

## Stable variables. / Stable 変数
When a canister is upgraded, the state is lost by default. This means all data application data will be lost, unless it's handled to persist when the canister is upgraded.  
キャニスターがアップグレードされると、デフォルトでステートが失われます。つまり、キャニスターのバージョンアップ時に永続するように処理されない限り、アプリケーションのすべてのデータが失われることになります。<br/>
This can be achieved by storing the data in stable variables, which will persist upgrades. To declare a variable as stable we use the `stable` keyword.  
これは、データをステーブル変数に格納することで実現でき、アップグレードを持続させることができます。変数をステーブルにしたものとして宣言するには、`stable` キーワードを使用します。
```motoko
stable var m : Int = 0;
```
The value of `m` will persits upgrades and not be lost. 
A stable variable is stored in the stable memory.  
`m`の値はアップグレードしても失われることはありません。
ステーブル変数は、ステーブルメモリに保存されます。
## Stable types. / Stable 型
Unfortunately, not all variables can be declared as stables.  
残念ながら、すべての変数がステーブルとして宣言できるわけではありません。
```motoko
stable let map = HashMap.HashMap<Principal, Student>(1, Principal.equal, Principal.hash);
```
If we try with the `HashMap` type that we've seen earlier we will encounter an error: `variable map is declared stable but has non-stable type`.  
先ほどの `HashMap` 型で試すと、`variable map is declared stable but has non-stable type` というエラーが発生します。

All primitives types are stable:  
すべてのプリミティブタイプは stable です：
- `Nat` 
- `Text`
- `Ìnt`
- All bounded numbers すべての有界数 : `Nat8`, `Nat16`, `Nat32`, `Nat64`, `Int8`, `Int16`, `Int32`, `Int64`.
- `Float`
- `Char`
- `Bool`
- `Array`

An object that contains methods (i.e a Class) cannot be stable. That's why `HashMap` & `TrieMap` cannot be declared as stable structures.  
メソッドを含むオブジェクト（つまりクラス）は、ステーブルな構造にはなり得ません。だから、`HashMap` や `TrieMap` はステーブルな構造体として宣言できないのです。

> It is possible to rewrite some libraries to convert them to stable types. For instance, [StableBuffer](https://github.com/canscale/StableBuffer) is a remake of the `Buffer` type allowing it to be called stable.  

> いくつかのライブラリを書き換えて、ステーブル型に変換することは可能です。例えば、[StableBuffer](https://github.com/canscale/StableBuffer) は `Buffer` 型をリメイクして stable と呼べるようにしたものです。

## Interface changes. / インターフェイスの変更
Another challenge when upgrading a canister in a distributed environment like the Internet Computer is that other canisters might be relying on the interface of the canister being upgraded.  
Internet Computer のような分散環境でキャニスターをアップグレードする場合のもう一つの課題は、他のキャニスターがアップグレードされるキャニスターのインターフェースに依存している可能性があることです。

Let's imagine that we have two canisters:  
２つのキャニスターがあることを想像してみましょう：
1. Canister A is the canister that we want to upgrade. It contains many public functions but we will just focus on `getDiploma`.  
キャニスター A は、アップグレードしたいキャニスターです。多くのパブリック関数が含まれていますが、ここでは`getDiploma`にのみ焦点を当てます。
```motoko
import HashMap "mo:base/HashMap";
import Principal "mo:base/Principal";
import Time "mo:base/Time";
actor School {

    type Diploma = {
        delivery_time : Time.Time;
        teacher : Principal;
        promotion : Nat;
    };

    let diplomas = HashMap.HashMap<Principal, HashMap>(0, Principal.equal, Principal.hash);

    public func getDiploma(p : Principal) : async ?Diploma {
        return diplomas.get(p);
    };

};
```

2. Canister B is the client canister that is relying on the interface of Canister A. We have to imagine that somewhere in the code of Canister B the `getDiploma` function of Canister A is called.  
キャニスター B のコードのどこかで、キャニスター A の `getDiploma` 関数が呼び出されていることを想像する必要があります。  
[TODO : Change canister ID];
```motoko
actor dApp {
    type Diploma = {
        delivery_time : Time.Time;
        teacher : Principal;
        promotion : Nat;
    };

    // We define the other canister in the code here.
    let schoolActor : actor {
        getDiploma(p : Principal) -> async ?Diploma;
    } =  actor("3db6u-aiaaa-aaaah-qbjbq-cai"); 

    public func shared ({ caller }) isAuthorized() :  async Bool {
        let answer = await schoolActor.getDiploma(caller);
        switch(answer){
            case(null){
                return false;
            };
            case(? some){
                return true;
            };
        };
    };
};
```
Suppose we're upgrading canister A and we decide to remove the `getDiploma` function. If we do that, it will cause problems for canister B because it relies on that function. But it's not just removing the function that could cause issues. If we modify the function's signature to something like this:  
キャニスター A をアップグレードする際に、`getDiploma` 関数を削除することにしたとします。そうすると、キャニスター B がその関数に依存しているため、問題が発生します。しかし、問題を引き起こす可能性があるのは、関数を削除するだけではありません。関数のシグネチャを次のように変更すると、問題が発生します：

```motoko
getDiploma(p : Principal) -> async Result.Result<Diploma, Text>;
```
That change alone would also break canister B's code.
Whenever a canister on the IC is upgraded, it causes a risk to all relying canisters, we have to find a way to not break things!  
その変更だけで、キャニスター B のコードも壊れてしまいます。
IC のキャニスターがアップグレードされるたびに、依存するすべてのキャニスターにリスクが発生するのですが、物事を壊さない方法を見つけなければなりません！<br/>

That's where the magic of **Candid** comes into play!  
そこで、**Candid** の魔法が活躍するのです！<br/> 
Candid defines a formalism and precise rules to make sure that any modification of the interface (adding new methods, changing function signatures, expecting additional arguments...) doesn't break existing clients.  
Candid は、インターフェイスの変更（新しいメソッドの追加、関数のシグネチャ変更、追加の引数の期待...）が既存のクライアントを壊さないことを確認するための形式論と正確なルールを定義しています。

For instance, evolving the signature of the `getDiploma` function from  
例えば、`getDiploma` 関数のシグネチャを進化させます。
```motoko
getDiploma(p : Principal) -> async ?Diploma;
```
to  
上記を下記へ
```motoko
getDiploma(p : Principal, bootcampYear: ?Nat) -> async ?Diploma;
```
Would not cause an issue, when reading messages from old clients, who do not pass that argument, a `null` value is assumed.  
問題ないでしょう。この引数を渡さない古いクライアントからメッセージを読み込む場合、 `null` 値が想定されます。

> In the following, all types and interfaces are exprimed in Candid format.

> 以下では、すべての型とインターフェースを Candid 形式で表現します。

Let's look at more examples of what can and can't be done. Imagine the following service  
できること、できないことの例をもっと見てみましょう。次のようなサービスを想像してください。
```
service counter : {
  add : (nat) -> ();
  subtract : (nat) -> ();
  get : () -> (int) query;
}
```
The function `add` could evolve from  
関数 `add` は進化することができます。
```
add : (nat) -> ();
```
to  
上記を下記へ
```
add : (int) -> ();
```
This is possible because every `nat` is also an `int`. If a client provides a `Nat` it will be compatible with the new expected type. We say that `int` is a supertype of `nat`. However evolving the other way wouldn't be possible since all `int` are not `nat`.  
これは、すべての `nat` が `int` でもあることから可能です。クライアントが `Nat` を提供する場合、それは新しい期待される型と互換性を持つことになる。つまり、`int`は`nat`のスーパータイプであると言えます。しかし、すべての `int` は `nat` ではないので、他の方法で進化させることは不可能です。

Additionally the function `add` and `substract` could evolve from  
さらに、関数 `add` と `substract` は、次のように進化する可能性があります。
```
add : (nat) -> ();
subtract : (nat) -> ();
```
to  
上記から下記へ
```
add : (nat) -> (new_val : nat);
subtract : (nat) -> (new_val : nat);
```
This is possible because any new returned value that is not expected by old clients will simply be ignored. However, adding new (non-optional) parameters wouldn't be possible.  
これは、古いクライアントが期待しない新しい戻り値は単に無視されるから可能です。しかし、新しい（オプションでない）パラメータを追加することはできないでしょう。

To safely upgrade a canister, follow those rules:  
キャニスターを安全にアップグレードするために、下記のこれらのルールに従います：
- New methods can freely be added. 
- 新しいメソッドを自由に追加することができます。
- Existing methods can return additional values. Old clients will simply ignore additional values.
- 既存のメソッドは、追加の値を返すことができます。古いクライアントは、単に追加の値を無視します。
- Existing methods can shorten their parameter list. Old clients will send the extra argument(s) but they will be ignored.
- 既存のメソッドは、パラメータリストをより短くできます。古いクライアントは余分な引数を送りますが、それらは無視されます。
- Exisiting methods can only add optional types as new parameters (type `opt`). When reading messages from old clients, who do not pass that argument, a `null` value is assumed.
- 既存のメソッドでは、オプションの型を新しいパラメータとして追加することしかできません (型 `opt`)。この引数を渡さない古いクライアントからメッセージを読み込む場合、`null`値が想定されます。
- Existing parameter types may be changed, but only to a `supertype` of the previous type. For instance a `nat` parameter can be changed to a `int`. 
- 既存のパラメータの型は変更することができますが、以前の型の `supertype` にのみ変更することができます。例えば、`nat` パラメータは `int` に変更できます。
- Existing result types may be changed, but only to a `subtype` of the previous type. For instance an `int` result can be changed to a `nat`. 
- 既存の result 型は変更できますが、以前のタイプの `subtype` にのみ変更できます。例えば、`int` の result は `nat` に変更できます。

> If you want more information on Candid, supertypes and subtypes, check the [reference guide](https://internetcomputer.org/docs/current/references/candid-ref).

> Candid、supertypes、subtypes についてもっと詳しく知りたい方は、[reference guide](https://internetcomputer.org/docs/current/references/candid-ref) をご覧ください。

## Data structure changes. / データ構造の変更
Another example of how data can be lost, is by changing the data types.  
データが失われるもう一つの例として、データ型を変更することが挙げられます。
```motoko
stable var state : Int
```
In this example the variable `state` is `Int`, but let's imagine that during an update the type is changed to `Text`  
この例では、変数 `state` は `Int` ですが、更新中に型が `Text` に変更されたとします。
```motoko
stable var state : Text
```
In this case the the current `Int` value will be lost. One way to avoid the data loss when changing the data types is to keep the original variable, and create a new variable for the new data type. This way the original data will not be lost due to canister upgrades.  
この場合、現在の `Int` 値は失われます。データ型の変更に伴うデータ損失を回避する一つの方法は、元の変数を保持し、新しいデータ型用の新しい変数を作成することです。こうすることで、キャニスターのアップグレードによって元のデータが失われることはありません。
## Stable type signature. / Stable 型の signature
The list of all stable variables of an actor is called the **stable signature**. The textual representation of the **stable signature** looks similar to an actor declaration.  
アクターのすべての stable 変数のリストは、**stable signature** と呼ばれます。stable signature のテキスト表現は、アクター宣言に似ています。
```motoko
actor {
  stable x : Nat;
  stable var y : Int;
  stable z : [var Nat];
};
```
> The stable signature of an actor can be generated using the Motoko compiler: [moc](https://internetcomputer.org/docs/current/motoko/main/compiler-ref).

> アクターの stable signature は、Motoko コンパイラを使って生成できます： [moc](https://internetcomputer.org/docs/current/motoko/main/compiler-ref)。

The stable signature is used to automatically check type compability before an upgrade. This is possible by comparing the signature of the new actor with the old one and using some rules based on Candid. For more information, see the [reference section on stable signatures](https://internetcomputer.org/docs/current/motoko/main/upgrades#stable-type-signatures).  
stable signature は、アップグレードの前に型の互換性を自動的にチェックするために使用されます。これは、新しいアクターのシグネチャーを古いものと比較し、Candid に基づくいくつかのルールを使用することで可能になっています。詳細については、[stable signatures に関する参照セクション](https://internetcomputer.org/docs/current/motoko/main/upgrades#stable-type-signatures) を参照してください。

## Metadata section. / メタデータセクション
The Motoko compiler embeds the **Candid interface** and **stable signature** of a canister as canister metadata, recorded in additional Wasm custom sections of a compiled binary.  
Motoko コンパイラは、キャニスターの **Candid インターフェース** と **stable シグネチャー** をキャニスターのメタデータとして埋め込み、コンパイルしたバイナリーの追加の Wasm カスタムセクションに記録します。

This metadata can be selectively exposed by the IC and used by tools such as `dfx` to verify upgrade.  
このメタデータは IC が選択的に公開し、`dfx` などのツールでアップグレードを検証するために使用できます。
```
$ dfx canister metadata [OPTIONS] <CANISTER_NAME> <METADATA_NAME>
```
## Checking upgrade compatibility / アップグレードの互換性を確認
When you upgrade a canister, `dfx` will automatically download the metadata of the old module and compare it with the new module:  
キャニスターをアップグレードすると、`dfx` は自動的に古いモジュールのメタデータをダウンロードし、新しいモジュールと比較します：
- Compare the Candid interface to make sure there is no breaking change.
- Candid のインターフェイスを比較し、壊れるような変更がないことを確認します。
- Compare the stable signatures to make sure there won't be data loss.
- stable signature を比較し、データの損失がないことを確認します。

If you are making a breaking change you will receive a warning.  
壊れるような変更をする場合は、警告が表示されます。

<p align="center"> <img src="assets/candid_warning.png" width="800px" style="border: 2px solid black;"></p>
<p align="center"> The type of warning you will encounter. </p>
<p align="center"> 遭遇する警告のタイプ </p>

This verification doesn't guarantee that the upgrade will go through. A problem can still happen during the upgrade process. However, it does guarantee that if the upgrade goes through you won't break existing cliens or lose data that was marked as `stable`.  
この検証は、アップグレードが成功することを保証するものではありません。アップグレードの過程で問題が発生することもあります。しかし、アップグレードが成功した場合、既存のクライアントを壊したり、`stable`とマークされたデータを失ったりしないことが保証されます。