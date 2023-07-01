# ブロック

## ブロックの復習

```ruby:sumple.rb
ages = [20, 56, 32]

ages.each do |age|
 puts age
end

# ターミナル出力結果
# 20
# 56
# 32
```

上記は、`eachメソッド`で配列の要素を1つずつ取り出してターミナルに出力しています。

見慣れたコードかもしれませんが、実はこの`do〜end`までをRubyでは**ブロック**と呼びます。また`|age|`のageは**ブロック変数**と呼ばれます。

Rubyにおいて、ブロックは頻出の文法なのでまずは用語をしっかり覚えておきましょう。

また、ブロックをメソッドの引数として渡すことができるのもブロックの特徴です。

例えば、Rubyに標準で組み込まれている`eachメソッド`は、ブロックを引数として受け取るメソッドの代表例です。

以下の図のように`do〜end`までのブロックそのものが`eachメソッド`の引数となり、繰り返し処理が行われています。

![image](https://github.com/koharayuki/til/assets/132040884/7b787f6e-fd72-4d38-bed7-4e010f89eead)

## ブロックの2種類の書き方

ブロックには2種類の書き方があります。

1つめが先ほど例に出したdo...endの形です。

```ruby:sumple.rb
ages = [20, 56, 32]

ages.each do |age|
 puts age
end
```

そして、もう一つが{}を用いた形です。

以下は、上記のコードを{}を用いて書き換えたものです。{}の中身は改行しても問題ありません。

```ruby:sumple.rb
# 改行なし
ages.each {|age| puts age}

# 改行あり
ages.each {|age|
 puts age
}
```

`do...end`と`{}`のどちらを使うかは明確に決まりはありません。

しかし、改行を含む長いコードの場合は`do...end`を使い、1行で収める場合は`{}`を使うことが多いです。

## メソッドでブロックを使う方法

Rubyには、これまでに学んだ`timesメソッド`や`eachメソッド`以外にも多くのメソッドにおいてブロックが用いられています。

では、ブロックはこのようにRubyで元から定義されているメソッドでしか使えないのでしょうか？

そんなことはありません。自分で定義したメソッドでもブロックを使うことができます。

ここでは、自分で定義したメソッドでブロックを用いる方法について解説します。

では、はじめに以下のコードを見てください。

```ruby:sumple.rb
def greeting
 puts "Hello"
end

greeting

# ターミナル出力結果
# Hello
```

※ただテキストを出力するメソッドを実行しているだけです。

```ruby:sumple.rb
def greeting
 puts "Hello"
end

greeting do
 puts "Goodbye"
end

# ターミナル出力結果
# Hello
```

`greetingメソッド`の呼び出し部分に適当なブロックを付けてみました。

実行結果を見てみると、先ほどと変化はありません。

メソッドに渡したブロックを実行するには、以下のようにメソッドの定義内に**yield**を記述する必要があります。

```ruby:sumple.rb
def greeting
 puts "Hello"
 yield
end

greeting do
 puts "Goodbye"
end

# ターミナル出力結果
# Hello
# Goodbye
```

すると、メソッドに紐付けたブロックの処理が実行されていることが確認できます。

## yield

yieldとは、メソッドに渡されたブロックを実行するための命令です。

英語のyieldには、本来「生み出す、降伏する、取って代わられる」などの意味がありますが、Rubyの文脈においては「取って代わられる」に近いです。

上記のコードを見ると、メソッド定義内のyieldが、メソッド呼び出し時に渡したブロックに取って代わられているのがわかります。

このように`yield`は、**メソッド呼び出し時に渡したブロックを実行するため**に使われます。

## yieldの基本的な使い方

```ruby:sumple.rb
def greeting
 puts "Hello"
 yield
end

greeting do
 puts "Goodbye"
end

# ターミナル出力結果
# Hello
# Goodbye
```

上記のコードでは、常に`Goodbye`というテキストが出力されてしまいます。

では、この`Goodbye`の部分を任意のものとするために`text`という変数にしましょう。

そのためには、**メソッドの定義内で`yield`に引数を与える必要があります。**

以下のコードを見てください。

```ruby:sumple.rb
def greeting
 puts "Hello"
 yield("Good afternoon")
end

greeting do |text|
 puts text
end

# ターミナル出力結果
# Hello
# Good afternoon
```

上記のコードでは、メソッドの定義内でyieldの引数としてGood afternoonという文字列を渡しています。そして、メソッドの実行側で、それをブロック変数（|text|）として受け取っています。

## ブロックをメソッドの引数に指定する方法

メソッド内でブロックを実行する方法はyeildのほかにもうひとつあります。それは、**ブロックをメソッドの引数に指定する方法**です。

メソッドの引数としてブロックを受け取る場合には、引数名の前に&をつけます。また、受け取ったブロックは`callメソッド`で実行します。

```ruby:sumple.rb
def greeting(&block)
 puts "Hello"
 block.call("Goodbye")
end

greeting do |text|
 puts text
end

# ターミナル出力結果
# Hello
# Goodbye
```

上記のコードでは、メソッドの引数としてブロックを受け取るために、メソッドの定義部分で`&block`と書いています。
このように、「&引数名」の形でブロックを受け取る引数のことを、**ブロック引数**と呼びます。

そして、そのブロックを実行するために`callメソッド`を実行しています。

`callメソッド`には引数を渡すことができます。今回は`Goodbyeという文字列`をブロックに渡しています。

すると、メソッド呼び出し時に渡しているブロックのブロック変数（|text|）にGoodbyeが代入され、ブロックが実行されます。

