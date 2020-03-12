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

