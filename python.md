# はじめに
Python 3系を使用します。  
インストールに関しては[Python環境構築ガイド](https://www.python.jp/install/install.html)が参考になります。

## 出力とコメント
`print()` で出力、 `#` で一行コメントアウトを行います。  
`'''`（シングルクォーテーション3つ）か `"""`（ダブルクォーテーション3つ）で囲むと複数行コメントアウトできます。
```python
# 1行コメントアウト
print(3)        # 3
print('Hello')  # Hello

'''
複数行
コメントアウト
'''
```
# データと型
## 数値
整数や小数など様々なものを扱えます。
```python
print(2)        # 2
print(1.3)      # 1.3
```

以下のような代数演算ができます。
```python
a + b           # 加算
a - b           # 減算
a * b           # 乗算
a / b           # 除算
a ** b          # 累乗
a // b          # 切り捨て除算
a % b           # 剰余
```

計算例です。
```python
print(7 + 2)    # 9
print(7 - 2)    # 5
print(7 * 2)    # 14
print(7 / 2)    # 3.5
print(7 ** 2)   # 49
print(7 // 2)   # 3
print(7 % 2)    # 1
```

## 文字列
アルファベットや数字などの文字を扱えます。  
`'`（シングルクォーテーション）か `"`（ダブルクォーテーション）で囲むと文字になります。
```python
print('abc')            # abc
print('1')              # 1
```

以下のような演算ができます。
```python
a + b                   # 連結
a * b                   # 反復
```

具体例です。
```python
print('for' + 'ever')   # forever
print('This' * 3)       # ThisThisThis
```

## 変数
ここで変数というものを導入します。そのためにまずオブジェクトについての説明をします。  
Pythonにおいてあらゆるものがオブジェクトです。 整数や小数、文字列もオブジェクトです。すべてのオブジェクトは何らかの型に分類でき、型ごとに属性を持っています。属性はデータと関数から構成されます。このデータのことをプロパティ、関数のことをメソッドといいます。このようなオブジェクトを格納する箱のことを変数といいます。  
`=` で変数にオブジェクトを代入することができます。`type()` を使うことで型を確認することができます。変数の型は代入したものに応じて自動で決定されます。
```python
# int型
x = 4
print(x)            # 4
print(type(x))      # <class 'int'> 

# float型
y = 3.14
print(y)            # 3.14
print(type(y))      # <class 'float'>

# str型
s = 'Hello'
print(s)            # Hello
print(type(s))      # <class 'str'>
```

`int()` や `str()` などを使うと型を変換することができます。
```python
demo = 5.4
print(demo)         # 5.4
print(type(demo))   # <class 'float'>

roto = int(demo)
print(roto)         # 5
print(type(roto))   # <class 'int'>

lute = str(demo)
print(lute)         # 5.4
print(type(lute))   # <class 'str'>
```

なお、変数の命名にはいくつかのルールがあります。
- 頭文字に数字は使えない
- `for` や `in` などの予約語（あらかじめ使われている文字列）は使えない
- 大文字と小文字は区別される
- 記号は `_`（アンダーバー）のみ使える

## リスト
リストは複数の要素を1つにまとめることができます。  
インデックス (添字) を用いて要素を取得できます。リストの先頭のインデックスは0です。その後、1、2、3、…と増えていきます。インデックスには負の値も指定できます。この場合、右から数えていきます。
```python
a = [10, 20, 30, 40]

print(a)                # [10, 20, 30, 40]
print(type(a))          # <class 'list'> 

print(a[0])             # 10
print(a[1])             # 20
print(a[2])             # 30
print(a[3])             # 40

# 負の値も指定できます
print(a[-1])            # 40
print(a[-2])            # 30
print(a[-3])            # 20
print(a[-4])            # 10
```

スライスという操作を用いて範囲を指定して要素にアクセスすることもできます。
```python
a = [10, 20, 30, 40, 50, 60]

print(a[0:3])           # [10, 20, 30]
print(a[4:6])           # [50, 60]

# スライスの始点と終点は省略可能
print(a[:3])            # [10, 20, 30]
print(a[2:])            # [50, 60]
print(a[:])             # [10, 20, 30, 40, 50, 60]

# ステップ数を指定することも可能
print(a[::2])           # [10, 30, 50]
print(a[1::2])          # [20, 40, 60]
print(a[::-1])          # [60, 50, 40, 30, 20, 10]         
```

入れ子にすると2次元にできます。
```python
a = [[10, 20, 30], [11, 21, 22]]
print(a)                # [[10, 20, 30], [11, 21, 22]]
```

リストの要素は書き換えることができます。
```python
a = [10, 20, 30]

a[1] = 50
print(a)                # [10, 50, 30]
```

リストに対して定義されたメソッドには例えば以下のようなものがあります。
```python
a = [20, 40, 30, 10]

# 昇順に並び替え
a.sort()
print(a)                    # [10, 20, 30, 40]

# 末尾に要素を追加
a.append(50)
print(a)                    # [10, 20, 30, 40, 50]

# 末尾の要素を削除
a.pop()
print(a)                    # [10, 20, 30, 40]

# リストのコピー
b = a.copy()
print(b)                    # [10, 20, 30, 40]
```

## タプル
リストと似たものとしてタプルがあります。  
リストと同じように複数の要素を1つに集めたもので、インデックスを用いて要素にアクセスすることができます。ただ、更新ができないので値を変更したり、要素を追加したりすることはできません。
```python
a = (10, 20, 30, 40)

print(a[0])         # 10
print(a[1])         # 20
```

## 辞書
ほかにもリストと似たものとして辞書型があります。  
辞書はキーと値で構成されます。
リストではインデックスと値を関連付けていましたが、辞書ではインデックスの代わりに自分で設定したキーというものを値と関連付けて使用します。
```python
p = {'height':0.4, 'weight':6.0, 'type':'Electric'}

print(p)                # {'height': 0.4, 'weight': 6.0, 'type': 'Electric'}
print(type(p))          # <class 'dict'>

print(p['height'])      # 0.4
print(p['weight'])      # 6.0
print(p['type'])        # Electric

# 書き換え
p['height'] = 1.2
print(p)                # {'height': 1.2, 'weight': 6.0, 'type': 'Electric'}

# 追加（指定したキーがなければ追加される）
p['number'] = 25
print(p)                # {'height': 1.2, 'weight': 6.0, 'type': 'Electric', 'number': 25}

# 削除
p.pop('type')
print(p)                # {'height': 1.2, 'weight': 6.0, 'number': 25}
```

## ブーリアン
`True` か `False` のどちらを持ちます。  
```python
c = True
print(c)        # True
print(type(c))  # <class 'bool'>
```

以下のような論理演算が行えます。
```python
a and b     # a かつ b が True であれば True
a or b      # a または b が True であれば True
not a       # a が False であれば True
```

具体例です。
```python
print(True and False)   # False
print(True or False)    # True
print(not True)         # False
```

# フロー制御
## 比較演算
数値などの比較を行い、その結果をブーリアンで返します。
```python
print(7 < 4)            # False
print(5 in [1, 2, 5])   # True
```

以下の演算子を使うことができます。
```python
a == b      # a が b と等しい
a != b      # a が b と異なる
a > b       # a が b より大きい
a < b       # a が b より小さい
a >= b      # a が b 以上
a <= b      # a が b 以下
a in b      # a が b に含まれる
a not in b  # a が b に含まれない
```

連結させることもできます。
```python
x = 8
print(4 <= x < 10)  # True
print(7 < x != 8)   # False
```

## if文
`if` を使うことで条件分岐を含む処理ができるようになります。以下のように記述します。
```python
if 条件式1:
    条件式1が真の時の処理
elif 条件式2:
    条件式1が偽で、条件式2が真の時の処理
else:
    すべての条件式が偽の時の処理
``` 
具体例です。
```python
b = 5

if b > 0:
    print('b is positive')
elif b < 0:
    print('b is negative')
else:
    print('b is zero')

# b is positive
```
`elif` は好きな数だけ使うことができます。
`elif` や `else` の処理が必要でなければそれらを省くこともできます。条件式には論理演算も使用できます。
```python
flag = True
x = 0

if flag and x != 4:
    x = 1

print(x)

# 1
```

以下のように条件分岐処理を一行に収めることもできます。
```python
flag = True
x = 0

x = 1 if flag and x != 4 else -1

print(x)        # 1
```

## for文
`for` を使うことでループ処理を行うことができます。次のように記述します。
```python
for 変数 in イテラブルなオブジェクト:
    処理
```

イテラブルとは要素を１つずつ返すことができることをいいます。`list` や `str`、 `dict`、 後述する `range` や `enumerate` などの型のオブジェクトはイテラブルです。  
以下は具体例です。
```python
for i in [10, 20, 30]:
    print(i)

# 10
# 20
# 30


for i in 'USA':
    print(i)

# U
# S
# A


# rangeを使うとある連続した値を取得できます。
for i in range(3):
    print(i)

# 0
# 1
# 2


# enumerateを使うとインデックスと要素を同時に取得できます。
abc = ['Alice', 'Bob', 'Chris']
for i, v in enumerate(abc):
    print(i, v)

# 0, Alice
# 1, Bob
# 2, Chris
```

### `range` や `enumerate` について
`range` や `enumerate` は `int` や `float`、 `list`などと同様にオブジェクトの型の1つです。

#### `range`
`range` は指定した開始数から終了数までの連続した値を持ちます。書式は以下のとおりです。start と step は省略することができます。start は省略すると0に、step は省略すると1になります。
```python
range(start, stop, step)
range(start, stop)          # stepを省略
range(stop)                 # start, stepを省略
```

具体例です。リストに変換してから出力すると実態がわかりやすいです。
```python
# start, stepを省略
a = range(5)

print(a)            # range(0, 5)
print(type(a))      # <class 'range'>

b = list(a)
print(b)            # [0, 1, 2, 3, 4]


# 省略なし
x = range(2, 14, 4)

print(x)            # range(2, 11, 4)
print(type(x))      # <class 'range'>

y = list(x)
print(y)            # [2, 6, 10]
```

#### `enumerate`
`enumerate` はカウンタとそれに対応する、引数として渡されたイテラブルなオブジェクトの値を持ちます。
```python
name = ['Alice', 'Bob', 'Chris']

abc = enumerate(name)
print(type(abc))        # <class 'enumerate'>

x = list(abc)
print(x)                # [(0, 'Alice'), (1, 'Bob'), (2, 'Chris')]
```

# リスト内包表記
リストを生成するときに次のような記述ができます。
```python
a = [i*10 for i in range(5)]
print(a)        # [0, 10, 20, 30, 40]

b = [i for i in range(10) if i % 3 != 0]
print(a)        # [1, 2, 4, 5, 7, 8]
```

# 関数
処理をまとめて名前を付けたものを関数といいます。書式は以下のとおりです。
```python
def 関数名(引数):
    処理
```
具体例です。
```python
def greeting():
    print('Hello')
    print('Bye')

greeting()


# Hello
# Bye
```

関数に入力（引数）と出力をもたせることもできます。
```python
def add(a, b):
    c = a + b
    return c

x = add(5, 7)
print(x)        # 12
```

# クラス
クラスはオブジェクトのひな型に相当します。
以下のように記述します。
```python
class クラス名():
    def __init__(self, 引数...):
        処理

    def メソッド名1(self, 引数...):
        処理
    
    def メソッド名2(self, 引数):
        処理
```
クラス名は慣例的に頭文字を大文字にします。クラスの中で定義された関数をメソッドといいます。__init__という名前のメソッドはコンストラクタといいます。コンストラクタはインスタンスを生成したときに自動で実行されます。クラスをもとに作られたオブジェクトのことをインスタンスといいます。selfはインスタンス自身を指します。コンストラクタの中で定義されるselfの付いた変数をインスタンス変数といいます。  
以下は具体例です。
```python
class Calculation():
    def __init__(self, a, b):       # コンストラクタ
        self.x = a                  # インスタンス変数への代入
        self.y = b                  # インスタンス変数への代入
    
    def add(self):                  # メソッド
        z = self.x + self.y
        return z

    def sub(self):                  # メソッド
        z = self.x - self.y
        return z


# インスタンスの生成
p = Calculation(7, 2)

# インスタンス変数の確認
print(p.x)          # 7
print(p.y)          # 2

# メソッドの実行
print(p.add())      # 9
print(p.sub())      # 5


# インスタンスの生成
r = Calculation(3, 10)

# インスタンス変数の確認
print(r.x)          # 3
print(r.y)          # 10

# メソッドの実行
print(r.add())      # 13
print(r.sub())      # -7
```

# モジュール
モジュールは関数やクラスなどを1つのファイルにまとめたものです。`import` で読み込むことができます。
```python
import モジュール名
```

## math
mathは、数学関数を提供します。
```python
import math

# 円周率
print(math.pi)              # 3.141592653589793

# ネイピア数
print(math.e)               # 2.718281828459045

# 切り上げ
print(math.ceil(5.6))       # 6

# 切り下げ
print(math.floor(5.6))      # 5

# 階乗
print(math.factorial(4))    # 24

# 最大公約数
print(math.gcd(12, 16))     # 4

# 平方根
print(math.sqrt(4))         # 2.0

# 三角関数
p = math.pi
print(math.sin(p/6))        # 0.49999999999999994
print(math.cos(p/3))        # 0.5000000000000001
print(math.tan(p/4))        # 0.9999999999999999

# 逆三角関数
print(math.asin(0.5))       # 0.5235987755982989
print(math.acos(0.5))       # 1.0471975511965979
print(math.atan(1))         # 0.7853981633974483
```

mathモジュールに限らず、以下のように記述すると、モジュール名を付けずに関数などを利用することができます。
```python
from math import sqrt

print(sqrt(3))              # 31.7320508075688772
```
```python
from math import *

print(sqrt(5))              # 2.23606797749979
print(floor(5.6))           # 5
```

## Numpy
Numpy は数値計算を効率的に行うためのモジュールです。
```python
import numpy as np

a = np.array([[1, 2], [3, 4]])
b = np.array([[2, 4], [1, 3]])
c = np.array([2, 4])
d = np.array([[2], [4]])

print(a)
# array([[1, 2],
#        [3, 4]])

print(c)
# array([2, 4])

print(d)
# array([[2],
#        [4]])

print(type(a))      # <class 'numpy.ndarray'>


''' 四則演算 '''
# 要素ごとに演算が行われます。

print(a+b)
# array([[3, 6],
#        [4, 7]])

print(a*b)
# array([[ 2,  8],
#        [ 3, 12]])


''' 自動補完（ブロードキャスト） '''
# 要素が足りない場合、自動で計算できる形に補完されます。

print(a-c)
# array([[-1, -2],
#        [ 1,  0]])

print(a/d)
# array([[0.5 , 1.  ],
#        [0.75, 1.  ]])

print(a*3)
# array([[ 3,  6],
#        [ 9, 12]])


''' 行列の積 '''

print(np.dot(a, b))
# array([[ 4, 10],
#        [10, 24]])


''' 配列の作成とサイズ変更 '''

x = np.arange(2, 14, 2)

print(x)        # array([ 2,  4,  6,  8, 10, 12])

print(x.reshape(2, 3))
# array([[ 2,  4,  6],
#        [ 8, 10, 12]])


''' 転置・逆行列・行列式 '''

# 転置
print(a.T)
# array([[1, 3],
#        [2, 4]])

# 逆行列
print(np.linalg.inv(a))
# array([[-2. ,  1. ],
#        [ 1.5, -0.5]])

# 行列式
print(np.linalg.det(a))     # -2.0000000000000004
```

# 参考
- [Python 公式ドキュメント](https://docs.python.org/ja/3/)
- [Python Japan](https://www.python.jp/index.html)
- [非公式Pythonダウンロードリンク](https://pythonlinks.python.jp/ja/index.html)
- [Pythonの組み込みデータ型の分類表（ミュータブル等）](https://gammasoft.jp/blog/python-built-in-types/#iterable)
- [とほほのPython入門](http://www.tohoho-web.com/python/index.html)
- [【Python】オブジェクト指向を理解するための超重要ワードまとめ](https://djangobrothers.com/blogs/basic_knowledge_of_python/)
- [Pythonによる制御工学入門](https://www.ohmsha.co.jp/book/9784274223907/)