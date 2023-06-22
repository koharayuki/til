# 問題.1
メソッドに3つの整数a b cを与えます。
・「aとbの差が1」または「aとcの差が1」であり、かつ「bとcとの数値の差が2以上」の場合はTrue
・それ以外はFalse
と出力するメソッドを作りましょう。

出力例：
close_far(1, 2, 10) → True
close_far(1, 2, 3) → False
close_far(4, 1, 3) → True

ヒント
返り値を絶対値（この場合は正の整数）に変換する際はabsメソッドを使いましょう。


# 解答

```
def close_far(a,b,c)
  x = (a-b).abs
  y = (a-c).abs
  z = (b-c).abs

  if x == 1 && z >= 2
    puts "True"
  elsif y == 1 && z >= 2
    puts "True"
  else
    puts "False"
  end
end
```

# 解説
まず、2~4行目の記述で、abcそれぞれの差分を算出し、絶対値に変換します。

そして6行目のx == 1 && z >= 2で、「aとbの差が1」であり、かつ「bとcとの数値の差が2以上」を検討しています。
同様に8行目のy == 1 && z >= 2で、「aとcの差が1」であり、かつ「bとcとの数値の差が2以上」を検討しています。

条件式は、以下のようにまとめて記述することもできます。

```
【例】条件式の省略
if (x == 1 && z >= 2) || (y == 1 && z >= 2)
  puts "True"
else
  puts "False"
end
```
