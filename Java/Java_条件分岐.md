# Rubyのif文との違い

Javaのif文は、Rubyとは記述方法が若干異なるものの、使い方はほとんど同じです。

# if文を理解しよう

Javaの条件分岐にはいくつか種類があります.

## if文を使ってみよう

###  if文を使ってみよう

<replitのエディタ>
```java
class Main {
  public static void main(String[] args) {
    int value = 3;

    if (value > 0){
      System.out.println("値は正です"); 
    }
  }
}
```

###  コードを実行しましょう

「値は正です」と出力されます。

https://tech-master.s3.amazonaws.com/uploads/curriculums//50a1b89d4356ae508b2eec327ec809ff.png
コードを見るとRubyと似ていることが分かります。


# if文の使い方を理解しよう

if文は以下のように記述します。

```java
if ( 条件式 ) {
  条件式を満たす時に実行する処理
}
```

Rubyでの記述方法と異なるのは以下の点です。

- 条件式を（）で囲む必要があること
- 行いたい処理を{}で囲む必要があること

また、Rubyのif文を学習した際に、さらに細かい条件を指定するためのelseやelsifについて学びました。

これらについても、RubyとJavaで大きな違いはありません。





