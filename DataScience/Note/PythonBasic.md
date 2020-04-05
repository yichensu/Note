# 基礎python語法

colab的執行：shift + enter

```py
type(100) #表示要問裡面東西的類型，現在是int
float(100) #直接將型別轉換成float 100.0
a = range(5) #長度為5的陣列，印出[0, 1, 2, 3, 4]
```
在轉換型態前會先辨識型態，若認得就會轉，不認得就不會轉

```py
//用法：
a = range(stop)
a = range(start, stop[, step])
>>> stop = 10 #這個只的是值
>>> range(stop) #range 就像array or vector
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> start = 2
>>> range(start, stop)
[2, 3, 4, 5, 6, 7, 8, 9]
>>> step = 2
>>> range(start, stop, step)
[2, 4, 6, 8]
```

Range 是 Python 產生整數數列的物件 (object) ，相較串列 (list) 可以節省記憶體使用，因此常用在 for 迴圈。

Range 的建構子 (constructor) 有兩種參數 (parameter) 版本，第一種是只要一個參數 stop ，這會產生從 0 開始，然後 1 然後 2 ，到 stop 結束的整數數列，第二種可用三個參數，從 start 到 stop 但不包含 stop ，或是從 start 到 stop ，每個數字間隔 step

range 就是一種 vector<int> 的 constructor，從 start 開始放值到 end 結束
```cpp
vector<int> v;
for (int i = start; i < end; i += step)
  v.push_back(i);
```

```py
>>> a = [33, 10 ,18] //陣列概念
>>> a+1 #不能直接+1，因為編譯器不懂要加到哪
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can only concatenate list (not "int") to list
>>> a[2]
18
>>> a[2]+1 #需要給明確的對象
19
>>> a[2] #但操作完，值不會動？？？
18
>>> a+[2] #直接在陣列後面加上去
[33, 10, 18, 2]
>>> a
[33, 10, 18] #但原本的陣列還是不會動...
>>> a[0], 'ddd'+str(a[1]+3), a[2]+3
(33, 'ddd13', 21) #用str進行資料轉換，文字間可相加
```

### python中常見括號使用
{} 存dictionary的資料，當作是找資料的key
example:
```py
tel = {'suling': 63097, 'tren': 63104} #像是json資料型態；創造一個叫做tel的dic，其中有兩個key跟value
list(tel.keys()) #['suling','tren']；提取key，並用list型態呈現
list(tel.values()) #[63097, 63104]；提取value，並用list型態呈現
tel['tren'] #63104；用key直提取其所包含value

a = range(5,0,-1)
print(list(range(5,0))) #跑不出來，因為預設step是1
#print是__str__
print(list(range(5,0,-1)))
print(list(range(0,-2))) #python很困惑，因為step default是1
print(list(range(0,-4,-2))) #[0,-2]
b = range(5,1,-2)
print(len(b)) #問b的長度: 2
print(sum(b)) #b裡面值的加總 5 + 3 = 8
```
[]存list的東西（）決定運算順序或呼叫函數

## 各種專有名詞

```py
import math #引入一個函式庫叫做math；#include <cmath>概念
math.factorial(x) #math package下面的內容
math.ceil(10.5) #取10.5的上界：11
math.floor(351.4) #取下界：351
math.fabs(-3) #取絕對值，會轉成float: -3

import random
random.random() #產生0-1之亂數，()內不需任何input
round(random.random()) #四捨五入；round內需要有input
def adjust_score(old): #可以自己定義函數，下列屆是函數內容；像是要調整分數的開根號乘以10
  new = math.sqrt(old)*10
  return new 
  #用縮排看出函數從屬關係
a = adjust_score(0)
b = adjust_score(60)
print(a,b)

k = input('k=?') #會用 k=? 開頭，然後要他人輸入東西
print(k) #會印出對方填的東西
#受試者可能會輸入各種東西，因此可以在外面有另一判斷限制

k = int(input('k='))
s = 0
for i in range(1,k+1):
  s = s + i
  print(i,s)
#填完k的輸出內容，可以1加到8
'''
k=8
1 1
2 3
3 6
4 10
5 15
6 21
7 28
'''
for i in[123,'huew',range(0,3)]: #記得加冒號
  print(i)
  #i每次都會迭代成list內的東西，跑三次

for i in range(3): #印三次NTU
  print('NTU')

r = 0
c = 0
while r < 0.9:
  c = c + 1
  r = random.random()
  print(c,r) #print寫在裡面會印出所有歷程，直到符合break條件

r = 0
c = 0
while r < 0.9:
  c = c + 1
  r = random.random()
print(c,r) #print在外面只會印出最後break結果 ex. 28 0.9921476651550276

#反應時間：三明治法則，若想算中間指令花多少時間都可以這樣估計
import time, random
def measure():
  print('get ready...', flush = True) #在遠端的時候沒加 flush = True 就會先暫存，等到滿才會印出來
  time.sleep(10*random.random()) #等待()中的時間，再做下列程序
  t0=time.time()
  input("Press [Enter] now!")
  return time.time()-t0
```
### 基礎指令

