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

クリック後、下記のようにモーダルウィンドウ画面が表示されます。
「ユーザーにFacebookアカウントのログインを許可する」を選択します。

![image](https://github.com/koharayuki/til/assets/132040884/b9d29d19-0a8b-4ee3-b4da-5564ef7b0336)

クリック後は、下記の画面が表示されます。
「アプリ表示名」には「sns」と入力しましょう。また、メールアドレスが間違っていないか、確認も行います。

![image](https://github.com/koharayuki/til/assets/132040884/2b06e5e6-66ad-46bd-926a-0f89bdeda6a3)

正常にアプリが作成されると以下の画面が表示されます。

![image](https://github.com/koharayuki/til/assets/132040884/06366fd7-b1ac-408a-9d38-7f8310474a48)

左のメニューにある「設定」の「ベーシック」クリックします。

![image](https://github.com/koharayuki/til/assets/132040884/6dc1a030-6705-449a-a8c7-7e2144022e9b)

以下のように設定画面が表示されます。

![image](https://github.com/koharayuki/til/assets/132040884/178cc285-e502-4b7f-aab4-adcb9dc4afb8)

設定画面に「アプリID」と「app secret」がそれぞれ記載されています。
これらは後の作業で使用するため、コピーしてメモ帳などに保存しておきます。

![image](https://github.com/koharayuki/til/assets/132040884/101b2014-82da-4c2a-9597-b019a9f1edb9)

「アプリID」と「app secret」を確認後は、画面を下にスクロールして、「＋ プラットフォームを追加」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/b956611a-e90b-47fa-9216-b818f817a8a3)

クリック後、下記モーダルウィンドウが表示されます。
モーダルウィンドウ内の「ウェブサイト」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/784fb29a-3957-4536-bd91-49b4537a9bcc)

ウェブサイトをクリックすると、下記のように入力欄が表示されます。
「サイトURL」の入力欄に「http://localhost:3000/」と入力します。
入力後、「変更を保存」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/5d669e29-9c0b-4b87-945e-ef2580fecb56)

※以上で、Facebookでの設定は終了です。

