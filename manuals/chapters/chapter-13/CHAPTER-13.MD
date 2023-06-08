# Chapter 13: Playing with time in Motoko. / 第13章 Motoko で時間で遊ぶ。
## 🕣 Time
A challenge that comes with a distributed system such as the Internet Computer is the notion of time. Each node has it's own internal horloge. To respected determinisn, the time provided to the canister is the **system time** - a value agreed upon by the subnet. The **system time** is represented as nanoseconds since 1970-01-01.  
Internet Computer のような分散型システムで課題となるのは、時間の概念です。各ノードには独自の内部時計があります。キャニスターに提供される時間は、サブネットで合意された値である **システム時間** であることを尊重します。**システム時間** は、1970-01-01 からのナノ秒として表されます。

In Motoko, the type `Time` is an aliast for `Int`.  
Motoko では、`Time` という型は `Int` のエイリアスです。
```motoko
public type Time = Int;
```
The Time module gives us access to the `now()` function that returns the system time.  
Time モジュールは、システム時刻を返す `now()` 関数へのアクセスを提供します。  
```motoko
import Time "mo:base/Time";
actor {
    public type Time = Time.Time;
    public func whatTimeIsIt() : async Time.Time {
        Time.now();
    };
};
```

The time returned by `Time.now()` is constant within a message execution.  
`Time.now()` が返す時刻は、メッセージの実行範囲内で一定です。
```motoko
import Time "mo:base/Time";
import Debug "mo:base/Debug";
actor {
    public type Time = Time.Time;

    func doSomething() :  () {
        Debug.print("Doing some work");
    };

    public func whatTimeIsIt() : async (Time, Time) {
        let a = Time.now();
        doSomething();
        let b = Time.now();
        return (a, b);
    };
};
```
The value of `a` and `b` will be the same. Try it out [here](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=4264079271).  
`a` と `b` の値は同じになります。試しに [こちら](https://m7sm4-2iaaa-aaaab-qabra-cai.ic0.app/?tag=4264079271) で試してみてください。
## ⏰ Timer / タイマー
Sometimes you need to run tasks a on regular basic (every minute/hour/day...). To run cronic tasks, you can use the [Timer library](https://internetcomputer.org/docs/current/motoko/main/base/Timer).  
定期的に（1分毎、1時間毎、1日毎...）タスクを実行する必要がある場合があります。定期的なタスクの実行には、[Timer library](https://internetcomputer.org/docs/current/motoko/main/base/Timer) を利用できます。

This library defines two types:  
本ライブラリでは、2つのタイプを定義しています：
1. `Duration` represents a delay before executing the job. The delay provided can be as small as possible but the resolution cannot be faster than the block rate.  
`Duration` は、ジョブを実行するまでの遅延を表します。提供される遅延は可能な限り小さくすることはできますが、ブロックレートより速くすることはできません。
```motoko
type Duration = {#seconds : Nat; #nanoseconds : Nat}
```
2. `TimerId` is an ID to identify the timer.  
`TimerId` は、タイマーを識別するための ID です。
```motoko
type TimerId = Nat
```

This library exposes different methods:  
このライブラリでは、さまざまなメソッドを公開しています：
- `setTimer` allows  you to set a `job` that will be executed once in the future after the given duration `d` has passed.
- `setTimer` は、与えられた時間 `d` が経過した後に、将来一度だけ実行される `job` を設定できます。
```motoko
func setTimer(d : Duration, job : () -> async ()) : TimerId
```
```motoko
let oneHourInSeconds = 60 * 60;
func endExam() : async () {
    Debug.print("🔚")
};
let id = setTimer(#seconds(oneHourInSeconds), endExam);
```

- `recurringTimer` allows you to set a `job` that will be executed chronically everytime the given duration `d` has passed. 
- `recurringTimer` は、与えられた期間 `d` が経過するたびに継続的に実行される `job` を設定できます。
```motoko
func recurringTimer(d : Duration, job : () -> async ()) : TimerId
```
```motoko
let oneDayInSeconds = 60 * 60 * 24;
func study() : async () {
    Debug.print("🙇")
};
let studyId = reccuringTimer(#seconds(oneDayInSeconds), study);
```
- `cancelTimer` will cancel an active timer. If the `id` provided is not recognized nothing happens.
- `cancelTimer` は、アクティブなタイマーをキャンセルします。指定された `id` が認識されない場合は、何も起こりません。
```motoko
let cancelTimer : TimerId -> ()
```
```motoko
func quitSchool() {
    cancelTimer(studyId);
};
```
## 🫀 Heartbeat / ハートビート
A canister can exposes a system function `heartbeat`. 
This function is automatically triggered by the protocol at every round of execution, approximately every second.  
キャニスターは、システム関数 `heartbeat` を公開できます。この関数は、プロトコルの実行ラウンドごとに、およそ１秒ごとに自動的にトリガーされます。

```motoko
import Debug "mo:base/Debug";
import Time "mo:base/Time";
actor {

    public type Time = Time.Time;

    var count : Nat = 0;
    var times : [Time] = [] 

    system func heartbeat() : async () {
        count += 1;
        if(count % 100 == 0) {
            // Every 10O invocations of the heartbeat function.
            times := Array.append<Time>(times, [Time.now()]);
        } 
    };
}
```

> The **heartbeat** functionality is being replace by **timers** due to prohibitive costs.

> **ハートビート** 機能は、法外なコストのため、**タイマー** に置き換えられています。