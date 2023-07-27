# あらかじめ用意されたオブジェクト

```javascript
irb(main):002:0> Array.new(3, "a")
=> ["a", "a", "a"]
```

JavaScriptでもこのように、あらかじめ用意されたオブジェクトがあります。

## ブラウザで用意されたオブジェクト

JavaScriptはブラウザで動くプログラミング言語です。そのため、JavaScriptにはあらかじめ、ブラウザを操作するメソッドを持つオブジェクトが定義されています。

その最上位であるオブジェクトが`windowオブジェクト`です。

## windowオブジェクト

windowオブジェクトとは、ブラウザの情報を持っているオブジェクトです。ブラウザの情報をもつため、ブラウザオブジェクトと呼ばれます。

JavaScriptで予め定義されているメソッドやオブジェクトは全てwindowオブジェクトのプロパティであると言えます。

![image](https://github.com/koharayuki/til/assets/132040884/80a5e08e-ec0b-4f42-9819-ead5cd24fc6f)

ブラウザオブジェクトは上図のような階層構造になっています。
最上位のWindowオブジェクトを起点として、下位にその他のオブジェクトが属する構造になっています。
ブラウザが起動するタイミングで自動的に生成され、JavaScriptからアクセスすることが出来ます。

windowオブジェクトの中でも、もっとも頻繁に使う可能性のあるdocumentオブジェクトを紹介します。

## documentオブジェクト

documentオブジェクトとは、ブラウザ上で表示された情報(HTML)を操作する事ができるオブジェクトです。

このdocumentオブジェクトは非常に多くのプロパティやメソッドを持っています。
したがって、documentオブジェクトはこれからHTMLに対して何か処理をする際は頻繁に使用するオブジェクトとなります。

## ブラウザのオブジェクトを取得する

ブラウザオブジェクトを取得し、JavaScriptのコードを記述して、今開いているブラウザに対して働きかけてみます。

### コンソールからブラウザにアラートを出す

```javascript
window.alert("ブラウザオブジェクトの取得に成功！")
```

ブラウザのコンソールを確認して、以下のように結果が表示されていれば成功です。

![image](https://github.com/koharayuki/til/assets/132040884/27bc28c1-a7f7-47a0-884b-83f30c6a762d)

windowオブジェクトにはalertメソッドが定義されています。<br>
したがって、`window.alert()`と記述することで今開いているブラウザにアラートを表示するという処理がされます。

### windowの記述を省略できることを確認する

先ほどと同様の実行結果になっていれば成功です。

windowオブジェクトの記述は省略されることが一般です。<br>
以後のJavaScriptの記述ではwindowは省略しています。しかし、windowオブジェクトはブラウザの情報を取得するという重要な役割を担っています。  
  
  
# HTMLの要素を取得し操作する方法

documentオブジェクトはブラウザ上の情報を操作する事ができるオブジェクトでした。
そのdocumentオブジェクトを用いて「HTMLの要素をJavaScript上で取得し操作する方法」を取り上げます。

## HTMLの要素をJavaScript上で操作する仕組み

### DOM（Document Object Model)

DOMとは、HTMLを解析しデータを作成する仕組みです。

### HTMLがWebページとして閲覧されるまでの流れ

HTMLで書かれたファイルは単なる文字情報なので、そのまま表示するととても見にくいものです。
 そのため、HTMLを解析し、CSSやJavaScriptによる装飾を行ってから画面に映すという工程を経て一般的なWebページは表示されます。

これを行っているのが、Google ChromeやSafariといったブラウザです。
ブラウザがHTMLやCSS、JavaScriptを受け取ってユーザーに届けるまでには、以下の図のような手順を踏んでいます。

![image](https://github.com/koharayuki/til/assets/132040884/0396370d-0f6d-4f35-be17-77c1b4ffbe86)

HTMLは階層構造になっており、DOMによって解析されたHTMLは、階層構造のあるデータとなります。これを、`DOMツリー`や`ドキュメントツリー`と呼びます。

![image](https://github.com/koharayuki/til/assets/132040884/db919fbe-387f-4e2b-9ce1-41e7eb227c74)

JavaScriptのメソッドを使うと、DOMツリーを操作することができます。
HTMLの要素名や、「id、class」といった属性の情報を元にDOMツリーの一部を取得し、CSSを変更したり、要素を増やしたり、消したりできます。
するとそれがブラウザに反映され、描画も変わります。

### 事前準備

雛形のコードを用いてDOMツリーの情報を取得する方法についてコードを書きながら触れていきます。<br>
続いて取得したDOMツリーの情報を操作する方法について取り上げます。  
  
  
# HTMLを取得する


DOMツリーからHTMLを取得する方法は大きく分けて3つあります。

- id名から取得する方法
- class名から取得する方法
- セレクタ名から取得する方法

## document.getElementById("id名")

document.getElementById("id名")は、DOMツリーから特定のHTMLの要素を取得するためのメソッドの1つです。引数に渡したidを持つ要素を取得します。

以下のように書くことで、マッチするidを持つHTMLの要素を取得することができます。

<特定のidを持つ要素の取得>
```javascript:特定のidを持つ要素の取得
//id名がhogeの要素を指定する場合
document.getElementById("hoge")
```

## document.getElementsByClassName("class名")

classを指定して取得する際はこちらを利用します。ここで気をつけたいのは、`getElements`と複数形になっていることです。
id名はhtml上に必ず1つしか存在しないため、document.getElementById("id名")を用いると1つの要素を取得することになります。
一方、HTML上に同じclass名を持つ要素は複数存在することが考えられるため、getElementsByClassName("class名")の場合は同じclassを持つ要素を全て取得することになります。

以下のように書くことで、class名とマッチするデータを取得することができます。

<特定のclass名を持つ要素の取得>
```javascript:特定のclass名を持つ要素の取得
//class名がfugaの要素を指定する場合
document.getElementsByClassName("fuga")
```

## document.querySelectorAll("セレクタ名")

セレクタ名とは、CSSでスタイルを適用するために指定している要素です。
セレクタ名を指定して取得する場合、`querySelectorAll`メソッドを使用します。HTML上から、引数で指定したセレクタに合致するものをすべて取得します。

最も頻繁に使用するセレクタ名として、**class名、id名、HTMLタグ**を覚えておきましょう。
書き方として、class名は`(".class名")`、id名は`("#id名")`、HTMLタグは`("タグ名")`と表記します。

<指定したセレクタ名を持つ要素すべてを取得>
```javascript:指定したセレクタ名を持つ要素すべてを取得
//class名がfugaの要素を指定する場合
document.querySelectorAll(".fuga")

//id名がhogeの要素を指定する場合
document.querySelectorAll("#hoge")

//h1タグの要素を指定する場合
document.querySelectorAll("h1")
```

関連して、`querySelector`というメソッドもあります。
`querySelector`を用いれば、HTML上から引数で指定したセレクタに合致する要素のうち一番最初に見つかった要素1つを取得することもできます。

<セレクタ名を指定した要素のうち、一番最初に見つかった要素だけ取得>
```javascript:セレクタ名を指定した要素のうち、一番最初に見つかった要素だけ取得
//id名,class名,タグ名の指定方法は、querySelectorAllメソッドと同じ
document.querySelector("セレクタ名") 
```










