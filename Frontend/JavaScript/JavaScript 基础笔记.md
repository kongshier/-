> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# 初识 JavaScript 

JavaScript负责页面中的的行为，是一门运行在客户端的脚本语言。  



[学习网站](https://zh.javascript.info/) 



解释型语言与编译型语言区别：

![image-20221114110556873](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221114110556873.png)



## JavaScript 作用

- 表单动态校验（密码校验）
- 网页特效
- 服务端开发
- 桌面端开发
- 等作用



JS引擎：浏览器使用JS引擎来执行JS代码，逐句执行代码



## JavaScript组成

~~~mermaid
graph LR
a(JavaScript)-->a1(ECMScript)
a(JavaScript)-->a2(DOM)
a(JavaScript)-->a3(BOM)
a2(DOM) -->b(Web APIs)
a3(BOM) -->b(Web APIs)
~~~

- ECMScript ：JavaScript 语法
  - 规定JS的编程语法和基础核心知识，遵循JS工业标准
- DOM：页面文档对象模型
  - 提供接口 API 对元素进行操作
- BOM：浏览器对象模型
  - 独立于内容的、可与浏览器窗口进行互动的对象结构。对浏览器窗口操作（弹出框等）



## JS的编写的位置  

1.可以编写到标签的指定属性中  （内嵌式）

```html  
<button onclick="alert('hello');">我是按钮</button>
<a href="javascript:alert('aaa');">超链接</a>
```

2.可以编写到script标签中  （行内式）

```html  
<script type="text/javascript">  
//编写js代码  
</script>  
```
3.可以将代码编写到外部的js文件中，然后通过标签将其引入  （外部引用式）

script标签一旦用于引入外部文件了，就不能在标签内编写代码了，即使编写了浏览器也会忽略  ,如果需要则可以在创建一个新的script标签用于编写内部代码  

```html  
<script type="text/javascript" src="文件路径"></script>  
```
## 输入、输出语句  

弹出一个警告框 ：

```javascript  
alert("msg");  
```
输入：
```javascript  
document.write("msg");  
```
在浏览器的控制台显示：  F12
```javascript  
console.log("msg");  
```
弹出输入框，输入内容

```js
promp("msg")
```



## 基本的语法  

js函数声明不需要；分号，但是赋值语句要加；分号  

```js
function functionName(arg0,arg1,arg2){  
//函数声明  
}  
var functionName = function(arg0,arg1,arg2){  
//函数表达式  
};(注意分号)  
```

### 注释  

单行注释  

```javascript  
//注释内容    （Vscode）快捷键 Ctrl + /
```
多行注释  
```javascript  
/*  
注释内容    快捷键（Shift + Ctrl + A）也可以自定义快捷键
*/  
```

### JS规范

- JS严格区分大小写 
- JS中每条语句以分号`(;)`结尾如果不写分号，浏览器会自动添加，但是会消耗一些系统资源，  而且有些时候，浏览器会加错分号，所以在开发中分号必须写  

- JS中会自动忽略多个空格和换行，所以可以利用空格和换行对代码进行格式化。  


## 字面量和变量  

### 字面量  

字面量实际上就是固定的值，比如 1 2 3 4 true false null NaN "hello"  



**字面量都是不可以改变的。**  



由于字面量不是很方便使用，所以在JS中很少直接使用字面量  

### 变量  

- 变量可以用来保存字面量，并且可以保存任意的字面量

- 变量用来存放数据的容器

==变量是程序在内存中用来存放数据的空间==



**声明变量格式**

```js
var 变量名;
let 变量名；
```

```javascript
var bs; // 声明但是没有赋初始值
var a =1;// 声明变量并且赋初始值  
var b =0;
```

**给变量赋值** 

```javascript
a = 1; 
```
#### 变量初始化

声明和赋值同时进行 

```javascript
var a = 456;   
```
```js
    <script>
        var age = 12 //声明并赋值 age
        alert('年龄为：' + age) 
    </script>
```

```js
    <script>
        var age = 12;
        var username = 'kcs';
        var address = 'gx';
        //控制台输出
        console.log("姓名：" + username + "\t" + "年龄：" + age + "\t" + "地址：" + address);
    </script>
```

### var 与 let 的却别



> var是函数作用域，而let是块作用域。在函数内声明了var，整个函数内都是有效的，在for循环内定义了一个var变量，实际上其在for循环以外也是可以访问的，而let由于是块作用域，所以如果在块作用域内（for循环内）定义的变量，在其外面是不可被访问的。



1. 如果在全局作用域中用`var`声明变量，此变量会默认成为`window`的一个属性，let声明的变量则不会添加到window对象中。
2. 在==es6之前==，是没有块级作用域，所谓块级作用域，就是用`{}`包含的区域，我们常用的有for，while，if等。但是在块级作用域中用`let`声明变量，那么此变量就有了块级作用域，就必须只有在此块级作用域才能访问此变量。
3. var声明的变量有变量提升特性，let声明则没有这个特性。变量提升：就是把变量提升提到函数的上面的地方。我么需要说明的是，变量提升只是提升变量的声明，并不会把赋值也提升上来。
4. var可以允许重复声明相同的变量，后者会覆盖前者，let则不能重复声明相同的变量。



### 变量值交换

方法一：定义一个临时变量

```js
// 变量交换
var apple1 = "青苹果"
var apple2 = "红苹果"
var temp;
        
console.log("交换前")
console.log("apple1:" + apple1)
console.log("apple2:" + apple2)
temp = apple1;
apple1 = apple2;
apple2 = temp;

console.log("交换后")
console.log("apple1:" + apple1)
console.log("apple2:" + apple2)
```

方法二：利用算数加减



> 让a先变成a与b的‘和'（也可以换成a和b的差，⼀样的），‘和'减去b巧妙的得到了a的变量值赋予b ，再通过‘和'减去a的值得到了b的值赋予a，或者是下⾯的变式（差的形式）

```js
let a=123,
    b=456;
    a+=b;
    b=a-b;
    a-=b;
console.log(a,b);
```

```js
let a=123,
    b=456;
    a -= b;
    b = a + b;
    a = b - a;
console.log(a,b);
```

方法三：利用位

> 通过底层位运算来进⾏交换变量值



```js
 let a = 123,
     b = 456;
     a ^= b;
     b ^= a;
     a ^= b;
     console.log(a, b);
 
//或者这样
a = (b^=a^=b)^a;
```

方法四：利用对象

> 把a先变成了⼀个对象，这个对象保存着应该交换后的键值对，最后赋值

```js
let a=123,
    b=456;
    a = {a:b,b:a};
    b = a.b;
    a = a.a；
    console.log(a,b);
```

方法五：数组

```js
 let a = 123,
     b = 456;
     a = [a, b];
     b = a[0];
     a = a[1];
     console.log(a, b);
```

方法六：ES6的解构赋值语法

```js
let a = 123,
    b = 456;
    [a,b] = [b,a];
    console.log(a, b);
```



## 变量语法

### 变量更新

- 当给同一个变量赋值多次时，以最后一次赋值的值为准。

### 同时声明多个变量

```js
var age,username,address,email; //只定义，未赋值，undefined

//同时赋值
var age = 18 ,username = "kcs" ,address = "gx",email = "12345789@qq.com";
```

### 特殊情况

- 只声明未赋值 ：undefiend
- 不声明不赋值，报错
- 不声明直接赋值使用：JS允许（不建议）



### 标识符命名规范

在JS中所有的可以自主命名的内容，都可以认为是一个标识符， 



标识符应该遵守==标识符的规范== 比如：变量名、函数名、属性名  

1. 标识符中可以含有字母（A-Za-z）、数字（0-9）、下划线（`_`）、美元符号$组成
   - userName、_name 
2. 不能以数字开头  
3. 严格区分大小写
4. 不能是关键字、保留字
5. 变量必须有意义，见名知意
6. 遵循驼峰命名。首字母小写，后面每个单词的首字母都是要大写
7. 操作符两侧有一个空格
8. 注释，先空格，再写注释
9. 括号qian'ho



### JavaScript常用关键字

不能使用关键字来作用 变量名

| 名称       | 作用                                                         |
| ---------- | ------------------------------------------------------------ |
| break      | 立即退出循环，阻止再次反复执行任何代码                       |
| case       | 配合switch完成判断                                           |
| catch      | 配合try进行错误判断                                          |
| continue   | 退出当前循环，根据控制表达式还允许继续进行下一次循环         |
| default    | 配合switch，当条件不存在时使用该项                           |
| delete     | 删除了一个属性                                               |
| do         | 用于do-while,后测试循环，即退出条件在执行循环内部的代码之后计算 |
| else       | 配合if条件判断，用于条件选择的跳转                           |
| finally    | 预防出现异常时用的，无论异常是否是否发生异常都会处理的       |
| for        | for语句，循环语句                                            |
| function   | 函数关键字                                                   |
| if         | if 语句用于判断                                              |
| in         | 1.配合for遍历对象，2.判断某个属性属于某个对象                |
| instanceof | 某个对象是不是另一个对象的实例                               |
| new        | 创建一个新对象                                               |
| return     | 从当前函数退出，并从那个函数返回一个值                       |
| switch     | 弥补if的多重判断语句                                         |
| this       | 总是指向调用该方法的对象                                     |
| throw      | 抛出异常                                                     |
| try        | 配合catch进行错误判断                                        |
| typeof     | 检测变量的数据类型                                           |
| var        | 声明变量                                                     |
| void       | 声明没有返回值                                               |
| while      | while判断语句，可配合do做前置判断，或独立使用做后置判断      |
| with       | with 语句用于设置代码在特定对象中的作用域                    |

### 保留字

未来可能是关键字

| break      | delete  | function   | return    | typeof       |
| ---------- | ------- | ---------- | --------- | ------------ |
| case       | do      | if         | switch    | var          |
| catch      | else    | in         | this      | void         |
| continue   | false   | instanceof | throw     | while        |
| debugger   | finally | new        | true      | with         |
| default    | for     | null       | try       |              |
| 未来保留字 |         |            |           |              |
| abstract   | double  | goto       | native    | static       |
| boolean    | enum    | implements | package   | super        |
| byte       | export  | import     | private   | synchronized |
| char       | extends | int        | protected | throws       |
| class      | final   | interface  | public    | transient    |
| const      | float   | long       | short     | volatile     |











# 数据类型 

==JavaScript 是一种弱类型语言、解释性语言== ，根据值来确定数据类型，js 变量的数据类型是可变的

## 六种数据类型  

 **JS中一共分成六种数据类型：5个基本数据类型+object**  

1.  String：字符串  
2.  Number：数字型（整型值、浮点型值）
3.  Boolean：布尔值  
4.  Null：空值  
5.  Undefined：未定义 、未初始化
6.  Object：对象  



**typeof运算符检查数据类型**  

> typeof 变量名



### 1.String 字符串  
JS中的字符串需要使用引号引起来==双引号或单引号==都行     



在字符串中使用 `\ `作为转义字符  

```javascript  
\'  ==> '  
\"  ==> "  
\n  ==> 换行  
\t  ==> 制表符  tab缩进
\\  ==> \
\b  ==> 空格
```

字符串嵌套（拼接字符串）：

> 外双内单，外单内双
>
> ```js
> var str1 = "哈'哈'哈"
> var str2 = '你好你"好你"好'
> ```



- 获取字符串长度：字符串变量名.length   `str.length`
- 字符串拼接：使用 `+`  字符相连，数值相加



### 2.Number 数字型

**JS中所有的整数和浮点数都是Number类型**  



> 数字型最大值：Number.MAX_VALUE =	1.7976931348623157e+308 
>
> 数字型最小值：Number.MIN_VALUE =	5e-324



特殊的数字：能赋值给变量 

- Infinity ： 正无穷 
  - a = Infinity ,能赋值  
- -Infinity ：负无穷  
- NaN ：非数字（Not A Number）
- isNaN：判断是否未数字型

 

进制数字表示：  

- 0b ：二进制
- 0 ：八进制  
- 0x ：十六进制  

### 3.Boolean 布尔值  
 布尔值主要用来进行逻辑判断，布尔值只有两个  

-  true 逻辑的真   非 0 为真 
-  false 逻辑的假   0 为假

```js
var flag = false;
var flag1 = true;
console.log(flag);
console.log(flag1);
```

### 4.Null 空值  

空值专门用来表示为空的对象，Null类型的值只有一个 ：null 

###  5.Undefined 未定义  
**声明的变量没有赋值，此变量的值就是undefined**  该类型的值只有一个 undefined 



### 6.引用数据类型	  
 Object 对象  

## 类型转换  

 类型转换就是指将其他（所需求）的数据类型，转换为String Number 或 Boolean  

### 1.转换为String  （字符串）

#### 方式一（强制类型转换）：  
**调用被转换数据的toString()方法** 

> 注意：**这个方法不适用于null和undefined** 
> 由于这两个类型的数据中没有方法，所以调用toString()时会报错 

#### 方式二（强制类型转换）：  
 **调用String()函数** 
 例子：

```javascript
var a = 123;  
a = String(a);  
```
原理：

- 对于Number、Boolean、String都会调用他们的 toString() 方法来将其转换为字符串
- 对于null值，直接转换为字符串 "null"
- 对于undefined直接转换为字符串 "undefined"  

#### 方式三（隐式的类型转换）:   
 **为任意的数据类型 +" "**  

例子：  

```javascript
var a = true;  
a = a + ""; 
```
 原理：和String()函数一样	 

```js
<script>
    var num = 123456;
    //转换成string
    var str = num.toString();
    console.log(str);
    console.log(typeof str);
    console.log(String(num)); 
	  console.log(num+''); 
</script>
```

 

### 转换为Number（数字型）

#### 方式一（强制类型转换）：  
**调用Number()函数** 
例子： 

```javascript
var s = "123";  
s = Number(s); 
```
 转换的情况：  
1. 字符串 > 数字
    - 如果字符串是一个合法的数字，则直接转换为对应的数字
    - 如果字符串是一个非法的数字，则转换为NaN 
    - 如果是一个空串或纯空格的字符串，则转换为0  

2. 布尔值 > 数字 
    - true 转换为1 
    - false 转换为0  

3. 空值 > 数字 
    - null转换为0  

4. 未定义 > 数字 
    - undefined 转换为NaN  


#### 方式二（强制类型转换）：  
调用`parseInt()`、`parseFloat()  `

对非String使用`parseInt()`、`parseFloat()`，**先将转换为String**，然后在进行`parseInt()` 
`parseInt()` 可以将**一个字符串中的有效的整数位**提取出来，并转换为Number 
例子：  

```javascript  
var a = "123.456px";  
a = parseInt(a); //123  
```
`parseFloat()`可以将一个**字符串中的有效的小数位**提取出来，并转换为Number 
例子：  

```javascript  
var a = "123.456px";  
a = parseFloat(a); //123.456  
```
#### 方式三（隐式的类型转换）： 利用算术运算：`+`、`-`、` *`、` / `
使用一元的 `+`  来进行隐式的类型转换 



例子：  

```javascript  
var a = "123";  
a = 0 + a;
a = 1 * a;
a = 1 / a;
```

案例1：

```js
<script>
    var year = prompt("请输入你的出生年份："); //输入的为字符串型
    var age = 2023 - year; // 隐式转换为 Number
    alert("你今年" + age + "岁了");
</script>
```

案例 2：

```js
<script>
    var num1 = parseFloat(prompt("请输入第一个加数"));
    var num2 = parseFloat(prompt("请输入第二个加数"));
    result = num1 + num2;
    alert("结果为：" + result);
</script>
```



### 转换为布尔值  

#### 方式一（强制类型转换）：  
使用Boolean()函数 
例子：  

```javascript
var s = "false";  
s = Boolean(s); //true 
```

转换的情况 

1. 字符串 > 布尔  
   - 除了空串其余全是true  
2. 数值 > 布尔  
   - 除了0和NaN其余的全是true  
3. null、undefined > 布尔  ：false  
4. 对象 > 布尔 ：true  

#### 方式二（隐式类型转换）：	  
**为任意的数据类型做两次非运算，即可将其转换为布尔值** 
例子：  

```javascript  
var a = "hello";  
a = !!a; //true   
```



# 基础语法  

## 运算符  
运算符也称为操作符 
通过运算符可以对一个或多个值进行运算或操作  

### typeof运算符  
用来检查一个变量的数据类型 

```js
typeof 变量 
```

它会返回一个用于描述类型的字符串作为结果  

### 算数运算符  

- +：&ensp;对两个值进行加法运算并返回结果    
- -：&ensp;对两个值进行减法运算并返回结果    
- *：&ensp;对两个值进行乘法运算并返回结果    
- /：&ensp;对两个值进行除法运算并返回结果    
- %：&ensp;对两个值进行取余运算并返回结果  



**除了加法以外，对非Number类型的值进行运算时，都会先转换为Number然后在做运算。** 

而做加法运算时，如果是两个字符串进行相加，则会做拼串操作，将两个字符连接为一个字符串。 
任何值和字符串做加法，都会先转换为字符串，然后再拼接字符串

### 一元运算符  

 一元运算符只需要一个操作数  
#### 一元的 +  
 就是正号，不会对值产生任何影响，但是可以将==非数字转换为数字== 
 例子：    

```javascript  
var a = true;  
a = +a;  
```
#### 一元的 -
 就是负号，可以对==数字进行符号位取反== 
 例子：  

```javascript  
var a = 10;  
a = -a;  
```

#### 自增  
自增可以使变量在原值的基础上自增1 

自增使用 `++ `

```js
var = 1;
i++;
alert(1);
```

自增可以使用 前++（++a）后++(a++) 

无论是++a 还是 a++都会立即使原变量自增1 
不同的是++a和a++的值变换顺序不同

- ++a的值是变量的新值（自增后的值） 
- a++的值是变量的原值（自增前的值）  

#### 自减  
自减可以使变量在原值的基础上自减1 
自减使用 `--`
自减可以使用 前`--a`后`a--` 
无论是a 还是 a都会立即使原变量自减1 
不同的是`++a`和`a--`的值变换顺序不同

- `--a`的值是变量的新值（自减后的值） 
- `a--`的值是变量的原值（自减前的值）  

### 逻辑运算符  

!  （非）

- 非运算可以对一个布尔值进行取反，true变false false边true 
- 当对非布尔值使用!时，会先将其转换为布尔值然后再取反 
- 可以利用!来将其他的数据类型转换为布尔值  

&& （与）

- ​	 &&可以对符号两侧的值进行==与==运算 
- ​	 只有两端的值都为 true 时，才会返回 true。只要有一个false就会返回false。
- ​	 与是一个短路的与，如果第一个值是false，则不再检查第二个值 
- ​	 对于非布尔值，它会将其转换为布尔值然后做运算，并返回原值 
- ​	 规则： 
  - 如果第一个值为 `false`，则返回第一个值  
  - 如果第一个值为 `true`，则返回第二个值  

||  （或）
	 ||可以对符号两侧的值进行或运算 
	 只有两端都是false时，才会返回false。只要有一个true，就会返回`true`。
	 或是一个短路的或，如果第一个值是true，则不再检查第二个值 
	 对于非布尔值，它会将其转换为布尔值然后做运算，并返回原值 
	 规则：	 
			1.如果第一个值为true，则返回第一个值 
			2.如果第一个值为false，则返回第二个值  

### 赋值运算符  

`= `
	可以将符号右侧的值赋值给左侧变量

```js
a = 11;
s = a;
```

`+=`      

```javascript
a += 5 相当于 a = a+5    
var str = "hello";  str += "world";  
```
`-=`    

```javascript
a -= 5  相当于 a = a-5  
```
`*=`    

```javascript  
a *= 5 相当于 a = a*5  
```
`/=`    

```javascript  
a /= 5 相当于 a = a/5	  
```

`%=`  

```javascript  
a %= 5 相当于 a = a%5 
```

### 关系运算符  

关系运算符用来比较两个值之间的大小关系的 

- `>`
- `>= ` 
- `<`  
- `<=`  

关系运算符的规则和数学中一致，用来比较两个值之间的关系

如果关系成立则返回`true`，关系不成立则返回`false`
如果比较的两个值是非数值，会将其转换为`Number`然后再比较
如果比较的两个值都是字符串，此时会比较字符串的Unicode编码，而不会转换为 Number

### 相等运算符  

相等，判断左右两个值是否相等，如果相等返回true，如果不等返回false 
相等会自动对两个值进行类型转换，如果**==对不同的类型进行比较，会将其转换为相同的类型然后再比较==**，转换后相等它也会返回 true，null == undifined  

#### **NaN** 

NaN不与任何值相等，报告它自身 `NaN == NaN` 结果为`false` 判断一个值是否是NaN 

使用isNaN()函数  

### 三元运算符： 

语法：

```js
条件表达式?语句1:语句2
```

执行流程： 

- 先对条件表达式求值判断
  1. 如果判断结果为true，则执行语句1，并返回执行结果 
  2. 如果判断结果为false，则执行语句2，并返回执行结果 

#### 优先级： 

1. JS中的运算符也是具有优先级
   - 比如 先乘除 后加减 先与 后或 

## 流程控制语句  

程序都是自上向下的顺序执行的， 
通过流程控制语句可以改变程序执行的顺序，或者反复的执行某一段的程序。  

### 条件分支语句  

#### 1.if语句

条件判断语句也称为 `if语句` 

- 根据不同的条件。执行不同的程序

语法一：  if {}

```javascript
 if(条件表达式){  
 	语句...  
 }  
```


```  
 执行流程：  
 if语句执行时，会先对条件表达式进行求值判断，  
 如果值为true，则执行if后的语句  
 如果值为false，则不执行  
```

 语法二：  if{}···else{}
```javascript
if(条件表达式){  
	语句...  
}else{  
	语句...  
} 
```
```  
 执行流程：  
	if...else语句执行时，会对条件表达式进行求值判断，  
		如果值为true，则执行if后的语句  
		如果值为false，则执行else后的语句  
```

 语法三：  if{} else if {}

```javascript  
if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else if(条件表达式){  
	语句...  
}else{  
	语句...  
}	  
```
```  
 执行流程  
	 if...else if...else语句执行时，会自上至下依次对条件表达式进行求值判断，  
		如果判断结果为true，则执行当前if后的语句，执行完成后语句结束。  
		如果判断结果为false，则继续向下判断，直到找到为true的为止。  
		如果所有的条件表达式都是false，则执行else后的语句  
```

#### 2.switch语句 

语法：  

```javascript  
switch(条件表达式){  
	case 表达式:  
		语句...  
		break;  
	case 表达式:  
		语句...  
		break;  
	case 表达式:  
		语句...  
		break;  
	default:  
		语句...  
		break;  
}  
```

执行流程： 

1.  switch()...case...语句在执行时，会依次将case后的表达式的值和switch后的表达式的值进行全等比较， 
2. 如果比较结果为false，则继续向下比较。如果比较结果为true，则从当前case处开始向下执行代码。 
3. 如果所有的case判断结果都为false，则从default处开始执行代码

### 循环语句  
通过循环语句可以反复执行某些语句多次 

#### 1. while循环 

 语法：  

```javascript  
while(条件表达式){  
    语句...  
}  
```

执行流程： 

1. while语句在执行时，会先对条件表达式进行求值判断
2. 如果判断结果为false，则终止循环 
3. 如果判断结果为true，则执行循环体 
4. 循环体执行完毕，最后再与条件表达式比较一次

#### 2. do...while循环 


```javascript  
do{  
语句...  
}while(条件表达式)  
```


执行流程 
1. do...while在执行时，会先执行do后的循环体，然后在对条件表达式进行判断
2. 如果判断判断结果为false，则终止循环
3. 如果判断结果为true，则继续执行循环体

 do while 和 while 的区别： 

- while：先判断后执行 
- do...while：先执行后判断 
- do...while可以确保循环体至少执行一次

#### 3. for循环 

语法：  

```javascript
for(①初始化表达式 ; ②条件表达式 ; ④更新表达式){  
    ③语句...  
}  
```
执行流程： 
1. 首先执行①初始化表达式，初始化一个变量
2. 然后对②条件表达式进行求值判断，如果为false则终止循环 
3. 如果判断结果为true，则执行③循环体 
4. 循环体执行完毕，执行④更新表达式，对变量进行更新
5. 更新表达式执行完毕重复② 



案例：计算学生成绩

```js
var classNum = prompt("请输入班级人数");
var avg = 0;
var sum = 0;
for (var i = 1; i <= classNum; i++) {
    var score = parseFloat(prompt("请输入第" + i + "个学生的成绩："));
    sum = sum + score;
}
alert("学生成绩：" + sum);
avg = sum / classNum;
alert("学生平均成绩：" + avg);
```



输入多个星星

```js
var startnum = prompt("输入显示的星星数");
var str = " ";
for(var i = 0; i < startnum; i++){
    //拼接字符串
    str+="❤️";
}
console.log(str);
```

```js
//打印五行五列心
var row = prompt("请输入行数：");
var clos = prompt("请输入列数：");
var str = "";
for (var i = 0; i < row; i++) {
    for (var j = 0; j < clos; j++) {
        str += "❤️";
    }
    str += "\n";
}
console.log(str);
```

```js
//打印到三角形
var row = prompt("请输入第一行的心数");
var str = "";
for (var i = 0; i < row; i++) {
    //从 i 开始 
    for (var j = i; j < row; j++) {
        str += "❤️";
    }
    str += "\n";
}
console.log(str);

//打印正三角形
var row = prompt("请输入第一行的心数");
var str = "";
for (var i = 0; i < row; i++) {
    //从 i 开始 
    for (var j = 0; j < i; j++) {
        str += "❤️";
    }
    str += "\n";
}
console.log(str);
```



打印九九乘法表

```js
var sum = "";
for (var i = 1; i <= 9; i++) {
    //从 i 开始 
    for (var j = 1; j <= i; j++) {
        sum += j + "*" + i + "=" + i * j+"\t";
    }
    sum += "\n";
}
console.log(sum);
```





#### 4. 死循环  

```javascript
// while
while(true){  

}  
 // for
for(;;){  

}
```
## 表达式、返回值

### 表达式

- 由数字、运算符、变量等组成的式子

```js
i = 1-4;
j = i + 4;
resule = (j+4)*4+(i*4)/2
```

### 返回值

- 经过四则运算得到的结果赋值给一个变量



ATM存取款

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ATM存取款</title>
    <script>
        //总金额
        var totalMoney = 0;
        do {
            var selection = parseFloat(prompt("请选择操作：\n 1.存钱\n 2.取钱 \n 3.显示金额 \n 4.退出"));
            switch (selection) {
                case 1:
                    var saveMoney = parseFloat(prompt("请输入存款金额"));
                    totalMoney += saveMoney;
                    if (isNaN(totalMoney)) {
                        alert("请输入数字");
                        break;
                    }
                    alert("你的余额为：" + totalMoney);
                    break;
                case 2:
                    //取款
                    var withdrawMoney = parseFloat(prompt("请输入取款金额"));
                    if (isNaN(withdrawMoney)) {
                        alert("请输入数字");
                        break;
                    }
                    if (totalMoney <= 0) {
                        alert("你的余额为0,请充值");
                        break;
                    }
                    if (totalMoney < withdrawMoney) {
                        alert("余额不足，请及时充值");
                        break;
                    }
                    if (totalMoney >= withdrawMoney) {
                        totalMoney -= withdrawMoney;
                        alert("你取走了：" + withdrawMoney + "\t你的余额为：" + totalMoney);
                        break;
                    }
                    break;
                case 3:
                    if (totalMoney == 0) {
                        alert("你还没有存款余额为0");
                        break;
                    }
                    alert("你的余额为：" + totalMoney);
                    break;
                case 4:
                    alert("退出程序");
                    break;
                default:
                    alert("请输入正确的数字!");
                    break;
            }
        }while(selection !==4);
    </script>
</head>
```







# 对象（Object）  

- 对象是一组无序的相关属性和方法的集合，是一种复合数据类型



对象的由属性和方法组成：

- 属性：事务的特征，在对象中用的属性来表示（名词）
- 方法：事物的行为，在对象中用方法来表示

## 对象的分类：  

1.内置对象 

[内置对象文档](https://developer.mozilla.org/zh-CN/)

```
- ES标准中定义的对象，具有一定的功能 
- 比如：`Math ` `String ` `Number ` `Boolean ` `Function`   `Object`....  
```

2.浏览器对象 

```
- 由JS的运行环境提供的对象，由浏览器提供的对象 
- 比如 BOM DOM  
```

3.自定义对象  

```
- 开发人员自己创建的对象  
```

## 对象操作

### 创建对象

1. 字面量创建对象：

```js
var obj = {
  属性名:属性值,
  属性名:属性值,
  属性名:属性值,
  //方法
  方法名:function(){
		方法体;
  }
}; 
```

例如：

```javascript
var obj = {
  name:"kcs",
  age:12,
  sex:"男",
  //方法
  say:function(){
		console.log("你好");
  }
}; 
```



2. 使用new创建对象：

```js
var 对象名 = new  Object();
```

```javascript
var obj = new Object();  
```
给new 对象，添加对象属性 、方法

```js
对象.属性名 = 属性值;  
对象["属性名"] = 属性值; //这种方式能够使用特殊的属性名 
对象.方法名 = function(){
 	代码块; 
}
```

3. 构造函数创建对象

- 构造函数将对象里相同的属性和方法抽象出来封装到函数
- 通过构造函数创建的对象，为构造函数实例化
- 通过同一个构造函数创建的对象，称为一类对象，构造函数是普通的函数，只是他的调用方式不同，直接调用，它就是普通函数，若是使用new来调用，则它就是构造函数 。

构造函数的执行流程：  

1. 创建一个新的对象  

2. 将新的对象作为函数的上下文对象（this）  

3. 执行函数中的代码  

4. 将新建的对象返回  

创建构造函数：格式

```js
function 构造函数名([参数列表]){  
    this.属性名 = 属性值;
    this.方法名 = function([参数列表]){  
        代码块;
    };  
}  
```

```js
function Person(name , age , gender){  
    this.name = name;  
    this.age = age;  
    this.gender = gender;  
    this.sayName = function(){  
        alert(this.name);  
    };  
}  
```

调用构造函数 

```
var 对象变量 =  new 构造函数名([实参列表]);
```

```js
// 方式一传参
var person = new Person("kcs",18,"男");
// 方式二传参
var person = new Person();
person.name="kcs";
person.age=18;
person.gender="男";
person.sayName();
// 输出构造函数的类型
console.log(typeof person);
```



`instanceof 使用`

- 用来检查对象是否是一个类的实例

```js
对象 instanceof 构造函数  
```

- 该对象是构造函数的实例，则返回true，否则返回false  
- **Object是所有对象的父类，所以任何对象和Object做instanceof都会返回true**  

### 调用对象的属性、方法

```js
对象.属性名 
// "属性名"可以使字符串常量，也可以是字符串变量
对象["属性名"] 

//调用方法
对象.方法名();
```

调用的对象中没有该属性，它不会报错，而是返回一个undefined  

### 删除对象中的属性 

语法：  

```javascript
delete 对象.属性名  
delete 对象["属性名"]  
```

### 变量、属性、方法、函数区别

- 变量：单独声明并赋值，直接使用变量名
- 属性：在对象里面不需要声明，调用时：`对象.属性名` 
- 方法：创建在对象里，调用`对象.方法名`
- 函数：单独声明且单独调用，单独存在

### 构造函数和对象

- 构造函数：相同部分，封装到函数，泛指一大类
- 创建对象：特指某一类，使用 `new` 创建对象进行实例化。

## 遍历

语法："属性名" in 对象 

```js
for( var key in 对象名){
	代码;
}
```

```
  循环遍历对象自身的和继承的可枚举属性(不含Symbol属性).  
```

```javascript  
var obj = {'0':'a','1':'b','2':'c'};  
  
for(var i in obj) {  
     console.log(i,":",obj[i]);  
}  
```

使用对象字面量，在创建对象时添加对象的属性 
语法： 

```javascript
var obj = {  
    属性名:属性值,  
    属性名:属性值,  
    属性名:属性值,  
    属性名:属性值  
} 
```


遍历对象  

```javascript  
for(var v in obj){  
    document.write("property：name ="+v+"value="+obj[v]+"<br/>" );
}
```



### 基本数据类型和引用数据类型 

基本数据类型 
	`String ` `Number  ` `Boolean ` `Null ` `Undefined `

引用数据类型 
	`Object ` 
**基本数据类型的数据，变量是直接保存的它的值。** 变量与变量之间是互相独立的，修改一个变量不会影响其他的变量。**引用数据类型的数据，变量是保存的对象的引用（内存地址）** 

- 如果多个变量指向的是同一个对象，此时修改一个变量的属性，会影响其他的变量
- 比较两个变量时，对于基本数据类型，比较的就是值
- 对于引用数据类型比较的是地址，地址相同才相同 



## this（上下文对象）  

调用函数时，解析器都会将一个上下文对象作为隐含的参数传递进函数。 使用this来引用上下文对象，根据函数的调用形式不同，this的值也不同。  

指向当前对象 this的不同的情况：  

1. 以函数的形式调用时，this 是window  
2. 以方法的形式调用时，this 就是调用方法的对象  
3. 以构造函数的形式调用时，this 就是新创建的对象  

## 原型（prototype）  

创建一个函数以后，解析器都会默认在函数中添加一个数prototype  

​	prototype属性指向的是一个对象，这个对象称为原型对象。  

当函数作为构造函数使用，**它所创建的对象中都会有一个隐含的属性执行该原型对象。**  

```javascript  
这个隐含的属性可以通过对象.__proto__来访问。  
```

**原型对象就相当于一个公共的区域，凡是通过同一个构造函数创建的对象他们通常都可以访问到相同的原型对象。**  

- 可以将对象中共有的属性和方法统一添加到原型对象中，  这样只需要添加一次，就可以使所有的对象都可以使用。  
- 当去访问对象的一个属性或调用对象的一个方法时，它会先自身中寻找，  如果在自身中找到了，则直接使用。  
- 如果没有找到，则去原型对象中寻找，如果找到了则使用，  **如果没有找到，则去原型的原型中寻找，**依此类推。直到找到Object的原型为止，Object的原型的原型为null，  
- 如果依然没有找到则返回undefined  

**hasOwnProperty()**  

- 这个方法可以用来检查**对象自身中**是否含有某个属性  

- 语法：对象.hasOwnProperty("属性名")  

## toString方法  

- 打印字符串格式  

```javascript  
//修改Person原型的toString  
Person.prototype.toString = function(){  
	return "Person[name="+this.name+",age="+this.age+",gender="+this.gender+"]";  
};  
```

  

## 垃圾回收（GC）  

- 当对象没有任何的变量或属性对它进行引用，将永远无法操作该对象，  该对象变成一个垃圾，这种对象过多会占用大量的内存空间，导致程序运行变慢， 这些垃圾必须进行清理。 

- 在JS中拥有自动的垃圾回收机制，会自动将这些垃圾对象从内存中销毁，  不需要也不能进行垃圾回收的操作  ，需要做的只是要将不再使用的对象设置null即可  







# JavaScript 类

## 类创建

- 类是用于创建对象的模板。

### 创建类的语法

```js
class ClassName {
  constructor() { ... }
}
```

解释：

​		使用 `class `关键字来创建一个类，类体在一对大括号 `{}`中，可以在大括号 `{}` 中定义==类成员的位置==，如方法或构造函数。每个类中包含了一个特殊的方法 `constructor()`，它是==类的构造函数==，这种方法用于==创建和初始化一个由 class 创建的对象==。



创建学生类：

```js
class Student { //创建一个Student类对象
  constructor(name, sno) { // Student类的构造方法，并且有两个参数
    this.name = name;  // 初始化name属性
    this.sno = sno;    // 初始化son属性
  }
}
```

### 使用类

```js
// 对上述创建的Student类进调用 在调用时传入两个参数，就会传递给上面name和sno
// 使用new  关键子初始化Studnet对象类
let st = new Student("kcs","22");
```

## 类表达式

> 类表达式是定义类的另一种方法。类表达式可以命名或不命名。命名类表达式的名称是该类体的局部名称。



```js
let Student = class { //创建一个匿名类（未给类命名）
  constructor(name, sno) { //两个参数
    this.name = name;  // 初始化name属性
    this.sno = sno;    // 初始化son属性
  }
}
console.log(Student.name);
// 输出 Student

//命名类
let st=class Student { //创建一个Student类对象
  constructor(name, sno) { 
    this.name = name;  
    this.sno = sno;    
  }
}
console.log(st.name);
// 输出 Student
```

### 构造方法

构造方法是一种特殊的方法：

- 构造方法名为 `constructor()`。
- 构造方法在创建新对象时会自动执行。
- 构造方法用于初始化对象属性。
- 如果不定义构造方法，JavaScript 会自动添加一个空(无参数)的构造方法。



## 类的方法

> 在使用关键字 `class` 创建一个类，除了可以使用构造方法外，还可以自定义一些属于该类的方法。



语法如下：

```js
class ClassName {
  constructor() { 代码块 }
  method_1() { 代码块 }
  method_2() { 代码块 }
  method_3() { 代码块 }
}
```

### 创建方法

为学生类创建一个age()方法，用于返回学生的年龄

```js
<p id="demo"></p>

<script>
	class Student{ //创建一个匿名类（未给类命名）
  	constructor(name, year) { //两个参数
    	this.name = name;  // 初始化name属性
    	this.year = year;    // 初始化year属性
  	}
  	age() {
      
      // date = new Date();  // 错误 必须严格 use strict 
    	let date = new Date(); // 当前的年份
    	return date.getFullYear() - this.year;//getFullYear返回一个四位数的年份
  	}
	}
	 // 使用new  关键子初始化Studnet对象类
	let student = new Student("kcs", 2001);
	document.getElementById("demo").innerHTML ="该学生 " + student.age() + " 岁了。";
</script>
```



> 严格使用 use strict ，不允许未声明的变量
>
> 类声明和类表达式的主体都执行在严格模式下。比如，构造函数，静态方法，原型方法，getter 和 setter 都在严格模式下执行。如果你没有遵循严格模式，则会出现错误



### 静态方法

静态方法是使用 static 关键字修饰的方法，又叫类方法，属于类的，但不属于对象，在实例化对象之前可以通过 `类名.方法名` 调用静态方法。静态方法不能在对象上调用，只能在类中调用。

```js
<p id="demo"></p>

class Student {
  constructor(name) {
    this.name = name;
  }
  static hello() {
    return "Hello!!";
  }
}
 
let st = new Student("kcs");
 
// 可以在类中调用 'hello()' 方法
document.getElementById("demo").innerHTML = Student.hello();
 
// 不能通过实例化后的对象调用静态方法
// document.getElementById("demo").innerHTML = noob.hello();
// 以上代码会报错
```

如果你想在对象 st 中使用静态方法，可以作为一个参数传递给它：

```js
class Student {
  constructor(name) {
    this.name = name;
  }
  static hello(x) {
    return "Hello " + x.name;
  }
}
let st = new Student("kcs");
document.getElementById("demo").innerHTML = Student.hello(st);
```



## 类关键字

| 关键字                                                       | 描述                   |
| ------------------------------------------------------------ | ---------------------- |
| [extends](https://www.runoob.com/js/jsref-class-extends.html) | 继承一个类             |
| [static](https://www.runoob.com/js/jsref-class-static.html)  | 在类中定义一个静态方法 |
| [super](https://www.runoob.com/js/jsref-class-super.html)    | 调用父类的构造方法     |

## 类继承

- 类继承使用 `extends `关键字，继承允许我们依据另一个类来定义一个类，这使得创建和维护一个应用程序变得更容易。
- `super()` 方法用于调用父类的构造函数。
- 当创建一个类时，您不需要重新编写新的数据成员和成员函数，只需指定新建的类继承了一个已有的类的成员即可。这个已有的类称为==基类（父类）==，新建的类称为==派生类（子类）==。

### 基础思想

> 哺乳动物是动物，狗是哺乳动物，因此，狗是动物等等。



<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221203214520460.png" alt="image-20221203214520460" style="zoom:50%;" />



### 创建基础类

```js
// 基类
class Animal {
    // eat() 函数
    // sleep() 函数
};
 
 
//派生类
class Dog extends Animal {
    // bark() 函数
};
```



动物类基础实现

```js
<p id="demo"></p>

<script>
  	// 父类
		class Animal {
  		constructor(name) {
    		this.sitename = name;
  		}
      // Animal 特有方法
  		present() {
    		return this.sitename+'会睡觉';
  		}
		}
		 // 基础类
		class Dog extends Animal {
  		constructor(name, age) {
    		super(name); // super()引用父类的构造方法,通过在构造方法中调用 super() 方法，调用了父类的构造方法，就可以访问父类的属性和方法。
    		this.age = age;
  		}
      // Dog 中特有的方法
  		show() {
        // 因为Dog基础了Animal 即实现了Animal的方法present
    		return this.present() + ', 它出生了 ' + this.age + ' 年。';
  		}
		}
		 // 创建Dog类对象
		let dog = new Dog("大黄", 5);
		document.getElementById("demo").innerHTML = dog.show();
</script>
```



## 访问器方法

### getter()方法

- 有一个返回值语句
- 使用get 关键字
- 没有任何参数

### setter()方法

- 使用 set 关键字
- 有一个参数（对应着类定义的属性）

### 总结

- 类中使用 `getter `和 `setter `来获取值和设置值。

- 类中添加 getter 和 setter 使用的是 get 和 set 关键字。

- **注意：**即使 getter 是一个方法，当你想获取属性值时也不要使用括号。

  `getter/setter` 方法的名称不能与属性的名称相同。

  很多开发者在属性名称前使用下划线字符 `_ `将 getter/setter 与实际属性分开

- get/set 访问器不是对象的属性，而是属性的特性，特性只有内部才用，因此在javaScript中不能直接访问他们，为了表示特性是内部值用两队中括号括起来表示如[[Value]]

```js
<script>
	class Student {
 	 constructor(name) {
    	 this._name = name;
  	 }
  	 get name() { //  获取到kcs
   	  return this._name;
 	   }
  	 set name(x) {
   	  this._name = x;
 	   }
	}
	let st = new Student("kcs"); // 初始化类，并给构造方法传递参数
	document.getElementById("demo").innerHTML = st.name;// 使用getter
  st.name = "hjy"; // 给name 设置值

</script>
```







# 函数（Function）  

函数也是一个对象，也具有普通对象的功能（属性），可以将重复的代码封装成一个函数，在需要的地方调用函数。

## 创建函数、函数声明 

```javascript
function 函数名([形参1,形参2,...,形参N]){  
语句...  
}  
```

函数表达式

```javascript
var 函数名 = function([形参1,形参2,...,形参N]){  
语句...  
};  
```

调用函数 

```
函数对象([实参1,实参2...实参N]);  
//以下为javaScript的内置函数
fun() sum() alert() Number() parseInt()  
```

```js
  //定义函数
  function getSum(){
      alert("调用了getSum函数");
  }
  //调用函数
  getSum();
```

调用函数时，函数中封装的代码会按照编写的顺序执行  

**立即执行函数** ：函数定义完，立即被调用，只会执行一次

```javascript
(function(a,b){  
    console.log("a = "+a);  
    console.log("b = "+b);  
})(123,456); 
```

## 形参和实参 

 形参：形式参数 (定义函数时给的参数)

- 定义函数时，可以在()中定义一个或多个形参，形参之间使用 , 隔开 
- 定义形参就相当于在函数内声明了对应的变量
- 形参会在调用时才赋值

 实参：实际参数 (调用函数时，给的参数)

- 调用函数时，可以在()传递实参，传递的实参会赋值给对应的形参,
- 调用函数时JS解析器不会检查实参的类型和个数，可以传递任意数据类型的值
- ==如果实参的数量大于形参，多余实参将不会赋值== 
- ==如果实参的数量小于形参，则没有对应实参的形参将会赋值undefined==  

### 返回值



返回值就是函数执行的结果，使用 return 来设置函数的返回值 

```js
return 值;
```

- return 后边的代码都不会执行，一旦执行到return语句时，函数将会立刻退出
- 可以返回任意类型的值
- 可以使用**变量**来存储返回的结果 
- 如果return后不跟值，或者是不写return则函数默认返回undefined
- 若是想返回多个值，可以使用数组封装。

### break、continue和return  

 break 

- 退出循环 

 continue 

- 跳过当次循环 

 return 

- 退出函数 

**参数，函数的实参也可以是任意的数据类型。**  



**方法（method）** 

- 可以将一个函数设置为一个对象的属性， 

- 当一个对象的属性是一个函数时， 称这个函数是该对象的方法。 

- 调用：

  - ```
    对象名.方法;
    ```

函数案例：

比较两个值的大小

```js
function getMax(num1,num2){
	num1 > num2 ? num1 : num2;
}
getMax(1,10);
```

冒泡排序：传递数组



```js
function bubbleSort(arr) {
    //外层循环控制多少趟
    for (var i = 0; i < arr.length - 1; i++) {
        //arr.length - i - 1 ：交换的次数
        for (var j = 0; j < arr.length - i - 1; j++) {
            //判断前后两个值的大小，然后进行交换
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
  return arr;
}
var result =bubbleSort([1, 56, 32, 44, 3, 23, 4, 12]);
console.log(result);
```

判断闰年

```js
<script>
    function isRunYear(year) {
        var flag = flag;
        if (year % 4 == 0 && year % 100 == 0) {
            flag = true;
        }
        return flag;
    }
    var year = isRunYear(2000);
    console.log(year);
</script>
```



## 函数的内置对象、属性、方法

`call()` 、`apply()` 

- 这两个方法都是函数对象的方法需要通过函数对象来调用  
- 通过两个方法可以直接调用函数，并且可以通过第一个实参来指定函数中this  
- 不同的是call是直接传递函数的实参而apply需要将实参封装到一个数组中传递  

`arguments  ` 

- arguments和this类似，都是函数中的隐含的参数 
- arguments是伪数组，封装函数执行过程中的实参  ，具有`length `属性，按索引方式存储数据，不具有pop、push等方法
- 所以即使不定义形参，也可以通过arguments来使用实参  
- **arguments中有一个属性callee表示当前执行的函数对象**  

`this`（调用函数的那个对象）  

this是函数的上下文对象，根据函数的调用方式不同会执向不同的对象  

1. 以函数的形式调用时，this是window  

 2. 以方法的形式调用时，this是调用方法的对象  
 3. 以构造函数的形式调用时，this是新建的那个对象  
 4. 使用call和apply调用时，this是指定的那个对象
 5. 在全局作用域中this代表window

## 作用域

- 作用域：变量的作用范围
- 提高程序的可靠性，减少命名冲突

### 1.全局作用域  

- 直接在script标签中编写的代码都运行在全局作用域中， **全局作用域在打开页面时创建，在页面关闭时销毁。** 全局作用域中有一个全局对象window，window对象由浏览器提供可以在页面中直接使用，它代表的是整个的浏览器的窗口。
- **在全局作用域中创建的变量都会作为window对象的属性保存**，在全局作用域中创建的函数都会作为window对象的方法保存 在全局作用域中创建的变量和函数可以在页面的任意位置访问
- 在函数作用域中也可以访问到全局作用域的变量
- 尽量不要在全局中创建变量

### 2.函数（局部）作用域  

- 作用的函数内

**变量提升**  变量预解析

- 在全局作用域中，使用**var关键字声明的变量会在所有的代码执行之前被声明，但是不会赋值**，可以在变量声明前使用变量。
- 在函数作用域中，使用var关键字声明的变量会在函数所有的代码执行前被声明；在函数内没有使用var关键字声明变量，则为全局变量 

**函数提升**  函数预解析

- 在全局作用域中，使用**函数声明创建的函数（function fun(){}）,会在所有的代码执行之前被创建**， 可以在函数声明前去调用函数，但是使用函数表达式`(var fun = function(){})`创建的函数没有该特性  
- 在函数作用域中，使用函数声明创建的函数，会在所有的函数中的代码执行之前就被创建好

> 变量提升：就是把变量提升提到函数的上面的地方。我么需要说明的是，变量提升只是提升变量的声明，并不会把赋值也提升上来。
> 函数提升：是把整个函数都提到前面去。
> 函数提升优先于变量提升。





### 变量作用域

- 局部变量
  - 在指定的范围内使用
  - 在函数内直接赋值，但没有声明
- 全局变量
  - 全部范围都可以使用

### 作用域链

- 内部函数访问外部函数的变量，采取链式查找的方式决定取值，由内向外查找变量

```js
var num = 123;
        
function f1() {
            
    var num = 456;

    function f2() {
        console.log(num);// 最后输出 456
    }
   f2();
}
f1();
```





# 数组（Array）  

## 概念

- 数组是指一组数据的集合，其中的每个数据被称作元素，在数组中可以存放任意类型的元素。数组是一种将一组数据存储在单个变量名下的优雅方式。
- 数组也是一个对象，是一个用来存储数据的对象和Object类似，但是它的存储效率比普通对象要高  
- 数组中保存的内容称为元素，数组使用索引（index）来操作元素  ，元素之间使用都好隔开
- ==索引指由0开始的整数==  ，通过索引获取对应的元素

## 数组的操作：  

创建数组  

```javascript  
// 使用对象
var arr = new Array();  
// 使用字面量创建空数组
var arr = [];  
```

向数组中添加元素  

语法；  

数组对象[索引] = 值;  

```javascript  
arr[0] = 123;  
arr[1] = "hello";  
```

创建数组时直接添加元素  

语法：  

```javascript
 var arr = [元素1,元素2....元素N]; 
```
 例子：
```javascript
 var arr = [123,"hello",true,null];  
```



### 新增元素

获取和修改数组的长度  

数组长度：  

- 数组.length  
- length获取到的是数组的最大索引+1 ，对于连续的数组，length获取到的就是数组中元素的个数  

修改数组的长度  

- 数组.length = 新长度  
- 如果修改后的length大于原长度，则多出的部分会空出来  
- 如果修改后的length小于原长度，则原数组中多出的元素会被删除  

向数组的最后添加元素 

- 数组[数组.length] = 值

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        var arr = ["js","java","html","css"];
        var arr1 = ["js","java","html","css"];
        for (var i = 0; i < arr.length; i++) {
            console.log(arr[i]);
        }
        arr.length=10;
        for (var i = 4; i < arr.length; i++) {
            console.log(arr[i]);
        }
        //对数组追加
        arr1[4] = "c++";
        console.log(arr1);
        //索引相同则是后者替换前者
        // 若是直接给数组名赋值 就是字符串了
    </script>
</head>
```



## 遍历数组  

- 将数组元素都访问一遍

- 遍历数组就是将数组中元素获取到，一般情况都是使用for循环来遍历数组

```javascript
for(var i=0 ; i<数组名.length ; i++){  
    //数组[i]  
}  
```


使用forEach()方法来遍历数组（不兼容IE8）  

```javascript
数组.forEach(function(value , index , obj){  
  
});  
```

forEach()方法需要一个回调函数作为参数， 数组中有几个元素，回调函数就会被调用几次 每次调用时，都会将遍历到的信息以实参的形式传递进来，  可以定义形参来获取这些信息。 

- value：正在遍历的元素 
- index：正在遍历元素的索引 
- obj：被遍历对象   



数组求和案例：

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>数组</title>
    <script>
        //1.遍历数组
        var arr = [];
        //设置数组长度
        var arraylength = prompt("请输入数组的长度：");

        for (var i = 0; i < arraylength; i++) {
            arr[i] = i + 1;
        }

        //求数组和
        var sum = 0; 
        for (var i = 0; i < arr.length; i++) {
            sum += arr[i];
        }
        //求数组值的平均 
        var avg = sum / arr.length;
        console.log(sum,avg);
        
    </script>
</head>
```

求数组中的最大值



```js
var arrmax = [1, 45, 78, 56, 12];
var max = arrmax[0];
for (var i = 1; i < arrmax.length; i++) {
    if (arrmax[i] > max) {
        max = arrmax[i];
    }
}
console.log(max);
```

刷选数组中符合条件的值，存放到新的数组中

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        //方法一 使用一个变量控制新数组的索引
        var arr = [1, 45, 78, 56, 12];
        var newArray = [];
        var j = 0;
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] >= 50) {
                //新数组的索引从0 开始
                newArray[j] = arr[i];
                j++;
            }
        }
        console.log(newArray);
        //方法二 newArray.length  newArray一开始的索引为0，所以没存一个元素，newArray.length就会增加，索引也增加
        var arr = [1, 45, 78, 56, 12];
        var newArray = [];
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] >= 50) {
                //新数组的索引从0 开始
                newArray[newArray.length] = arr[i];
            }
        }
        console.log(newArray);
    </script>
</head>

```



删除数组的指定元素，并将其他的元素放置新的数组



```js
    <script>
        //方法一 使用一个变量控制新数组的索引
        var arr = [1, 45, 120, 11, 0, 0, 0, 78, 56, 12];
        var newArray = [];
        for (var i = 0; i < arr.length; i++) {
            if (arr[i] != 0) {
                //新数组的索引从0 开始
                newArray[newArray.length] = arr[i];
            }
        }
        console.log(newArray);
    </script>
```



翻转数组元素

```js
var arr = [1, 45, 120, 11, 78, 56, 12];
var newArray = [];
//倒置 
for (var i = arr.length-1; i >=0; i--) {
    //新数组的索引从0 开始
    newArray[newArray.length] = arr[i];
}
console.log(newArray);
```



冒泡排序

- 将数组的元素进行排序（大到小、小到大）
- 一次比较两个元素，判断条件，进行交换位置

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>冒泡排序</title>
    <script>
        var arr = [1,56,32,44,3,23,4,12];
        //外层循环控制多少趟
        for (var i = 0; i < arr.length-1; i++){
            //arr.length - i - 1 ：交换的次数
            for (var j = 0; j <arr.length - i - 1; j++) {
                //判断前后两个值的大小，然后进行交换
                if (arr[j] > arr[j+1]){
                    var temp = arr[j];
                    arr[j] = arr[j+1];
                    arr[j+1] =temp;
                }
            }
        }
        console.log(arr);
    </script>
</head>
```



## 数组的方法  

| functionName | function                                                     | usage                                   |
| ------------ | ------------------------------------------------------------ | --------------------------------------- |
| push()       | 用来向数组的末尾添加一个或多个元素，并返回数组新的长度       | 语法：数组.push(元素1,元素2,元素N)pop() |
| pop()        | 用来删除数组的最后一个元素，并返回被删除的元素               |                                         |
| unshift()    | 向数组的开头添加一个或多个元素，并返回数组的新的长度         |                                         |
| shift()      | 删除数组的开头的一个元素，并返回被删除的元素                 |                                         |
| reverse()    | 可以用来反转一个数组，它会对原数组产生影响                   |                                         |
| concat()     | 可以连接两个或多个数组，它不会影响原数组，而是新数组作为返回值返回 |                                         |

### slice(sart,[end])  

- 从数组中截取指定的元素 
- ，不影响原数组，截取到的内容封装为一个新的数组并返回  

```
参数：  
	1.截取开始位置的索引（包括开始位置）  
	2.截取结束位置的索引（不包括结束位置）  
		 第二个参数可以省略不写，如果不写则一直截取到最后  
	 参数可以传递一个负值，如果是负值，则从后往前数  
```
###  splice()  

- 删除数组中指定元素，并使用新的元素替换，会将删除的元素封装到新数组中返回

```
参数：  
	1.删除开始位置的索引  
	2.删除的个数  
	3.三个以后，都是替换的元素，这些元素将会插入到开始位置索引的前边  
```
### join([splitor])  
可以将一个数组转换为一个字符串 
参数： 
需要一个字符串作为参数，这个字符串将会作为连接符来连接数组中的元素 ，如果不指定连接符则默认使用,  

### sort()  

对数组中的内容进行排序，默认是按照Unicode编码进行排序，调用以后，会直接修改原数组。可以自己指定排序的规则，需要一个回调函数作为参数 

指定排序的规则 
在sort()添加一个回调函数，来指定排序规则， 回调函数中需要定义两个形参,  浏览器将会分别使用数组中的元素作为实参去调用回调函数 ，使用哪个元素调用不确定，但是肯定的是在数组中a一定在b前边  

- 浏览器会根据回调函数的返回值来决定元素的顺序，  如果返回一个大于0的值，则元素会交换位置 ，如果返回一个小于0的值，则元素位置不变 ，如果返回一个0，则认为两个元素相等，也不交换位置  
	
- 如果需要升序排列，则返回 a-b 
	如果需要降序排列，则返回 b-a  
```  javascript
function(a,b){  
	//升序排列  
	//return a-b;  
	  
	//降序排列  
	return b-a;  
}  
```





# 常用类和方法  

## 包装类  

在JS中为提供了**三个包装类：**  `String()`  `Boolean()` `Number()`  通过三个包装类可以创建基本数据类型的对象  

```javascript
var num = new Number(2);  
var str = new String("hello");  
var bool = new Boolean(true); 
```


> ==实际应用中千万不要这么干==
>
> 当去操作一个基本数据类型的属性和方法时， **解析器会临时将其转换为对应的包装类，然后再去操作属性和方法，**  操作完成以后再将这个临时对象进行销毁。  

## Date  

日期的对象，在JS中通过Date对象来表示一个时间  

创建对象 
 创建一个当前的时间对象  

```javascript
 var d = new Date();  
```

 创建一个指定的时间对象  
```javascript
	var d = new Date("月/日/年 时:分:秒");  
```



简单倒计时案例

```js
<head>
    <meta charset="UTF-8">
    <title>倒计时</title>
    <script>
        function countDown(time) {
            // 当前事件的毫秒数
            var nowTime = +new Date();
            // 输入时间的毫秒值
            var inputTime = +new Date(time);
            // 剩余时间的总秒数
            var resultTime = (inputTime - nowTime) / 1000;
            // 天
            var day = parseInt(resultTime / 60 / 60 / 24);
            day = day < 10 ? "0" + day : day;
            // 时
            var hour = parseInt(resultTime / 60 / 60 % 24);
            hour = hour < 10 ? "0" + hour : hour;
            // 分
            var minutes = parseInt(resultTime / 60 / 60 % 24);
            minutes = minutes < 10 ? "0" + minutes : minutes;
            // 秒
            var second = parseInt(resultTime / 60 / 60 % 24);
            second = second < 10 ? "0" + second : second;

            return day + "天" + hour + "时" + minutes + "分" + second + "秒";
        }
        //调用函数
        console.log(countDown("2022-11-22 18:00:00"));
    </script>
</head>
```

### 方法：

| name              |                                                              |
| ----------------- | ------------------------------------------------------------ |
| getDate()         | 当前日期对象是几日（1-31）                                   |
| getDay()          | 返回当前日期对象时周几（0-6                                  |
| getMonth()        | 返回当前日期对象的月份（0-11）                               |
| getFullYear()     | 从 Date 对象以四位数字返回年份。                             |
| getHours()        | 返回 Date 对象的小时 (0 ~ 23)。                              |
| getMinutes()      | 返回 Date 对象的分钟 (0 ~ 59)。                              |
| getSeconds()      | 返回 Date 对象的秒数 (0 ~ 59)。                              |
| getMilliseconds() | 返回 Date 对象的毫秒(0 ~ 999)。                              |
| getTime()         | 返回当前日期对象的时间戳	 时间戳，指的是从1970年月1日 0时0分0秒，到现在时间的毫秒数，计算机底层保存时间都是以时间戳的形式保存的。 |
| Date.now()        | 可以获取当前代码执行时的时间戳                               |

## Math

Math属于一个工具类，它不需要创建对象，它里边封装了属性运算相关的常量和方法  

|                 方法                 | 说明                    |
| :----------------------------------: | :---------------------- |
|               Math.PI                | 常量，圆周率            |
|              Math.abs()              | 绝对值运算              |
|             Math.ceil()              | 向上取整                |
|             Math.floor()             | 向下取整                |
|             Math.round()             | 四舍五入取整            |
|            Math.random()             | 生成一个0~1之间的随机数 |
| `Math.round(Math.random()*(y-x)+x);` | 生成一个x~y之间的随机数 |
|            Math.pow(x,y)             | 求x的y次幂              |
|             Math.sqrt()              | 对一个数进行开方        |
|              Math.max()              | 求多个数中最大值        |
|              Math.min()              | 求多个数中的最小值      |



猜数字游戏案例：

```js
<head>
    <meta charset="UTF-8">
    <title>猜数字游戏</title>
    <script>
        //控制范围变量
        var start = 1;
        var end = 100;
        //随机生成数
        function getRandom(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + min;

        }
        //获得随机数
        var random = getRandom(start, end);
        alert("开始猜字游戏");
        //计数
        var count = 10;
        while (true) {
            var num = parseFloat(prompt("剩余" + count + "次机会，请输入" + start + "~" + end + "之前的数字："));

            if (num < random) {
                alert("猜小了");
            } else if (num > random) {
                alert("猜大了");
            } else {
                alert("恭喜你才对了");
                break;
            }
            count--;
        }
    </script>
</head>
```



## 字符串操作方法

|                             方法                             | 说明                                                         |
| :----------------------------------------------------------: | ------------------------------------------------------------ |
| ` String.prototype.padStart(maxLength, fillString='')`<br />``String.prototype.padEnd(maxLength, fillString='')`` | 填充字符串                                                   |
|                           `length`                           | 获取字符串长度                                               |
|                          `charAt()`                          | 根据索引获取指定的字符                                       |
|                        `charCodeAt()`                        | 根据索引获取指定的字符编码                                   |
|                          `concat()`                          | 拼接字符串                                                   |
|                   `String.fromCharCode()`                    | 根据字符编码获取字符                                         |
|                         `indexOf()`                          | 查找指定索引的内容，从前向后找                               |
|                       `lastIndexOf()`                        | 从一个字符串中检索指定内容，从后向前找                       |
|                    `slice(start,[end]) `                     | 根据索引截取指定的字符串内容（左开右闭）<br />传负数，则从后往前数 |
|                         ` substr()`                          | 截取字符串，参数二：截取数量                                 |
|                        `substring()`                         | 截取字符串，参数二小于参数一，会自动调整。不能负数作为参数，否则调整为0。 |
|                       `toLowerCase() `                       | 将字符串转换为小写并返回                                     |
|                       `toUpperCase() `                       | 将字符串转换为大写并返回                                     |

获取字符串最多的字符

```js
<head>
    <meta charset="UTF-8">
    <title>统计字符串最多的字符</title>
    <script>
        var str = "dbasjidbffssslndsdas";
        var s = {};
        for (var i = 0; i < str.length; i++) {
            //获取字符
            var char = str.charAt(i);
            //比较字符
            if (s[char]) {
                //存在，加一
                s[char]++;
            } else {
                s[char] = 1;
            }
        }
        console.log(s);

        //遍历属性值
        var max = 0;
        var ch = "";
        for (var key in s) {
            if (s[key] > max) {
                max = s[key];
                ch = key;
            }
        }
        console.log(max);
        console.log("最多的字符是：" + ch);
    </script>
</head>
```

​		  

# 正则表达式  

[详细解释](https://www.w3school.com.cn/js/js_regexp.asp)



正则用来定义一些字符串的规则，程序可以根据这些规则来判断一个字符串是否符合规则，也可以将一个字符串中符合规则的内容提取出来。 
创建正则表达式  

```js
var reg = new RegExp("正则","匹配模式"); 
// 注意：使用构造函数时，由于它的参数是一个字符串，而\是字符串中转义字符，如果要使用\则需要使用\\来代替  
 var reg = /正则表达式/匹配模式 （匹配模式可以多个一起写：/gi）  
```

## 语法：  

匹配模式：  

- i：忽略大小写（ignore）  
- g：全局匹配模式（默认为1次）  
- 设置匹配模式时，可以都不设置，也可以设置1个，也可以全设置，设置时没有顺序要求 
  

### 正则表达方法  

|    方法     | 说明                                                         |
| :---------: | ------------------------------------------------------------ |
| `split() `  | 指定内容将一个字符串拆分为一个数组。可以接收一个正则表达式，此时会根据正则表达式去拆分数组 |
| `match() `  | 根据正则表达式，从一个字符串中将符合条件的内容提取出来。默认情况下的match只会找到第一个符合要求的内容，找到以后就停止检索。全局匹配模式，这样就会匹配到所有的内容 |
| `replace()` | 将字符串中指定内容替换为新的内容。参数一：被替换的内容；参数二：新的内容  空串则为删除 |
|  search()   | 搜索字符串中是否含有指定内容。serach()只会查找第一个。正则表达式作为参数 |





