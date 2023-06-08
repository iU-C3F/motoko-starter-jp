# DoubleSpendIssue / 二重支払い問題

This project demonstrates the double spend vulnerability as was presented during the Motoko Bootcamp of 2023. This code is vulnerable on purpose and should not be used in production.  
このプロジェクトは、2023 年の Motoko Bootcamp で発表された、二重支払いの脆弱性を実証しています。このコードは意図的に脆弱性を持たせているので、本番で使用しないでください。

The `SimpleLedger` canister mimicks a ledger but the only supported operations are to deposit tokens and view a balance. The tokens are created out of thin air in a sense that there is no transfer from another account. This is just for demo purposes and doesn't make sense.  
`SimpleLedger` キャニスターは台帳を模倣していますが、サポートされている操作はトークンの入金と残高の確認だけです。トークンは、他の口座から転送されないという意味で、何もないところから作成されます。これはデモのためのもので、意味はありません。

The `DEX` canister holds balances for it's users. Users can get their funds refunded back to the SimpleLedger by calling the refund function. By calling refund multiple times in quick succession, someone can transfer the same balance on the DEX multiple times to the SimpleLedger. Thereby creating new tokens.  
`DEX` キャニスターは、ユーザーの残高を保持します。ユーザーは refund 関数を呼び出すことで、SimpleLedger に資金を払い戻すことができます。払い戻しを何度も連続して呼び出すことで、誰かが DEX の同じ残高を SimpleLedger に何度も転送すできます。それによって新しいトークンが生まれます。

To initialize the balance of the user on the DEX, an `init_account` function is available. To retrieve the local and ledger balance, two getter functions are available.  
DEX 上のユーザーの残高を初期化するために、`init_account` 関数が利用可能です。ローカルと元帳の残高を取得するために、２つのゲッター関数が利用可能です。

Check out the Motoko lecture for more information and to learn how to exploit and mitigate the vulnerabilities present in this code. Have fun!  
このコードに存在する脆弱性を利用し、緩和する方法を学ぶために、より詳細な情報を得るために、Motoko の講義をチェックしてください。楽しんでください！