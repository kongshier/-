> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 1 Python简介

更新至3.0版本

 **特点**

1. 跨平台语言
2. 解释型语言  （无编译）
3. 交互式语言
4. 面向对象语言

# 2 Python 基础

## 2.1 输出、输入函数

==print函数==  

允许的输出内容：

1. 数字
2. 字符串 （要+单引号 / 双引号）
3. 表达式

**输出到文件中**

open

~~~python
# 指定所在的输出文件位置，使用 file = 变量
fo = open('E:/pythonProject/demo-project/text.txt','a+')
print('hellopython',file=fo)
fo.close()  # 关闭流
~~~



### 2.1 .1 输入函数

input () 

```py
i = str(input('请输入内容：'))
print(i)
```



## 2.2 转义字符

| 样式   | 含义                                  |
| ------ | ------------------------------------- |
| \123   | 1~3位八进制数据所表示的字符，如\256   |
| \uF890 | 4位十六进制数据所表示的字符，如\u0014 |
| ’      | 单引号字符                            |
| \      | 反斜杠字符                            |
| \t     | 水平制表符 占四个制表位               |
| \v     | 垂直制表符                            |
| \r     | 回车                                  |
| \n     | 换行符                                |
| \b     | 退格                                  |
| \f     | 换页                                  |
| \a     | 响铃                                  |



### 运算符

高到低的顺序列出了所有的运算符，如下表：

| 运算符                                                       | 描述                           |
| ------------------------------------------------------------ | ------------------------------ |
| `[]` `[:]`                                                   | 下标，切片                     |
| `**`                                                         | 指数                           |
| `~` `+` `-`                                                  | 按位取反, 正负号               |
| `*` `/` `%` `//`                                             | 乘，除，模，整除               |
| `+` `-`                                                      | 加，减                         |
| `>>` `<<`                                                    | 右移，左移                     |
| `&`                                                          | 按位与                         |
| `^` `\|`                                                     | 按位异或，按位或               |
| `<=` `<` `>` `>=`                                            | 小于等于，小于，大于，大于等于 |
| `==` `!=`                                                    | 等于，不等于                   |
| `is`  `is not`                                               | 身份运算符                     |
| `in` `not in`                                                | 成员运算符                     |
| `not` `or` `and`                                             | 逻辑运算符                     |
| `=` `+=` `-=` `*=` `/=` `%=` `//=` `**=` `&=` `|=` `^=` `>>=` `<<=` | （复合）赋值运算符             |

**比较运算符有的地方也称为关系运算符，包括`==`、`!=`、`<`、`>`、`<=`、`>=`**

**逻辑运算符有三个，分别是`and`、`or`和`not`**



## 2.3 进制与编码

### 1 二进制

#### 1 基本单位

- 信息存储量是度量存储器存放程序和数据的数量。
- 位（Bit）：计算机当中最小的信息单位
  	存放一个二进制位数，即 0 或 1
- 字节（Byte）：计算机中的基本信息单位常用的单位
- 字（Word）：有字节组成
- 字长：字的位数
  	字长越长，计算机性能越好
- 千字节（KB）
- 容量单位：  位（bit）-> 字节 B ->  千字节 KB -> 兆字节 MB -> 吉字节 GB ->  TB ->  PB ->  EB、ZB、YB 、NB、DB等 

#### 2 单位换算

- 1字节(Byte) = 8位(bit) 2^3方
- 1KB( K，千字节) = 1024B  2^10方

- 1MB( M，兆字节) = 1024KB

- 1GB( G，吉字节，千兆) = 1024MB

- 1TB( T，万亿字节，太字节) = 1024GB

- 1PB( P，千万亿字节，拍字节) = 1024TB

- 1EB( E，百亿亿字节，艾字节) = 1024PB



### ASCII码

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/ASCII.png" alt="ASCII"  />

## 2.4 标识符和保留字

保留字：具有特殊意义，不能用来做变量或者对象

标识符：变量、函数、类、模块和其他对象起的名字

规则：

1. 字母、数字、下划线
2. 不能以数字开头
3. 不能是保留字
4. 严格区分大小写

## 2.5 变量的定义和使用

- 标识
- 类型
- 值

## 2.6 数据类型

- int  ：无小数部分
- str：
- float：有小数部分
- bool  ： true 、 false

### 2.6.1 类行转换

~~~py
name = '张三'
age = 12
print ('name : ' + name + 'age:' + str(age))
~~~



2.7 分支语句

~~~py
if  
else  if (elif)
else
~~~

~~~py
"""
        3x - 5  (x > 1)
f(x) =  x + 2   (-1 <= x <= 1)
        5x + 3  (x < -1)
"""
x = float(input('x = '))
if x > 1:
    y = 3 * x - 5
elif x >= -1:
    y = x + 2
else:
    y = 5 * x + 3
print('f(%.2f) = %.2f' % (x, y)) #保留两位小数 
~~~

#### 练习：百分制成绩转换为等级制成绩。

> **要求**：如果输入的成绩在90分以上（含90分）输出A；80分-90分（不含90分）输出B；70分-80分（不含80分）输出C；60分-70分（不含70分）输出D；60分以下输出E。

~~~py
 # 百分制成绩转换为等级制成绩

score = float(input('请输入成绩: '))
if score >= 90:
    grade = 'A'
elif score >= 80:
    grade = 'B'
elif score >= 70:
    grade = 'C'
elif score >= 60:
    grade = 'D'
else:
    grade = 'E'
print('对应的等级是:', grade)
~~~



pass语句：知识一个占位符，什么都不做

- 搭建好代码结构之后，还不知道具体的代码怎么写

~~~py
a = 1
if a == 1:
    pass
else:
    pass
~~~

## 2.8 循环结构

### range()函数

- 用于生成一个整数数列
- 可迭代对象

语法：

~~~py
range(start, stop)
~~~

- start表示这一些列数字中的第一个数字；stop-1表示这一系列数字中的最后一个数字。
- [ start ,stop) ：区间范围

三种方式

1. range(stop)

   创建一个（0,stop)之间的整数序列,步长为1

2. range(start,stop)

   创建一个（start,stop)之间的整数序列，步长为1

3. range(start,stop,step)

   创建一个[start,stop)之间的整数序列,步长为step
   

> `range(101)`：可以用来产生0到100范围的整数，需要注意的是取不到101。
>
> `range(1, 101)`：可以用来产生1到100范围的整数，相当于==前面是闭区间==后面是开区间。
>
> `range(1, 101, 2)`：可以用来产生1到100的奇数，其中2是步长，即每次数值递增的值。
>
> `range(100, 0, -2)`：可以用来产生100到1的偶数，其中-2是步长，即每次数字递减的值。



### 1  for -in  

- 明确知道了循环的次数


1~100 求和

~~~py
sum = 0
for x in range(101):  # range(1,101)
    sum += x
print(sum)
~~~

~~~py
for i in 'python':
    print(i)
# 将字符串的每个字母遍历输出    
~~~

不需要使用到变量，则使用下划线代替

~~~py
for _ in range(10):
    print('人生苦短，我一直在学习')
~~~



### 2 while

- 不知道循环次数


猜数字游戏：猜数字游戏的规则是：计算机出一个1到100之间的随机数，玩家输入自己猜的数字，计算机给出对应的提示信息（大一点、小一点或猜对了），如果玩家猜中了数字，计算机提示用户一共猜了多少次，游戏结束，否则游戏继续。

```py
# AUTHOR: Kcs
# TIME  : 2022/7/8 18:54
import random  # 导入随机数的
answer = random.randint(1, 101)  # 随机数范围

counter = 0
while True:
    counter += 1
    number = int(input('请输入100以内的数字：'))
    if number <answer:
        print('数字小了')
    elif number >answer:
        print('数字大了')
    else:
        print('恭喜你猜对了，奖励你一个欧里给')
        break
print('你总共猜了%d次'% counter)
if counter > 5:
    print('智商底下，请先补充智商')
```



九九乘法表：

```py
# AUTHOR: Kcs
# TIME  : 2022/7/8 19:04
for i in range(1, 10):
    for j in range(1, i + 1):
        print('%d*%d = %d' % (i, j, i * j), end='\t')
    print()
```



### 练习

#### 练习1：输入一个正整数判断是不是素数。

> **提示**：素数指的是只能被1和自身整除的大于1的整数。

```py
# AUTHOR: Kcs
# TIME  : 2022/7/8 19:36
# 判断素数

from math import sqrt

num = int(input('请输入一个正整数：'))
end = int(sqrt(num))
flag = True
for x in range(2, end + 1):  # 判断是否有其他的因数
    if num % x == 0:
        flag = False
        break
if flag and num != 1:   #没有其他的因数并且不是1
    print('%d是素数' % num)
else:
    print('%d不是素数' % num)
```





