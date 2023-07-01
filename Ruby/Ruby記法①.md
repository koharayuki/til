# 条件分岐

## if文以外の条件分岐

これまで、Rubyの条件分岐にはif文を用いました。

しかし、Rubyにはif文以外にも条件分岐を表現する文法としてcase文があります。

###  case文

case文とは、条件分岐を表現するための文法です。複数の条件を指定する時に、if文のelsifを重ねるよりもシンプルにコードを書くことができます。

並列する条件が多数ある場合は、if文よりもcase文を使った方がコードとして読みやすくなります。

case文の構文は以下の通りです。

```ruby:sample.rb
case 対象のオブジェクトや式
when 値1
 # 値1に一致する場合に実行する処理
when 値2
 # 値2に一致する場合に実行する処理
when 値3
 # 値3に一致する場合に実行する処理
else
 # どれにも一致しない場合に実行する処理
end
```

## 具体的なコードを見てみよう

【if文】
```ruby:sample.rb
country = "Japan"

if country == "Japan"
 puts "こんにちは"
elsif  country == "America"
 puts "Hello"
elsif  country == "France"
 puts "Bonjour"
elsif  country == "China"
 puts "你好"
elsif  country == "Italy"
 puts "Buon giorno"
elsif  country == "Germany"
 puts "Guten Tag"
else
 puts "..."
end
```

【case文】
```ruby:sample.rb
country = "Japan"

case country
when "Japan"
 puts "こんにちは"
when "America"
 puts "Hello"
when "France"
 puts "Bonjour"
when "China"
 puts "你好"
when "Italy"
 puts "Buon giorno"
when "Germany"
 puts "Guten Tag"
else
 puts "..."
end
```

上記では、`case country`の部分が条件の対象となります。そして、`when`で指定した値と`country`の中身が一致するかで条件を判定しています。

if文と比べると記述がシンプルになっていることが確認できます。このように並列する条件が多数ある場合は、case文を使うことを検討しましょう。


# 繰り返し処理

繰り返し処理で思い浮かぶのはeachメソッドではないでしょうか。eachメソッドは、配列に対して使うことができるメソッドでした。

Rubyでは他にも繰り返し処理用の構文が用意されています。

## 条件式付きの繰り返し処理

Rubyの繰り返し処理用の構文の中の1つがwhile文です。

###  while文

繰り返し処理を行うためのRubyの構文です。指定した条件が真である間、処理を繰り返します。

while文の構文は以下の通りです。

```ruby:sample.rb
while 条件式 do
 # 条件が真である時に繰り返す処理
end
```

※条件式の後のdoは省略することができます。

## 具体的なコードを見てみよう

```ruby:sample.rb
number = 0

while number <= 10
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
```

上記のコードでは、一番初めに変数numberに0を代入しています。そしてwhile number <= 10の部分では、条件を判定しています。ここでは条件式の後のdoを省略しています。

当然、条件は0 <= 10で真になるので、puts numberで0が出力されます。number += 1では、変数numberに1を加えています。

endまで行ったらwhile文は繰り返し処理を行うかどうかの判定を行ないます。先ほど変数numberの値は1になったので、条件は1 <= 10で真になりますね。

したがって、再度while文の中の処理を実行します。これを条件が偽になるまで繰り返します。結果的にターミナルには0から10までの連番が出力されます。

