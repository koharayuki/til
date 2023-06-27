# 配列のさまざまな記述方法を理解しよう

配列の宣言方法として、以下の３種類を理解しましょう。

## 1.配列の宣言と同時に、要素の作成も行う方法

先ほど実行したコードでは、以下のように配列の宣言と要素の作成を別に行っていました。

```java
int[] scores;
scores = new int[3];
```

この２つは、以下のように1行で記述することもできます。

```java
int[] scores = new int[3];
```

## 2.配列の宣言時に型推論を使用する方法

変数の宣言について学習した際に、型推論について学びました。この型推論は配列でも使用することができます。

型推論を使った配列の宣言は以下のようになります。

```java
var scores = new int[3];
```

int型の要素３つを代入することで、scoresはそれらを格納する配列であることが推論されています。


## 3.配列の宣言から値の代入まで全て同時に行う方法

配列の宣言時に代入する値が確定している場合は、以下のように記述を省略することができます。

```java
int[] scores = {1, 5, 10};
```

この記述方法が最も簡潔ですが、宣言時に代入する値が確定していない場合は使用できません。

# リストを理解しよう

リストは、Rubyの配列と似たデータ管理の仕組みです。
以下の特徴があります。

- 要素を順序づけて管理する
- 要素を事後的に追加したり削除できる

また、Javaのリストには、以下の2種類があります。

- ArrayList
- LinkedList


# ArrayListを理解しよう

ArraListは「可変長配列」を使用するための仕組みです。可変長配列とは、文字通り長さ（要素数）を変更できる配列のことです。

Rubyの配列は可変長なので、Javaの配列よりもArrayListの方が性質や使い方が近いものとなっています。

## ArrayListを使ってみよう

```java:Main.java
import java.util.ArrayList;

class Main {
  public static void main(String[] args) {
    ArrayList<Integer> scores = new ArrayList<Integer>();

    scores.add(1);
    scores.add(5);
    scores.add(10);
    scores.add(15);

    System.out.println(scores.get(0));
    System.out.println(scores.get(1));
    System.out.println(scores.get(2));
    System.out.println(scores.get(3));
  }
}
```

ArrayListを使用する際は、事前にライブラリのインポートが必要です。
上記のコードを記述する際は、`1行目にimport文があることに注意しましょう。`

##  コードを実行してみよう

以下のように４つの要素の内容が出力されます。

https://tech-master.s3.amazonaws.com/uploads/curriculums//0e3d044e46ffad610503f0538a1b9893.png

# ArrayListの使い方を理解しよう

先ほど記述したコードでは、以下の４つを行なっています。

1.ライブラリをインポートする

2.ArrayListの宣言を行う

3.ArrayListに値を代入する

4.ArrayListから要素を取り出す

## 1.ライブラリをインポートする

ArrayListを使用する際は、ライブラリのインポートが必要です。
インポートするには、ファイルの冒頭に以下の記述を行います。

```java
import java.util.ArrayList;
```

なお、インポートする際のライブラリの指定方法などを覚える必要はありません。後のレッスンで導入する開発環境を利用すると、自動的に補完することができます。

## 2.ArrayListの宣言を行う

ArrayListの宣言と初期化は以下のように行います。

```java
ArrayList<データ型> scores = new ArrayList<データ型>();
```

先ほどのコードでは、整数を格納するArrayListを作成したので、以下のように記述しました。

```java
ArrayList<Integer> scores = new ArrayList<Integer>();
```

ここで行っているのは、以下の２つの動作です。

1.整数（Integer）を格納するArrayListを「score」という名称で宣言

2.ArrayListの要素を作成

そして、①に②を代入しています。

なお、要素のデータ型を右辺でも指定していますが、これは省略することが可能です。
以下のように記述しても問題なく動作します。

```java
ArrayList<Integer> scores = new ArrayList<>();
```

## 3.ArrayListに値を代入する

ArrayListに要素を追加するためにはaddメソッドを使用します。

記述は、`add(要素として追加する値)`のように行います。

先ほど実行した以下のコードでは、scoresという名称のArrayListに「1」を追加しました。

```java
scores.add(1);
```

addメソッドを使用すると、要素はArrayListの`末尾に追加`されます。

## 4.ArrayListから要素を取り出す

要素を取り出す際は、getメソッドを使用します。

記述は、`get(取得したい要素のインデックス）`のように行います。配列から要素を取り出す際と同様に、「1番目」の要素を取り出したい時は、インデックスとして「0」を指定します。

先ほど実行した以下のコードでは、scoresから、1番目の要素を取得しています。

```java
scores.get(0)
```

