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

<サンプルコード>
```java
class Main {
  public static void main(String[] args) {
    int value = 3;

    if (value > 0){
      System.out.println("値は正です"); 
    }else if (value < 0){
      System.out.println("値は負です"); 
    }else {
      System.out.println("値は0です"); 
    }
  }
}
```

基本的に使い方は同じで、以下のように記述します。

```java
if (条件A) { 
  // 処理A
} else if () {
  // 処理B
} else {
  // 処理C
}
```

条件を満たすかどうかで分岐が行われ、以下の動作になります。

- 条件Aが「真」の時は処理Aが実行される
- 条件Aは「偽」で、条件Bが「真」の時は処理Bが実行される
- 全ての条件が「偽」の時は処理Cが実行される

このように処理の流れはRubyと一緒ですが、Rubyの「elsif」は、Javaでは「else if」と記述することに注意しましょう。




