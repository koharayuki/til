##  クラスを分割する

以下のようにruby_application_trainingディレクトリ内に、ファイルを生成します。

<img width="555" alt="スクリーンショット 2023-07-05 12 36 51" src="https://github.com/koharayuki/til/assets/132040884/a1372df5-9140-4e83-9296-a65d1682ab6b">

続いて、クラスごとに記述を分けましょう。この時、`application.rb`ですべてのファイルを読み込むことにします。


- ruby_application_training/application.rb
```ruby:ruby_application_training/application.rb
require "./drink"
require "./vending_machine"
require "./user"

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

puts "あなたはお客さんです。投入金額を決めてください。"
money = gets.to_i
user = User.new(money)

vending_machine.pay(user)
```

- ruby_application_training/drink.rb
```ruby:ruby_application_training/drink.rb
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
```

- ruby_application_training/user.rb
```ruby:ruby_application_training/user.rb
class User
  def initialize(money)
    @money = money
  end

  def money
    @money
  end

  def choose_drink
    gets.to_i
  end
end
```

- ruby_application_training/vending_machine.rb
```ruby:ruby_application_training/vending_machine.rb
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

  def pay(user)
    puts "商品を選んでください"
    chosen_drink = user.choose_drink
    change = user.money - self.drinks[chosen_drink].fee
    if change >= 0
      puts "ご利用ありがとうございました！お釣りは#{change}円です。"
    else
      puts "投入金額が足りません"
    end
  end
end
```

これで、下図のようにファイルを分け、そして読み込むことができるようになりました。

