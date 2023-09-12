※サンプルアプリを使って実装過程を掲載します。

## SNSアカウントで新規登録

![image](https://github.com/koharayuki/til/assets/132040884/8d24ff47-1153-4a2d-be5f-ec0fdcfe6c51)

## SNSアカウントでログイン

![image](https://github.com/koharayuki/til/assets/132040884/0373ac49-51dc-438e-ba5a-0e9ff8e0a33e)

deviseを用いたログイン機能に加えて、deviseにさらなるカスタマイズを加えます。
「Facebook」「Google」の外部APIを利用し、FacebookやGoogleのアカウント情報から「名前」と「メールアドレス」の情報を取得します。
これによりサインアップ時に「名前」と「メールアドレス」は入力せずにサインアップができる機能を実装します。

# 外部APIの設定

## Facebookの設定

最初にFacebookの管理者用ページでアプリの作成や設定を行います。

Facebookへのログイン操作を求められた場合は、メールアドレス・パスワードの入力を行ってください。

ログイン後は、画面上部のナビバーに「マイアプリ」と表示されるのでクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/044eddde-3eb6-45c7-8986-fedc7a632364)

マイアプリクリック後は、下記画面に遷移します。
下記画面から、アプリの登録を行います。「アプリを作成」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/22fbcd30-60dd-44d7-b524-e8facc68404e)




















