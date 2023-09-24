# Googleの設定

Google Cloud console
<https://console.cloud.google.com/apis/credentials>

アクセス後ヘッダーにある「プロジェクトの選択」をクリックします。
クリック後、下記のようにモーダルウィンドウが表示されます。モーダルウィンドウ内、右上にある「新しいプロジェクト」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/13fb7a4e-4259-4eab-81c2-3af39248b05d)

遷移後の画面では、プロジェクト名を記入します。「snsgoogle」と入力しましょう。入力後に「作成」をクリックしましょう。

![image](https://github.com/koharayuki/til/assets/132040884/ceefea2a-94e8-4fa9-b1c2-d72007c58ee0)

遷移後の画面では、画面左側の「OAuth同意画面」をクリックしします。
すると、下記の画面に遷移します。「外部」にチェックを入れて「作成」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/232e727b-e2bf-4422-8e65-b914868fb71c)

次の画面では、アプリケーション名に「sns」と入力します。
また、「ユーザーサポートメール」と「デベロッパー連絡先情報」にメールアドレスを入力します。

※「デベロッパー連絡先情報」は、画面を下にスクロールすると入力欄があります。

![image](https://github.com/koharayuki/til/assets/132040884/4d2b530d-c98e-47d8-a94a-e36168a44308)

全て入力を終えたら、「保存して次へ」をクリックします。

画面左側の「認証情報」をクリック後、ヘッダー付近に表示されている「＋ 認証情報を作成」をクリックします。
クリックすると、プルダウンリストが表示されます。リスト内の「OAuthクライアント ID」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/09538e80-c699-4017-b4ff-613963ec45ef)

遷移後の画面では、以下の通りに設定します。

| 項目                     | 設定内容                                                      |
| ----------------------- | ------------------------------------------------------------ |
| アプリケーションの種類	  　　   | ウェブアプリケーション 　　　　　　　　　　　　　　　                                      |
| 承認済みリダイレクトURI		  | http://localhost:3000/users/auth/google_oauth2/callback　　　　 　　　　　 |

入力後、「作成」をクリックします。

![image](https://github.com/koharayuki/til/assets/132040884/1b3b3eb4-cea0-4a33-89b2-0232c30f1932)

遷移後の画面では、モーダルウィンドウが表示されます。
モーダルウィンドウ内の「クライアントID」と「クライアントシークレット」が表示されます。両方とも後々扱う値になりますので、コピーしてメモ帳などに記載します。

![image](https://github.com/koharayuki/til/assets/132040884/5c887eb7-a321-440a-8948-5ac92378ad5d)

最後に、画面左側に表示されている、「ライブラリ」をクリックします。
遷移先のページで「google+」と検索して、「google+ API」を選択します。

![image](https://github.com/koharayuki/til/assets/132040884/ad348913-95bc-40d5-9554-eea6719fea1a)

遷移後の画面で、「有効にする」をクリックします。

