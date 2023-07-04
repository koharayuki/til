# 例外処理を実装する

※例外が発生して処理が止まる前に、例外処理を実装しておく必要があります。

1つ目の「メインの処理に失敗したらそのときだけ別の処理を実行して、そのままメインの処理を続ける」
というパターンの例外処理を実装します。

今回のアプリだと「特定のレコードの更新に失敗したら、どのレコードで更新に失敗したかをログに記録し、そのまま全レコードへの更新を続行する」という実装内容です。

例外処理の実装方法はいくつかありますが、簡単なものでは、**beginブロック**の中に`rescue`を記述する方法があります。

## begin

beginは、例外となりそうな箇所を囲い処理を実行できる文法です。
どんな条件でも最低1回は処理を実行するため、例外処理を始めるときなどに使用します。

```ruby:begin
begin
  # 例外が起きると想定される処理
end
```

beginを利用して処理を実行しても、例外を捉えなければ、どのタイミングで例外処理を行うか決めることができません。

例外を捉えるためには、beginブロック内でrescueを記述します。

# rescue

rescueは、発生した例外を捕捉し、例外が起こった際に呼び出される条件節です。
begin以外の中にも記述できますが、主に、例外が発生しそうな部分をbeginから始まるブロックで囲み、ブロックの内部にrescueを記述して使用します。

```ruby:rescue
begin
  # 数値を0で割ろうとすると、ZeroDivisionError例外が発生する
  1 / 0
rescue
  # 例外が発生した時にrescue以下の処理が呼ばれる
  puts '0で割ることはできません'
end
```

beginブロック内のrescueの記述の形は、ifとelseのものと同様インデントを入れる必要はありません。

上記のRubyプログラムを実行すると、`1 / 0`の処理を行った際に、数値は0で割れないためZeroDivisionErrorという例外が発生します。
beginブロックの内部で例外が発生すると、rescue以下の処理が実行されます。その後、end以降の処理も続いて実行されていきます。

通常、each, times, whileなどの繰り返しの最中に例外が発生した場合、繰り返し処理は途中で中止され、次のループが実行されることはありません。一方、繰り返し処理の内部にrescueを記述した場合は、例外が発生したとしても次のループに移ります。


# rescueを用いたRakeタスクの実装

distribute_ticket:executeタスクを、rescueを使って実装し直します。
distribute_ticket.rakeを以下のように編集しましょう。
今回はrescueを使った実装を行うので、タスク名は`rescue`とします。

```ruby:lib/tasks/distribute_ticket.rake
namespace :distribute_ticket do
  desc "全ユーザーのticket_countをrescueしながら10増加させる"
  task rescue: :environment do
    User.find_each do |user|
      begin
        user.increment!(:ticket_count, 10)
      rescue => e
        Rails.logger.debug e.message
      end
    end
  end
end
```

`find_eachメソッド`は、利用するモデルに紐づくテーブルのすべてのレコードに対して、`eachと同じような繰り返し処理`を行います。
今回であればusersテーブルの1行目から順番にレコードが取り出され、ブロック変数userに代入、endまでの処理が行われます。終わったら次のレコードが取り出され同様に処理されます。これを最後のレコードまで繰り返します。

通常、save, create, update, destroyなどのレコードを操作するメソッドは、実行に失敗したら`false（createメソッドの場合はオブジェクト）`を返すため、例外を生じることがありません。

しかし、メソッド名の末尾に「!」をつけると、実行に失敗したとき`false`を返すのではなく例外を発生させることができます。
先ほど挙げたメソッドで言うと、`save!`, `create!`, `destroy!`が例外を発生させるメソッドになります。

※すべてのメソッドが「!」を付けると例外を返すようになる訳ではありません。また、真偽値を返すメソッドと「!」付きの例外を発生させるメソッドは、正確には同一メソッドではなく別メソッドです。

`rescue => e`という記述がありますが、これは発生した例外をrescue ~ end間の処理内で`e`という変数に入れて扱う、という意味です。

続く`Rails.logger.debug e.message`では、発生した例外をログに記録しています。

##  作成したRakeタスクを実行する

`Rakeタスク`の実装が完了したので、ターミナルから実行します。
実行するタスクは`rescue`です。

```ターミナル
% rails distribute_ticket:rescue
```

コマンドを実行後、usersテーブルのticket_countの値がどうなったか確認してみましょう。
idが500以降のレコードについても、ticket_countが増加していれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/c053b4d7-2294-4fcd-ae22-2e9f4fa2b7e3)

大量のレコードを扱う処理で、例外が発生しても繰り返しを続行したい場合、rescueは簡単で便利です。
ただし、rescueを安易に使用すると、処理を続けてはいけない例外でも処理してしまったり、意味のない例外処理を作るおそれがあるので、その点は注意しましょう。


# 例外を自分で発生させる方法

例外は、求めていない結果として起こるものでしたが、実は自分で例外を発生させることができます。

なぜ例外を自分で発生させるのか？という疑問を持った方も居るかもしれません。
このような実装は、「不具合の原因となる箇所で例外を明示して、処理を止めたいとき」などのために行うものです。

プログラムは、例外の原因と発生が必ずしも同じ箇所になるとは限りません。そのため、問題のある値が登場する箇所で例外を発生させた方が、原因の特定が早くなり修正もしやすくなるため利用されます。

## raise

raiseは、例外を発生させることができる文法です。
第一引数に発生させたい例外クラス、第二引数にエラーメッセージを記述して使用します。

```ruby:raise
raise 発生させたい例外クラス, 'エラーメッセージ'
```

