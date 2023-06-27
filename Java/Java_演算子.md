# Rubyの演算子との違い

Javaの代数演算子・比較演算子は、使用する記号も演算の行い方もRubyと同じです。

# 代数演算子を理解しよう

## 代数演算子の種類

Javaで使用する代数演算子には以下の種類があります。

| 演算子 | 使い方  | 意味  |
| ----- | ------ | ---- |
| +     | a + b  |加算  |　
| -     | a - b  |減算  |　
| *     | a * b  |乗算  |　
| /     | a / b  |除算  |　
| %     | a % b  |剰算  |

## 代数演算子を使ってみよう

### Javaで四則演算を行なってみよう

```java:Main.java
class Main {
    public static void main(String[] args) {
        System.out.println(1000 + 2000);
        System.out.println(3000 - 1500);
        System.out.println(50 * 40);
        System.out.println(600 / 15);
        System.out.println(5 % 2);
    }
}
```
### コードを実行しよう

https://tech-master.s3.amazonaws.com/uploads/curriculums//f9c466ce00f0bbd4463f1b8c01a68e91.png

特に違和感を感じる部分はないのではないでしょうか。


# 比較演算子を理解しよう

代数演算子と同様に、比較演算子についてもRubyと違いはありません。

## 比較演算子の種類

| 演算子  | 使い方   | 意味                 |
| ------ | ------- | ------------------- |
| ==     | a == b  |aとbが等しい場合true    |　
| <      | a < b   |aがbより小さい場合true   |　
| >      | a > b   |aがbより大きい場合true   |　
| <=     | a <= b  |aがb以下の場合true     |　
| >=     | a >= b  |aとb以上の場合true      |　
| !=     | a! = b  |aとbが等しくない場合true  |　

このように使う記号や意味はRubyの場合と全く一緒です。


