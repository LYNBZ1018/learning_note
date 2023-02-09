## Basic

### tips

1. `__name__`

```markdown
if __name__ == "__main__"
__name__  #是文件的名字
	在自己的.py文件中时是 __main__
	被别的文件import时就是 文件的名字
```



2. `print`

```python
print('')  # 可以用于换行
print('Hello', end = '')  # 取消换行 也可以加入其它字符
print(' '.join(map(str, list1)))
```









### Variable & String



1. `“”` 和 `’‘`，作用完全一样，如果语句中有 `‘` 就需要用 `“”` 括起来。`"Let's go!"`  `'\"Life is short, let\'s learn Python.\"\n'`

2. 原语句，在句子前加上 `r` <u>转义字符不再起作用</u>，`print(r'hello\tworld\n')`

3. 句子为结束，`\`加到句子结尾表示**句子未结束**，

   ```python
   print('hello world\
    nihao\
    hi')
   ```

4. `''' '''` 三引号，可以用于注释，用于字符串跨行(不用换行符)



1. 字符串乘法复制，`print('I love you.\n' * 3000)`





#### **转义字符表**

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20221016183440.png" alt="1" style="zoom: 67%;" />

### 常数

1. 整数可以做大整数运算

2. 浮点数不精准 `0.1 + 0。2 == 0.3  # False`

   ```python3
   import decimal
   a = decimal.Decimal('0.1')
   b = decimal.Decimal('0.2')
   c = decimal.Decimal('0.3')
   a + b == c  # True
   ```

3. 复数 `x = 3 + 4j` `x.real #实部  x.imag  # 虚部`

4. 符号

   ```python
   1. // # 整除 进行整除后区不大于目标数的最大整数
   	-3 // 2 == -2
   2. divmod(3, 2)  # 返回 // 和 % 结果
   	divmod(3, 2)  # (1, 1)
       divmod(-3, 2)  # (-2, 1)
   3. abs  # 实数的绝对值 和 复数的模
   4. int('520')  float('1e6')
   5. pow(2, 3)   2 ** 3
   	pow(2, 3, 5)  # 2^3 % 5 = 3
   ```

   

### 布尔

- 定义为 False 的对象：None 和 False
- 值为 0 的数字类型：0, 0.0, 0j, Decimal(0), Fraction(0, 1)
- 空的序列和集合：'', (), [], {}, set(), range(0)

```python
from fractions import Fractino
bool(Fraction(0, 1))  # False
float(Fraction(3, 4))  # 0.75
```

**运算符**

`not > and > or`

短路原则

```python
3 or 4  # 3
0 or 4  # 4
3 and 4  # 4
0 and 4  # 0
```



#### 运算优先级

