# SQLによるテーブルの操作

## データベースを指定する

まずは操作するテーブルがあるデータベースを指定する必要があります。その場合は`USE文`を用います。

## USE文

`USE`文は、どのデータベースを使用するのかを指定するSQLの文です。
`USE 《database名》`と指定することでデータベースを選択します。

テーブルを操作する場合は、はじめに「どのデータベースにあるテーブルか」を選択する必要があるため、USEを使います。Sequel Proで、はじめにデータベースを選択することと同じです。

###  データベースを作成して選択する

下記のように`CREATE`を実行してデータベースを作成します。

```ターミナル（MySQL）
mysql> CREATE DATABASE sqltest;
Query OK, 1 row affected (0.00 sec)
```

続いて`USE`を実行してデータベースを選択します。

```ターミナル（MySQL）
mysql> USE sqltest;
Database changed
```

これで、作成したデータベースを使用できます。


## テーブルとカラムを作成する

データベースの作成のときと同様に、テーブルを作成する際は`CREATE TABLE`文を使用します。

実行時には以下のようにテーブル名を指定する必要があります。また、そのテーブルに作成するカラムの名前とそのカラムの型を指定できます。

```ターミナル（MySQL）:CREATEでテーブルを作成
mysql> CREATE TABLE テーブル名 (カラム名1 カラム名1の型, カラム名2 カラム名2の型, …);
```

Railsでテーブルを作る際は、`rails g model モデル名`でそのテーブルに紐づくモデルを作成し、そのときに作られたマイグレーションを`rails db:migrate`で実行する、という手順を踏んでいました。

その`rails db:migrate`が実行される裏側では、この`CREATE TABLE`というSQL文が動いていたということです。

例として、商品の情報を保存することを想定し、"goods"という名前のテーブルを作ります。
そして、テーブルには商品idを数値で保存するidカラムと、商品名を文字列で保存するnameカラムを作成します。

また、カラムを作成する場合には型の指定が必要です。Railsでは数値を入れる型は"Integer"、文字列を入れる型は"String"となっていました。
MySQLで数値型や文字列型を定義する際は以下のような型名を使用します。

| 型名         | 保存できる値         |
| ----------- | ------------------ |
| INT	     　　　　　　　| 数字　　　　　　　　　　　　　　　　　　　　　　　　　　  |
| VARCHAR(M)　 　　| 最大M文字の文字列　　　　  |

今回は"INT"型のカラム"id"と、"VARCHAR(255)"型のカラム"name"のある"goods"テーブルを作成します。

###  コマンドでテーブルを作成する

カラムとその型を指定し、テーブルを作成します。

```ターミナル（MySQL）
mysql> CREATE TABLE goods (id INT, name VARCHAR(255));
```

以下のような表示があれば、SQL文が実行されています。

```ターミナル（MySQL）
mysql> CREATE TABLE goods (id INT, name VARCHAR(255));
Query OK, 0 rows affected (0.01 sec)
```

作成を確認するために、ここで`SHOW TABLES`文を使用し、テーブルの一覧を確認してみましょう。

###  作成したテーブルを表示する

```ターミナル（MySQL）
mysql> SHOW TABLES;
```

以下のように"Tables_in_sqltest"に"goods"というテーブルが確認できれば、テーブルが正しく作成されたということになります。

```ターミナル（MySQL）
mysql> SHOW TABLES;
+-------------------+
| Tables_in_sqltest |
+-------------------+
| goods             |
+-------------------+
1 row in set (0.00 sec)
```

## テーブルの構造を確認する

追加したカラムを確認するために、テーブルの構造を表示してみましょう。
テーブル構造を確認するためには以下のようなSQL文を記述します。

```ターミナル（MySQL）:SHOWでテーブルの構造を表示
mysql> SHOW columns FROM 《テーブル名》;
```

## FROM句

`FROM`句は、対象となるテーブルを指定する際に使用するSQLの句です。

下記のように使用します。

```ターミナル（MySQL）:FROMでテーブルを指定
mysql> FROM 《テーブル名》
```

テーブル名の部分を"goods"に置き換えて実行してみます。

下記のコマンドを実行してください。

```ターミナル（MySQL）
mysql> SHOW columns FROM goods;
```

以下のような表示があれば、正常に実行できています。

```ターミナル（MySQL）
mysql> SHOW columns FROM goods;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int(11)      | YES  |     | NULL    |       |
| name  | varchar(255) | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
2 rows in set (0.01 sec)
```