* / 會算到小數點下一位
* % 取餘數（mod）
* // 整數除法
* 可以用 print("Type of x:", type(x)) 來確認資料型態（但python通常會自己去判斷）
* python沒有++ && ||，要直接使用+=1 and or
* word_list = ['pen','apple'] #可直接初始化
* 雖然可同時放不同型態東西但管理不易，並不建議
* len(word_list)可以得到list目前長度
* list.sort()可得排序後list（str應該是用字母順序去排，通常是順序，若要反序可以在()內加入reverse) == sort(list,key,reverse)
* 反轉範例：
 word_list.sort(reverse=True)
### list-add/remove
```py
word_list.append('some') #新增值在list後面
word_list.insert(2,'option') #把option這個物件插入在list[2]的位置
word_list.remove('apple') #移除list中的'apple'物件
word_list.pop(0) #移除在list[0]的物件，但會自動跟你說那個物件是什麼，不用特別print 如'pen'
word_list.extend(['happy','cat']) #在後面連接list
#也可以用+合併，如
[1, 2, 3] + [4, 5] #（效果同extend()）
 [1, 5] * 3 #創建3個一樣的list #[1, 5, 1, 5, 1, 5]
```

### list-slice
[start:stop:step]
會從start開始，取到stop-1，隔step步取
```py
word_list = ['pen','apple','life','try']
word_list[1:3] #從[1]開始，到[3-1]，得['apple','life']
word_list[1:] #沒有給結束就是全印，['apple', 'life', 'try']
word_list[:3] #從頭取到[3-1]，得['pen', 'apple', 'life']
word_list[1::2] #從[1]開始，間隔2取，['apple', 'try']
word_list[::2]  #從投開始，間隔2取，['pen', 'life']
word_list[:]    #取全部
word_list[-1]   #取最後一個，['try']
word_list[-2]   #取最後第二個，['life']
word_list[-2:]  #取最後兩個，['life', 'try']
word_list[::-2] #從最後一個，往前間隔2，['try', 'apple']
```
### dict
```py
dictionary = {'apple':0, 'banana':1, 'cat':2}
#前者為key，後者為value
dictionary = {} #宣告空dict
```
* 動態存取key對應value的資料型態
* key是唯一值不能重複
* key只能為「值不可變動」的資料型態（string, int, tuple...）
* value可為任何資料型態
* dictionary[key]: 取key對應到的value >> dictionary['apple'] #0
* 同樣可用len(dict)得長度 #3

#### 新增刪除dict
```py
dict1['open'] = 4 #運用key直接將值為4，key為'open'加入dict1最後面
del dict1['apple'] #用key刪除特定資料
```
### set
```py
my_set = {'apple','banana','cat'}
#裡面值為唯一值且不會重複
my_set = set() #宣告空的set

# 可以透過set轉換，刪除list重複資料
my_list = ['amber', 'jean', 'jane', 'jean']
print(set(my_list)) #{'jane', 'jean', 'amber'}
#但這樣資料型態不同？？
my_set.add('dog') #增加物件
my_set.remove('banana') #移除物件（都是透過key)
```
**set不能直接取值：因為沒有特別的位置**
##### set取值方法
* C++採用紅黑樹演算法：https://www.itread01.com/content/1546932973.html
* python 採用hash table演算法：https://hg.python.org/releasing/3.6/file/tip/Objects/setobject.c?fbclid=IwAR3XVZUeT-0ilk464xBiZQNxHuDb_N2jdIK-rCdgA04bO7Apg0q89euMH5M
```py
for e in my_set:
#e is the element in my_set
  print(e)

#較多data可以用iter，每次取不一樣
it = iter(my_set)
print(next(it)) #印出第一個
print(next(it)) #印出第二個
print(next(it)) #印出第三個
```

