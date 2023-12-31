# 無限ループ

繰り返し処理を実装する際に、覚えておきたい概念として`「無限ループ」`があります。もしかしたら、みなさんも日常会話で聞いたことがあるかもしれません。

この無限ループという言葉は、元はプログラム上で使われていた用語です。改めて説明するまでもないですが、無限ループとは「処理が永遠に繰り返されること」を指します。

ここでは無限ループを2つのサンプルコードで紹介します。

まずは1つめです。先ほどのコードを再掲します。

```ruby:sample.rb
number = 0

while number <= 10
 puts number
 number += 1 
end
```

例えば上記のコードからnumber += 1の部分を削除したらどうなるでしょうか？

number変数の値は常に0のままなので、while number <= 10の判定は常に真となり、無限に0がターミナルに出力されます。

これが`無限ループ`です。

では2つめです。上記のコードを少し編集しました。

```ruby:sumple.rb
number = 0

while true
 puts number
 number += 1
end

# ターミナル出力結果
# 0
# 1
# 2
# 3
# 4
# 5
# 6
# 7
# 8
# 9
# 10
# .
# .
# .
```

while trueの部分に着目してください。while文ではwhileの右の式を判定し、最終的に真偽値（true/false）に変換して繰り返すかどうかを決めます。

上記のコードは、この特性を利用し、**条件式の部分にはじめからtrueと書くことによって意図的に無限ループを発生させている**のです。

`※無限ループはコンピュータに大きな負荷をかけてしまうので、繰り返し処理を実装する場合は特に注意が必要です。`


# ループから抜け出す方法

自分で設定したループからわざわざ抜け出す必要なんてあるのかと疑問に思われるかもしれませんが、ある特定の条件になったらループから抜け出すという処理はよく使います。

ループから抜け出すにはbreakを使います。

##  break

`break`は、eachメソッドやwhile文などのループから脱出するために使われます。

```ruby:sumple.rb
number = 0

while number <= 10
 puts number
 number += 1
end
```

実行結果が0〜10までの連番になることは解説しました。では上記のコードを一部編集します。以下を見てください。

```ruby:sumple.rb
number = 0

while number <= 10
 if number == 5
   break
 end
 puts number
 number += 1
end

# ターミナル出力結果
# 0
# 1
# 2
# 3
# 4
```

上記のコードでは、if文を追加しています。そしてnumber変数の値が5だったときにbreakを実行しています。

すると、実行結果を見てもわかる通り、出力結果は4で止まっています。

つまり、number変数の値が5の時にif文内のbreakが実行され、ループから抜け出していることが確認できます。

このようにif文などの条件分岐とbreakを使うと、特定の条件のときにループを脱出することができます。

