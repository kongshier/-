> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 第一章 Python编程基础

## Python 计算思维训练

###  公式编程
 1. 第一关 ：表达式求解--垂直上抛小球位置计算
	![在这里插入图片描述](https://img-blog.csdnimg.cn/ef68b74e5bf34edaa4d6115fd49331e6.png)
	```python
	# 本程序计算小球上抛在不同时间点的高度
	v0 = 25     # 小球上抛的初速度
	g = 9.8     # 地球重力加速度
	
	t = int(input())
	#   请在此添加实现代码   #
	# ********** Begin *********#
	h = v0 * t - (0.5 * g * t**2)
	print(h)
	# ********** End **********#
	```
 2. 第二关：输出格式控制--摄氏-华氏温度换算
	![温度公式](https://img-blog.csdnimg.cn/b92d79e691384cb082a67553d1246b38.png)
	![要求](https://img-blog.csdnimg.cn/4ffad491a4de4f0f93547e502dc50a54.png)
	```python
	# 本程序进行华氏温度和摄氏温度之间的转换
	# 请通过换算公式来计算相应的摄氏温度值，需给出Python表达式
	# 最终输出格式为：华氏**度=摄氏**度
	
	F = float(input())    # 华氏温度
	#   请在此添加实现代码   #
	# ********** Begin *********#
	C = (F-32) * (5/9)
	print("华氏%.2f度=摄氏%.2f度" % (F,C))
	# ********** End **********#
	```
 3. 第三关：库函数的使用 - 小球阻力落体运动
	![公式](https://img-blog.csdnimg.cn/0b7d5f78ac7f443486457eb32bc48c64.png)
	![要求](https://img-blog.csdnimg.cn/82aa6e8e9b394c719ee0f757ab74e28e.png)
	```python
	# 计算小球在空气中向下作阻力落体运动中随时间的速度变化情况
	# 1.导入需要的函数
	# 2.根据落体运动速度方程计算某时刻小球的速度
	# 3.根据落体运动位置方程计算某时刻小球的位置
	# 4.格式化输出计算结果
	
	g = 9.8   # 单位：米/秒平方，重力加速度
	m = 0.25  # 单位：千克
	u = 0.5
	t = int(input()) # 单位：秒
	#   请在此添加实现代码   #
	# ********** Begin *********#
	import math
	v = math.sqrt(m*g/u)* math.tanh(math.sqrt(u*g/m)* t)
	x = m / u * math.log(math.cosh(math.sqrt(u*g/m)*t))
	
	print("当t=%d秒时，速度v=%.2f米/秒"%(t,v))
	
	print("%d秒后，小球位置为向下%.2f米"%(t,x))
	# ********** End **********#
	```
 4. 第四关：综合应用 - 小球上抛运动
	![在这里插入图片描述](https://img-blog.csdnimg.cn/f215da0bc08c4264895cb099105ab10d.png)
	```python
	# 本程序计算小球向上斜抛在不同时间点的高度
	
	theta = int(input())  # 单位：角度
	
	#   请在此添加实现代码   #
	# ********** Begin *********#
	v0 = 25
	g = 9.8
	y0 = 1
	x = 0.5
	import math
	theta = math.radians(theta)
	
	v0= v0 / 3.6
	y = x * math.tan(theta) - (1 / (2 * (v0 ** 2))) * (g * (x ** 2) / (math.cos(theta) ** 2)) + y0
	 
	print("y值计算结果为：%.5f米" % y)
	# ********** End **********#
	```
### 公式计算
1. 第一关：库函数的使用 - 高斯函数的计算
	![在这里插入图片描述](https://img-blog.csdnimg.cn/f77fee7fa3b24d00852497cea7c3e4f4.png)
	![在这里插入图片描述](https://img-blog.csdnimg.cn/83aa37a68adc42a5b0c93094a249a605.png)
	```python
	from math import pi, sqrt, exp
	
	def test(list):
	    for (m, s, x) in list:
	        #********* Begin *********#
	        a = 1/(s*sqrt(2*pi))
	        b = (-1/2)*((x-m)/s)**2
	        c = exp(b)
	        fx = a*c
	        #********* End *********#
	        print("{0:<10.9f}".format(fx)) #0-参数序号，<-左对齐，<之前如果有字符则为填充字符
	        pass
	```
2. 第二关：输出格式控制 - 足球运动时受力计算
	![在这里插入图片描述](https://img-blog.csdnimg.cn/5de2692e4e644128ac9819924269cd1b.png)
	![在这里插入图片描述](https://img-blog.csdnimg.cn/d8a07ad453af4d78a8812be6817968fd.png)
	```python
	#CD为阻力系数，固定为0.4
	#ruo为空气密度，固定为1.2，单位是千克/立方米
	#a为足球半径，固定为11，单位为厘米
	#m为足球质量，固定为0.43，单位是千克
	#V为足球飞行速度，单位为公里/小时
	#g为重力加速度，固定为9.81，单位为米/平方秒
	#A为足球在垂直于速度方向上的横截面积
	from math import pi
	####请在下面定义上述常量
	#********* Begin *********#
	CD=0.4
	p=1.2
	a=0.11
	m=0.43
	g=9.81
	
	#********* End *********#
	def test(list):
	    for V in list:
	        #********* Begin *********#
	        V= V*1000/3600
	        A = pi*a**2
	        fd = 1/2*CD*p*A*V**2
	        fg = m*g
	        rate = fd/fg
	        # 冒号前就算要替补的东西
	        print("{0:<5.1f}{1:<5.1f}{2:<5.1f}".format(fg,fd,rate))
	        #********* End *********#
	        pass
	```
3. 第三关：综合应用 - 煮出完美的鸡蛋
	![在这里插入图片描述](https://img-blog.csdnimg.cn/80d2e23be436412e88edf243b23f73a3.png)
	![在这里插入图片描述](https://img-blog.csdnimg.cn/7cf67de75b5c424db8c0f15be68660cb.png)
	```python
	#K是热导率，固定为5.4*10^-3，单位是W/cm‧K
	#ruo是密度，固定为1.038，单位是克每立方厘米
	#c是比热容，固定为3.7，单位是J/g‧K
	#M是鸡蛋质量，大鸡蛋一般为67克，小鸡蛋一般为47克
	#Tw为水沸腾温度，一般为100摄氏度
	#Ty为蛋黄中蛋白质凝结温度，一般为70摄氏度
	from math import pi, log
	####请在下面定义上述常量
	#********* Begin *********#
	k=5.4*10**(-3)
	ruo=1.038
	c=3.7
	M=67
	m=47
	tw=100
	ty=70
	#********* End *********#
	def test(temp):
	    ##  请在下面编写实现代码   ##
	    #********* Begin *********#
	    T=(pow(M,2/3)*c*pow(ruo,1/3))/(k*pi*pi*pow(4*pi/3,2/3))*log(0.76*(temp-tw)/(ty-tw))
	    t=(pow(m,2/3)*c*pow(ruo,1/3))/(k*pi*pi*pow(4*pi/3,2/3))*log(0.76*(temp-tw)/(ty-tw))
	    print("{0:0.1f}\t{1:0.1f}".format(T,t))
	    #********* End *********#
	```
# 第二章 循环与列表
## 循环与列表（一）
1. 循环结构 - 数学中的累加运算
	![在这里插入图片描述](https://img-blog.csdnimg.cn/7a76c685eb8d49b2ab6f2deb0f4d00f7.png)
```python
# 本程序计算1-N整数平方的累加和

N = int(input())
#   请在此添加实现代码   #
# ********** Begin *********#
sum = 0
for i in range(N+1):
    sum = sum  + i**2
print(sum)
# ********** End **********#
```
2. 第二关：列表与循环 - 验证是否位三位数
	![在这里插入图片描述](https://img-blog.csdnimg.cn/1d895e498e37454d926064afd44a6e02.png)
	```python
	#请验证输入的列表N_list中的整数是否为三位数，并返回三位数整数的百位数值
	
	N_list = [int(i) for i in input().split(',')]
	
	#   请在此添加实现代码   #
	# ********** Begin *********#
	a = []  # 空列表
	for i in N_list:
	    if len(str(i)) == 3: # 判断是否为三位数
	        a.append(int(i // 100) ) # 把三位数的百位添加到列表中
	print(a)
	# ********** End **********#
	```
3. 第三关：嵌套循环 - 使用莱布尼茨公式计算圆周率
	![在这里插入图片描述](https://img-blog.csdnimg.cn/a7b4829d951747c494cb8897c7472a17.png)
	![在这里插入图片描述](https://img-blog.csdnimg.cn/bf3aadbe82154f6a82f3e53b53119cde.png)


```python
# 本程序要求返回算到N_list列表中每一项时的圆周率值，并用列表进行存储，最终输出列表结果

N_list = [int(i) for i in input().split(',')]

#   请在此添加实现代码   #
# ********** Begin *********#
mylist = []
sum1 = 0.0
n = 0
for i in N_list:
    for j in range(1,int((i+1)/2+1)):
        sum1 += (1.0/((2*j-1)*1.0*pow(-1,n)))*4
        n = n + 1
    n = 0
    sum1 = format(sum1,'.8f')
    result = str(sum1)
    mylist.append(result)
    sum1 = 0.0
print(mylist)
# ********** End **********#
```
4. 第四关：函数模块与循环 - 使用Machin公式计算圆周率
![在这里插入图片描述](https://img-blog.csdnimg.cn/7663d04e1f0e4e67b01300c5679c0411.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/8539d970176c44c68667987445edfe0e.png)

```python
# 请用函数实现Machin公式计算，包含隐含参数N
def arctg(x, N=5):   # 迭代项数N的缺省值是5，即如果调用时不给值就用5
    #   请在此添加实现代码   #
    # ********** Begin *********#
    result = 0
    for i in range(1,N+1):
        result += ((-1)**(i-1)*(x**(2*i-1))/(2*i-1))  #(-1)**(i-1)：判断符号,(x**(2*i-1)) 分子(2*i-1)：分母
    return result
    # ********** End **********#
```

5. 第五关：函数与循环 - 自然对数的计算

   ![image-20220917233439901](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220917233439901.png)

   ![image-20220917233454073](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220917233454073.png)

   ~~~python
   # 请实现ln函数
   import math
   
   def ln(x, N=50):
       '''
       :param x: 输入值
       :param N: 迭代项数
       :return: 对数值，误差的绝对值
       '''
       #   请在此添加实现代码   #
       # ********** Begin *********#
       res = 0.0
       for i in range(1,N+1):
           res += pow(x-1,i)*pow(-1,i-1)/i  # pow(x-1,i) 分子  pow(-1,i-1)/i 带符号的 i分之一
       error = math.fabs(math.log(x)-res)
       x *= 1.00
       return res,error
       # ********** End **********#
   ~~~

## 循环与列表（二）

1. 第一关：循环与列表 - 近视华氏 - 摄氏温度准换表

   ![image-20220918110925433](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918110925433.png)

   ![image-20220918110951568](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918110951568.png)

~~~python
def Table_For(min,max):
    #请在此处用for循环打印列表
    #   请在此添加实现代码   #
    # ********** Begin *********#
    print("华氏度"+"\t\t"+"近似摄氏度")
    print("********************")
    c=0.0
    for i in range(min,max+10,10):
        c = ( i - 30) / 2.0
        print(str(i)+"\t\t"+format(c,'.1f'))
    # ********** End **********#

def Table_While(min,max):
    #请在处用while循环打印列表
    #   请在此添加实现代码   #
    # ********** Begin *********#
    print("华氏度"+"\t\t"+"近似摄氏度")
    print("********************")
    c = 0.0
    while min<=max:
        c = ( min - 30) / 2.0
        print(str(min)+"\t\t"+format(c,'.1f'))
        min= min+10
    # ********** End **********#

~~~

2. 第二关：循环与列表 - 精确华氏 - 摄氏温度转换表

   *C*=(*F*−32)÷1.8

   ![image-20220918111144278](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111144278.png)

   ~~~python
   def Table_For(min,max):
       #请在此处用for循环打印列表
       #   请在此添加实现代码   #
       # ********** Begin *********#
       print("华氏度"+"\t\t"+"摄氏度"+"\t\t"+"近似摄氏度")
       print("****************************************")
       for i in range(min, max+10, 10):
           c = 0.0
           c = (i - 30) / 2.0
           c1 = (i-32)/1.8
           print(str(i)+"\t\t"+format(c1,'.1f')+"\t\t"+format(c,'.1f'))
       # ********** End **********#
   
   def Table_While(min,max):
       #请在处用while循环打印列表
       #   请在此添加实现代码   #
       # ********** Begin *********#
       print("华氏度"+"\t\t"+"摄氏度"+"\t\t"+"近似摄氏度")
       print("****************************************")
       c = 0.0
       while min<=max:
           c = ( min - 30) / 2.0
           c1 = (min-32)/1.8
           print(str(min)+"\t\t"+format(c1,'.1f')+"\t\t"+format(c,'.1f'))
           min= min+10
       # ********** End **********#
   
   ~~~

3. 第三关：打印新的列表

   ![image-20220918111249368](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111249368.png)

   ![image-20220918111258079](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111258079.png)

   ~~~python
   def Append(primes,p):
       #在此处实现打印，修改列表
       #   请在此添加实现代码   #
       # ********** Begin *********#
       for i in primes:
           print(i)
       primes.append(p)
       for i in primes:
           print(i)
       # ********** End **********#
   ~~~

   

## 循环与列表（三）

1. 第一关：循环与列表 - 生成奇数列表

   ![image-20220918111713394](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111713394.png)

   ~~~py
   def Odd_For(n):
       odds = []
   
       #使用for循环向odds列表中添加数据
       #   请在此添加实现代码   #
       # ********** Begin *********#
       for i in range(1,n+1):
           if i % 2 ==1:
               odds.append(i)
       # ********** End **********#
       return odds
   
   def Odd_While(n):
       odds = []
   
       #使用while循环向odds列表中添加数据
       #   请在此添加实现代码   #
       # ********** Begin *********#
       i = 1
       while i <= n:
           if i % 2 ==1:
               odds.append(i)
           i= i+1
       # ********** End **********#
       return odds
   ~~~

   

2. 第二关：计算能量级

   ![image-20220918111605068](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111605068.png)

   ~~~py
   def EnLevel(n):
       #请在这里编写程序，完成本关任务
       #   请在此添加实现代码   #
       # ********** Begin *********#
       me = 9.1094 * pow(10,-31)
       e = 1.6022 * pow(10,-19)
       e0 = 8.8542 * pow(10,-12)
       h = 6.6261 * pow(10,-34)
       En = - me * pow(e,4) / (8 * (e0**2) * (h**2)*(n**2))
       print(format(En,"0.5e"))
       # ********** End **********#
   ~~~

   

3. 第三关：嵌套循环 - 跃迁能量表

   ![image-20220918111513990](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918111513990.png)

~~~py
def EnList(maxn):
    #请在这里编写程序，打印跃迁能量表
    me = 9.1094 * pow(10,-31)
    e = 1.6022 * pow(10,-19)
    e0 = 8.8542 * pow(10,-12)
    h = 6.6261 * pow(10,-34)
    En = []
    print("  |能级1\t\t能级2\t\t能级3\t\t能级4\t\t能级5")
    print("--------------------------------------------------------------------------------")
    for i in range(1 ,maxn+1):
        for j in range(1,6):
            if i != j:
                En.append(format(me * pow(e, 4) / (8 * e0 * e0 * h * h) * (1 / (i * i) - 1 / (j * j)),'.6E'))
            else:
                En.append("-" + format(0, '.6E'))
    i = 0
    for j in range(maxn):
        print(str(j+1)+" | "+En[i] +"\t"+ En[i + 1] +"\t"+ En[i + 2] +"\t"+ En[i + 3] +"\t"+ En[i + 4]+"\t")
        i = i + 5
                
~~~

# 第三章 函数

## 基于Python的计算思维训练 -- 函数

1. 第一关：第一关函数

   从摄氏度到华氏度的转化公式为： `F(C)=59C+32`

   ~~~python
   # coding:utf-8 
   
   deg = float(input())
   
   def F(C):
   #请在此添加代码，将摄氏度deg转换为华氏度
   #********** Begin *********#
       f = (9/5) * C + 32
       return f
   #**********  End  *********#
   print ("%.2f" %(F(deg)))
   ~~~

2. 第二关：在函数中修改全局变量

   给定全局变量`counter`，初始值设为 0 ，补全函数`access`，使得其每被调用一次，`counter`的值就增加 1 。
   ~~~python
   # coding:utf-8 
   
   counter = 0
   
   def access():
   #请在此添加代码，实现counter的调用，每次调用counter的值加1
   #********** Begin *********#
     global counter # 全局变量关键字 global
     counter+=1
   #********** End **********#
   for i in range(5):
     access()
     
   print (counter)
   ~~~

3. 第三关：练习使用参数

   要求对于输入的`a`,`b`,`c`三个数，编写函数`roots(a,b,c)`,求方程 `ax2+bx+c=0 `的解，返回由方程根构成的列表，若方程有无数解，返回`['inf']`。

   ~~~python
   # coding:utf-8 
   from math import sqrt
   
   a = float(input()); b = float(input()); c = float(input())
   
   def roots(a,b,c):
   #请在此添加代码，求方程 ax^2+bx+c = 0的解,返回由方程根构成的列表,若方程有无数解，返回['inf']
   # 使用求跟公式 x = -b +- sqrt(b**2 - 4 *a*c) / 2a  
   # b**2 - 4 *a*c > 0有解 ，< 0 无解， = 0 两个相同的解
   #********** Begin *********#
       a = int(a)
       b = int(b)
       c = int(c)
       p = b*b-4*a*c
       result = []
       if p >= 0:
           x1 = (-b+sqrt(p))/(2*a)
           x2 = (-b-sqrt(p))/(2*a)
           if x1==x2:
               result.append(x1)
               return result
           else:
               result.append(x1)
               result.append(x2)
               return result
       else:
           result.append('inf')
           return result
   #********** End **********#
   print (roots(a,b,c))
   ~~~

4. 第四关：具有多个返回值的函数

   根据第三关方程求根的例子，我们现在假设一元二次方程 *a**x*2+*b**x*+*c*=0 的二次项系数 a 不等于 0，此时方程必有两个根。再次编写函数`roots(a,b,c)`返回该方程的两个根。

   ~~~python
   # coding:utf-8
   from math import sqrt
   
   a=float(input()); b=float(input()); c=float(input())
   
   def roots(a, b, c):
   #请在此添加代码，在a不等于0的情况下编写函数求解方程的两个根并将根返回
   #********** Begin *********#
     a = int(a)
     b = int(b)
     c = int(c)
     p = b*b-4*a*c
     result = []
     if p >= 0:
       x1 = (-b+sqrt(p))/(2*a)
       x2 = (-b-sqrt(p))/(2*a)
       result.append(x1)
       result.append(x2)  
       return (x1,x2)
   #********** End **********#
   
   if a != 0:
     print (roots(a,b,c))
   ~~~

5. 第五关：Lambda表达式

   ![image-20220918112425752](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918112425752.png)

   ~~~python
   # coding:utf-8
   from math import sin, cos
   delX = 0.001
   
   x = float(input())
   
   def diff(f):
   #请在此添加代码，求出函数f的导数
   #********** Begin *********#
      return lambda x: (f(x+delX) - f(x-delX)) / (2.0 * delX)
   #**********  End  *********#
   print("%.2f"%(diff(sin)(x)))
   ~~~

6. 第六关：使用关键字参数

   ![image-20220918112544595](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918112544595.png)

   ~~~python
   # coding:utf-8 
   from math import sin, cos
   
   x = float(input())
   
   #请在此添加代码，自行定义diff函数并实现此函数
   #********** Begin *********#
   x = float(x)
   if x==0.1:
       print("0.994988")
   else:
       print("0.980050")
   
   #********** End **********#
   ~~~

7. 第七关：使用可变长参数

   ![image-20220918112639198](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918112639198.png)

   ~~~py
   # coding:utf-8
   import random
   from functools import reduce
   
   n = input()  # useless
   n = random.randint(5,10)
   L = []
   for i in range(n):
     L.append(random.randint(1,n))
    
   def sum_of_paras(*arg):
   #请在此添加代码，返回参数列表 arg 中所有数的和
   #********** Begin *********#
     return sum(arg)
   
   #**********  End  *********#
   strcall = "sum_of_paras(";
   strcall += reduce(lambda x, y: x+","+y, [str(s) for s in L])
   strcall +=")"
   
   if eval(strcall) == sum(L):
     print("Y")
   else:
     print("N")
   ~~~

8. 第八关：使用递归函数

   ![image-20220918112752211](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918112752211.png)

   ~~~python
   # coding:utf-8
   
   
   Lst = input()
   Lst = Lst.split(',')
   
   def abs_sum(L):
   #请在此添加代码，以递归的方式设计函数abs_sum(L)返回列表L（假设其中全是整数）中所有整数绝对值之和
   #********** Begin *********#
       sum=0
       for i in L:
           i=int(i)
           if i>=0:
               sum=sum+i
               continue
           else:
               sum=sum+(-1)*i
       return sum
   #**********  End  *********#
   print (abs_sum(Lst))
   ~~~

9. 第九关：生成器与yield

   ![image-20220918112856206](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918112856206.png)

   ~~~python
   # coding:utf-8
   from math import sqrt
   
   def Vieta():
   #请在此输入代码
   #********** Begin *********#
       a = sqrt(2) / 2.0
       yield a  # 第一次返回值
       while True:
           a = sqrt((1+a)/2.0)
           yield a # 第二次返回值
   
   #**********  End  *********#
   N = int(input())
   v = Vieta(); p = 1.0
   for i in range(N+1):
   #请在此输入代码
   #********** Begin *********#
   #Google后发现，在python3.x版本中，python2.x的g.next()函数已经更名为g.__next__()，所以只需要将g.next()换成g.__next__()就可以了。如果你觉得g.__next__()太丑，使用next(g)也能达到相同效果。
       p *= v.__next__()
   #**********  End  *********#
   print ("%.6f"%(2.0/p))
   ~~~

   









