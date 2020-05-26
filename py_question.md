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
