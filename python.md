# Python 早引きメモ
プログラミングするときのコピペメモ

## 入力
１行の中に複数の値が入っているのを、分けて変数に入れる
`1 2` -> `a=1, b=2`

```python
a,b = (int(x) for x in input().split())
```

多重リスト

```
table = [[0] * W for i in range(H)]
```


複数行の場合
最初に、行数を指定

```python
num = int(input())
a=list(range(num))
b=list(a)

for i in range(num):
    a[i],b[i]=(int(x) for x in input().split())
```

## 出力

```python
num = "Yeah"
print("Hello",num) # HelloYeah
print(num,end='')  # Yeah (改行しない)
```

## if文
インデントに注意！

```python
if a == 0:
  ~~
elif a < 0:
  ~~
else:
  ~~
```

## for文
値で指定 i =0,1,2,3,4

```python
for i in range(5):
```

リストで指定

```python
list1 = ["Suzuki","Noguchi","Takayama"]
for i in list1:
```

## while文

```python
while n<1000:
```

## リストのソート

```python
list1.sort() #値の小さい順 or 文字コード順にソート
list1.reverse() #値の大きい順 or 文字コードの逆順にソート
```

## リストの最大値・最小値
最大値 `max(リスト)`　最小値 `min(リスト)`

```python
print(max(list1),min(list2))
#最大値のインデックス
list3.index(max(list3))
#最大値のインデックス（複数あるとき＝リスト内包表記）
[i for i, j in enumerate(list4) if j == max(list4)]
```


## 時間計算
時間だけでも、日付をふくめたdatetime型で扱うと楽

```python
import datetime

h,m = (int(x) for x in input().split())
time[i] = datetime(2020, 1, 1, h, m, 00)       # datetime(年,月,日,時,分,秒)で入力

if time[i] < datetime(2020, 1, 1, 9, 00 ,00):  # 比較もできる
  hometime = time[i] - timedelta(minutes=30)   # 差し引きは、timedeltaで
  print(hometime.strftime("%H:%M"))            # 出力は、.strftime("%H:%M:%S")
```

## 素数判定
引用しました。

>「素数とは、1とその数自身以外に正の約数を持たない、1より大きい整数」
素数の定義から単純に考えると、1とその数自身以外で割り切れないことを確認すれば、素数かどうかを判定できます。以下のような手順になります。

>>n を判定したい数とする
2 から n - 1 までで n を割ってみる
もしどこかで割り切れたら n は合成数
最後まで割り切れなかったら n は素数

```python
n = 100
for p in range(2, n):
    if n % p == 0:
            print("not Prime")
            break
        else:
            continue
        break
    else:
        print("Prime")
```

## 文字列処理
文字列完全一致 `==`・不一致 `!=`

```python
print('abc' == 'abc') # True
print('abc' == 'ABC') # False
print('abc' != 'ABC') # True
```

文字列一部一致

```python
print('xyz' in 'aaa-xyz-zzz') # True
```

文字列前方一致・後方一致

```python
s = 'aaa-xyz-zzz'
print(s.startswith('aaa')) # True
print(s.startswith('zzz')) # False
print(s.endswith('zzz')) # True
print(s.endswith('xyz')) # False
print(s.endswith(('xxx', 'yyy', 'zzz')))# True  タプルでor検索
```

大文字小文字変換

```python
s = 'Abcあいうえお'
print(s.lower()) # abcあいうえお
print(s.upper()) # ABCあいうえお
```

指定した文字列