### 判斷式
* if...elif...elif...else （不是else if）
* 要用縮排包好
```py
#找出a/b/c最大值
max_value = 0
if a >= b:
  if a >= c:
    max_value = a
  else
    max_value = c
else
  if b >= c:
    max_value = b
  else
    max_value = c

#簡化但較不易懂寫法
if a >= b:
  max_value = a if a >= c else c
else
  max_value = b if b >= c else c

#不符合條件就做什麼事
user_input = input('continue?')

if not (user_input == 'y' or user_input == 'Y'):
  print('game over') #直接加在if後面
```
### while
```py
count = 0

while count <= 3:
  print('the count is', count) #只有str可以用+連接，其他要用','隔開
  count += 1
print('the end of while', count)

is_do = False
while not is_do: #一樣寫not
#do something

#### 印出結果
'''
the count is 0
the count is 1
the count is 2
the count is 3
the end of while 4
'''
```
### for迴圈
for 自訂變數 in **range, list, set, dict** :
所以可以插入某數字，也可以是list
像是 
```py
my_list == ['apple', 'banana', 'cat', 'dog']
for i in my_list: #代表i依序apple、banana、cat、dog
#寫法1：走過指定數字範圍 range(star,stop,step)
my_list = ['apple', 'banana', 'cat', 'dog']
for i in range(1,len(my_list), 1):
  print(my_list[i])
#會依序印出banana cat dog
#start default = 0, step default = 1, so can only write as for i in range(len(my_list)): if want to print every element

#寫法2：走過某個list, dict, set 
for element in my_list:
  print(element)
# if just want to via a piece path, can write as for element in my_list[1:3]

#若想同時知道index與value，可使用enumerate()，且要給兩變數去當作index與value
for i, element in enumerate(my_list):
  print(i,element)

#### 印出結果
'''
0 apple
1 banana
2 cat
3 dog
'''
```

### for迴圈新增物件
```py
int_list = [1,2,3,4,5]

str_list = []

for num in int_list:
  str_list.append(str(num)) #要轉型別為str
  print(str_list)  

#### 印出結果
'''
['1']
['1', '2']
['1', '2', '3']
['1', '2', '3', '4']
['1', '2', '3', '4', '5']
'''
#也可以簡化成一行，前面會有output物件，後面是條件
str_list = [str(num) for num in int_list]

#實作把字與index彼此對應
test_list = ['升息', '友達', '反應', '手機', '支付']

for i, element in enumerate(test_list):
  print('\'',element,'\'','編號為:', i) #字對應index
  print(i,'號字為:', element) #index對應字
'''
' 升息 ' 編號為: 0
0 號字為: 升息
' 友達 ' 編號為: 1
1 號字為: 友達
' 反應 ' 編號為: 2
2 號字為: 反應
' 手機 ' 編號為: 3
3 號字為: 手機
' 支付 ' 編號為: 4
4 號字為: 支付
'''
#另種做法
word2id = {} 
id2word = [] 

for i,term in enumerate(test_list):
  word2id[term] = i
  id2word.append(term)
  print(word2id)
  print(id2word)
```
### function
```py
def add_and_multiply(a,b): #a/b是input的東西
  return a+b, a*b  #自己寫一個函式

#input方法
##按順序輸入
add_and_multiply(5,3)
##指定參數名，這樣就不用管順序
add_and_multiply(a = 5, b = 3)
#output方法
##有幾個回傳值就用幾個接
add_result,mul_result = add_and_multiply(5,3)
##若只想接一個
_, mut_result = add_add_multiply(5,3)
```
### 讀寫檔案
* './example.txt'：是檔案路徑
* 'r'是模式
>* 'r' / 'rb'：以str / byte為單位**讀取(read)**
>* 'w' / 'wb'：以str / byte為單位**寫入(write)**，而且會覆蓋原檔案內容
>* 'a'：在檔案內容最後**接著寫入(append)**，比write安全，不會整塊被蓋掉

*as後的變數(file)只在with這段區塊有效
```py
with open('./example.txt','r') as file:
#raw_lines = file.readlines()，若mode = 'r'
#file.write('anything you want)，若mode = 'w' or 'a'
```
### import套件
若沒有import需要用的函式庫，將出現NameError
有三種方法
```py
import re #直接import名為re的套件
import pandas as pd #import名為pandas的套件，並名為pd，是用套件名字較長的情境
from collections import Counter #從collections這個套件中取一部分名為counter的函式或類別來用
#若一開始是import collections，使用Counter是需要寫collection.Counter()，若採from...import...方式，則只要寫Counter()

#使用Counter去算字頻
from collections import Counter

my_list = ['a','b','e','b']
my_counter = Counter(my_list)
print('b出現{}次'.format(my_counter['b']))
```
### str.format()：透過{}和:替代之前的%
```py
"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
'hello world'
 
"{0} {1}".format("hello", "world")  # 设置指定位置
'hello world'
 
"{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'
```
#### 設置參數
```py
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
print("网站名：{name}, 地址 {url}".format(name="菜鸟教程", url="www.runoob.com"))
 
# 通过字典设置参数
site = {"name": "菜鸟教程", "url": "www.runoob.com"}
print("网站名：{name}, 地址 {url}".format(**site))
 
# 通过列表索引设置参数
my_list = ['菜鸟教程', 'www.runoob.com']
print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的

'''
网站名：菜鸟教程, 地址 www.runoob.com
'''
```
### 字詞統計 - str.count()
whole_string

### 如何辨識dict
1. dict.copy() #比較耗時
2. list(dict.keys()) 