# オブジェクト指向とは

「ある役割を持ったモノ」ごとにクラス（プログラム全体の設計図）を分割し、
モノとモノとの関係性を定義していくことでシステムを作り上げようとするシステム構成の考え方のことです。

# アプリケーション実装
※自動販売機のようなサンプルアプリ(自販機アプリケーション)を例に解説を進めます。

## 用意すべきクラスを考える

アプリケーションを実装する前に、まずはこのアプリケーションについてどのようなクラスを用意すべきなのかを考えます。クラスを考える際は、「このアプリケーションにおいて、どのような処理が存在するのか」に着目します。

この自販機アプリケーションには、以下のような処理が存在しそうです。

- 商品のデータを作成する
- ユーザーに販売している商品一覧を見せる
- 購入したい商品を決める
- お金を投入する
- 投入金額からお釣りの計算をする（購入処理を行う）
これらの処理を、役割の種類ごとに分類し、それぞれをクラスとします。上記を分類すると、以下のような形になります。

| クラス             | 意味           | 何をするのか                                            |
| ---------------- | -------------- | ---------------------------------------------------- |
| Drink            | 販売する飲み物    | 投入された飲み物を実体のあるデータ(インスタンス)にする。          |　
| VendingMachine   | 自販機          | ユーザーに販売している商品を見せて、投入金額からお釣りの計算をする。  |　
| User             | 購入する人       | 購入したい商品を決めて、お金を投入する。                       |　

このアプリケーションには、このように少なくとも3つのクラスが必要ということになります。

「自販機アプリケーションなので、自販機クラスだけ用意すればいいのでは？」と考えた方かもいるかと思います。しかし、その場合、以下のように「自販機が行うべきでないこと」も、自販機のクラスに含まれてしまうことになります。

