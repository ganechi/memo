# Pythonで、JSON形式を扱う

## はじめに必要なimport

```python
import requests
import json
```

## GETする

```python
get1 = requests.get('<URL>')
```

## JSON形式 -> 辞書に変換


## 辞書の処理
```python

x = "Windows"
y = "Mac"
num = 3

## 辞書を作成（変数を指定できる）
mydict = {1:x, 2:y, num:"Linux"}

print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Linux'}

## 後からの書き換えは、無効
y = "MAC"
num = 300

print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Linux'}

## 辞書で、キーを指定して、それぞれ対応した値を取得
print(mydict[1]) # Windows
#print(mydict[0]) # KeyERROR

key2 = 2
print("キー：" + str(key2) + "、値：" + mydict[key2]) # キー：2、値：Mac
## print内は、すべて型を揃えることに注意

## 存在しないキーが指定された時、Defaultを返す
print(mydict.get(1,"NotFound")) # Windows 
print(mydict.get(0,"NotFound")) # NotFound

## 要素の値を更新 or 追加
mydict[3] = "Ubuntu"
print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Ubuntu'}

mydict[4] = "CentOS"
print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Ubuntu', 4: 'CentOS'}

## 他の辞書と結合
youdict = {4:"Japan",5:"USA"}
mydict.update(youdict)
print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Ubuntu', 4: 'Japan', 5: 'USA'}
## 他の辞書側は、そのまま
print(youdict) # {4: 'Japan', 5: 'USA'}

## 辞書の長さ
print(len(mydict)) # 5

## 辞書から要素を削除
del mydict[4] #キー = 4を削除
#del mydict[0] # keyERROR
print(mydict) # {1: 'Windows', 2: 'Mac', 3: 'Ubuntu', 5: 'USA'}

## 要素を取得した上で、辞書から削除
print(mydict.pop(5)) # USA
print(mydict) #{1: 'Windows', 2: 'Mac', 3: 'Ubuntu'}

## 存在しないキーが指定された時、Defaultを返す
print(mydict.pop(0,"NotFound")) #NotFound

## 最後に追加された要素を取得した上で削除
print(mydict.popitem()) # (3, 'Ubuntu')
print(mydict) # {1: 'Windows', 2: 'Mac'}

## 全ての要素を削除する
print(youdict.clear()) # None

## 指定のキーが、辞書に含まれているか
print(1 in mydict) # True
print(0 in mydict) # False
# not in で逆の出力ができる

## 辞書に含まれるキーの一覧
print(mydict.keys()) # dict_keys([1, 2])
for mykey in mydict.keys(): ## 順に取得できる
    print(mykey) # 1 \\ 2

## 辞書に含まれる値の一覧
print(mydict.values()) # dict_values(['Windows', 'Mac'])
myvalue = list(mydict.values()) ## リストに変換
print(myvalue) # ['Windows', 'Mac']


## 辞書に含まれるキーと値の組み合わせ一覧
print(mydict.items()) # dict_items([(1, 'Windows'), (2, 'Mac')])
for mykey,myvalue in mydict.items(): ## 順に取得できる
    print(mykey,myvalue) # 1 Windows \\ 2 Mac
mylist = list(mydict.items()) ## リストに変換
print(mylist) # [(1, 'Windows'), (2, 'Mac')]

```
