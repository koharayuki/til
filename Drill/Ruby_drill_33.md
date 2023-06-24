# 問題.1
- 西暦の年数および月を入力し、その月の日数を求めるプログラムを書きます。
- その場合、閏年について考慮する必要があります。

- 閏年は以下の判断基準で決まります。

①\. その西暦が4で割り切れたら閏年である
②\. ただし、例外として100で割り切れる西暦の場合は閏年ではない
③\. ただし、その例外として400で割り切れる場合は閏年である

- つまり、西暦2000年は閏年であり、西暦2100年は閏年ではありません。
- これらに対応できるように、出力例と雛形をもとに実装しましょう。

### 出力例
- 1990年2月 =>"1990年2月は28日間あります"
- 2000年2月 =>"2000年2月は29日間あります"
- 2100年2月 =>"2100年2月は28日間あります"
- 2000年3月=>"2000年3月は31日間あります"

# 解答
```
def get_days(year, month)
  month_days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  if month == 2
    if year % 4 == 0
      if year % 100 == 0 && year % 400 != 0
        days = 28
      else
        days = 29
      end
    else
      days = 28
    end
  else
    days = month_days[month - 1]
  end

  return days
end

puts "年を入力してください："
year = gets.to_i
puts "月を入力してください："
month = gets.to_i

days = get_days(year, month)
puts "#{year}年#{month}月は#{days}日間あります"

```


# 解説
- 2月以外は各月の日数が決まっています。したがって、まずは以下のようにコードを記述しましょう。
```
def get_days(year, month)
  month_days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31] # 各月の日数は配列で管理
  return month_days[month - 1]
end

puts "年を入力してください："
year = gets.to_i
puts "月を入力してください："
month = gets.to_i

days = get_days(year, month)
puts "#{year}年#{month}月は#{days}日間あります"
```

- そして、2月の時だけ条件式を用いて出力をします。
```
def get_days(year, month)
  month_days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  if month == 2 # 2月のとき
    # 閏年のときはdaysに29を代入
    # それ以外はdaysに28を代入
  else
    days = month_days[month - 1]
  end

  return days
end

puts "年を入力してください："
year = gets.to_i
puts "月を入力してください："
month = gets.to_i

days = get_days(year, month)
puts "#{year}年#{month}月は#{days}日間あります"
```

- 閏年か判定します。閏年の条件は3つありましたが、以下のようにまとめることができます。

- ① その年が4で割り切れること
- ② ただし、年が100で割り切れて400で割り切れない場合は閏年ではない

- したがって、以下のような条件分岐を設けることができます。

```
【例】
year = 指定の年

if year % 4 == 0  # 年が4で割り切れること
  if year % 100 == 0 && year % 400 != 0  # 年が100で割り切れて400で割り切れない場合
    # 閏年でない
  else
    # 閏年
  end
end
```

- 上記のロジックを反映しましょう。
```
def get_days(year, month)
  month_days = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
  if month == 2
    if year % 4 == 0  # 年が4で割り切れること
      if year % 100 == 0 && year % 400 != 0  # 年が100で割り切れて400で割り切れない場合
        days = 28 # 閏年でない
      else
        days = 29 # 閏年
      end
    else
      days = 28   # 閏年でない
    end
  else
    days = month_days[month - 1]
  end

  return days
end

puts "年を入力してください："
year = gets.to_i
puts "月を入力してください："
month = gets.to_i

days = get_days(year, month)
puts "#{year}年#{month}月は#{days}日間あります"
```