![image](https://github.com/koharayuki/til/assets/132040884/86b6097b-e718-4e20-add7-d8b3d90a78ce)

このようなアプリケーションになってしまうと、後からこのアプリケーションを修正する人は 「**なぜ自販機自身が投入金額を決めているの**？」 と疑問を抱き、このアプリケーションの仕様が捉えにくくなります。すなわち、修正がしにくくなり、保守性が悪くなってしまうのです。

それぞれのクラスには、明確な役割が1つだけ与えられている必要があります。これを**単一責任の原則**といいます。

### 単一責任の原則

アプリケーションの設計を考える上で、必要となる決まりの1つです。上記の自販機アプリケーションでは、自販機・飲み物・購入する人の役割が1つ程度になるように分割されています。このように、「1つのクラスは1つの振る舞いしか持たない」という原則を意識しないと、他者からみた時に意図のわからないアプリケーションが完成してしまいます。


# クラスを定義する

これまでに、このアプリケーションは、3つのクラスによって成立することを学びました。それでは、まずは`application.rb`に必要なクラスを定義しましょう。

```ruby:ruby_application_training/application.rb
class Drink
end

class VendingMachine
end

class User
end
```

# 商品が登録できるようにする

自販機で飲み物を販売するためには、商品となる飲み物のデータを生成する必要があります。

##  飲み物のデータを生成する

以下のようにDrinkクラスを定義し、3つデータが登録できるようにします。生成した飲み物のデータは配列`drinks`の中に格納します。最後に配列の中身を確認するために、`puts drinks`で出力します。

```ruby:ruby_application_training/application.rb
class Drink
  def initialize(name, fee)
    @name = name
    @fee = fee
  end

  def name
    @name
  end

  def fee
    @fee
  end
end

class VendingMachine
end

class User
end

puts "商品を用意してください。"
drinks = []
3.times do |i|
  puts "商品名を入力してください。"
  drink_name = gets.chomp
  puts "金額を入力してください。"
  drink_fee = gets.to_i
  drinks << Drink.new(drink_name,drink_fee)
end

puts drinks
```

29行目に着目しましょう。`Drink.new(drink_name,drink_fee)`として、Drinkクラスのインスタンスを生成しています。実引数として渡しているのは、飲み物の名称と金額です。Drinkクラス内では、与えられた値をもとに、インスタンス変数を生成しています。

そして、`drinks << Drink.new(drink_name,drink_fee)`の記述で、用意した配列drinksに生成したインスタンスを追加しています。

下図のような流れになります。

![image](https://github.com/koharayuki/til/assets/132040884/8fdd9447-dcf5-4638-ac5a-054d5e3ece5a)

上記のコードが記述できたら、コードを実行しましょう。以下のように3つのデータが出力すれば成功です。
これはDrinkクラスから生成したインスタンス（飲み物のデータ）です。`3.times`を用いて3回入力しているので、3つのデータが生成できます。

![image](https://github.com/koharayuki/til/assets/132040884/abfbaa36-05d0-4552-a75d-fe3070ff18a5)


# 商品を表示する

商品の登録ができたので、それらをユーザーが購入できるように表示します。商品の情報を表示するのはVendingMachineクラスの役割です。

```ruby:ruby_application_training/application.rb
class Drink
  def initialize(name, fee)
    @name = name
    @fee = fee
  end

  def name
    @name
  end

  def fee
    @fee
  end
end

class VendingMachine
  def initialize(drinks)
    @drinks = drinks
  end

  def drinks
    @drinks
  end

  def show_drinks
    puts "いらっしゃいませ。以下の商品を販売しています"
    i = 0
    self.drinks.each do |drink|
      puts "【#{i}】#{drink.name}: #{drink.fee}円"
      i += 1
    end
  end
end

class User
end

puts "商品を用意してください。"
drinks = []
3.times do |i|
  puts "商品名を入力してください。"
  drink_name = gets.chomp
  puts "金額を入力してください。"
  drink_fee = gets.to_i
  drinks << Drink.new(drink_name,drink_fee)
end

vending_machine = VendingMachine.new(drinks)
vending_machine.show_drinks
```

48行目に着目しましょう。`vending_machine = VendingMachine.new(drinks)`でVendingMachineクラスのインスタンスを生成しています。
インスタンス生成の際、39~46行目で登録した3つの商品情報を含む配列drinksを、実引数として渡しています。initializeメソッドで生成した`@drinks`には、受け取った配列の情報が代入されています。

そして48行目で生成したインスタンスに対して、49行目でshow_drinksメソッドを適用します。show_drinksメソッドは、`@drinks`に含まれる配列の情報を1つずつ表示しています。
`self.drinks.each do |drink|`の**self**は、show_drinksメソッドを適用された**インスタンス自身**が、同じクラス内で定義されているインスタンスメソッド`drinks`を利用することを宣言しています。
なお、このタイミングで1つ前のステップで記述した`puts drinks`は削除してください。

## self

Rubyのインスタンスメソッド内でのselfは、**selfが記載されているインスタンスメソッドを適用したインスタンス**を意味するキーワードです。今回の場合、selfが記載されているインスタンスメソッドが「25行目のshow_drinks」で、これを適用したインスタンスが「48行目で生成されたVendingMachineクラスのインスタンス」です。つまり、今回のselfは「48行目で生成されたVendingMachineクラスのインスタンス」を指しています。

また、29行目の`puts "【#{i}】#{drink.name}: #{drink.fee}円"`という記述は、Drinkクラスのインスタンスがインスタンスメソッド「name」と「fee」を利用している形です。
この2つのメソッドの中身はそれぞれ@nameと@feeのみで、つまり自身のインスタンス変数の値を、戻り値としています。

このようなインスタンス変数の値のみを戻り値としたメソッドのことを特別に**ゲッター**と呼びます。

## ゲッター

クラスに設定したインスタンス変数の値を、インスタンスから読み取って表示するためだけに定義するメソッドです。
上のdrinkクラスのように、インスタンスを生成してそれぞれ別々の値をインスタンス変数に定義し、あとでその情報を利用することはよくあります。
なので、クラスを定義する際はゲッターを用意することがほとんどです。

**ゲッター**と対になる概念を**セッター**と呼びます。

## セッター

あるインスタンスが持つインスタンス変数の値を更新するためだけのメソッドのことを**セッター**と呼びます。
今回は出てきませんが、具体的なセッターの定義例を以下に示します。

```ruby:sample.rb
class Human
  #humanクラスのインスタンス変数は@name, @ageとする。
  def initialize
    puts "名前を入力してください"
    @name = gets.chomp
    puts "年齢を入力してください"
    @age = gets.to_i
  end

  #ゲッター
  def name
    @name
  end

  def age
    @age
  end

  #セッター
  def name=(set)
    @name = set
  end

  def age=(set)
    @age = set
  end
end
```

セッターのメソッド名は必ず`def インスタンス変数名=`とします。=が名前に含まれているのがポイントです。

上記の例のように定義したセッターは、以下のように利用します。

```ruby:sample.rb
  human = Human.new
  #initializeメソッドで@nameに"takashi", @ageに25を代入したとする
  #ゲッターでインスタンス変数の値を確認
  puts human.name
  #=> "takashi"
  puts human.age
  #=> 25

  #セッターを利用して、インスタンス変数の値を書き換える
  human.name = "satoshi"
  human.age = 20

  #再びゲッターでインスタンス変数の値を確認
  puts human.name
  #=> "satoshi"
  puts human.age
  #=> 20
  ```

セッターの使い方は少し特殊です。実はRubyには、「名前に`=`がついたメソッドの呼び出しの際のメソッド名`=`の前後はいくら半角スペースを空けても構わない」という仕様と、
「引数の()は省略できる」という仕様があります。これを利用して、あたかも変数代入かのようにセッターを利用するのが慣例となっています。
上の例では、`human.name`という変数に"satoshi"を再代入しているように感じます。しかし実態は`human.name=("satoshi")`となっており、
`name=`という名前に=を含むメソッドが定義され引数を受け取って、メソッド内でインスタンス変数に再代入する、ということをやっています。

少し脱線しましたが、ここまでのコードは下図のような流れになります（途中のコードを省略しています）。

![image](https://github.com/koharayuki/til/assets/132040884/34d8961a-de87-4682-aa0e-d043c48daac1)

上記のコードが記述できたら、コードを実行しましょう。以下のように3つの商品が表示すれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/983ee586-faf2-48d4-aac1-f96d1e71404d)


# 投入金額を決める

これまでの実装で、登録した商品を表示するところまでできました。続いて、表示された商品から、自販機に投入する金額を決めます。投入金額を決めるのは購入者の役割なので、Userクラスに記述します。

##  商品を表示する









