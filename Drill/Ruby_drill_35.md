# 問題.1
- 以下の仕様を満たすアプリケーションを作成しましょう。また、注意書きを確認し、雛形を使用して実装してください。

# 仕様
- 実行すると [1] : 点数を登録する, [2] : 点数を確認する, [3] : 終了する という選択肢を表示し、ユーザーに入力を求め、その入力に従い以下のような各処理を行う
- アプリケーションを終了するまで、処理を繰り返す

 [1]の処理
- 名前、年齢、国語・数学・英語の3教科の点数を入力させて、保存する

 [2]の処理
- 投稿された情報から番号と名前で一覧を表示し（例 1: yamada）、見たい個人の番号の入力を求める
- 入力された個人の名前、年齢、国語・数学・英語の3教科の点数を表示する

 [3]の処理
- アプリケーションを終了する

-https://tech-master.s3.amazonaws.com/uploads/curriculums//6b2181a33e4e0abce6f5f88d703437a5.gif
## 注意
- 引数などは雛形で考慮していないため、必要に応じて引数を設定すること

## ヒント
 registration_student メソッド
 このメソッドで処理したい内容は下記の通りです。

- student というハッシュを定義する
- 生徒名/生徒の年齢と国語/数学/英語を入力させ、student というハッシュに代入する
- students という配列に、先ほど定義した student というハッシュを追加する
### 必要な知識

- gets と chomp
- to_i
- ハッシュ
- 配列と配列演算子(<<)
#### show_student_name メソッド
#### このメソッドで処理したい内容は下記の通りです。

- registration_student で追加した配列の中身を一覧表示する
- 配列の要素であるハッシュの値を一覧表示させるために、要素番号を入力するように促し、対応する要素を取得する
- 入力した要素番号のハッシュの値を一覧で表示する
### 必要な知識
### eachメソッド

# 解答
```
def registration_student(students)
  # 生徒の名前と年齢を登録できるようにする
  student = {}
  puts '生徒名を入力してください'
  student[:name] = gets.chomp
  puts '生徒の年齢を入力してください'
  student[:age] = gets.chomp

  # 登録した生徒の国語、数学、英語の点数を登録できるようにする
  puts "国語の得点は？"
  student[:japanese] = gets.to_i
  puts "数学の得点は？"
  student[:math] = gets.to_i
  puts "英語の得点は？"
  student[:english] = gets.to_i
  students << student

end

def show_student_name(students)
  # 登録された生徒の名前を番号を振って表示する
  i = 0
  students.each do |student|
    puts "#{i}: #{student[:name]}"
    i += 1
  end
  puts '見たい生徒の番号を入力してください'
  num = gets.to_i

  student = students[num]
  # 選択された生徒の名前、年齢、国語、数学、英語の点数を表示できるようにする
  puts "名前: #{student[:name]}"
  puts "年齢: #{student[:age]}"
  puts "国語: #{student[:japanese]}"
  puts "数学: #{student[:math]}"
  puts "英語: #{student[:english]}"
end

students = []

while true
  puts '行いたい項目を選択してください'
  puts '[1]点数を登録する'
  puts '[2]点数を確認する'
  puts '[3]終了する'
  input = gets.to_i
  if input == 1
    registration_student(students)
  elsif input == 2
    show_student_name(students)
  elsif input == 3
    exit
  else
    puts '無効な値です'
  end
end
```

それぞれを各パートに分けて解説します。

メソッド外の処理
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
students = []

while true
  puts '行いたい項目を選択してください'
  puts '[1]点数を登録する'
  puts '[2]点数を確認する'
  puts '[3]終了する'
  input = gets.to_i
  if input == 1
    registration_student(students)
  elsif input == 2
    show_student_name(students)
  elsif input == 3
    exit
  else
    puts '無効な値です'
  end
end
このコードで処理したい内容は下記の通りです。

students という配列を定義する
メニューを表示し、入力待ちにさせる
入力した数値に対応するメソッドを実行する
以上のメニュー画面の表示を繰り返す
registration_student メソッド
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
def registration_student(students)
  # 生徒の名前と年齢を登録できるようにする
  student = {}
  puts '生徒名を入力してください'
  student[:name] = gets.chomp
  puts '生徒の年齢を入力してください'
  student[:age] = gets.chomp

  # 登録した生徒の国語、数学、英語の点数を登録できるようにする
  puts "国語の得点は？"
  student[:japanese] = gets.to_i
  puts "数学の得点は？"
  student[:math] = gets.to_i
  puts "英語の得点は？"
  student[:english] = gets.to_i
  students << student

end
このメソッドで処理したい内容は下記の通りです。

student というハッシュを定義する（3行目）
生徒名/生徒の年齢と国語/数学/英語の点数を入力させ、student というハッシュに代入する（5~15行目）
students という配列に、先ほど定義した student というハッシュを追加する（16行目）
show_student_name メソッド
 1
 2
 3
 4
 5
 6
 7
 8
 9
10
11
12
13
14
15
16
17
18
def show_student_name(students)
  # 登録された生徒の名前を番号を振って表示する
  i = 0
  students.each do |student|
    puts "#{i}: #{student[:name]}"
    i += 1
  end
  puts '見たい生徒の番号を入力してください'
  num = gets.to_i

  student = students[num]
  # 選択された生徒の名前、年齢、国語、数学、英語の点数を表示できるようにする
  puts "名前: #{student[:name]}"
  puts "年齢: #{student[:age]}"
  puts "国語: #{student[:japanese]}"
  puts "数学: #{student[:math]}"
  puts "英語: #{student[:english]}"
end
このメソッドで処理したい内容は下記の通りです。

配列の情報のうち、登録されている生徒名を番号を添えて一覧表示する（3~7行目）
配列の要素であるハッシュの値を一覧表示させるために、要素番号を入力するように促し、 対応する要素を取得する（8~11行目）
指定された要素に含まれる各値を表示する （13~17行目）