#### 练习2：输入两个正整数，计算它们的最大公约数和最小公倍数。

> **提示**：两个数的最大公约数是两个数的公共因子中最大的那个数；两个数的最小公倍数则是能够同时被两个数整除的最小的那个数。

```py
# AUTHOR: Kcs
# TIME  : 2022/7/8 19:45
x = int(input('x='))
y = int(input('y='))
# 如果x大于y就交换x和y的值
if x > y:
    # 交换数值
    x, y = y, x
# 两个数中较小的数开始递减的循环
for fac in range(x, 0, -1):
    if x % fac == 0 and y % fac == 0:
        print('%d和%d的最大公约数是%d' % (x, y, fac))
        print('%d和%d的最小公倍数是%d' % (x, y, x * y // fac))
        break
```



## 构造程序逻辑

1. 水仙花数：

   水仙花数也被称为超完全数字不变数、自恋数、自幂数、阿姆斯特朗数，它是一个3位数，该数字每个位上数字的立方之和正好等于它本身，例如：$1^3 + 5^3+ 3^3=153$。

~~~py
for num in range(100, 1000):
    low = num % 10
    mid = num // 10 % 10
    high = num // 100
    if num == low ** 3 + mid ** 3 + high ** 3:
        print(num)
~~~



2. 反转正整数

   将12345变成54321

   ~~~py
   num = int(input('num = '))
   reversed_num = 0
   while num > 0:
       reversed_num = reversed_num * 10 + num % 10
       num //= 10
   print(reversed_num)
   ~~~

3. 生成**斐波那契数列**的前20个数。

   斐波那契数列的特点是数列的前两个数都是1，从第三个数开始，每个数都是它前面两个数的和，形如：1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

   ```py
   a = 0
   b = 1
   for _ in range(20):
       a, b = b, a + b
       print(a, end=' ')
   ```

4. **百钱百鸡**问题。

   公鸡5元一只，母鸡3元一只，小鸡1元三只，用100块钱买一百只鸡，问公鸡、母鸡、小鸡各有多少只？

   ```py
   """
   1只公鸡5元 1只母鸡3元 3只小鸡1元 用100元买100只鸡
   问公鸡 母鸡 小鸡各有多少只
   """
   
   for x in range(0, 20): # 5元的张数
       for y in range(0, 33): # 3元的张数
           z = 100 - x - y  # 1元的张数
           if 5 * x + 3 * y + z / 3 == 100:
               print('公鸡: %d只, 母鸡: %d只, 小鸡: %d只' % (x, y, z))
   ```

5. 找出10000以内的**完美数**。

   完美数又称为完全数或完备数，它的所有的真因子（即除了自身以外的因子）的和（即因子函数）恰好等于它本身。例如：6（$6=1+2+3$）和28（$28=1+2+4+7+14$）就是完美数。

   ```py
   import math
   
   for num in range(2, 10000):
       result = 0
       for factor in range(1, int(math.sqrt(num)) + 1):
           if num % factor == 0:
               result += factor
               if factor > 1 and num // factor != factor:
                   result += num // factor
       if result == num:
           print(num)
   ```

6. 输出**100以内所有的素数**。

   ```py
   import math
   
   for num in range(2, 100):
       is_prime = True
       for factor in range(2, int(math.sqrt(num)) + 1):
           if num % factor == 0:
               is_prime = False
               break
       if is_prime:
           print(num, end=' ')
   ```

## 2.9 函数和模块

### 函数

函数创建：

- 使用 def  关键字

  ~~~py
  def 函数名(参数)
  
  def add(n):
      
  def add(*s):#*表示s为可变参数    
  ~~~

  ```py
  # 在参数名前面的*表示args是一个可变参数  将传入的参数相加
  def add(*args):
      total = 0
      for val in args:
          total += val
      return total
  
  # 在调用add函数时可以传入0个或多个参数  
  print(add())
  print(add(1))
  print(add(1, 2))
  print(add(1, 2, 3))
  print(add(1, 3, 5, 7, 9))
  ```

#### 递归函数

- 递归调用与终止条件

```py
# 递归求阶乘
def fac(n):
    if n == 1:
        return 1
    else:
        return n * fac(n - 1)

print("阶乘是%d" %  fac(4))
```

斐波那契数列

```py
#斐波那契数列

def fac(n):
    if n==1 or n==2:
        return 1
    else:
        return fac(n-1) + fac(n-2)

print(fac(5))

#输出前20个数
for i in range(1,21):
    print(fac(i),end=" ")
```



 

### 模块

> 每一个python文件就是一个模块，通过**import** 导入指定的模块到python文件来 ，避免了函数名称冲突，也清晰知道了调用的函数来自哪里。

#### 语句

1 **import** 语句

- 调用模块中的函数格式：

  > 模块名. 函数名

  

~~~py
import module1[, module2[,... moduleN]]
~~~

例如调用math

~~~py
import math
# 调用math中的函数
math.abs()
~~~

2 **from**…**import** 语句

语法格式：

~~~py
from modname import name1[, name2[, ... nameN]]
~~~

- modname：模块名
- name1：函数名

eg：

~~~py
# 要导入模块 fib 的 fibonacci 函数
from fib import fibonacci
~~~

#### from…import* 语句 （少使用）

> 把一个模块的所有内容全都导入到当前的命名空间

~~~py
 # from modname import *
from math import *
~~~





`module1.py`

```Python
def foo():
    print('hello, world!')
```

`module2.py`

```Python
def foo():
    print('goodbye, world!')
```

`test.py`

```Python
from module1 import foo
foo()

from module2 import foo
foo()

print('=========二==========')

import module1 as m1
import module2 as m2

m1.fc()
m2.fc()

import module3
```

`module3.py` 

```py
def foo():
    pass

def bar():
    pass

# __name__是Python中一个隐含的变量它代表了模块的名字
# 只有被Python解释器直接执行的模块的名字才是__main__
if __name__ == '__main__':
    print('call foo()')
    foo()
    print('call bar()')
    bar()
```

#### 内置模块

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711151506986.png" alt="image-20220711151506986" style="zoom: 80%;" />

#### 第三方的模块

~~~py
pip install 模块名  #安装第三方模块

import 模块名 # 引用第三方模块名
~~~









### 变量作用域

减少对全局变量的使用，则会减少对cpu的占用时间，降低耦合度

- 局部变量：定义在函数内 
- 全局变量：不定义在任何一个函数内  **globa** 声明全局变量
- 嵌套作用域：**nonlocal**声明变量



#### 主程序运行



~~~py
if __name__ ='__main__':
    print(add(a,b))
~~~



主程序：

add1.py

~~~py
def add(a,b):
    return a+b

if __name__ ='__main__':
    print(add(1,2))
~~~



test.py

~~~py
import add1
print(add(10,20))
# 这样才不会把主程序中的print给显示到控制台上
~~~



### python 的 包

- 分层次的目录结构，功能相似的模块放在一个包下
- 规范代码
- 避免模块代码冲突

> 包含 有 `__init__.py` 的为：包

导包：

~~~py
import 包名.模块名
~~~





## 2.10 字符串

> 在字符串前面使用一个 r 就会显示出字符串的原本内容 \ 不会出现转义

~~~py
s1 = r'\'hello, world!\''
s2 = r'\n\\hello, world!\\\n'
print(s1, s2, end='')
~~~

### 对字符串的操作

1. `+`：拼接字符

2. `*` ：重复字符串内容

3. in \ not in ：是否包含字符串（成员运算）

