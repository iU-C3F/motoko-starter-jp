# Chapter 7: Non-primitives Types. / 非プリミティブ型
## 👯 Tuples / タプル
Tuples are basic units that can encompass multiple elements. While the elements can vary in data type, once declared, the number and type of elements in a tuple cannot be altered. For instance, you could make a tuple that holds a student's name, age & favorite programming language.  
タプルは、複数の要素を包含することができる基本単位です。要素のデータ型は様々ですが、一度宣言したタプルの要素の数と型は変更できません。例えば、生徒の名前、年齢、好きなプログラミング言語を保持するタプルを作成できます。
```motoko
type Student = (Text, Nat, Text);
let me : Student  = ("Bob Smith", 25, "Motoko");
```
In more complex situations, we would create our own object with named fields, making it more readable.  
より複雑な状況では、名前付きフィールドを持つ独自のオブジェクトを作成し、より読みやすいものにします。

The empty tuple type `()` is called the `unit` type. It is usually used as return type for function that returns nothing.  
空のタプル型 `()` は `unit` 型と呼ばれます。これは通常、何も返さない関数の戻り値型として使われます。
```motoko
public func print(t : Text) : async () {
    Debug.print(t);
};
```
## 🎨 Objects / オブジェクト
Objects are more readable than tuples since each field has a name. The  different fields are also each assigned a type which cannot be modified once declared.  
オブジェクトは、各フィールドに名前がついているため、タプルよりも読みやすくなっています。また、異なるフィールドにはそれぞれ型が割り当てられており、一度宣言すると変更できません。   
 Let's define an object called `student`, which contains 4 fields: 
 ここでは、4つのフィールドを持つ `student` というオブジェクトを定義します： 
 - name which is a `Text` indicating the name of the student.
 - name は生徒の名前を示す `Text` です。
 - age which is a `Nat` indicating the age of the student.
 - age は生徒の年齢を示す `Nat` です。
 - favoriteLanguage which is a `Text` indicating the favorite programming language of the student.
 - favoriteLanguage は、学生の好きなプログラミング言語を示す `Text` です。
 - graduate which is a `Bool` indicating if the students has already graduated from the Motoko Bootcamp. 
 - graduate は、その受講生がすでに Motoko ブートキャンプを卒業しているかどうかを示す `Bool` です。

```motoko
let student = {
    name = "John";
    age = 35;
    favoriteLanguage = "Motoko";
    graduate = true;
};
```
Similar to other variables in Motoko, objects can be mutable or immutable. The object we've just defined is immutable, once the fields have been assigned a value they cannot be modified.  
Motoko の他の変数と同様に、オブジェクトにもミュータブルとイミュータブルがあります。先ほど定義したオブジェクトはイミュータブルで、一度フィールドに値が割り当てられたら変更することはできません。

```motoko
let student = {
    name = "John";
    age = 35;
    favoriteLanguage = "Motoko";
    graduate = true;
};
student.age += 1;  
```
This code will throw an error `expected mutable assignment target`.  
このコードでは、`expected mutable assignment target` というエラーが発生します。  

To create an object that can be modified, we must use the `var` keyword in the field definition. Let's modify the previous example so that only the student's age can be changed, while the other fields remain constant.  
変更可能なオブジェクトを作成するには、フィールドの定義に `var` キーワードを使用する必要があります。前の例を修正して、生徒の年齢だけを変更できるようにし、他のフィールドは一定のままにしておきましょう。
```motoko
let student = {
    name = "John";
    var age = 35;
    favoriteLanguage = "Motoko";
    graduate = true;
};
student.age += 1; 
```
Objects are often assigned types. In this case we need to create **custom type**.  Let's define a type called `Student` which corresponds the object we've previously created.  
オブジェクトには、しばしば型が割り当てられます。この場合、**カスタムタイプ** を作成する必要があります。 ここでは、先に作成したオブジェクトに対応する `Student` という型を定義してみましょう。
```motoko
type Student = {
    name : Text;
    age : Nat;
    favoriteLanguage : Text;
    graduate : Bool;
};
```

## 🌈 Variants / バリアント
A variant allows you to create a type that contains different cases. A value from the variant type represents one value that is exactly one of the given cases, or tags. Let's define a variant type for a `Vehicle` which can be either a car, a moto or a plane.  
バリアントでは、異なるケースを含むタイプを作成できます。バリアント型の値は、与えられたケース、つまりタグのうちのちょうど１つである１つの値を表します。例えば、車、バイク、飛行機のいずれかになる `Vehicle` のバリアントタイプを定義してみましょう。

```motoko
type Vehicle = {
    #Car;
    #Moto;
    #Plane;
};
```
Each tag can be associated it's own custom type.  
各タグは、独自のカスタムタイプに関連付けることができます。
```motoko
type Car = { make : Text; model : Text; year : Nat; color: Text };
type Moto = { make : Text; model : Text; year : Nat; type : Text };
type Plane = { make : Text; model : Text; year : Nat; seats : Nat };

type Vehicle = {
    #Car : Car;
    #Moto : Moto;
    #Plane : Plane;
};
```

Variants are often used with `switch/case`, which allows to perform control flow on a variant object.  
バリアントはしばしば `switch/case` と共に使用され、バリアントオブジェクトに対して制御フローを実行できます。
```motoko
public func start(v : Vehicle) : async Text {
    switch(v){
        case(#Car(car)){
            // We can access the car object. For instance we can access the make field by using car.make / car オブジェクトにアクセスできます。例えば、car.make を使って make フィールドにアクセスできます。
            let make = car.age;
            return("Vroom 🏎️");
        };
        case(#Moto(m)){
            // We can give the object any name that is convenient. In this case we can access the type by using m.type.
            let type = m.type; / オブジェクトには都合の良い名前を付けることができます。この場合、m.type を使うことで type にアクセスできます。
            let type = m.type；
              return("Roar 🏍️");
        };
        case(#Plane(x)){
            // Here we go again.. we can access the number of seats by using x.seats / またまたです。x.seats を使って座席数にアクセスできます。
            let seats = x.seats;
             return("Whoosh 🛫");
        };
    };
};
```
## ✍️ Mutable Arrays / ミュータブル配列
Read [this section](https://web3.motoko-book.dev/common-programming-concepts/types/mutable-arrays.html?highlight=Mutable%20arrays#mutable-arrays) from the Motoko Book.  
Motoko ブックの [このセクション](https://web3.motoko-book.dev/common-programming-concepts/types/mutable-arrays.html?highlight=Mutable%20arrays#mutable-arrays) を読んでください。
## ⏭️ Iterators / イテレータ
Read [this section](https://web3.motoko-book.dev/base-library/utils/iter.html?highlight=Itera#iteriterate) from the Motoko Book.  
Motoko ブックの [このセクション](https://web3.motoko-book.dev/base-library/utils/iter.html?highlight=Itera#iteriterate) を読んでください。