実行結果から、goodsテーブルにはidとnameという2つのカラムがあることが確認できました。


# カラムを追加する

カラム情報の更新には`ALTER`文を使用します。

## ALTER文

`ALTER`文は、データベースやテーブルを編集できるSQLの文です。
`ALTER TABLE`文を実行すると、テーブルに対してカラムの追加や削除ができます。

```ターミナル（MySQL）:ALTERでカラム情報の更新
mysql> ALTER TABLE 《テーブル名》 操作
```

カラムを追加するSQL文は以下のような文法で記述します。

```ターミナル（MySQL）:カラムを1つだけ追加する場合
mysql> ALTER TABLE テーブル名 ADD カラム名 カラムの型;
```

```ターミナル（MySQL）:カラムを複数追加する場合
mysql> ALTER TABLE テーブル名 ADD (カラム名 カラムの型, ……);
```

今回は"price"と"zaiko"という2つのカラムを、共に"int"型で作成してみましょう。

```ターミナル（MySQL）
mysql> ALTER TABLE goods ADD (price int, zaiko int);
```

以下のように結果が表示されていれば、正常に実行できています。

```ターミナル（MySQL）
mysql>  ALTER TABLE goods ADD (price int, zaiko int);
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

カラムを追加したので、テーブルの構造がどう変化したか確認してみましょう。

```ターミナル（MySQL）
mysql> SHOW columns FROM goods;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int(11)      | YES  |     | NULL    |       |
| name  | varchar(255) | YES  |     | NULL    |       |
| price | int(11)      | YES  |     | NULL    |       |
| zaiko | int(11)      | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
4 rows in set (0.00 sec)
```

上記のようにカラムが追加されていれば成功です。

## カラムを変更する

カラムの変更は、先ほどと同様に`ALTER TABLE`文を使用し、以下のような文法でSQL文を記述します。

```ターミナル（MySQL）
mysql> ALTER TABLE テーブル名 CHANGE 古いカラム名 新しいカラム名 新しいカラムの型;
```

先ほど"zaiko"というカラムを追加しましたが、他のカラムに合わせてカラム名を英語表記にするため、"stock"という名前に変更してみます。

※ALTER文でカラムを変更します。

```ターミナル（MySQL）
mysql> ALTER TABLE goods CHANGE zaiko stock int;
```

以下のような表示があれば、正常に実行できています。

```ターミナル（MySQL）
mysql> ALTER TABLE goods CHANGE zaiko stock int;
Query OK, 0 rows affected (0.00 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

またこのとき、カラムの型は変更しなくても、再度記述をしなくてはなりません。
そのため、カラムの変更をするときはこの型の部分を間違えないように注意する必要があります。

先ほどと同様にカラムが変更されていることを確認します。

```ターミナル（MySQL）
mysql> SHOW columns FROM goods;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int(11)      | YES  |     | NULL    |       |
| name  | varchar(255) | YES  |     | NULL    |       |
| price | int(11)      | YES  |     | NULL    |       |
| stock | int(11)      | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
4 rows in set (0.01 sec)
```

上記のように表示されていれば、正常に変更されています。

## カラムを削除する

カラムの削除にも`ALTER TABLE`文を使用し、以下のようにSQL文を記述します。

```ターミナル（MySQL）:ALTERでカラムを削除
mysql> ALTER TABLE テーブル名 DROP カラム名;
```

"stock"カラムが不要になった、と想定してカラムの削除を行ってみます。

※ALTER文を使いカラムを削除します。

```ターミナル（MySQL）
mysql> ALTER TABLE goods DROP stock;
```

以下のように表示がされていれば正常に実行できています。

```ターミナル（MySQL）
mysql> ALTER TABLE goods DROP stock;
Query OK, 0 rows affected (0.01 sec)
Records: 0  Duplicates: 0  Warnings: 0
```

先ほどと同様にカラムが削除されていることを確認します。

```ターミナル（MySQL）
mysql> SHOW columns FROM goods;
+-------+--------------+------+-----+---------+-------+
| Field | Type         | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id    | int(11)      | YES  |     | NULL    |       |
| name  | varchar(255) | YES  |     | NULL    |       |
| price | int(11)      | YES  |     | NULL    |       |
+-------+--------------+------+-----+---------+-------+
3 rows in set (0.01 sec)
```

カラムがきちんと削除されていることを確認できれば成功です。