4. [ ]   \ [ n: m] [n开始：m结束）：切片运算，截取字符串 

5. ==用单引号、双引号、三个单引号创建字符串都只有一个地址，id 都一样== ：字符串驻留机制

   - == ：比较内容
   - is：比较地址
   - 字符串的长度为0或1时
   - 符合标识符的字符串
   - 字符串只在编译时进行驻留，而非运行时
   - [-5.256]之间的整数数字

   

   查询方法

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710102600564.png" alt="image-20220710102600564" style="zoom:80%;" />

   

   大小写转换

   !(Python基础.assets/image-20220710104156865.png)

   ![image-20220710104256045](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710104256045.png)

   字符串内容对齐

   ![image-20220710105916871](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710105916871.png)

   切割字符串

   ![image-20220710114301787](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710114301787.png)

~~~py
str1 = 'hello, world!'
# 通过内置函数len计算字符串的长度
print(len(str1)) # 13

# 获得字符串首字母大写
print(str1.capitalize()) # Hello, world!

# 获得字符串每个单词首字母大写
print(str1.title()) # Hello, World!

# 获得字符串变大写后
print(str1.upper()) # HELLO, WORLD!

# 从字符串中查找子串所在位置
print(str1.find('or')) # 8
print(str1.find('shit')) # -1
# 与find类似但找不到子串时会引发异常

# print(str1.index('or'))
# print(str1.index('shit'))
# 检查字符串是否以指定的字符串开头
print(str1.startswith('He')) # False
print(str1.startswith('hel')) # True

# 检查字符串是否以指定的字符串结尾
print(str1.endswith('!')) # True

# 将字符串以指定的宽度 居中 并在两侧填充指定的字符
print(str1.center(50, '*'))

# 将字符串以指定的宽度 左对齐 并在两侧填充指定的字符
print(str1.ljust(50, '*'))

# 将字符串以指定的宽度 靠右放置 左侧填充指定的字符
print(str1.rjust(50, ' '))
str2 = 'abc123456'

# 检查字符串是否由数字构成
print(str2.isdigit())  # False

# 检查字符串是否以字母构成
print(str2.isalpha())  # False

# 检查字符串是否以数字和字母构成
print(str2.isalnum())  # True

str3 = '  jackfrued@126.com '
print(str3)

# 获得字符串修剪左右两侧空格之后的拷贝
print(str3.strip())
~~~

### 格式化字符串

```py
# 格式化字符串
a, b = 10, 45
print(f'{a}*{b} = {a * b}')
```



## 列表  list[ ]

- 结构化的、非标量类型、有序序列
- 类似数组

创建列表：

1. 使用[ ]

2. 使用**list**()

   ~~~py
   lst = ['nihao','buhoa',123]
   lst2 = list(['nihao','buhoa',123])
   ~~~

特点：

- 有序排序
- 具有索引映射
- 可以存储重复数据
- 元素数据类型混存
- 根据需求动态分配和回收内存

列表的一些列操作

~~~py
lst = ['nihao','buhoa',123]
lst2 = list(['nihao','buhoa',123])

#索引地址
print(lst.index(1))

list1 = [1, 3, 5, 7, 100]
print(list1) # [1, 3, 5, 7, 100]

# 乘号表示列表元素的重复
list2 = ['hello'] * 3
print(list2) # ['hello', 'hello', 'hello']

# 计算列表长度(元素个数)
print(len(list1)) # 5

# 下标(索引)运算
print(list1[0]) # 1
print(list1[4]) # 100
# print(list1[5])  # IndexError: list index out of range
print(list1[-1]) # 100
print(list1[-3]) # 5
list1[2] = 300
print(list1) # [1, 3, 300, 7, 100]

# 切片运算
print(list1[1:4:1])#从索引1开始，4结束(不包括4)，步长为1，步长不写默认为1
print(list1[:2:2])
print(list1[1:4:])
print(list1[1:4:2])

# in \ not in
print(10 in list1)
print('ks' not in list1)


# 通过循环用下标遍历列表元素
for index in range(len(list1)):
    print(list1[index])
    
# 通过for循环遍历列表元素
for elem in list1:
    print(elem)
    
# 通过enumerate函数处理列表之后再遍历可以同时获得元素索引和值
for index, elem in enumerate(list1):
    print(index, elem)
    
~~~

#### 列表的增删改操作

1. 增：

   - append：在末尾追加元素

   - extend：在末尾添加至少一个元素

   - insert：在列表任意位置插入一个元素

   - 切片

     ~~~py
     lst = [1, 3, 5, 7, 100]
     lst.append(50)
     lst2 = [45,51,65]
     lst.extend(lst2) [1, 3, 5, 7, 100,45,51,65]
     lst.append(lst2) #  [1, 3, 5, 7, 100,[45,51,65]]
     ~~~

     

2. 删

   - remove()：删除一个元素，重复删除第一个元素
   - pop()：根据索引移除元素，不指定索引，则删除最后一个元素
   - clear() :清空列表的元素

   ~~~py
   list1 = [1, 3, 5, 7, 100]
   # 先通过成员运算判断元素是否在列表中，如果存在就删除该元素
   if 3 in list1:
   	list1.remove(3)
   if 1234 in list1:
       list1.remove(1234)
   print(list1) # [1, 400, 5, 7, 100, 200, 1000, 2000]
   # 从指定的位置删除元素
   list1.pop(0)
   list1.pop(len(list1) - 1)
   print(list1) # [400, 5, 7, 100, 200, 1000]
   
   #切片 不产生新对象
   list1[1:3] = []
   print(list1)
   # 清空列表元素
   list1.clear()
   
   # 删除列表
   del list1
   ~~~

   

3. 改

   - 指定索引修改元素

   ~~~py
   list1 = [1, 3, 5, 7, 100]
   list1[1] = 55
   print(list1)
   ~~~

   

4. 排序

   - 调用sort(),降序reverse  = True  ，升序则是False

   - 调用内置函数sorted()函数，会产生一个新的列表对象

     ~~~py
     list1 = [1, 7,3, 100,5,45]
     desc_lst = sorted(list1,reverse = True) # 降序
     print(list1)
     
     list1 = ['orange', 'apple', 'zoo', 'internationalization', 'blueberry']
     list2 = sorted(list1)
     # sorted函数返回列表排序后的拷贝不会修改传入的列表
     # 函数的设计就应该像sorted函数一样尽可能不产生副作用
     list3 = sorted(list1, reverse=True)
     # 通过key关键字参数指定根据字符串长度进行排序而不是默认的字母表顺序
     list4 = sorted(list1, key=len)
     print(list1)
     print(list2)
     print(list3)
     print(list4)
     # 给列表对象发出排序消息直接在列表对象上进行排序
     list1.sort(reverse=True)
     print(list1)
     ~~~

     

#### 列表生成式

- 必须具有一定的规则

~~~py
lst = [ i for i in range(1,11)]
print(lst)  #[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

lst1 = [ i*i for i in range(1,11)]
print(lst1) # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

lst12= [ i*2 for i in range(1,6)]
print(lst12) #[2, 4, 6, 8, 10]
~~~

- for 前面的 i * i 是：列表元素的表达式

## 元组 tuple ( ) 

- 元素不可以修改
- 没有对元素的添加、删除、修改操作，当然如果一个方法要返回多个值，使用元组也是不错的选择。
- 元组在创建时间和占用的空间上面都优于列表



#### 创建元组

- 直接小括号
- 使用内置函数tuple()
- 一个元组的元素要使用逗号隔开

~~~py
# 定义元组
t = ('小明', 48, True, '广西')
print(t)
#内置函数创建元组
t = tuple(('apple', 'banana', 'orange'))
print(t)

t1 = tuple("pity",) # 必须加上逗号和小括号

# 获取元组中的元素
print(t[0])
print(t[3])

# 遍历元组中的值
for member in t:
    print(member)
    
# 重新给元组赋值
# t[0] = '王大锤'  # TypeError
# 变量t重新引用了新的元组原来的元组将被垃圾回收

t = ('王大锤', 20, True, '云南昆明')
print(t)

# 将元组转换成列表
person = list(t)
print(person)

# 列表是可以修改它的元素的
person[0] = '李小龙'
person[1] = 25
print(person)
~~~



## 集合 { } set( )

- 可变序列
- 不存在重复元素
- 无序的

创建集合

1. 使用{}
2. 使用内置函数 set()

```py
# 创建集合的字面量语法
set1 = {1, 2, 3, 3, 3, 2}
print(set1)  #{1, 2, 3}
print('Length =', len(set1))  #Length = 3
# 创建集合的构造器语法
set2 = set(range(1, 10))   # 1~9 的数
set3 = set((1, 2, 3, 3, 2, 1)) 
print(set2, set3) #{1, 2, 3, 4, 5, 6, 7, 8, 9} {1, 2, 3}
# 创建集合的推导式语法(推导式也可以用于推导集合)
set4 = {num for num in range(1, 100) if num % 3 == 0 or num % 5 == 0}
print(set4) 
#空集合
s = set()
print(s)
```

集合的操作

1. in \ not in：判断集合操作
2. 新增操作
   - add()：添加一个元素
   - update()：至少添加一个元素
3. 删除
   - remove()：删除一个指定元素，不存在抛出异常
   - discard()：删除指定元素
   - pop()：删除任意一个元素
   - clrear()：清空集合

```Python
set1 = {1, 2, 3, 3, 3, 2}

# 判断
print(10 in set1)
print(10 not in set1)
#新增
set1.add(4)
set1.add(50)
set2.update([11, 12])
set2.update((12,45,55))
#删除
set2.discard(5)
if 4 in set2:
    set2.remove(4)
print(set1, set2)
print(set3.pop()) # pop 没有参数的，每次删除最后一个元素
print(set3)
```

集合的运算

- 成员
- 交集
- 并集
- 差集

```Python
set1 = {1, 2, 3, 3, 3, 2}
set2 = set(range(1, 10))  
set3 = set((1, 2, 3, 3, 2, 1)) 

# 交集
print(set1 & set2)
# print(set1.intersection(set2))

#并集
print(set1 | set2)
# print(set1.union(set2))
#差集
print(set1 - set2)
# print(set1.difference(set2))
#对称差运
print(set1 ^ set2)
# print(set1.symmetric_difference(set2))

# 子集
print(set2 <= set1)
# print(set2.issubset(set1))
print(set3 <= set1)
# print(set3.issubset(set1))

# 超集
print(set1 >= set2)
# print(set1.issuperset(set2))
print(set1 >= set3)
# print(set1.issuperset(set3))
```

#### 集合生成式

~~~py
s1 = { i for i in range(1,11)}

s2 = { i*i for i in range(1,11)}

s3 = { i *2 fro in range(4)}  # 生成1~4的平方
print(s3)
~~~



## 字典 { } dict( )

特点：

- 键不可以重复，值可以重复
- 无序
-  key必须是不可变对象

- 可变容器模型
- 字典的每个元素都是由一个键和一个值组成的==键值对==，键和值通过冒号分开
- 使用内置函数dict()

```py
# 创建字典的字面量语法
scores = {'小明': 15, '小张': 17, '小李': 12}
print(scores)
d = dict(name = 'jack',age = 18)
print(d)
# 创建字典的构造器语法
items1 = dict(one=1, two=2, three=3, four=4)

# 通过zip函数将两个序列压成字典
items2 = dict(zip(['a', 'b', 'c'], '123'))

# 创建字典的推导式语法
items3 = {num: num ** 2 for num in range(1, 10)}#前一个num表示增量 后一个则是增量的平方
print(items1, items2, items3)

# 通过键可以获取字典中对应的值
print(scores['小明'])
print(scores['小李'])  
print(scores['小三'])  #KeyError  找不到报错
# get方法也是通过键获取对应的值但是可以设置默认值
print(scores.get('小明'))
print(scores.get('小三')) # None 找不到显示none

# 对字典中所有键值对进行遍历
for key in scores:
    print(f'{key}: {scores[key]}')
    
for item in scores:
    print(itmes.scores)    
    
# 添加字典中的元素
scores['诸葛王朗'] = 71
#修改
scores['小张'] = 65
scores.update('冷面'=67, '方启鹤'=85)
print(scores)

# 使用in \ not in 判断键是否在字典当中
if '小张' in scores:
    print(scores['小张'])
print(scores.get('小张'))

# 删除字典中的元素  从最后一个开始删除
print(scores.popitem())
print(scores.popitem())
print(scores.pop('小明', 100))

# 清空字典
scores.clear()
print(scores)
```

#### 获取字典视图

- keys() ：获取字典中所有的key
- values()：获取字典中所有的value
- items()：获取字典中的所有键值对

~~~py
scores = {'小明': 15, '小张': 17, '小李': 12}
#获取键
keys=scores.keys()
print(list(keys))
#获取值
values=scores.values()
print(list(values))
#获取键值对
items=scores.items()
print(list(items))
~~~

#### 字典生成式

- 内置函数zip()

  可迭代的对象作为参数，将对象中对应的元素打包成一个元组，然后返回有这些元组组成的lie'b

### 总结：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710100955074.png" alt="image-20220710100955074" style="zoom:80%;" />



## 练习

#### 练习1：在屏幕上显示跑马灯文字

```Python
import os
import time

def main():
    content = '北京欢迎你为你开天辟地…………'
    while True:
        # 清理屏幕上的输出
        os.system('cls')  # os.system('clear')
        print(content)
        # 休眠200毫秒
        time.sleep(0.2)
        content = content[1:] + content[0]

if __name__ == '__main__':
    main()
```

#### 练习2：设计一个函数产生指定长度的验证码，验证码由大小写字母和数字构成。

参考答案：

```Python
import random


def generate_code(code_len=4):
    """
    生成指定长度的验证码

    :param code_len: 验证码的长度(默认4个字符)

    :return: 由大小写英文字母和数字构成的随机验证码
    """
    all_chars = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
    last_pos = len(all_chars) - 1
    code = ''
    for _ in range(code_len):
        index = random.randint(0, last_pos)
        code += all_chars[index]
    return code
```

#### 练习3：设计一个函数返回给定文件名的后缀名。

参考答案：

```Python
def get_suffix(filename, has_dot=False):
    """
    获取文件名的后缀名

    :param filename: 文件名
    :param has_dot: 返回的后缀名是否需要带点
    :return: 文件的后缀名
    """
    pos = filename.rfind('.')
    if 0 < pos < len(filename) - 1:
        index = pos if has_dot else pos + 1
        return filename[index:]
    else:
        return ''
```

#### 练习4：设计一个函数返回传入的列表中最大和第二大的元素的值。

参考答案：

```Python
def max2(x):
    m1, m2 = (x[0], x[1]) if x[0] > x[1] else (x[1], x[0])
    for index in range(2, len(x)):
        if x[index] > m1:
            m2 = m1
            m1 = x[index]
        elif x[index] > m2:
            m2 = x[index]
    return m1, m2
```

#### 练习5：计算指定的年月日是这一年的第几天。

参考答案：

```Python
def is_leap_year(year):
    """
    判断指定的年份是不是闰年

    :param year: 年份
    :return: 闰年返回True平年返回False
    """
    return year % 4 == 0 and year % 100 != 0 or year % 400 == 0


def which_day(year, month, date):
    """
    计算传入的日期是这一年的第几天

    :param year: 年
    :param month: 月
    :param date: 日
    :return: 第几天
    """
    days_of_month = [
        [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31],
        [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    ][is_leap_year(year)]
    total = 0
    for index in range(month - 1):
        total += days_of_month[index]
    return total + date


def main():
    print(which_day(1980, 11, 28))
    print(which_day(1981, 12, 31))
    print(which_day(2018, 1, 1))
    print(which_day(2016, 3, 1))


if __name__ == '__main__':
    main()
```

#### 练习6：打印[杨辉三角](https://zh.wikipedia.org/wiki/%E6%9D%A8%E8%BE%89%E4%B8%89%E8%A7%92%E5%BD%A2)。

参考答案：

```Python
def main():
    num = int(input('Number of rows: '))
    yh = [[]] * num
    for row in range(len(yh)):
        yh[row] = [None] * (row + 1)
        for col in range(len(yh[row])):
            if col == 0 or col == row:
                yh[row][col] = 1
            else:
                yh[row][col] = yh[row - 1][col] + yh[row - 1][col - 1]
            print(yh[row][col], end='\t')
        print()


if __name__ == '__main__':
    main()
```

## 综合案例

#### 案例1：双色球选号。

```Python
from random import randrange, randint, sample


def display(balls):
    """
    输出列表中的双色球号码
    """
    for index, ball in enumerate(balls):
        if index == len(balls) - 1:
            print('|', end=' ')
        print('%02d' % ball, end=' ')
    print()


def random_select():
    """
    随机选择一组号码
    """
    red_balls = [x for x in range(1, 34)]
    selected_balls = []
    selected_balls = sample(red_balls, 6)
    selected_balls.sort()
    selected_balls.append(randint(1, 16))
    return selected_balls


def main():
    n = int(input('机选几注: '))
    for _ in range(n):
        display(random_select())


if __name__ == '__main__':
    main()
```

> **说明：** 上面使用random模块的sample函数来实现从列表中选择不重复的n个元素。

#### 综合案例2：[约瑟夫环问题](https://zh.wikipedia.org/wiki/%E7%BA%A6%E7%91%9F%E5%A4%AB%E6%96%AF%E9%97%AE%E9%A2%98)。

```Python
"""
《幸运的基督徒》
有15个基督徒和15个非基督徒在海上遇险，为了能让一部分人活下来不得不将其中15个人扔到海里面去，有个人想了个办法就是大家围成一个圈，由某个人开始从1报数，报到9的人就扔到海里面，他后面的人接着从1开始报数，报到9的人继续扔到海里面，直到扔掉15个人。由于上帝的保佑，15个基督徒都幸免于难，问这些人最开始是怎么站的，哪些位置是基督徒哪些位置是非基督徒。
"""


def main():
    persons = [True] * 30
    counter, index, number = 0, 0, 0
    while counter < 15:
        if persons[index]:
            number += 1
            if number == 9:
                persons[index] = False
                counter += 1
                number = 0
        index += 1
        index %= 30
    for person in persons:
        print('基' if person else '非', end='')


if __name__ == '__main__':
    main()

```

#### 综合案例3：[井字棋](https://zh.wikipedia.org/wiki/%E4%BA%95%E5%AD%97%E6%A3%8B)游戏。

```Python
import os


def print_board(board):
    print(board['TL'] + '|' + board['TM'] + '|' + board['TR'])
    print('-+-+-')
    print(board['ML'] + '|' + board['MM'] + '|' + board['MR'])
    print('-+-+-')
    print(board['BL'] + '|' + board['BM'] + '|' + board['BR'])


def main():
    init_board = {
        'TL': ' ', 'TM': ' ', 'TR': ' ',
        'ML': ' ', 'MM': ' ', 'MR': ' ',
        'BL': ' ', 'BM': ' ', 'BR': ' '
    }
    begin = True
    while begin:
        curr_board = init_board.copy()
        begin = False
        turn = 'x'
        counter = 0
        os.system('clear')
        print_board(curr_board)
        while counter < 9:
            move = input('轮到%s走棋, 请输入位置: ' % turn)
            if curr_board[move] == ' ':
                counter += 1
                curr_board[move] = turn
                if turn == 'x':
                    turn = 'o'
                else:
                    turn = 'x'
            os.system('clear')
            print_board(curr_board)
        choice = input('再玩一局?(yes|no)')
        begin = choice == 'yes'


if __name__ == '__main__':
    main()
```



## 2.11异常

### 1 try except

~~~py
try: 
	····(可能会出现异常的代码)
except: 
    ·····(异常处理)
~~~

~~~python
try:
    a = int(input("输入被除数："))
    b = int(input("输入除数："))
    c = a / b
    print('结果:%0.2d' %c)
except Exception:
    print("除数不可以为0")
print('程序结束')   
~~~



#### 多个except结构

- 捕获异常顺序按照先子类后父类的顺序  BaseException是最大的异常处理



### 2 try except else结构

> 如果try 中没有抛出异常，则执行else块，try抛出异常则执行except块

```py
try:
    a = int(input("输入被除数："))
    b = int(input("输入除数："))
    c = a / b
except BaseException as e:
    print("除数不可以为",e)
else:
    print('结果:%0.2d' % c)
```

### 3 try except else finally结构

> finally 无论是否发生异常都会执行，用作释放try申请的资源



~~~py
try:
    a = int(input("输入被除数："))
    b = int(input("输入除数："))
    c = a / b
except BaseException as e:
    print("除数不可以为",e)
else:
    print('结果:%0.2d' % c)
finally:
    print('照样执行finally！！')
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710123240197.png" alt="image-20220710123240197" style="zoom:80%;" />

### 异常处理模块

Traceback ：打印异常信息





# 3 面向对象

## 3.1 类和对象

- 类是抽象的概念，而对象是具体的东西
- 对象都有属性和行为

### 3.1.1 类

- class 定义类
- 类属性 ：类里面的变量
- 实例方法：类里面的方法
- 静态方法：@staticmethod 注释的   ==使用类名直接访问==
- 类方法：@classmethod 注释的  ==使用类名直接访问==
- 内置方法：

  - 初始化方法  `__init__ ` 方法，是对象的内置方法。
  - `__del__` : 对象被从内存中销毁前，会被自动调用
  - `__str__` : 返回对象的描述信息，print函数输出使用  ，==必须返回一个字符串==

```py
class Student(object):
    native = 广西
    def __init__(self,name,age):
        self.name = name   # 实体属性
        self.age = age
    def study(self,course_name):
        print('%s正在学习%s'%(self.name,course_name))

    def watch_movie(self):
        if self.age <5:
            print('只能看电影')
        else:
            print('随便看')
```



### 3.1.2 对象

- 创建实例对象：实例名 = 类名（）

```py
def main():
    # 创建学生对象并指定姓名和年龄
    stu1 = Student('小米', 18)
    # 给对象发study消息
    stu1.study('Python程序设计')
    
    # 给对象发watch_av消息
    stu1.watch_movie()
    
    stu2 = Student('小张', 15)
    stu2.study('思想品德')
    stu2.watch_movie()

if __name__ == '__main__':
    main()
```



### 3.1.3 访问可见性

> 在Python中，属性和方法的访问权限只有两种，也就是==公开的和私有的==，如果希望属性是==私有的==，在给属性命名时可以用两个==下划线作为开头==

- 以单下划线来限制访问。单下划线开头的属性和方法外界仍然是可以访问的，所以更多的时候它是一种暗示或隐喻



### 3.1.4  面向对象的支柱

1. 封装 ：提高程序的安全性
   - 将==属性和方法封装到一个抽象类==中

   - 创建类对象，对象调用封装里面的方法

   - 对象的方法都封装在类的内部

     ~~~py
     # AUTHOR: Kcs
     # TIME  : 2022/7/10 18:26
     class Student:
         def __init__(self, name, age):
             self.__age = age  # 双下滑线 表示：不希望在类外部被访问到
             self.name = name
     
         def show(self):
             print(self.name, self.__age)
     
     stu = Student('张三', 45)
     
     # print(stu.name,stu.__age)
     print(dir(stu))
     
     # 若是想要被访问到双下滑线的信息
     print(stu._Student__age)
     
     ~~~

     

2. 继承：提高代码的复用性

   - Python支持多继承

   - 定义子类时，必须在其构造方法中调用父类的构造函数

     ~~~py
     class A(object):
         pass
     
     
     class B(object):
         pass
     
     
     class C(A, B):
         pass
     ~~~

     ~~~py
     # AUTHOR: Kcs
     # TIME  : 2022/7/10 18:43
     class Person(object):
         def __init__(self, name, age):
             self.name = name
             self.age = age
     
         def info(self):
             print(self.name, self.age)
     
     
     class Student(Person):
         def __init__(self, name, age, sno):
             super(Student, self).__init__(name, age)
             self.sno = sno
     
     
     class Teacher(Person):
         def __init__(self, name, age, prof):
             super(Teacher, self).__init__(name, age)
             self.prof = prof
     ~~~

   - 重写方法

     ~~~py
     class Person(object):  # 不写括号 就默认是继承object类
         def __init__(self, name, age):
             self.name = name
             self.age = age
     
         def info(self):
             print(self.name, self.age)
     
     
     class Student(Person):
         def __init__(self, name, age, sno):
             super(Student, self).__init__(name, age)
             self.sno = sno
     #重写方法
         def info(self):
             print('我是学生,我叫：', self.name, '我的学号是：', self.sno)
     
     
     class Teacher(Person):
         def __init__(self, name, age, prof):
             super(Teacher, self).__init__(name, age)
             self.prof = prof
     #重写方法 
         def info(self):
             print('我是老师,我叫：', self.name, '我的职位是：', self.prof)
     ~~~

     object中的方法：

     ~~~py
     ['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__']
     ~~~

     

3. 多态：提高程序的可扩展性和可维护性

   ~~~py
   # AUTHOR: Kcs
   # TIME  : 2022/7/10 19:40
   
   # 多态
   # 以动物来描述多态
   class Animal(object):
       def eat(self):
           print("动物吃东西。。。")
   
   
   class Dog(Animal):
       def eat(self):
           print("狗吃骨头。。。")
   
   
   class Cat(Animal):
       def eat(self):
           print("猫吃鱼。。。")
   
   
   class Person(object):
       def eat(self):
           print('人吃五谷杂粮。。。')
   
   
   #函数
   def func(obj):
       obj.eat()
   
   
   func(Animal())
   func(Cat())
   func(Dog())
   
   func(Person())
   ~~~

   



### 练习

#### 练习1：定义一个类描述数字时钟。

参考答案：

```Python
import time
import os

class Clock(object):

    # Python中的函数是没有重载的概念的
    # 因为Python中函数的参数没有类型而且支持缺省参数和可变参数
    # 用关键字参数让构造器可以传入任意多个参数来实现其他语言中的构造器重载
    def __init__(self, **kw):
        if 'hour' in kw and 'minute' in kw and 'second' in kw:
            self._hour = kw['hour']
            self._minute = kw['minute']
            self._second = kw['second']
        else:
            tm = time.localtime(time.time())
            self._hour = tm.tm_hour
            self._minute = tm.tm_min
            self._second = tm.tm_sec

    def run(self):
        self._second += 1
        if self._second == 60:
            self._second = 0
            self._minute += 1
            if self._minute == 60:
                self._minute = 0
                self._hour += 1
                if self._hour == 24:
                    self._hour = 0

    def show(self):
        return '%02d:%02d:%02d' % (self._hour, self._minute, self._second)


if __name__ == '__main__':
    # clock = Clock(hour=10, minute=5, second=58)
    clock = Clock()
    while True:
        os.system('clear')
        print(clock.show())
        time.sleep(1)
        clock.run()
```

#### 练习2：定义一个类描述平面上的点并提供移动点和计算到另一个点距离的方法。

参考答案：

```Python
from math import sqrt


class Point(object):

    def __init__(self, x=0, y=0):
        """初始化方法
        
        :param x: 横坐标
        :param y: 纵坐标
        """
        self.x = x
        self.y = y

    def move_to(self, x, y):
        """移动到指定位置
        
        :param x: 新的横坐标
        "param y: 新的纵坐标
        """
        self.x = x
        self.y = y

    def move_by(self, dx, dy):
        """移动指定的增量
        
        :param dx: 横坐标的增量
        "param dy: 纵坐标的增量
        """
        self.x += dx
        self.y += dy

    def distance_to(self, other):
        """计算与另一个点的距离
        
        :param other: 另一个点
        """
        dx = self.x - other.x
        dy = self.y - other.y
        return sqrt(dx ** 2 + dy ** 2)

    def __str__(self):
        return '(%s, %s)' % (str(self.x), str(self.y))


def main():
    p1 = Point(3, 5)  # 目标的坐标
    p2 = Point()
    print(p1)
    print(p2)
    p2.move_by(-1, 2)  
    print(p2)
    print(p1.distance_to(p2))


if __name__ == '__main__':
    main()
```



### 特殊方法和特殊属性

 <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710195402287.png" alt="image-20220710195402287" style="zoom:80%;" />

`__new__`  `__init__`

![image-20220710201027344](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710201027344.png)



### 3.1.5 类的拷贝

变量的赋值操作：

- 两个变量指向同一个对象

#### 1 类的先拷贝

- 一般是浅拷贝
- 拷贝时，对象包含的子对象内容不拷贝，so，源对象与拷贝对象会引用同一个子对象

#### 2 类的深拷贝

- 使用copy模块的deepcopy函数，递归拷贝对象中包含的子对象，源对象和拷贝对象所有的子对象也不相同

~~~py
# AUTHOR: Kcs
# TIME  : 2022/7/10 20:14

class Cpu:
    pass


class Disk:
    pass


class Computer:
    def __init__(self, cpu, disk):
        self.cpu = cpu
        self.disk = disk


# (1) 变量的赋值
cpu1 = Cpu()

cpu2 = cpu1

# print(cpu1 is cpu2)  # True
print(cpu1, id(cpu1))
print(cpu2, id(cpu2))

# (2)类的浅拷贝
disk = Disk()

computer = Computer(cpu1, disk)
# 浅拷贝

import copy

computer2 = copy.copy(computer)
print(computer, computer.cpu, computer.disk)
print(computer2, computer2.cpu, computer2.disk)
#  <__main__.Computer object at 0x0000022F2738FE80> <__main__.Cpu object at 0x0000022F2738FFD0> <__main__.Disk object at 0x0000022F2738FEB0>
#  <__main__.Computer object at 0x0000022F2738FDC0> <__main__.Cpu object at 0x0000022F2738FFD0> <__main__.Disk object at 0x0000022F2738FEB0>

# (3)类的深拷贝
computer3 = copy.deepcopy(computer)
print(computer, computer.cpu, computer.disk)
print(computer3, computer3.cpu, computer3.disk)

# <__main__.Computer object at 0x000001E49664FE80> <__main__.Cpu object at 0x000001E49664FFD0> <__main__.Disk object at 0x000001E49664FEB0>
# <__main__.Computer object at 0x000001E49664F9D0> <__main__.Cpu object at 0x000001E49664DC90> <__main__.Disk object at 0x000001E49664DBD0>
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710205204695.png" alt="image-20220710205204695" style="zoom: 80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220710205239420.png" alt="image-20220710205239420" style="zoom: 80%;" />





## 3.2  面向对象进阶

### 3.2.1 @property装饰器

> 访问属性可以通过属性的getter（访问器）和setter（修改器）方法进行对应的操作
>
> 对属性的访问既安全又方便

~~~py
class Person(object):

    def __init__(self, name, age):
        self._name = name
        self._age = age

    # 访问器 - getter方法
    @property
    def name(self):
        return self._name

    # 访问器 - getter方法
    @property
    def age(self):
        return self._age

    # 修改器 - setter方法
    @age.setter
    def age(self, age):
        self._age = age

    def play(self):
        if self._age <= 16:
            print('%s正在玩飞行棋.' % self._name)
        else:
            print('%s正在玩斗地主.' % self._name)


def main():
    person = Person('王大锤', 12)
    person.play()
    person.age = 22
    person.play()
    # person.name = '白元芳'  # AttributeError: can't set attribute


if __name__ == '__main__':
    main()
~~~

### \_\_slots\_\_魔法

- 限定自定义类型的对象只能绑定某些属性
- 只对当前类的对象生效，对子类并不起任何作用

class Person(object):

```py
class Person(object):
    # 限定Person对象只能绑定_name, _age和_gender属性
    __slots__ = ('_name', '_age', '_gender')

    def __init__(self, name, age):
        self._name = name
        self._age = age

    @property
    def name(self):
        return self._name

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, age):
        self._age = age
```





# 4 文件



## 4.1 编码格式

- Python的解释器使用Unicode
- py文件使用UTF-8存储

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711153447502.png" alt="image-20220711153447502" style="zoom:80%;" />

在文件的开头修改编码格式

#encoding = 编码格式 



## 4.2 文件读写原理 （IO操作）

原理：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711165728749.png" alt="image-20220711165728749" style="zoom:80%;" />





### 4.2.1 读写操作

内置函数open() 创建文件对象

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711170007749.png" alt="image-20220711170007749" style="zoom:80%;" />



语法规则：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711170026806.png" alt="image-20220711170026806" style="zoom:80%;" />

```py
# 创建文件对象
file = open('text1.txt', 'r', encoding='UTF-8')
# 输出文件内容
print(file.readline())
# 关闭文件流
file.close()
```

打开文件模式

| 模式 | 描述                                                         |
| :--: | :----------------------------------------------------------- |
|  t   | 文本模式 (默认)。                                            |
|  x   | 写模式，新建一个文件，如果该文件已存在则会报错。             |
|  b   | 二进制模式。                                                 |
|  +   | 打开一个文件进行更新(可读可写)。                             |
|  U   | 通用换行模式（不推荐）。                                     |
|  r   | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
|  rb  | 以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。 |
|  r+  | 打开一个文件用于读写。文件指针将会放在文件的开头。           |
| rb+  | 以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。 |
|  w   | 打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
|  wb  | 以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
|  w+  | 打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。 |
| wb+  | 以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。 |
|  a   | 打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
|  ab  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。 |
|  a+  | 打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。 |
| ab+  | 以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。 |

```py
# 创建文件对象
file = open('text2.txt', 'a', encoding='UTF-8')
# 输出文件内容
file.write('加入字符串\n')
# 关闭文件流
file.close()
```

复制文件：

```py
# 创建文件对象
source_file = open('text2.txt', 'rb')
# 输出文件内容
target_file= open('copy1.txt','wb')
# 关闭文件流

# 一边读一边写
target_file.write(source_file.read())

source_file.close()

target_file.close()
```

文件当中的常用方法：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711171935950.png" alt="image-20220711171935950" style="zoom:80%;" />

| 序号 | 方法及描述                                                   |
| :--: | :----------------------------------------------------------- |
|  1   | [file.close()](https://www.runoob.com/python/file-close.html)<br />关闭文件。关闭后文件不能再进行读写操作。 |
|  2   | [file.flush()](https://www.runoob.com/python/file-flush.html)<br />刷新文件内部缓冲，直接把内部缓冲区的数据立刻写入文件, 而不是被动的等待输出缓冲区写入。 |
|  3   | [file.fileno()](https://www.runoob.com/python/file-fileno.html)<br />返回一个整型的文件描述符(file descriptor FD 整型), 可以用在如os模块的read方法等一些底层操作上。 |
|  4   | [file.isatty()](https://www.runoob.com/python/file-isatty.html)<br />如果文件连接到一个终端设备返回 True，否则返回 False。 |
|  5   | [file.next()](https://www.runoob.com/python/file-next.html)返回文件下一行。 |
|  6   | [file.read([size\])](https://www.runoob.com/python/python-file-read.html)<br />从文件读取指定的字节数，如果未给定或为负则读取所有。 |
|  7   | [file.readline([size\])](https://www.runoob.com/python/file-readline.html)<br />读取整行，包括 "\n" 字符。 |
|  8   | [file.readlines([sizeint\])](https://www.runoob.com/python/file-readlines.html)<br />读取所有行并返回列表，若给定sizeint>0，则是设置一次读多少字节，这是为了减轻读取压力。 |
|  9   | [file.seek(offset[, whence\])](https://www.runoob.com/python/file-seek.html)<br />设置文件当前位置 |
|  10  | [file.tell()](https://www.runoob.com/python/file-tell.html)<br />返回文件当前位置。 |
|  11  | [file.truncate([size\])](https://www.runoob.com/python/file-truncate.html)<br />截取文件，截取的字节通过size指定，默认为当前文件位置。 |
|  12  | [file.write(str)](https://www.runoob.com/python/python-file-write.html)<br />将字符串写入文件，返回的是写入的字符长度。 |
|  13  | [file.writelines(sequence)](https://www.runoob.com/python/file-writelines.html)<br />向文件写入一个序列字符串列表，如果需要换行则要自己加入每行的换行符。**** |

#### with 语句 （上下文管理器）

- 会自动关闭文件流对象

> with可以自动管理上下文资源，不论什么原因跳出with块，都能确保问价能正确的关闭，以此来达到释放资源的目的

**语法**：

![image-20220711173638666](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711173638666.png)



```py
# AUTHOR: Kcs
# TIME  : 2022/7/11 17:34

"""
MyContentMar 实现了__enter__ ，__exit__该类对象遵守了上下文管理器协议
该类的实例对象，就是上下文管理对象
"""


class MyContentMar(object):
    # 进入时调用
    def __enter__(self):
        print('__enter__被调用了')
        return self

    # 退出时调用
    def __exit__(self, exc_type, exc_val, exc_tb):
        print('__exit()__方法被调用了')

    # 实例对象调用的方法
    def show(self):
        print('show方法被调用了')


# 创建上下文管理利器实例对象
with MyContentMar() as mc:
    print(mc.show())
```

```py
"""
with copy file
"""
with open('text1.txt', 'rb') as source_file:
    with open('copywith.txt', 'wb') as target_file:
        target_file.write(source_file.read())
```



### 目录

- mkdir()方法：创建目录，参数为：目录名称
- chdir()方法：改变目录，参数：设定的目录结构
- rmdir()方法：删除目录，删除目录之前会先删除内容



### OS文件/ 目录方法

| 序号 | 方法及描述                                                   |
| :--: | :----------------------------------------------------------- |
|  1   | [os.access(path, mode)](https://www.runoob.com/python/os-access.html) 检验权限模式 |
|  2   | [os.chdir(path)](https://www.runoob.com/python/os-chdir.html) 改变当前工作目录 |
|  3   | [os.chflags(path, flags)](https://www.runoob.com/python/os-chflags.html) 设置路径的标记为数字标记。 |
|  4   | [os.chmod(path, mode)](https://www.runoob.com/python/os-chmod.html) 更改权限 |
|  5   | [os.chown(path, uid, gid)](https://www.runoob.com/python/os-chown.html) 更改文件所有者 |
|  6   | [os.chroot(path)](https://www.runoob.com/python/os-chroot.html) 改变当前进程的根目录 |
|  7   | [os.close(fd)](https://www.runoob.com/python/os-close.html) 关闭文件描述符 fd |
|  8   | [os.closerange(fd_low, fd_high)](https://www.runoob.com/python/os-closerange.html) 关闭所有文件描述符，从 fd_low (包含) 到 fd_high (不包含), 错误会忽略 |
|  9   | [os.dup(fd)](https://www.runoob.com/python/os-dup.html) 复制文件描述符 fd |
|  10  | [os.dup2(fd, fd2)](https://www.runoob.com/python/os-dup2.html) 将一个文件描述符 fd 复制到另一个 fd2 |
|  11  | [os.fchdir(fd)](https://www.runoob.com/python/os-fchdir.html) 通过文件描述符改变当前工作目录 |
|  12  | [os.fchmod(fd, mode)](https://www.runoob.com/python/os-fchmod.html) 改变一个文件的访问权限，该文件由参数fd指定，参数mode是Unix下的文件访问权限。 |
|  13  | [os.fchown(fd, uid, gid)](https://www.runoob.com/python/os-fchown.html) 修改一个文件的所有权，这个函数修改一个文件的用户ID和用户组ID，该文件由文件描述符fd指定。 |
|  14  | [os.fdatasync(fd)](https://www.runoob.com/python/os-fdatasync.html) 强制将文件写入磁盘，该文件由文件描述符fd指定，但是不强制更新文件的状态信息。 |
|  15  | [os.fdopen(fd[, mode[, bufsize\]])](https://www.runoob.com/python/os-fdopen.html) 通过文件描述符 fd 创建一个文件对象，并返回这个文件对象 |
|  16  | [os.fpathconf(fd, name)](https://www.runoob.com/python/os-fpathconf.html) 返回一个打开的文件的系统配置信息。name为检索的系统配置的值，它也许是一个定义系统值的字符串，这些名字在很多标准中指定（POSIX.1, Unix 95, Unix 98, 和其它）。 |
|  17  | [os.fstat(fd)](https://www.runoob.com/python/os-fstat.html) 返回文件描述符fd的状态，像stat()。 |
|  18  | [os.fstatvfs(fd)](https://www.runoob.com/python/os-fstatvfs.html) 返回包含文件描述符fd的文件的文件系统的信息，像 statvfs() |
|  19  | [os.fsync(fd)](https://www.runoob.com/python/os-fsync.html) 强制将文件描述符为fd的文件写入硬盘。 |
|  20  | [os.ftruncate(fd, length)](https://www.runoob.com/python/os-ftruncate.html) 裁剪文件描述符fd对应的文件, 所以它最大不能超过文件大小。 |
|  21  | [os.getcwd()](https://www.runoob.com/python/os-getcwd.html) **返回当前工作目录** |
|  22  | [os.getcwdu()](https://www.runoob.com/python/os-getcwdu.html) 返回一个当前工作目录的Unicode对象 |
|  23  | [os.isatty(fd)](https://www.runoob.com/python/os-isatty.html) 如果文件描述符fd是打开的，同时与tty(-like)设备相连，则返回true, 否则False。 |
|  24  | [os.lchflags(path, flags)](https://www.runoob.com/python/os-lchflags.html) 设置路径的标记为数字标记，类似 chflags()，但是没有软链接 |
|  25  | [os.lchmod(path, mode)](https://www.runoob.com/python/os-lchmod.html) 修改连接文件权限 |
|  26  | [os.lchown(path, uid, gid)](https://www.runoob.com/python/os-lchown.html) 更改文件所有者，类似 chown，但是不追踪链接。 |
|  27  | [os.link(src, dst)](https://www.runoob.com/python/os-link.html) 创建硬链接，名为参数 dst，指向参数 src |
|  28  | [os.listdir(path)](https://www.runoob.com/python/os-listdir.html) 返回path指定的文件夹包含的文件或文件夹的名字的列表。 |
|  29  | [os.lseek(fd, pos, how)](https://www.runoob.com/python/os-lseek.html) 设置文件描述符 fd当前位置为pos, how方式修改: SEEK_SET 或者 0 设置从文件开始的计算的pos; SEEK_CUR或者 1 则从当前位置计算; os.SEEK_END或者2则从文件尾部开始. 在unix，Windows中有效 |
|  30  | [os.lstat(path)](https://www.runoob.com/python/os-lstat.html) 像stat(),但是没有软链接 |
|  31  | [os.major(device)](https://www.runoob.com/python/os-major.html) 从原始的设备号中提取设备major号码 (使用stat中的st_dev或者st_rdev field)。 |
|  32  | [os.makedev(major, minor)](https://www.runoob.com/python/os-makedev.html) 以major和minor设备号组成一个原始设备号 |
|  33  | [os.makedirs(path[, mode\])](https://www.runoob.com/python/os-makedirs.html) 递归文件夹创建函数。像mkdir(), 但创建的所有intermediate-level文件夹需要包含子文件夹。 |
|  34  | [os.minor(device)](https://www.runoob.com/python/os-minor.html) 从原始的设备号中提取设备minor号码 (使用stat中的st_dev或者st_rdev field )。 |
|  35  | [os.mkdir(path[, mode\])](https://www.runoob.com/python/os-mkdir.html) 以数字mode的mode创建一个名为path的文件夹.默认的 mode 是 0777 (八进制)。 |
|  36  | [os.mkfifo(path[, mode\])](https://www.runoob.com/python/os-mkfifo.html) 创建命名管道，mode 为数字，默认为 0666 (八进制) |
|  37  | [os.mknod(filename[, mode=0600, device\])](https://www.runoob.com/python/os-mknod.html) 创建一个名为filename文件系统节点（文件，设备特别文件或者命名pipe）。 |
|  38  | [os.open(file, flags[, mode\])](https://www.runoob.com/python/os-open.html) 打开一个文件，并且设置需要的打开选项，mode参数是可选的 |
|  39  | [os.openpty()](https://www.runoob.com/python/os-openpty.html) 打开一个新的伪终端对。返回 pty 和 tty的文件描述符。 |
|  40  | [os.pathconf(path, name)](https://www.runoob.com/python/os-pathconf.html) 返回相关文件的系统配置信息。 |
|  41  | [os.pipe()](https://www.runoob.com/python/os-pipe.html) 创建一个管道. 返回一对文件描述符(r, w) 分别为读和写 |
|  42  | [os.popen(command[, mode[, bufsize\]])](https://www.runoob.com/python/os-popen.html) 从一个 command 打开一个管道 |
|  43  | [os.read(fd, n)](https://www.runoob.com/python/os-read.html) 从文件描述符 fd 中读取最多 n 个字节，返回包含读取字节的字符串，文件描述符 fd对应文件已达到结尾, 返回一个空字符串。 |
|  44  | [os.readlink(path)](https://www.runoob.com/python/os-readlink.html) 返回软链接所指向的文件 |
|  45  | [os.remove(path)](https://www.runoob.com/python/os-remove.html) 删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。 |
|  46  | [os.removedirs(path)](https://www.runoob.com/python/os-removedirs.html) 递归删除目录。 |
|  47  | [os.rename(src, dst)](https://www.runoob.com/python/os-rename.html) 重命名文件或目录，从 src 到 dst |
|  48  | [os.renames(old, new)](https://www.runoob.com/python/os-renames.html) 递归地对目录进行更名，也可以对文件进行更名。 |
|  49  | [os.rmdir(path)](https://www.runoob.com/python/os-rmdir.html) 删除path指定的空目录，如果目录非空，则抛出一个OSError异常。 |
|  50  | [os.stat(path)](https://www.runoob.com/python/os-stat.html) 获取path指定的路径的信息，功能等同于C API中的stat()系统调用。 |
|  51  | [os.stat_float_times([newvalue\])](https://www.runoob.com/python/os-stat_float_times.html) 决定stat_result是否以float对象显示时间戳 |
|  52  | [os.statvfs(path)](https://www.runoob.com/python/os-statvfs.html) 获取指定路径的文件系统统计信息 |
|  53  | [os.symlink(src, dst)](https://www.runoob.com/python/os-symlink.html) 创建一个软链接 |
|  54  | [os.tcgetpgrp(fd)](https://www.runoob.com/python/os-tcgetpgrp.html) 返回与终端fd（一个由os.open()返回的打开的文件描述符）关联的进程组 |
|  55  | [os.tcsetpgrp(fd, pg)](https://www.runoob.com/python/os-tcsetpgrp.html) 设置与终端fd（一个由os.open()返回的打开的文件描述符）关联的进程组为pg。 |
|  56  | [os.tempnam([dir[, prefix\]])](https://www.runoob.com/python/os-tempnam.html) 返回唯一的路径名用于创建临时文件。 |
|  57  | [os.tmpfile()](https://www.runoob.com/python/os-tmpfile.html) 返回一个打开的模式为(w+b)的文件对象 .这文件对象没有文件夹入口，没有文件描述符，将会自动删除。 |
|  58  | [os.tmpnam()](https://www.runoob.com/python/os-tmpnam.html) 为创建一个临时文件返回一个唯一的路径 |
|  59  | [os.ttyname(fd)](https://www.runoob.com/python/os-ttyname.html) 返回一个字符串，它表示与文件描述符fd 关联的终端设备。如果fd 没有与终端设备关联，则引发一个异常。 |
|  60  | [os.unlink(path)](https://www.runoob.com/python/os-unlink.html) 删除文件路径 |
|  61  | [os.utime(path, times)](https://www.runoob.com/python/os-utime.html) 返回指定的path文件的访问和修改的时间。 |
|  62  | [os.walk(top[, topdown=True[, onerror=None[, followlinks=False\]]])](https://www.runoob.com/python/os-walk.html) 输出在文件夹中的文件名通过在树中游走，向上或者向下。 |
|  63  | [os.write(fd, str)](https://www.runoob.com/python/os-write.html) 写入字符串到文件描述符 fd中. 返回实际写入的字符串长度 |
|  64  | [os.path 模块](https://www.runoob.com/python/python-os-path.html) 获取文件的属性信息。 |

```py
import os

# 打开记事本
os.system('notepad.exe')

# 打开计算器
os.system('calc.exe')

# 直接打开可执行文件
os.startfile('D:\\Other Download\\Typora\\Typora.exe')
```



#### os.path模块操作目录

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220711210235930.png" alt="image-20220711210235930" style="zoom:80%;" />



案例：列入指定目录下的所有py文件

```py
import os

path = os.getcwd()
lst = os.listdir(path)

for filename in lst:
    if filename.endswith('.py'):
        print(filename)
```



案例：遍历指定目录下的所有文件

```py
import os

path = os.getcwd()

lst_file = os.walk(path)

for dirpath, dirname, filename in lst_file:
    print(dirpath)
    print(dirname)
    print(filename)
    print('========================')
    
    
```

```py
import os

path = os.getcwd()

lst_file = os.walk(path)

for dirpath, dirname, filename in lst_file:
    """ print(dirpath)
     print(dirname)
     print(filename)
    print('========================')"""
    for dir in dirpath:
        print(os.path.join(dirpath, dir))

    for file in filename:
        print(os.path.join(dirpath, file))
```



## 4.3 file对象



### 4.3.1 file对象的属性



| 属性           | 描述                                                         |
| :------------- | :----------------------------------------------------------- |
| file.closed    | 返回true如果文件已被关闭，否则返回false。                    |
| file.mode      | 返回被打开文件的访问模式。                                   |
| file.name      | 返回文件的名称。                                             |
| file.softspace | 如果用print输出后，必须跟一个空格符，则返回false。否则返回true。 |



# 学生信息管理系统



## 需求分析：

### 功能：

- 添加学生及成绩信息
- 将学生信息保存到文件中
- 修改和删除学生信息
- 查询学生信息
- 根据学生成绩进行排序
- 统计学生的总分

## 系统设计：

### 系统功能结构：

- 录入学生信息模块
- 查找学生信息模块
- 删除学生信息模块
- 修改学生信息模块
- 学生成绩排名模块
- 统计学生总人数模块
- 显示全部学生信息模块

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712105031352.png" alt="image-20220712105031352" style="zoom:80%;" />

### 系统业务流程：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712105905502.png" alt="image-20220712105905502" style="zoom:80%;" />



## 系统开发必备：

python解释器：python 3.10

开发工具：Pycharm

python内置模块：os，re



## 主函数设计：

效果图：

**![image-20220712114304942](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712114304942.png)**



### 主函数业务流程图：

![image-20220712110331043](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712110331043.png)



### 实现主函数：

| 编号 | 功能                               |
| ---- | ---------------------------------- |
| 0    | 退出系统                           |
| 1    | 录入学生信息,调用insert()函数      |
| 2    | 查找学生信息,调用search()函数      |
| 3    | 删除学生信息,调用delete()函数      |
| 4    | 修改学生信息,调用modifv()函数      |
| 5    | 对学生成绩排序,调用sort()函数      |
| 6    | 统计学生总人数,调用total()函数     |
| 7    | 显示所有的学生信息，调用show()函数 |



## 学生信息维护模块设计 

###  **录入学生信息功能**

- 从控制台录入学生信息，并且把信息保存到磁盘文件中

#### 业务流程：

![image-20220712120119100](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712120119100.png)





#### 具体实现

- save(student)函数,用于将学生信息保存到文件
- insert()函数,用于录入学生信息



### 删除学生信息功能

- 从控制台录入学生id，到磁盘文件中找到对应的学生信息，并将其删除

#### 业务流程

![image-20220712132758567](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712132758567.png)

#### 具体实现

- delete ()函数
- 调用show()函数显示学生信息，



### 修改学生信息功能

- 从控制台录入学生ID，到磁盘文件中找到对应的学生信息，将其进行修改

#### 业务流程

![image-20220712140628421](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712140628421.png)



#### 具体实现



## 查询/统计模块设计

### 查询学生信息功能

- 从控制台录入学生id或姓名，到磁盘文件中找到对应的学生信息

#### 业务流程

![image-20220712154357209](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712154357209.png)



具体实现

- 编写主函数中调用的查找学生信息的函数search()
- 定义显示查询结果的函数show_student(query_student)

### 统计学生人数功能

#### 业务流程

![image-20220712165255675](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712165255675.png)



### 显示所有学生信息功能

#### 业务

![image-20220712165639478](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220712165639478.png)





## 排序模块设计





## 项目打包



















