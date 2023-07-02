# 既存クラスの引き継ぎ

Rubyではデータの元となる設計図を作り、その設計図を元に実体となるデータを作るという手順を踏み、
この設計図を**クラス**、実体となるデータを**インスタンス**と呼びます。

このクラスは親子関係を作ることができます。`親子関係とは、既存のクラスの情報を元に新しいクラスを作る`ということです。

これを「**クラスの継承**」と呼びます。

##  クラスの継承

クラスの継承とは既存のクラスを元に新しいクラスを作ることです。

このとき、新しいクラスを`子クラス（またはサブクラス）`、元になったクラスを`親クラス（またはスーパークラス）`と呼びます。

![image](https://github.com/koharayuki/til/assets/132040884/476fc5db-7c35-437b-a086-2bd5c3d85f21)

### 「なぜクラスの継承が必要なのでしょうか？」
  
それは、クラスの継承を使えば、共通する部分をまとめることができて効率的だからです。

例えば、パトカー、消防車、救急車のクラスを作成するならば、3つに共通する情報をまとめた自動車クラスを作成し、その自動車クラスを継承したクラスを作成したほうが効率的です。

そうすれば、各クラスは自動車が共通して持つ情報を引き継ぎつつ、それぞれ独自の情報を持つことができます。

![image](https://github.com/koharayuki/til/assets/132040884/f4361d6f-e3c0-494a-b952-75e9125138ee)

このクラスの継承はプログラミングにおいて効率的なコードを書く上で非常に重要な知識となります。


# 継承の仕組み

## 継承の書き方

あるクラスを継承して新しいクラスを作る場合には以下のように「`新しいクラス < 元となるクラス`」と書きます。

```ruby:sumple.rb
class PoliceCar < Car

end
```

## 継承されるもの

クラスを継承すると、親クラスから子クラスへ以下のものが引き継がれます。

- 親のインスタンス変数
- 親のインスタンスメソッド

例えば、Carクラスを継承したPoliceCarクラスを作成するコードを以下に示します。

```ruby:sumple.rb
class Car
 def initialize(car_type, capacity)
   @name = car_type
   @capacity = capacity
 end

 def info
   puts "車種：#{@name}　乗車定員：#{@capacity}人"
 end

end

class PoliceCar < Car

end

police_car = PoliceCar.new("パトカー", 5)

police_car.info

# ターミナル出力結果
# 車種：パトカー　乗車定員：5人
```

上記を見てみると、`PoliceCarクラス`の中には何も記述をしていませんが、継承元の`Carクラス`の**インスタンス変数およびインスタンスメソッド**を使うことが確認できます。

# インスタンスメソッドを追加する方法

続いて子クラスに独自のインスタンスメソッドを追加する方法については

**子クラス内に新しくメソッドの定義を追加する**だけです。

先ほどのPoliceCarクラスを例に説明をします。以下を見てください。

```ruby:sumple.rb
class Car
 def initialize(car_type, capacity)
   @name = car_type
   @capacity = capacity
 end

 def info
   puts "車種：#{@name}　乗車定員：#{@capacity}人"
 end

end

class PoliceCar < Car

 def siren
   puts "ウゥ〜ウゥ〜"
 end

end

police_car = PoliceCar.new("パトカー", 5)

police_car.siren

# ターミナル出力結果
# ウゥ〜ウゥ〜
```

上記では、`PoliceCarクラス`内に`sirenメソッド`を新たに追加し、それを実行しています。

このように**子クラスにインスタンスメソッドを追加する**ことで、そのクラス固有のメソッドを定義することができます。


# メソッドを上書きする方法

`親クラスにあるメソッドと同じ名前のメソッドを子クラスで定義すると、メソッドを上書きすることができます。`

これをメソッドの「**オーバーライド**」と呼びます。

###  オーバーライド

オーバーライドとは、親クラスのメソッドを子クラスに同名のメソッドを定義することによって上書きすることを指します。

```ruby:sumple.rb
class Car
 def initialize(car_type, capacity)
   @name = car_type
   @capacity = capacity
 end

 def info
   puts "車種：#{@name}　乗車定員：#{@capacity}人"
 end

end

class PoliceCar < Car

 def info
   puts "車種：#{@name}　乗車定員：#{@capacity}人　パトロール時間：24時間"
 end

 def siren
   puts "ウゥ〜ウゥ〜"
 end

end

police_car = PoliceCar.new("パトカー", 5)

police_car.info

# ターミナル出力結果
# 車種：パトカー　乗車定員：5人　パトロール時間：24時間
```

上記では、`Carクラス`で定義された`infoメソッド`と同名のメソッドを`PoliceCarクラス`内で定義しています。

これによって、`PoliceCarクラス`を元に生成されたインスタンスで`infoメソッド`を実行すると、**上書きされた処理が実行される**ようになります。

