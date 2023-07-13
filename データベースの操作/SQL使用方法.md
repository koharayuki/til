# SQLの使用

## ターミナルでの使用方法

ターミナルでは、MySQLというRDBMSを使用してSQLを実行できます。
MySQLを使用するには、ターミナルからログインします。下記のコマンドを実行してください。

```ターミナル
# ホームディレクトリに戻る
% cd

# MySQLに接続
% mysql -u root
```

`-u root`というオプションで、ユーザーは「ルート」でログインするという意味になります。
ここでいうルートとは、MySQLであらかじめ用意されているユーザーのことです。
このユーザーのパスワードは空で設定されているため、ログインにパスワードは必要ありません。

コマンドを入力して、以下のような画面が表示されれば準備は完了です。

# MySQLに接続すると以下のような表示になる

```ターミナル
% mysql -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 428
Server version: 5.6.47 Homebrew

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

SQLは`mysql>`の続きから、入力して実行ができます。

また、SQLはGUIツールであるSequel Pro（シークエルプロ）でも使用できます。

# Sequel Proでの使用方法

Sequel Proを使用する場合も、ユーザーでログインする必要があります。

Sequel Proを使用してログインする際は、下記のように入力します。

![image](https://github.com/koharayuki/til/assets/132040884/3f1139e1-873f-4fe8-9cd3-15733439a0eb)

これで準備は完了です。

アプリケーションのデータベースを選択すると、以下のように上部に「クエリ」というボタンがあります。クリックすると、選択しているデータベースに関するSQLを記述することができます。

![image](https://github.com/koharayuki/til/assets/132040884/ee0aa1e8-4a01-4378-b2d4-0f7cf7e63762)

# SQLによるデータベースの操作

SQL（エス・キュー・エル/シークェル）とは「Structured Query Language」の略で、`RDBの操作を行うための言語`です。

SQLはデータベースやテーブルに対してさまざまな命令を行いますが、その命令は大きく以下の3つに分類されます。

- データを定義する「DDL（Data Definition Language）」
- データを操作する「DML（Data Manipulation Language）」
- データを制御する「DCL (Data Control Language)」

## DDL（Data Definition Language）

データを定義するSQLです。以下のような作成/更新/削除などの命令文があります。

| 命令	         | 機能                     |
| ------------ | ----------------------- |
| CREATE	     | データベースやテーブルの作成  |
| ALTER		     | データベースやテーブルの更新  |
| DROP		     | データベースやテーブルの削除  |

## データベースの作成

SQLを使って、データベースを作成してみます。ここでの作業はターミナルを使用して行います。

これまではrails db:createというコマンドを実行することで、Ruby on Railsがデータベースを作成してくれていましたが、今回はSQLを使用してデータベースを作成してみます。

## CREATEクリエイト文

`CREATE文`は、データベースやテーブルを作成できるSQLの文です。
`CREATE DATABASE`文を実行すると、指定した名前のデータベースが作成されます。
実行時には以下のようにデータベース名の指定が必要です。

```mysql:CREATEでデータベースを作成
mysql> CREATE DATABASE 《データベース名》;
```

ちなみにSQL文は小文字でも動作します。ただし、SQL文と他の文字列が混ざると読み辛くなることから、大文字で記述することが一般的です。

それでは実際に「sqltest」という名前のデータベースを作成してみましょう。

## ターミナルで以下のSQLを実行









