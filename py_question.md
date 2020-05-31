## Question 1.
5/30 インターンシップ合同説明会　コーディングテスト解説例題 Q1
### 問題
標準入力から入力を受け取り、ブレース展開をして標準出力へ出力するプログラムを作成してください

### 入力例
```
{あかい,あおい,きいろい}はな
```

### 出力例
```
あかいはな
あおいはな
きいろいはな
```

### 作成プログラム
```python
import re

str = input()

# 正規表現で、{の前、{}の中、}の後に切り分ける
str1 = re.findall('{(.*)}', str)
str_bef = re.findall('(.*){', str)
str_aft = re.findall('}(.*)', str)

# split関数で、{}の中のリストをコンマで切り分ける
str1_list=str1[0].split(',')

# {}内の文字に、前後の文字を加えて、１行ずつ出力する
for term in str1_list:
    print(str_bef[0],term,str_aft[0],sep='')
```

## 改良プログラム
```python
import re

str = input()

# 正規表現で、{,}で切り分ける(区切り文字もリストに含める)
str_list = re.split('({|})',str)
#print(str_list)

output = [''] # 結果出力のリスト
flg = "out" # {}の内外のフラグ

for term in str_list:
    # { がきたら、{}内のフラグ
    if term == '{':
        flg="in"
    # } がきたら、{}外のフラグ
    elif term == '}':
        flg="out"
    # {}以外の文字
    else:
        if flg == "out": # {}の外
            for i in range(len(output)):
                output[i] += term
        if flg == "in": # {}の中
            in_list = term.split(',')
            tmp = []
            for i in range(len(output)):
                for j in range(len(in_list)):
                    tmp.append(output[i]+in_list[j])
            output = tmp

if flg=="in" :
    print("ERROR : {}の指定が不正です")
else:
    for term in output:
        print(term)
```

## Question 2.
5/30 インターンシップ合同説明会　コーディングテスト解説例題 Q1
### 問題文

ある地点から別の地点へ荷物を送るとき、複数の配送センターを経由して最終的な配送センターに荷物が送られるものとします。
以下の仕様のもと、ある配送センターの住所と別の配送センターの住所が与えられたときに、どのような経路で荷物が送られるかを出力するプログラムを作成してください。

配送センターの情報は、ウェブAPIからJSON形式で取得することができます。  
配送センターの情報のURLは `https://pn-c9759a75.herokuapp.com/${address}` の形式で、 `${address}` の部分には実際の住所の文字列が入ります。  
また、 `https://pn-c9759a75.herokuapp.com/` にアクセスすると、配送センターの住所の一覧を取得することができます。

配送センターの情報は、具体的には下記のようなものです。

```json
{
  "address": "us/newyork/newyork",
  "routes": {
    "uk": "uk/england/london",
    "us/california": "us/california/losangeles",
    "us/newyork/buffalo": "us/newyork/buffalo",
    "default": "us/california/losangeles"
  }
}
```

配送センターの情報には、住所（ `address` ）と経路（ `routes` ）とが含まれています。住所は、国、地域、都市を/でつなげた形式で表現されます。  
経路は、次に荷物を送る配送センターを示しています。  
経路は、宛先と配送センターの住所の組み合わせで、宛先が荷物の住所に前方一致する場合に、その配送センターに送られます。  
また、`default` は特別な宛先で、他に合致する宛先がなかったときには、その配送センターに送られるということを示しています。  
  
たとえば、先ほどのJSONのような情報があったときに、荷物を `us/newyork/newyork` から `us/california/sandiego` という住所に送りたいとします。  
経路の宛先には `us/california` があるので、荷物は次に `us/california/losangeles` へ送られます。  
荷物を `japan/tokyo/shinjuku` に送りたいときには、荷物は `default` である `us/california/losangeles` へと送られます。

想定される実行例は下記の通りです。

```
$ ruby q3.rb us/newyork/newyork us/california/sandiego
us/newyork/newyork
us/california/losangeles
us/california/sandiego
```

### 作成プログラム
```python
import requests
import json
import pprint

# 入力から、出発地・到着地を受け取る（本当はコマンドライン引数）
start,goal = (x for x in input().split())

now = start
print(now)

while True:
    # GET
    get1 = requests.get('https://pn-c9759a75.herokuapp.com/' + now)
    #print(get1)
    json1 = get1.json()
    #pprint.pprint(json1) # test
    
    #配送先のリスト
    print(list(json1['routes'].keys()))
    
    #Defalutへのフラグ
    flg = 0
    
    #goalとの前方一致を調査
    for route in list(json1['routes'].keys()):
        #print(route,goal.startswith(route)) #文字列の最初から検索
        if(goal.startswith(route)):
            now = json1['routes'][route] #配送先の辞書引き
            flg=1
            print(now)
    
    #一致がなければ、Defaultへ
    if(flg==0):
        now = json1['routes']['default']
    
    if(goal == now):
        print("GOAL!!!")
        break
    
    #初期化
    json1.clear()
```
