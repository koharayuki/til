# Rubyの繰り返しとの違い

配列から要素を取り出す処理を繰り返し行うために、Rubyカリキュラムではeachメソッドを学習しました。

Javaにも似た機能を持つ「拡張for文」があります。Rubyのeachメソッドと用途は同じですが、記述の仕方は大きく異なります。

なお、Javaには「拡張」ではない通常の「for文」もあります。

# 拡張for文を理解しよう

## 拡張for文を使ってみよう

###  配列から要素を取り出そう

配列から要素を取り出すために、拡張for文を使ってみましょう。

```java:Main.java
class Main {
  public static void main(String[] args) {
    int[] scores = {1, 5, 10};

    for(int score : scores) {
      System.out.println(score);  
    }
  }
}
```

###  コードを実行しましょう

scoresという配列の要素として、「1, 5, 10」を代入していますが、以下のように拡張for分によって取り出して出力できていることが分かります。

![image](https://github.com/koharayuki/til/assets/132040884/3da5c922-f489-4a9d-9926-5b83424d42fc)

ArrayListからも要素を取り出す場合も使い方は一緒です。

#  ArrayListから要素を取り出そう

```java:Main.java
import java.util.ArrayList;

class Main {
  public static void main(String[] args) {
    ArrayList<Integer> scores = new ArrayList<Integer>();

    scores.add(1);
    scores.add(5);
    scores.add(10);
    scores.add(15);

    for(int score : scores) {
      System.out.println(score);  
    }
  }
}
```

###  コードを実行しましょう

以下のようにArrayListの要素を取り出すことができています。

![image](https://github.com/koharayuki/til/assets/132040884/fbec575c-ae0d-43e2-916b-180b303c0db8)

配列とArrayListとでは、作成方法は異なるものの、要素を取り出すためのコードは同じであることが分かります。

配列の場合と比べて要素の数を１つ増やしていますが、取り出すためのコードはそのままで正しく動作しています。

# 拡張for文の使い方を理解しよう

拡張for文を使用する際の構文を確認しましょう。

```java
for ( 要素を格納する変数宣言  :  配列あるいはArrayListの変数名) {
  取り出した要素を使用して行う処理
}
```

この記述を行うと、以下のように動作します。

1.配列、あるいはArrayListから要素を1つ取り出す

2.取り出した要素を変数に代入する

3.{}内の処理を行う

4.配列、あるいはArrayListの要素数分だけ処理を繰り返す

先ほど以下のようにコードを記述しましたが、変数scoresから要素を取り出し、ing型の変数scoreに代入するという動作になっています。

```java
for(int score : scores) {
  System.out.println(score);  
}
```

Rubyのeachメソッドとは書き方が異なるものの、使い方は似ていることがわかったのではないでしょうか。

