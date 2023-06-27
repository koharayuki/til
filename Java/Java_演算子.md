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

```
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