![image](https://github.com/koharayuki/til/assets/132040884/da775458-45a2-450b-8e58-6b6b3c0257e6)

記述を分けることができたら、念のため再度`application.rb`を実行して、問題なく動作することを確認しましょう。


## 機能の追加と単一責任の原則

ここまでで一通りの実装は完了しました。次に、以下のような追加実装を考えましょう。

----------------------------------------------------------------
### 購入後に、スロットゲームを実行し、3桁の数字が揃ったらあたりでもう1本プレゼント
----------------------------------------------------------------

自販機ではよくある機能です。ここでは、スロットゲームの結果だけを購入後に表示しましょう。

![image](https://github.com/koharayuki/til/assets/132040884/1651a017-62f8-4ab7-a251-307fc42b51e8)


# 追加機能について考える

この機能を追加しようと考えた時に、VendingMachineクラスにメソッドを追加した、以下のような実装が思いつきます。

- スロットゲーム機能を追加した自販機
```ruby:スロットゲーム機能を追加した自販機
class VendingMachine
  def initialize(drinks)
    @drinks = drinks
  end

  def drinks
    @drinks
  end

  def play_slot
    result = []
    3.times do 
      result << rand(0..9)
    end
    puts "スロットゲームの結果は#{result.join}です！"
    if result[0] == result[1] && result[0] == result[2]
      puts "おめでとうございます！"
    else
      puts "残念でした〜"
    end 
  end

  def show_drinks
    puts "いらっしゃいませ。以下の商品を販売しています"
    i = 0
    self.drinks.each do |drink|
      puts "【#{i}】#{drink.name}: #{drink.fee}円"
      i += 1
    end
  end

  def pay(user)
    puts "商品を選んでください"
    chosen_drink = user.choose_drink
    change = user.money - self.drinks[chosen_drink].fee
    if change >= 0
      puts "ご利用ありがとうございました！お釣りは#{change}円です。"
      play_slot
    else
      puts "投入金額が足りません"
    end
  end
end
```

しかし、ここで考えたいのは「スロットゲームを実行すること」は本当に自販機の役割なのか、ということです。スロットゲームが無くても、自販機としての役割は全うできるように思えます。
また、`単一責任の原則`の考えに沿っても、自販機の役割が増えすぎてふさわしくないように思えます。
したがって、このスロットゲームの機能も、飲み物・自販機・ユーザーとは異なる別のクラスとして取り扱うことにしましょう。
このように、スロットゲームのような**目に見えない機能や振る舞いも、役割が異なれば別クラスに分ける必要があります**。
また、今後「ポイントカード機能」「曜日で安くなる機能」「最新のニュースを自販機上に表示する機能」のように追加の機能が増える場合も、新しくクラスを作成して実装する必要があります。


# 追加機能を実装する

## slot_game.rbを作成する

<img width="555" alt="スクリーンショット 2023-07-05 12 47 23" src="https://github.com/koharayuki/til/assets/132040884/d08bb5e2-d82d-43fb-b2b3-810e373b7899">

##  スロットゲーム機能を追加する

以下のようにコードを編集する。まずは、`slot_game.rb`を**require**を用いて読み込む。

- ruby_application_training/application.rb
```ruby:ruby_application_training/application.rb
require "./drink"
require "./vending_machine"
require "./user"
require "./slot_game"

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

puts "あなたはお客さんです。投入金額を決めてください。"
money = gets.to_i
user = User.new(money)

vending_machine.pay(user)
```

続いて、`slot_game.rb`に、スロットゲームそのものの処理を記述する。

- ruby_application_training/slot_game.rb
```ruby:ruby_application_training/slot_game.rb
class SlotGame
  def play_slot
    result = []
    3.times do 
      result << rand(0..9)
    end
    puts "スロットゲームの結果は#{result.join}です！"
    if result[0] == result[1] && result[0] == result[2]
      puts "おめでとうございます！"
    else
      puts "残念でした〜"
    end 
  end
end
```

まず5行目の記述で、3つのランダムな値を生成して配列resultに代入します。続いて7行目でjoinメソッドを用いて配列に含まれる値を、ひと続きに表示します。
その後、8行目で3つの値が揃っているかどうかを判断します。

最後に、`slot_game.rb`に定義したメソッドを呼び出します。

- ruby_application_training/vending_machine.rb
```ruby:ruby_application_training/vending_machine.rb
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

  def pay(user)
    puts "商品を選んでください"
    chosen_drink = user.choose_drink
    change = user.money - self.drinks[chosen_drink].fee
    if change >= 0
      puts "ご利用ありがとうございました！お釣りは#{change}円です。"
      SlotGame.new.play_slot
    else
      puts "投入金額が足りません"
    end
  end
end
```

25行目の記述で、SlotGameクラスのインスタンスを生成しつつ、play_slotメソッドを呼び出しています。

ここまで実装できたら、コードを実行する。以下のようにスロットゲームの結果も購入完了と同時に表示されることを確認する。

![image](https://github.com/koharayuki/til/assets/132040884/0799255c-70e6-43f8-94fc-33c256d6c53b)


# クラスの決め方を振り返る

今回は、飲み物・自販機・ユーザーのようにクラスを切り分けました。このように考えた背景を深掘ってみましょう。

## 単一責任の原則を振り返ろう

これまでに作成したアプリケーションの作り方を振り返りましょう。

単一責任の原則を最初に学び、データと処理のまとまりごとにクラスを分けて実装しました。上記のアプリケーションでは、飲み物・自販機・ユーザーといったように分けて実装しました。

追加で機能を実装する際も、既存のクラスの役割と異なれば、別のクラスを作成して実装しました。スロットゲームの機能を持ったSlotGameクラスがこれにあたります。

このように、データと処理のまとまりごとに分けて実装する考えを、オブジェクト指向といいます。

## オブジェクト指向

アプリケーションを作成するときに、登場する役割ごとに分けて実装する方針のことを言います。RubyなどのWebアプリケーションに使用される言語の多くが、オブジェクト指向で実装する必要があります。

オブジェクト指向のメリットは以下の2点です。

- 役割ごとにオブジェクトを分けることで、実装がしやすくなる
- 役割ごとにオブジェクトを分けることで、あとからコードを改変するときも、他のオブジェクトに影響しなくなる（コードの改変がしやすくなる）
オブジェクトとは、Rubyにおけるクラスやインスタンス、その他の値のことを意味します。例えば、文字列や数値、配列やハッシュなど、これまで値と呼んできたものも全てオブジェクトです。
この他にも、Rubyでは様々な便利な特徴を持ったオブジェクトが用意されていて、組み込みライブラリという形やGemという形で使用できます。
クラスに含まれる値や処理のまとまり（= オブジェクト）を意識しながら、実装することがオブジェクト指向なのです。


# オブジェクト指向は誰によって決められるのか考えよう

オブジェクトの切り分けは、1つの正解におさまるのでしょうか？その答えとしては 「いいえ」 となります。オブジェクトの切り分けに「これ」という1つの正解はありません。これがオブジェクト指向の難しいところになります。

オブジェクト指向はあくまで設計思想の1つです。

- オブジェクトを綺麗に切り分けなくてもとりあえず動くアプリケーションは完成してしまった
- 最初のアプリケーション設計から仕様変更が生じて、オブジェクトの切り分けを見直す必要がでてきてしまった
- AさんとBさんの考えるアプリケーション設計が異なる
ということはよくあります。

それでも、オブジェクト指向を意識しないアプリケーションには、以下のようなデメリットがあります。

- オブジェクト内にさまざまな役割が入り組んでいて、どこに何があるのかわからない
- 1つの機能を変えた途端、その変更とは関係のないはずの機能が動かなくなってしまった
このような問題が生じるコードは、複雑に絡み合うことから「**スパゲッティコード**」と呼ばれます。スパゲッティコードは、開発現場においては非常に大きな問題です。
したがって、オブジェクト指向という「正解のない問題」に、エンジニアは挑み続ける必要がありますし、エンジニアを目指す人はオブジェクト指向を意識した実装ができるようになる必要があるのです。


# Ruby on Railsにおけるオブジェクト指向

「クラス名のファイルに、そのクラスの内容を記述する」点は、Ruby on Railsではモデルのファイルでよく見られる光景です。

![image](https://github.com/koharayuki/til/assets/132040884/599c0056-b7c3-4f33-8696-033009663cad)

このように、Ruby on Railsのアプリケーションも、さまざまなオブジェクトによって構成されています。

PicTweet(tweetアプリケーション)を例に出せば、モデルというオブジェクトの中に、Userモデル・Tweetモデル・Commentモデルがあります。

![image](https://github.com/koharayuki/til/assets/132040884/5e2389bd-9cc9-4ad6-aaa5-3ab1f45e0850)

オブジェクトとして存在することは、オブジェクト指向に従えば 「**ある役割**」 をそれぞれ持っているはずです。
たとえば、Ruby on Railsにおけるモデルは「バリデーションを設定する」「アソシエーションを定義する」という責任があります。

※Ruby on Railsのモデルで単一責任の原則を達成するために、バリデーションを別クラスに切り出すことも可能です。

