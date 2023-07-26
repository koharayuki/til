# オブジェクトの作成

## JavaScriptにおけるオブジェクトの概念

JavaScriptにおけるオブジェクトとは、データや処理といった情報を1つにまとめた集合体です。
例えば、以下のような情報があるとします。

| データ                                      | 処理               |
| ------------------------------------------ | ----------------- |
| ・名前：テストさん <br>・性別：男性<br>・年齢：25歳	   | ・歩く<br>・食べる     |　

これらの情報を「human」として1つにまとめると、オブジェクトが出来上がります。

![image](https://github.com/koharayuki/til/assets/132040884/ea2915c0-0724-4996-8b8f-54529ebbcd49)

上図における「データ」や「処理」はどの様にJavaScriptのコードで表すことができるのでしょうか？まずは、「データ」について解説します。

データとは、「キー」と「バリュー」のセットを指します。
このキーとバリューがセットになったものを`プロパティ`と言います。

##  プロパティ

プロパティとは、ハッシュ形式（キーとバリューの組み合わせ）で書かれる値のことで、オブジェクトの要素（中身）を決める役割をします。
つまり、「`オブジェクトは、プロパティの集合体から成り立っている`」と言うことができます。

プロパティの書き方は、以下の通りです。

![image](https://github.com/koharayuki/til/assets/132040884/fd7eeca0-ece2-40f5-a39e-ccde08c9d693)

### 変数を定義し、その中にプロパティを記述する方法を確認する

以下のコードは、変数humanを定義し、その中にプロパティを記述した場合です。
例として、プロパティは「name」「gender」「age」の3つです。

```javascript:オブジェクトとプロパティ
let human = { 
  name: "Jhon",
  gender: "man",
  age: 24,
 }
 ```

上記のように、プロパティは複数記述することが可能です。

![image](https://github.com/koharayuki/til/assets/132040884/cbc73496-ff7d-448a-8eb8-e0d17f8b1f9b)  
  
  
# オブジェクトのプロパティを操作

### オブジェクトの値を取得する

プロパティの値を取得したい場合は、`オブジェクト名.プロパティ名`のように記述することで、オブジェクトのプロパティの値を取得することができます。

```javascript:コンソール
let human = { name: 'yamada' }

console.log(human.name)
```

以下のようにコンソール上にyamadaの文字列が表示されていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/2593b181-f120-42c7-8adc-5e41be046e89)

上記のコードを例にするとオブジェクト名がhumanで、プロパティ名がnameです。したがって、`human.name`と記述することでyamadaという値が取得することができました。

### オブジェクトにプロパティを追加する

オブジェクトにプロパティを追加する方法は以下の2つあります。

- オブジェクト.プロパティに値を代入する
- オブジェクト['プロパティ']に値を代入する

上記の記述によって、オブジェクトにプロパティを追加することができます。以下のコードを実行して確認してみましょう。

```javascript:コンソール
let human = { name: 'yamada' }
console.log(human)

human.age = 25
human['address'] = 'Tokyo'

console.log(human)
```

ブラウザのコンソールを確認して、以下のように結果が表示されていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/20ef33fe-41b8-45c4-a438-098e9e10d8ce)

はじめにhumanオブジェクトを定義した時は、nameプロパティの値のみがhumanに格納されている状態でした。
そこから`human.age = 25`と`human['address'] = 'Tokyo'`と記述することで、nameプロパティに加え、
新しくageプロパティとaddressプロパティの値をhumanオブジェクトに格納することができました。

### プロパティの値を変更する

`オブジェクト名.プロパティ = 変更したい値`と記述することで、プロパティの値を変更することができます。

```javascript:コンソール
let human = {
  name: "yamada",
  age: 25,
  address: 'Tokyo'
}

console.log(human.name)

human.name = "yabe"
console.log(human.name)
```

ブラウザのコンソールを確認して、以下のように結果が表示されていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/9f489ff4-b1b3-43a7-a02e-63ce9c4cefd5)

human.nameは元々は"yamada"という値が格納されていました。<br>
しかし、`human.name = "yabe"`と記述することで、yamadaという値をyabeに上書きすることができました。

##  (JavaScriptにおける) メソッド

JavaScriptおけるメソッドとは、プロパティに紐づけられた処理のこと指します。プロパティには、「〇〇をしてほしい」という処理を、**関数**を用いることで代入できます。

メソッドの書き方は、以下の通りです。

![image](https://github.com/koharayuki/til/assets/132040884/e1eb46f6-8056-4f9d-97e0-a083d0c8b45d)

※以下のコードでは、6行目にメソッドを定義し、9行目で実行しています。

```javascript:オブジェクトのメソッド
let human = {
  name: "Tom",
  gender: "man",
  age: 22,

  talk: function(){...},
}

human.talk()
// talkメソッドが実行される
```

上記のコードでは、変数humanが定義され、そのhumanの要素（name, gender, age）が記述されています。
このような要素を持ったhumanに対して`”話す” という処理（動作）`をして欲しい場合、9行目のように「human.talk」と記述することができます。  

  
# オブジェクトのメソッドを操作する

```javascript:オブジェクトのメソッド
let human = {
  name: "Tom",
  gender: man,
  age: 22,

  walk: function(){...},
  talk: function(){...},
  eat: function(){...}
}

human.walk()
// walkメソッドが実行される

human.talk()
// talkメソッドが実行される

human.eat()
// eatメソッドが実行される
```

### メソッドを実行する

```javascript:コンソール
let human = {
  name: "yamada",
  age: 25,
  address: 'Tokyo',

  talk: function(){
    console.log(`私の名前は${human.name}、${human.age}歳です。住所は${human.address}です`)
  }
}

human.talk()
```

ブラウザのコンソールを確認して、以下のように結果が表示されていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/862509eb-d34d-474a-8655-e2a0890396e1)

humanオブジェクトの中にtalkというメソッドを定義しました。<br>
このメソッドの役割はconsole.logを用いて、あらかじめ記述した文字列をコンソール上に表示することです。<br>
human.talk()という記述でメソッドが実行され、talkメソッドの処理が実行されました。

