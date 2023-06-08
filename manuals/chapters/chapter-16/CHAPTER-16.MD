# Chapter 16: Binary operations in Motoko / 第16章 Motoko におけるバイナリ演算
## 🧮 Binary operations / バイナリ演算
Motoko supports Bitwise operations (manipulation of the bits) through bounded integers (`Nat8`,`Nat16`, `Nat32`, `Nat64` & `Int8`,`Int16`, `Int32`, `Int64`).  
Motoko は、有界整数 (`Nat8`, `Nat16`, `Nat32`, `Nat64` & `Int8`, `Int16`, `Int32`, `Int64`) によるビット演算（ビットを操作すること）に対応しています。
- AND (Symbol `&`): This operation takes two binary values and performs a logical AND operation on each pair of corresponding bits. The result is a binary value where each bit is set to 1 only if the corresponding bits in both operands are set to 1.
- AND（記号 `&`）： この演算は２つのバイナリ値を取り、対応するビットの各ペアに対して論理 AND 演算を実行します。結果は、両方のオペランドの対応するビットが１に設定されている場合にのみ、各ビットが１にセットされるバイナリ値です。
```motoko
let a = 31 : Nat8;  // Binary 0011111
let b = 33  : Nat8; // Binary 0100001
let c = a & b (1)  // Binary 0000001 
assert(c == 1) // true
```
- OR (Symbol `|` ): This operation takes two binary values and performs a logical OR operation on each pair of corresponding bits. The result is a binary value where each bit is set to 1 if either or both corresponding bits in the operands are set to 1.  
- OR (記号 `|`)： この演算は、２つのバイナリ値を取り、対応するビットの各ペアに対して論理 OR 演算を実行する。結果は、オペランドの対応するビットのいずれか、または両方が１に設定されている場合、各ビットが１にセットされるバイナリ値です。
```motoko
let a = 31 : Nat8;  // Binary 0011111
let b = 33  : Nat8; // Binary 0100001
let c = a | b (63)  // Binary  0111111
```
- XOR (Symbol `^`): This operation takes two binary values and performs a logical XOR (exclusive OR) operation on each pair of corresponding bits. The result is a binary value where each bit is set to 1 if only one of the corresponding bits in the operands is set to 1.
- XOR（記号 `^`）： この演算は、２つのバイナリ値を取り、対応するビットの各ペアに対して論理 XOR（排他的論理和）演算を実行します。結果は、オペランドの対応するビットのうち１つだけが１に設定されている場合、各ビットが１にセットされるバイナリ値です。
```motoko
let a = 31 : Nat8;  // Binary 0011111
let b = 33  : Nat8; // Binary 0100001
let c = a ^ b (62)  // Binary  0111110
```
- Shift Left (Symbol `<<`): This operations moves the bits to the left by a specified number of positions, adding zeros to the right.  
- 左シフト（記号 `<<`）．ビットを指定された数だけ左に移動し、右にゼロを追加する操作です。
```motoko
let a = 64 : Nat8; //    binary 01000000
let c = a << 1 (128) //  binary 10000000 
```
- Shift right (Symbol `>>`): This operations moves the bits to the right by a specified number of positions, adding zeros to the left.  
- 右シフト（記号 `>>`）： ビットを指定された数だけ右に移動させ、左にゼロを追加する操作です。
```motoko
let a = 64 : Nat8; //    binary  01000000
let c = a << 1 (32) //   binary  00100000
```
- Rotation left (Symbol `<<>`): This operations shifts the bits of a binary value to the left by a specified number of positions, and then rotating the shifted bits back to the right end of the value.
- 左回転（記号 `<<>`）．バイナリ値のビットを指定された数だけ左に移動し、そのビットを回転させて値の右端に戻す操作です。
```motoko
let a = 128 : Nat8;     //  binary  1000000
a <<> 1 (1)             //  binary  0000001 
```
- Rotation right (Symbol `<>>`): This operations shifts the bits of a binary value to the right by a specified number of positions, and then rotates the shifted bits back to the left end of the value. 
- 右回転（記号 `<>>`）．バイナリ値のビットを指定された数だけ右にシフトし、シフトされたビットを回転させて値の左端に戻す操作です。
```motoko
let a = 64 : Nat8;      // binary 001000000
a <>> 1 (32)            // binary 000100000
```