例外クラスには、NoMethodError, RuntimeError, SyntaxError, NameErrorなどがあります。

## raiseを用いたRakeタスクを実装する

raiseを使って例外を発生させます。タスク名はraiseにします。
エラーメッセージは、原因を特定しやすいものにしておきます。

```ruby:lib/tasks/distribute_ticket.rake
namespace :distribute_ticket do
  desc "全ユーザーのticket_countをrescueしながら10増加させる"
  task rescue: :environment do
    User.find_each do |user|
      begin
        user.increment!(:ticket_count, 10)
      rescue => e
        Rails.logger.debug e.message
      end
    end
  end

  desc "全ユーザーの中にticket_countが10枚追加されると最大値より大きくなるレコードがある場合に例外を発生させる"
  task raise: :environment do
    User.find_each do |user|
      begin
        if user.ticket_count > 2147483647 - 10
          raise RangeError, "#{user.id}は、チケット取得可能枚数の上限を超えてしまいます！"
        end
      rescue => e
        Rails.logger.debug e.message
      end
    end
  end
end
```

ticket_countカラムの値がinteger型の最大値（2147483647）より10枚少ない（2147483647 - 10）ときに、さらに10枚追加するとチケット枚数が最大値に達します。
例えば、あるレコードのチケット枚数が「2147483640」だった場合、10枚追加されると最大値より大きくなってしまいます。
そのような状況が起きる前に、チケット枚数が10枚追加されると最大値より大きくなるレコードに対しては、条件分岐を用いて例外を発生させ、エラーメッセージをログに記録します。
今回はrescueも使用しているので、例外が発生しても処理は継続します。

## 作成したRakeタスクを実行する

Rakeタスクの実装が完了したので、ターミナルから実行します。
※実行するタスクはraiseです。

```ターミナル
% rails distribute_ticket:raise
```

実行したらログを確認し、エラーメッセージが記録されていることを確認しましょう。

![image](https://github.com/koharayuki/til/assets/132040884/d2bf1fa8-ff0a-4894-af18-6bf5cfb03516)

今回は例外を発生させることを試すだけなので、あまりメリットを感じなかったかもしれません。
しかし、コードが増えてプログラムが大きくなってくると、ログを残して原因を特定しやすくしておくことは効率よくプログラムする上で重要です。

想定されていないパラメーターを受け取ったときや、不正なアクセスが来たときなど、例外の原因となる箇所で処理を止められるように、存在は覚えておきましょう。


# 切り離せない複数の処理を1つにまとめる方法

チケット補填の処理の途中で1件でも例外が起きると処理が中止されるため、タイミングによってはチケットをもらえる人ともらえない人が生まれてしまいます。処理に1つでも問題があれば、処理を止め全ユーザーへの補填をなかったことにしたいところですが、rescueではこれを表現できません。

このセクションでは2つ目の「メインの処理に失敗したらそのときだけ別の処理を実行して、メインの処理すべてをなかったことにして中止する」
というパターンの例外処理を実装します。

今回のアプリだと「特定のレコードの更新に失敗したら、どのレコードで更新に失敗したかをログに記録し、レコードへの更新をすべてなかったことにして処理を中止する」という実装内容です。

この実装には、例外処理と合わせて使用するトランザクションについて学ぶ必要があります。

## トランザクション

レコードの更新を行う複数の処理を1つにまとめて行うことを指します。
トランザクションを利用することにより、「処理の一部は成功し、一部は失敗した」という事象は発生せず、すべての処理の成功または失敗のみの状態を作ることができます。

Railsでトランザクションを利用する場合は、以下のように記述します。

```ruby:Railsにおけるトランザクションの利用
ActiveRecord::Base.transaction do
  # 処理1
  # 処理2
  # ...
end
```

たとえば、ECサイトの購入処理では、「商品の料金支払い処理」「注文確定処理」を常に1つのまとまりとして考えられるべきでしょう。
トランザクションを利用することで、「料金の支払いに失敗したけど、商品は購入できた」「料金は支払ったけど、注文の確定に失敗し商品が届かなかった」といった事態を防ぐことができます。

##  トランザクションを用いたRakeタスクを実装する

```ruby:lib/tasks/distribute_ticket.rake
namespace :distribute_ticket do
  desc "全ユーザーのticket_countをrescueしながら10増加させる"
  task rescue: :environment do
    User.find_each do |user|
      begin
        user.increment!(:ticket_count, 10)
      rescue => e
        Rails.logger.debug e.message
      end
    end
  end

  desc "全ユーザーの中にticket_countが最大値のものを含んでいれば例外を発生させる"
  task raise: :environment do
    User.find_each do |user|
      begin
        if user.ticket_count > 2147483637
          raise RangeError, "#{user.id}は、チケット取得可能枚数の上限を超えてしまいます！"
        end
      rescue => e
        Rails.logger.debug e.message
      end
    end
  end

  desc "全ユーザーのticket_countをトランザクションで10増加させる"
  task transact: :environment do
    ActiveRecord::Base.transaction do
      User.find_each do |user|
        user.increment!(:ticket_count, 10)
      end
    end
  end
end
```

##  作成したRakeタスクを実行する

※distribute_ticketを指定、動かすタスクはtransactです。

```ターミナル
% rails distribute_ticket:transact
```

実行後に、usersテーブルを確認して、どのレコードも値が変化していなければ成功です。

![image](https://github.com/koharayuki/til/assets/132040884/1a7da29e-c6ab-4ecc-8af6-46d18824a030)

