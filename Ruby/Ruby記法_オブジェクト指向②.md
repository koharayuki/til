# 投入金額を決める

これまでの実装で、登録した商品を表示するところまでできました。続いて、表示された商品から、自販機に投入する金額を決めます。投入金額を決めるのは購入者の役割なので、Userクラスに記述します。

##  商品を表示する

Userクラスに、投入金額を定義します。

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
  def initialize(money)
    @money = money
  end

  def money
    @money
  end
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

puts "あなたはお客さんです。投入金額を決めてください。"
money = gets.to_i
user = User.new(money)
```

59行目で投入金額を、ユーザーに入力させます。そして60行目のuser = User.new(money)で、Userクラスのインスタンスを生成して変数userに代入します。


# 選んだ商品を購入する

最後に、選んだ商品を購入できるようにしましょう。投入金額が足りない場合は、「投入金額が足りません」と表示するようにします。

###  商品を購入するための記述

ここでのポイントは、「購入する商品の選択は購入者が行い、決済は自販機が行う」という点です。UserクラスとVendingMachineクラスそれぞれに処理を記述します。

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

77行目でVendingMachineクラスに定義した、payメソッドを呼び出しています。実引数としては、直前の75行目で定義したインスタンスuserを渡します。

34行目からのpayメソッドに注目しましょう。36行目の`chosen_drink = user.choose_drink`では、Userクラスに定義したchoose_drinkメソッドを呼び出しています。
37行目の`change = user.money - self.drinks[chosen_drink].fee`では、「ユーザーの投入金額」と「選ばれた商品の金額」の差分を計算して、その結果を変数`change`に代入しています。
すなわち、`change`にはお釣りの金額が含まれることになります。

このように、VendingMachineクラスのメソッド内で、Userクラスのインスタンスについてメソッドを実行する必要があります。したがって、77行目でUserクラスのインスタンスを、実引数として渡す必要がありました。

このコードは、下図のような流れになります（途中のコードを省略しています）。

![image](https://github.com/koharayuki/til/assets/132040884/a6714386-47c6-49ad-921c-7ef870baef21)

ここまで実装できたら、コードを実行しましょう。以下の通り一連の流れが実装できれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/bcda2d79-1867-4fe8-a762-ae9201b1a3d6)

# ファイルを分割する

ここまでで、飲み物自販機のアプリケーションを作成することができました。しかし、コードが長くなり、且つクラスの分かれ目も見分けにくくなっています。
したがって、ファイルを分割し、1つのファイル（今回はapplication.rb）で読み込んであげるようにしましょう。

この時に役立つのが、`require`です。`require`はRubyファイルを読み込むためのメソッドです。前の章ではライブラリ（ライブラリもあくまでRubyのファイルの集合体です）を読み込むために使用しました。

ライブラリを読み込む際は、requireに続いてライブラリの名前を記述するだけで完了しました。しかし、開発者自身で設置したRubyファイルを読み込むには、ディレクトリを明示して記述する必要があります。

それでは、クラスごとにファイルを分割し、`require`を用いて読み込みましょう。

## クラスを分割する

同じディレクトリ内(同じ階層)にapplication.rb、 drink.rb, user.rb, vending_machine.rbなどのファイルを作る。

 ruby_application_training
 |
 -application.rb
 drink.rb
 user.rb
 vending_machine.rb


続いて、クラスごとに記述を分けましょう。この時、`application.rb`ですべてのファイルを読み込む`ことにします。












