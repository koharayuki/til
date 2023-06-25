# 問題.1
配列の内部に、複数のユーザーの情報をハッシュとして持つ変数user_dataがあります。

```
user_data = [
 {user: {profile: {name: 'George'}}},
 {user: {profile: {name: 'Alice'}}},
 {user: {profile: {name: 'Taro'}}},
]
```
user_dataを利用して、全てのユーザーの名前だけが出力されるようにRubyでコーディングしてください。
ただし、出力結果は次のようになるものとします。

```
George
Alice
Taro
```

# 模範解答

```
user_data.each do |u|
  puts u[:user][:profile][:name]
end

あるいは
user_data.each{ |u| puts u.dig(:user, :profile, :name) }
```

# 解説
ハッシュから特定の値を取得する場合は、その値に対応するキーを指定します。以下の書き方で取得ができます。

```
ハッシュ[取得したい値のキー]
```

また、二重ハッシュから特定の値を取得する場合は、取得したい値のキーまで連続して指定すると取得できます。

```
ハッシュ[取得したい値のキー][取得したい値のキー]
```
今回取得したい値は、George, Alice, Taroという値です。
よって、取得したい値に対応するキーはnameというキーだということが分かります。
そのため、nameというキーまで連続して指定すると、George, Alice, Taroという値を取得できます。

```
ハッシュ[:user][:profile][:name]
```

また、今回は配列の中にハッシュが格納されています。
そのため、each文でハッシュの1つ1つを取り出した上で、上記の記述を行うことが必要です。

```
user_data.each do |u|
  puts u[:user][:profile][:name]
end
```

発展的な別解として、digメソッドを用いても取得できます。digメソッドはRubyに標準で組み込まれているメソッドで、多重階層にあるハッシュの値をまとめて取得できます。
