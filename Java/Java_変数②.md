# 変数を理解する

ここからJavaでの変数の使い方を学習していきます。

変数の役割は、Javaの場合でもRubyと変わりありません。
ただし、先にもご紹介した通りJavaでは「宣言」を行わないと変数を使うことはできません。

## 変数の宣言と使い方

変数を宣言するためには、以下のように型名に続けて変数名を記述します。

```
型名　変数名;
```

行末に「;（セミコロン）」がついていることに注意しましょう。

Javaでは、命令の終わりにセミコロンが必要で、書き忘れるとエラーになります。

宣言した後の変数は、Rubyと同様に使うことができます。

```java:Main.java
class Main {
  public static void main(String[] args) {
    int radius;
    radius = 5;
    System.out.println(radius * radius * 3.14);
  }
}
```
なお、上記の1,2,6,7行目はJavaでは必ず書かなくてはいけないコードです。これらのコードを削除しないよう注意しましょう。

下記の「//ここに処理を記述する」と書かれた箇所にコードを記述していきます。

```java
class Main {
  public static void main(String[] args) {
    //ここに処理を記述する
  }
}
```

実行すると、計算結果が「78.5」と表示されます。

いま実行したコードの意味を確認しておきましょう。

```java
int radius;
radius = 5;
System.out.println(radius * radius * 3.14);
```

1.int radius;によって、int型の変数radiusを宣言する

2.radius = 5;によって、変数radiusに整数の5を代入する

3.printlnを実行して、計算結果を出力する。



このコードについて、今は必ず書かなくてはいけないテンプレートのようなものだと捉えてください。

また、System.out.printlnは、（）で囲んだ中身を出力するメソッドで、Rubyのputsに相当するものです。

このように、Javaで変数を使用する際には、まず型の宣言が必要です。

ただし、Javaには「型推論」と呼ばれる仕組みがあり、宣言に関するコードを省略することができます。

# 型推論を理解する

まず型推論を利用した変数の宣言方法について見てみましょう。

```java
var 変数名 = 値
```

このように、「var」を使って宣言を行い、初期値を代入します。

この記述を行うと、値の種類によってデータ型が推論され、推論されたデータ型で宣言が行われます。

###  型推論を使ってみよう

```java
class Main {
  public static void main(String[] args) {
    var radius = 5;
    System.out.println(radius * radius * 3.14);
  }
}
```

### プログラムを実行しよう

先ほどと同じ演算結果が出力され、正しく動作していることがわかります。

このようにvarを使用すると、代入する値（今回の例では5）からデータ型を推論してくれるため、int型であるという宣言が不要になります。

###  データ型の種類を確認しよう

```java
class Main {
  public static void main(String[] args) {
    var radius = 5;
    System.out.println(radius * radius * 3.14);

    `System.out.println(((Object)radius).getClass().getSimpleName());`
  }
}
```
上記のように追加の記述をします。

### プログラムを実行しよう

実行すると「Integer」と表示され、変数radiusが整数型で宣言されていることがわかります。

なお、データ型の「int」といま出力された「Integer」は異なるものですが、ここではどちらも同じく整数型を表すものと捉えてください。

ここまで学習したように、Javaで変数を使用する際は宣言が必要です。ただし、宣言と同時に初期値を代入する場合は、省略することも可能です。