![image-20221017220257341](https://gitee.com/lynbz1018/image/raw/master/img/20221017220258.png)



### 分支和循环

#### if-else

1. 可以用作cpp中的三目运算符 ? :

   ```python
   def gcd(a: int, b: int):
       return b if a % b == 0 else gcd(b, a % b)
   ```

   



#### for

```python
range(stop)
range(start, stop)
range(start, stop, step)
range(10, 0, -1)
```



### List

```python
a = [1, 2, 3, 4, 5]
a[1:3]  # 2, 3 不包括尾部
a[:3]  # 1, 2, 3
a[0:5:2]  # 1, 3, 5
```



**增加**

```python
a = [1, 2, 3, 4, 5]

a.append(6)  # 只能追加一个值
a.extend([7, 8])
a[len(a):] = [9, 10, 11]

a.insert(0, 0)
a.insert(len(a), 12)  #  只能插入一个值
```



**删除**

```python
a.remove(10)  # 按值删除 删除值为10的下标最小的一个值
a.remove(a[10])  # 按下标删除

a.pop(10)  # 按下标挤出

a.clear()  # 清空列表
```



**替换**

```python
a = [1, 2, 3, 4, 5]
a[3:] = [7, 8]  # 1 2 3 7 8
```



```python
a.sort()  # 排序
a.reverse()  # 调转
a.count()  # 计数
a.index(value, start, stop)  # 找value的index 多个相同的会返回第一个找到的下标
a.copy()
```



**列表的加法和乘法**

加法是连接

乘法是多倍复制

```python
a = [1, 2, 3]
b = [4, 5, 6]
a + b  # 1, 2, 3, 4, 5, 6  
a * 2  # 1, 2, 3, 1, 2, 3
```



**嵌套列表**

```python
A = [0] * 3
for i in range(3):
    A[i] = [0] * 3

A = [[0] * 3 for i in range(3)]

B = [[0] * 3] * 3  # 错误的 B[0] is B[1]  True

a = 'lyn'
b = 'lyn'
a is b  # True
```

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20221025175502.png" alt="image-20221025175500795" style="zoom:67%;" />



**深拷贝、浅拷贝**

```python
import copy
# 都是浅拷贝 只拷贝外层的
b = a[:]
b = a.copy()
b = copy.copy(a)

b = copy.deepcopy(a)
```



#### **列表推导式**

[express for target in iterable]

[express for target1 in iterable1 if condition1

​				 for target1 in iterable2 if condition2

​				  ...]

```python
a = [i for i in range(10)]
a = [i * 2 for i in a]

a = [0] * 3
for i in range(3):
    a[i] = [0] * 3

cnt = 1
for i in range(3):
    for j in range(3):
        a[i][j] = cnt
        cnt += 1
        
diag = [a[i][i] for i in range(3)]
rdiag = [a[i][2 - i] for i in range(2, -1, -1)]
```



```python
a = [i + 1 for i in range(11) if i % 2 == 0]  # 1 3 5 7 9 11 线运行左边的再判断if
flatten = [col for row in a for col in row]

a = [[i, j] for i in range(10) if i % 2 == 0 for j in range(10) if j % 3 == 0]
```



### Tuple

用`()`表示，相当于一个低配的列表

不支持修改

```python
a = (1, 2, 3)  # 也可以不写括号
a.count(3)
a.index('2')

# 嵌套
a = ((1, 2, 3), (4, 5, 6))

# 只有一个元素的元组
a = (1,)

# 解包
a = (1, 2, 3)
x, y, z = a

x, y = 10, 20  # 先对值进行打包，再进行解包赋值给变量
```



### Str



#### **大小写**

```python
x = 'I love Python'
x.capitalize()  # 一个句话的第一个字母大写其余小写
x.casefold()  # 全部小写
x.title()  # 每个单词第一个字符大写
x.swapcase()  # 大小写翻转
x.upper()  # 大写
x.lower()  # 小写  只能用于英文  casefold可以用于其他的
```



#### **填充**

```python
x = 'String'
x.center(10, '-')
x.ljust(10, '_')
x.rjust(10, '+')
x.zfill(100)  # 用0在前边填充
```



#### **查找**

```python
x.count('x')
x.count('x', 0, 3)

x.find('x')  # 从左开始
x.rfind('x')  # 右开始
```



**替换**

```python
new_code = code.expandtabs(4)  # 用空格代替Tab，一个Tab制定4个空格
code.replace('old', 'new', -1)  # 默认-1表示全部替换

tables = str.maketrans('ABCDEFG', '1234567', 'love')  # 忽略掉'love'
code.translate(tables)  # 根据表格进行转换
```



#### **判断**

![image-20221028212502111](https://gitee.com/lynbz1018/image/raw/master/img/20221028212503.png)



```python
x.startswith('x', start, end)  # end是结尾的下一个下标
x.endswith('x', start, end)

x.isupper()  # all upper
x.islower()  # all lower

x.title()  #  字母开头是否是大写
x.isalpha()  # 是否都是字母
x.isprintable()   # 是否是可打印字符
x.alnum()  # 是否是字母或数字
x.isidentifier()  # 是否是正确的标识符

import keyword
keyword.iskeyword('if')  # 判断是否是保留标识符
```



#### 删除

```python
x.lstrip()
x.rstrip()
x.strip('w.com')

x.removeprefix('www.')  # 严格去除
x.removesuffix('.com') 
```



#### 拆分&拼接

```python
x.partition('.')  # split into three
x.rpartition('/')  # split from the back

x.split('.', -1)  # split multiple times, default to -1
x.rsplit('.')  # split from the back

# The newline character is \n in linux, \r in mac, \r\n in win
x.splitlines()  # split by line break
x.splitlines(True)  # include line break

# join(iterable)
'.'.join(['www', 'supcache', 'com'])  # www.supcache.com
''.join(('hello', 'world'))  # more efficient splicing with join function
```



#### 格式化

```python
'1+1={}, 2^2={}, 3^3={}'.format(1 + 1, 2 ** 2, 3**3)
'{1} {0}'.format('world', 'hello')

# index:position fillcharacter length
# <left ^center >right
'{0:>010}{1:^+8}{2:<010}'.format(1, 2, 3)
```



**syntaxsugar**

```python
f'1+1={1+1} 2^2={2**2}'
```

f F, only for versions after 3.6

format is more application

![image-20221028230315643](https://gitee.com/lynbz1018/image/raw/master/img/20221028230317.png)

![image-20221028230728704](https://gitee.com/lynbz1018/image/raw/master/img/20221028230729.png)



### 序列

序列可以分为**可变序列**和**不可变序列**

**列表**就是可变数组

**元组**和**字符串**是不可变数组



序列通用运算 `+ *`

```python
id(x)
x = 'lyn'
y = 'lyn'
x is y  # whether the id are the same
x is not y

x = [3]
y = [1, 2, 3]
3 in y  # True
x in y  # False
del x, y  # delete x, y

# claer list
y.clear()
del y[:]
```



#### 列表 元组 字符串 相互转换

```python
# list() tuple() str()

a = list(range(10))
min(a)
max([], default=0)

len(a)  # length
sum(a)  # summation

sorted(a)
sorted(a, reverse=True)
a = ['curry', 'durant', 'green', 'kaly']
sorted(a, key = len)

reversed(a)  # return an iterator
list(reversed(a))
list(reversed(range(a)))
```



```python
x = [1, 1, 1]
y = [1, 0, 1]
all(x)
any(x)

# enumerate()
list(enumerate(a, start=1))  # (index, value) start is the start value

# zip()
x = 'lyn'
y = [1, 2, 3, 4]
z = [1, 2, 3, 4, 5]
zipped = zip(x, y, z)
list(zipped)  # [('l', 1, 1), ('y', 2, 2), ('n', 3, 3)]

# itertools.zip_longest
import itertools
zipped = itertools.zip_longest(x, y, z)  # take the longest one as standard, fill in none for empty

# map
list(map(pow, [2, 3, 10], [8, 2, 3]))  # will be terminated in the shortest place

# filter()
list(filter(str.islower, 'LYNbz'))  # the result will be returned only if the result is true

# iterator
a = [1, 2, 3, 4, 5]
it = iter(a)
for i in range(5):
	next(it)  # The value of the iterator is not available after output
```



### Map

```python
a = {'1': 'a', '2': 'b', '3': 'c'}
b = dict(a='1', b='2', c='3')  # The key cannot start with a number
c = dict(zip([1, 2, 3], ['a', 'b', 'c']))

# fromkeys
a = dict.fromkeys('supcache', 24)  # {'s': 24, 'u': 24, 'p': 24, 'c': 24, 'a': 24, 'h': 24, 'e': 24}
a['L'] = 1024

# pop
a.pop('s', 'none')  # pop(key, default)
a.popitem()  # Delete the last joined

# del
del a['c']
a.clear()
del a

# update()
a.update('a':1, 'c':2)

# get() setdefault()
a.get('a', 'none')
a.setdefault('d', 'no')  # If there is no corresponding key, a new key-value pair will be added

a.copy()
len(a)
'c' in a
'd' not in a
list(a)  # key list
list(a.values())
reverse
```



**视图**

`keys() values() items()`

![image-20221030001254703](https://gitee.com/lynbz1018/image/raw/master/img/20221030001256.png)



### Set

```python
a = {1, 2, 3, 4}
b = {s for s in 'supcache'}
c = set('supcache')

x = a.copy()
'c' in a

# issubset() issuperset()
set('sup').issubset(set('supcache'))
set('supcache').issuperset(set('sup'))

# union() intersection() difference() symmetric_difference()
a = set('Python')
a.union({1, 2, 3}, 'Java')  # |
a.intersection('python')  # &
a.difference('python')  # -
a.symmetric_difference('pythonJava')  # ^ {'a', 'P', 'J', 'p', 'v'}

# update()
a.update([1, 2, 3], 'Java')  # 1, 2, 3, 'J', 'a', 'v'
a.intersection_update('Java')  # 'J', 'a', 'v'
a.difference_updae('v')  # 'J', 'a'
a.symmetric_difference_update('ay')  # 'J', 'y'

a.add('Python')  # 'Python'

# remove() discard()
a = set('Python')
a.remove('P')  # Deleting elements that are not present will report an error
a.discard('t')  # Deleting elements that are not present will be silent and no error reporting will be done

# pop()
a.pop()  # Delete a random

# Only immutable types can be hashed
x = frozenset('Python')
y = {x, 'J', 'a', 'v'}
```



### Function

```python
def func(name, times):
    for i in range(times):
        print(f'Hello {name}')
        
def func():
    pass  # placaeholder

print(func())  # No return value, default returns a none 

def func(a, b, c):
    print(f'{a} {b} {c}')
    
# Location Parameters
func('I', 'Love', 'Python')  # I love Python

# Keyword Parameters
func(c = 'cpp', a = 'I', b = 'Love')  # I Love cpp

# The position parameter must precede the keyword parameter
func('I', 'Love', c = 'Python')

# Default Parameters
# All default parameters must be followed by non-default parameters
def func(a, b, c = 'Python'):
    print(f'{a} {b} {c}')
    
# / The left side cannot be used with keyword parameters and the right side can be used
def func(a, /, b, c):
    print(a, b, c)
func(1, b = 2, c = 3)

# * The right side must be used with keyword parameters
def func(a, *, b, c):
    print(a, b, c)
func(1, b = 2, c = 3)

# Collection parameters
def func(*args):
    for i in range(len(args)):
        print(args[i], end = ' ')
func(1, 2, 3, 4, 5)  # 1 2 3 4 5

# When there are collection parameters, other parameters should be indicated by keyword parameters
def func(*args, a, b):
    for i in range(len(args)):
        print(args[i], end = ' ')
    print(a, b)
func(1, 2, 3, 4, 5, a = 8, b = 9)

# The collection parameter can also be a dictionary
def func(**kwargs):
    print(kwargs)
func(a = 1, b = 2, c = 3)  # {'a': 1, 'b': 2, 'c': 3}

# Mixed use
def func(a, *b, **c):
    print(a)
    print(b)
    print(c)
    
func(1, 'a', 'b', 'c', aa = 1, bb = 2, cc = 3)

1
('a', 'b', 'c')
{'aa': 1, 'bb': 2, 'cc': 3}

# Unpacking
args = (1, 2, 3)
kwargs = dict(zip(['aa', 'bb', 'cc'], [1, 2, 3]))
func(0, *args, **args)
```



#### **作用域**

```python
# nonloacl

def func():
    x = 100
    def funca():
        nonlocal x
        x = 200
        print(id(x), x)
    funca()
    print(id(x), x)

func()
2306442533328 200
2306442533328 200
```



#### **闭包**

```python
def power(exp):
    def exp_of(base):
        return base ** exp
    return exp_of

square = power(2)
cube = power(3)
square(3)
9
cube(3)
27

def outer():
    x = 0
    y = 0
    def inner(x1, y1):
        nonlocal x, y
        x += x1
        y += y1
        print(f'x: {x}, y: {y}')
    return inner
move = outer()
x: 1, y: 2
move(-1, 5)
x: 0, y: 7
```



#### **装饰器**

```python
def time_master(func):
    def call_func():
        print('start...')
        start = time.time()
        func()
        stop = time.time()
        print('end....')
        print(f'all time: {(stop - start):.2f}')
    return call_func

@time_master  # myfunc = time_master(myfunc)
def myfunc():
    time.sleep(2)
    print('Hello World!')

    
myfunc()
start...
Hello World!
end....
all time: 2.0
```



**Multiple decorators**

Syntactic sugar works from the bottom up

```python
def add(func):
    def inner():
        x = func()
        return x + 1
    return inner

def square(func):
    def inner():
        x = func()
        return x ** 2
    return inner

def cube(func):
    def inner():
        x = func()
        return x ** 3
    return inner

@add
@square
@cube
def test():
    return 2

print(test())  # (2 ** 3) ** 2 + 1 = 65
65
```



#### lambda 表达式

```python
lambda argu1, argu2, argu3, ... , argun : express
squarey = lambda y : y * y
squarey(3)

mapped = map(lambda x : ord(x) + 10, 'supcache')
list(mapped)

list(filter(lambda x : x % 2, range(10)))
```



#### generator 生成器

Replace 'return' with 'yield', the function returns the value of 'yield' each time

```python
def count():
    i = 0
    while i <= 5:
        yield i  # return i
        i += 1
        
c = count()
list(c)  # [0, 1, 2, 3, 4, 5]
for i in range(6):
    next(c)
    
def fib():
    back1, back2 = 0, 1
    while (True):
        yield back1  # return back1
        back1, back2 = back2, back1 + back2

f = fib()
for i in range(10):
    next(f)
```



**A list expression is also a generator that generates all the elements and puts them into a list**

`(i ** 2 for i in range(10))`

`<generator object <genexpr> at 0x000001FB08F2AE30>`



#### Higher-Order Function

A function with a function as an argument becomes a higher-order function

```python
# reduce
def add(a, b):
    return a + b
import functools
functools.reduce(add, [1, 2, 3, 4, 5])  # add(add(add(add(1, 2), 3), 4), 5)

functools.reduce(lambda x, y : x * y, range(1, 5))  # 24


```





### 文件读取

```python
f = open('test.txt', 'w')
f.write('hell0')
f.writelines(['hello\n', 'world\n'])

f  # 是一个文件指针，指向最后后 EOF 要重新读就要指向开始的位置
f = open('test.txt', 'r+')
for i in range(3):
    line = f.read.lins(3)
    print(line)
f.tell()  # 21
f.seek(0)  # 指向0

f.flush()  # 清除缓存区
f.close()
```

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20221126000339.png" alt="image-20221126000338103" style="zoom: 67%;" />

```python
from pathlib import Path
p = Path.cwd()
q = p / 'test.txt'
q.is_dir()
q.is_file()

q.name  # 最后一个名字 test.txt
q.stem  # 获取文件名 test
q.suffix  # 获取后缀 .txt
q.parent  # 获取父级目录
q.parts  # ('C:\\', 'Users', 'lyn95', 'AppData', 'Local', 'Programs', 'Python', 'Python310', 'test.txt')
q.stat().st_size  # 文件大小

Path('../test.txt').resolve()  # 转换为绝对路径
p.iterdir()  # 目录下所有的文件
[x for x in p.iterdir() if x.is_file()]

n = p / 'test/A/B/C'
n.mkdir(parents=True, exist_ok=True)  # 第一个参数 可以递归创建 第二个参数 如果已经创建了不会报错

m = 'D:/left/desk/test.txt'
f = m.open('W')
f.write('hello world')
f.close()

m.rename(m.parent/'Newtest.txt')
n = m.parent/'test/A/B/C'  # test文件夹
n.unlink()  # 先删除文件才能删除文件夹
for i in range(4):
    n.rmdir()
    n = n.parent

n = Path.cwd()
list(n.glob('*/*.py'))  # 当前目录下的所有.py文件
list(n.glob('**/*.py'))  # 当前目录包括子目录下的
```



```python
with  # 上下文管理器 自动关闭文件
from pathlib import Path
p = Path('D:/left/desk/test.txt')
with open(p, 'w') as f:
    f.write('hello world\n')
    
pickle  # 以二进制存取
import pickle
str = 'hello world'
with open(p.parent/'write.pkl', 'wb') as f:
    pickle.dump(str, f)

with open(p.parent/'write.pkl', 'rb') as f:
    s = pickle.load(f)
print(s)
```



### 异常 exception

```python
try except  ###
try:
    1 / 0
except ZeroDivisionError as e:
    print('error\n', e)
    
try:
    1 / 0
    'hello' + 110
except (ZeroDivisionError, ValueError, TypeError):
    pass

try except else  ###
try:
    1 / 1
except:
    print('divid error')
else:
    print('yyy')

try except finally  ###
try:
    1 / 0
except ZeroDivisionError as e:
    print(e)
finally:
    print('yyy')
```



<img src="https://gitee.com/lynbz1018/image/raw/master/img/20221126164333.png" alt="image-20221126164332130" style="zoom:50%;" />

```python
raise ValueError('error')  # Manually throwing exceptions

# Exception chain
raise ValueError('error') from ZeroDivisionError
try:
    1 / 0
except:
    raise ValueError('note 0') from ZeroDivisionError

# assert
a = 10
assert a == 10  # Nothing can happen if the result is correct
assert a == 9  # AssertionError
```



### 类与对象 class object

```python
# Encapsulation
class Person:
    name = 'supcache'
    def get_name(self):
        print(self.name)  # supcache
    def print_blank(self):  # Pass 'self' default when no parameters are needed
        print('hello')
       
# Inheritance
class A:
    name = 666
    def hello(self):
        print('I am A')
class B(A):
    name = 888
    def hello(self):
        print('I am B')
tmp = B()
tmp.hello()  # I am B

class C(A, B)  # visit from the left, if you don't find it, look in the next one
class A:
    x = 10
    y = 100
class B:
    x = 225
class C(A, B):
    pass
tmp = C()
tmp.x  # 10

isinstance(tmp, C)  # True
isinstance(tmp, A)  # True

tmp.__dict__  # View the properties owned by an instance

class A:
    x, y = 10, 100
    def set_xy(self, x, y):
        self.x = x
        self.y = y
a = A()  # a.__dict__ null
a.set_xy(1, 2)  # a.__dict__ {'x': 1, 'y': 2}

  # At first the instance is instantiated from the class and has no properties, and only after instantiating itself through the set function does it have properties
```



#### Constructors

```python
#  __init__
class A:
    def __init__(self, x, y):
        self.x = x
        self.y = y
  	def add(self):
        return self.x + self.y
    def mul(self):
        return self.x * self.y
a = A(3, 4)
a.add()  # 7
a.mul()  # 12

# Rewrite
class B(A):
    def __init__(self, x, y, z):
        A.__init(self, x, y)
        self.z = z
    def add(self):
        return A.add(self) + self.z
    def mul(self):
        return A.mul(self) * self.z
b = B(1, 2, 3)
b.add()  # 6
b.mul()  # 6

# MRO Method Resolution Order
# super().__init__()
class A:
    def __init__(self):
        print('A')
class B1(A):
    def __init__(self):
        super().__init__()
        print('B1')
class B2(A):
    def __init__(self):
        super().__init__()
        print('B2')
class C(B1, B2):    
    def __init__(self):
        super().__init__()
        print('C')
c = C()
A
B2
B1
C
 # Avoid duplicate calls
C.mro()
[<class '__main__.C'>, <class '__main__.B1'>, <class '__main__.B2'>, <class '__main__.A'>, <class 'object'>]
```



#### Polymorphism

```python
class Shape:
    def __init__(self, name):
        self.name = name
    def area(self):
        pass
    def print_info(self):
        print(self.name)
        print(self.area())
class Circle(Shape):
    def __init__(self, radius):
        super().__init__('Circle')
        self.radius = radius
    def area(self):
        return 3.14 * self.radius * self.radius
    def print_info(self):
        super().print_info()
class Triangle(Shape):
    def __init__(self, base, height):
        super().__init__('Triangle')
        self.base = base
        self.height = height
    def area(self):
        return self.base * self.height / 2
    def print_info(self):
        super().print_info()
        
c = Circle(10)
c.print_info()
Circle
314.0
t = Triangle(3, 4)
t.print_info()
Triangle
6.0
```





#### Private Variables  \__slots__

```python
# Pricate variables are prefixed with two underscores
class C:
    def __init__(self, x):
        self.__x = x
    def get_x(self):
        print(self.__x)
    def set_x(self, x):
        self.__x = x
c = C(10)
c.__x  # error
c.get_x()  # 10
c.set_x(100)
c.__dict__  # {'_C__x': 100}
c._C__x  # 可以访问私有变量
```



`After defining slots, you can no longer add attributes dynamically`

```python
class A:
    __slots__ = ['__x', '__y']
    def __init__(self, x, y):
        self.__x = x
    def get_x(self):
        print(self.__x)
    def get_y(self):
        print(self.__y)
    def set_x(self, x):
        self.__x = x
    def set_y(self, y):
        self.__y = y
a = A(10, 100)
a.__dict__  # error
a.__slots__  # ['__x', '__y']
```



#### \__del__

```python
class D:
    def __init__(self, name, func):
        self.name = name
        self.func = func
    def __del__(self):
        self.dunc(self)
def outter():
    x = 0
    def inner(y = None):
        nonlocal x
        if y:
            x = y
        else:
            return x
    return inner
f = outter()
d = D('sup', f)
d.name  # sup
d  # <__main__.D object at 0x0000022281AB3F10>
del d  # At the beginning y is empty and will assign self to x
f()
<__main__.D object at 0x0000022281AB3F10>
```



重写运算方法

```python
__add__(self, other)
class S1(str):
    def __add__(self, other):
        return len(self) + len(other)
s1 = S1('hello')
s2 = S1('worldddd')
s1 + s2
13

__radd__(self, other)  # 左右两侧对象类型不同，右侧没有定义__add__或者返回一个NotImplemented，就会在右边找有没有定义 __radd__

__iadd__(self, other)  # x += y
```



#### 属性访问

```python
class A:
    def __init__(self, name, age):
        self.__name = name
        self.__age = age
a = A('lyn', 18)
a._A__name
hasattr(a, '_A__name')  # 有没有属性
getattr(a, '_A__name')  # 获取属性的值
setattr(a, '_A__age', 20)  # 改变属性
del a._A__name  # 删除属性
```

```python
# getattr()  和 __getattribute__() 对应
class A:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __getattribute__(self, attrname):
        print('test')
        return super().__getattribute__(attrname)
    
a = A('sup', 18)
getattr(a, name)
test
sup
a.age  # 访问属性时也是调用了 __getattribute__()函数
test
18

# 访问不存在的属性时才会调用__getattr__()
class A:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __getattribute__(self, attrname):
        return super().__getattribute__(attrname)
    def __getattr__(self, attrname):
        if (attrname == 'supcache'):
            print('supcache~')
        else:
            raise AttributeError(attrname) 
```



```python
class A:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __setattr(self, attrname, value):
        self.__dict__[sttrname] = value

a = A('aa', 18)
setattr(a, 'name', 'ss')
a.name
'ss'     

class A:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    def __delattr__(self, attrname):
        del self.__dict__[attrname]
```



#### 索引 切片 迭代协议

```python
class D:
    def __init__(self, data):
        self.data = data
    def __getitem__(self, index):
        return self.data[index]
    def __setitem__(self, index, value):
        self.data[index] = value

    
d = D([1, 2, 3, 4, 5])
d[1]  # __getitem__
2
d[1] = 1  # __setitem__
d.__dict__
{'data': [1, 1, 3, 4, 5]}
d[::2]  # [::2]  [slice(None, None, 2)]
[1, 3, 5]
d[slice(None, None, 2)]
[1, 3, 5]

d = D([1, 2, 3, 4, 5])  # 如果类中没有实现__iter__ __next__ 就会使用__getitem__ 代替执行
for i in d:
    print(i, end=' ')

1 2 3 4 5
```



```python
class Double:
    def __init__(self, start, stop):
        self.value = start - 1
        self.stop = stop
    def __iter__(self):
        return self
    def __next__(self):
        if self.value == self.stop:
            raise StopIteration
        self.value += 1
        return self.value * 2

    
d = Double(1, 5)
for i in d:
    print(i, end = ' ')

    
2 4 6 8 10 
```



#### 代偿

```python
class C:
    def __init__(self, data):
        self.data = data
    def __contains__(self, item):
        return item in self.data

    
c = C([1, 2, 3, 4, 5])
3 in c
True

# 没有实现__contains__ 时 可以用 __iter__ __next__ 代替使用
class C:
    def __init__(self, data):
        self.data = data
    def __iter__(self):
        print("Iter", end = '->')
        self.i = 0
        return self
    def __next__(self):
        print("Next", end = '->')
        if self.i == len(self.data):
            raise StopIteration
        item = self.data[self.i]
        self.i += 1
        return item

    
c = C([1, 2, 3, 4, 5])
3 in c
Iter->Next->Next->Next->True

class C:
    def __init__(self, data):
        self.data = data
    def __getitem__(self, index):
        print("GetItem", end = "->")
        return self.data[index]

    
c = C([1, 2, 3, 4, 5])
3 in c
GetItem->GetItem->GetItem->True
6 in c
GetItem->GetItem->GetItem->GetItem->GetItem->GetItem->False
```



![image-20230104155831749](https://gitee.com/lynbz1018/image/raw/master/img/20230104155837.png)



```python
str
repr
eval  # 剥去引号 执行句子

repr('1 + 3')
"'1 + 3'"
eval('1 + 3')
4
eval(repr('hello'))
'hello'

str('sup')
'sup'
repr('sup')
"'sup'"
```

72 over



## 算法Python代码

### 快速排序

```python
def quick_sort(q, l, r):
    if l >= r:
        return
    i = l - 1
    j = r + 1
    x = q[l + r >> 1]
    while i < j:
        i += 1
        while q[i] < x:
            i += 1
        j -= 1
        while q[j] > x:
            j -= 1
        if i < j:
            q[i], q[j] = q[j], q[i]
        
        quick_sort(q, l, j)
        quick_sort(q, j + 1, r)

n = int(input())
a = list(map(int, input().split()))
quick_sort(a, 0, n - 1)
print(" ".join(map(str, a)))
```



### 第K小的数

```python
def quick_sort(arr: list, l: int, r: int, k: int):
    if l >= r:
        return arr[l]
    i = l - 1
    j = r + 1
    x = arr[(l + r) // 2]
    while i < j:
        i += 1
        while arr[i] < x:
            i += 1
        j -= 1
        while arr[j] > x:
            j -= 1
        if i < j:
            arr[i], arr[j] = arr[j], arr[i]

        if j - l + 1 >= k:
            return quick_sort(arr, l, j, k)
        else:
            return quick_sort(arr, j + 1, r, k - (j - l + 1))

n, k = map(int, input().split())
nums = list(map(int, input().split()))
res = quick_sort(nums, 0, n - 1, k)
print(res)
```



### 归并排序

```python
n = int(input())
a = list(map(int, input().split()))

def merge_sort(q):
    if len(q) <= 1:
        return
    
    mid = len(q) // 2
    L = q[: mid]
    R = q[mid: ]
    merge_sort(L)
    merge_sort(R)
    
    i = j = k = 0
    while i < len(L) and j < len(R):
        if L[i] <= R[j]:
            q[k] = L[i]
            i += 1
        else:
            q[k] = R[j]
            j += 1
        k += 1
        
    while i < len(L):
        q[k] = L[i]
        k += 1
        i += 1
    while j < len(R):
        q[k] = R[j]
        k += 1
        j += 1

if __name__ == "__main__":
    merge_sort(a)
    print(" ".join(map(str, a)))
```



### 数的范围

```python
n = q = x = 0
n, q = map(int, input().split())
a = list(map(int, input().split()))
while q > 0:
    q -= 1
    x = int(input())
    l = 0
    r = n - 1
    while l < r:
        mid = l + r >> 1
        if a[mid] < x:
            l = mid + 1
        else:
            r = mid
    if a[l] != x:
        print('-1 -1')
        continue
    l1 = l
    r1 = n
    while l1 + 1 < r1:
        mid = l1 + r1 >> 1
        if a[mid] <= x:
            l1 = mid
        else:
            r1 = mid
    print("%d %d" % (l, l1))  # 格式化输出
```

