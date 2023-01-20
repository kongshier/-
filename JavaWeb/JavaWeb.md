> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 1.MyBatis

官网： [Mybatis ](https://mybatis.org/mybatis-3/)  https://mybatis.org/mybatis-3/

## 1.1概念

1. MyBatis是一款优秀的**持久层框架**，用于简化JDBC开发
   - 负责将数据保存到数据库的那一层代码
   - JavaEE三层架构：表现层、业务层、持久层
2. 框架
   - 框架就是一个半成品软件，是一套可重用的、通用的、软件基础代码模型
   - 在框架的基础之上构建软件编写更加高效、规范、通用、可扩展。
3. JDBC缺点
   - 硬编码   配置文件
     - 注册驱动、获取链接    写了一堆链接字符串  
     - SQL语句   也写了一堆代码字符串
   - 操作繁琐  自动完成
     - 手动设置参数
     - 手动封装结果集

## 1.2MyBatis 快速入门

步骤

1. 创建user表，添加数据
2. 创建模块，导入坐标
3. 编写MyBatis核心配置文件 –> 替换链接信息，解决硬编码问题
4. 编写SQL映射文件 -->统一管理Sql语句，解决硬编码问题
5. 编码
   1. 定义POJO类
   2. 加载核心配置文件，获取SqlSessionFactory对象
   3. 获取SqlSession对象，执行SQL语句
   4. 释放资源



### 代码

pom.xml配置文件

```xml
<!--mybatis 依赖-->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.5</version>
</dependency>

<!--mysql 驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <version>5.1.46</version>
</dependency>

<!--junit 单元测试-->
<dependency>
    <groupId>junit</groupId>
    <artifactId>junit</artifactId>
    <version>4.13</version>
    <scope>test</scope>
</dependency>

<!-- 添加slf4j日志api -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.20</version>
        </dependency>
        <!-- 添加logback-classic依赖 -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-classic</artifactId>
            <version>1.2.3</version>
        </dependency>
        <!-- 添加logback-core依赖 -->
        <dependency>
            <groupId>ch.qos.logback</groupId>
            <artifactId>logback-core</artifactId>
            <version>1.2.3</version>
        </dependency>
```



mybatis-config.xml

```xml
<typeAliases>
    目标对象的包
    <package name="com.itheima.pojo"/>
</typeAliases>

<!--
environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
-->
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>

    <environment id="test">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>
</environments>
<mappers>
    <!--加载sql映射文件-->
    类路径
   <!-- <mapper resource="com/itheima/mapper/UserMapper.xml"/>-->

    <!--Mapper代理方式-->
    <package name="com.itheima.mapper"/>

</mappers>
```



Demo.java

```java
/**
 * Mybatis 快速入门代码
 
 2、3两点就把之前的jdbc给替换了
 */
public class MyBatisDemo {

    public static void main(String[] args) throws IOException {

        //1. 加载mybatis的核心配置文件，获取 SqlSessionFactory
        //从官网复制过来
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);

        //2. 获取SqlSession对象，用它来执行sql
        SqlSession sqlSession = sqlSessionFactory.openSession();
        //3. 执行sql 参数是命名空间的名称 test是上一级的名称 selectAll才是想要的查询名称，一级级通过，方便查询
        List<User> users = sqlSession.selectList("test.selectAll");
        System.out.println(users);
        //4. 释放资源
        sqlSession.close();
    }
}
```



## 1.3Mapper

目的

- 解决原生方式中硬编码
- 简化后期执行SQL

### 1.3.1Mapper代理开发规则

1. 定义与SQL映射文件同名的Mapper接口，并且将Mapper接口和SQL映射文件放置在同一目录下
   - 在资源文件夹中新建包时，把   .  用 /  代替  这样在文件中才会体现分层结构  
2. 设置SQL映射文件的namespace属性为Mapper接口全限定名
3. 在Mapper|接口中定义方法，方法名就是SQL映射文件中sql语句的id，并保持参数类型和返回值类型一致
4. 编码
   1. 通过SqlSession的getMapper方法获取Mapper接口的代理对象
   2. 调用对应方法完成sql的执行



==细节:如果Mapper接口名称和SQL映射文件名称相同，并在同一目录下，则可以使用包扫描的方式简化SQL映射文件的加载==

在核心的配置文件xml中

```xml
<mappers>
    <!--加载sql映射文件-->
   <!-- <mapper resource="com/itheima/mapper/UserMapper.xml"/>-->

    <!--Mapper代理方式  包扫描方式 指定包的路径 -->
    <package name="com.itheima.mapper"/>

</mappers>
```



## 1.4Mybatis.xml核心配置为文件

要安装官方文件的顺序 进行配置

```xml
<!--
environments：配置数据库连接环境信息。可以配置多个environment，通过default属性切换不同的environment
-->
<environments default="development">
    <environment id="development">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>

    <environment id="test">
        <transactionManager type="JDBC"/>
        <dataSource type="POOLED">
            <!--数据库连接信息-->
            <property name="driver" value="com.mysql.jdbc.Driver"/>
            <property name="url" value="jdbc:mysql:///mybatis?useSSL=false"/>
            <property name="username" value="root"/>
            <property name="password" value="123456"/>
        </dataSource>
    </environment>
</environments>
```





# 2.JavaSpring

## 2.1js简介

JavaScript是一门跨平台、==面向对象的脚本语言==，来控制网页行为的，它能使网页可交互

W3C标准:网页主要由三部分组成

- 结构:HTML
- 表现: CSS
- 行为: JavaScript

JavaScript和Java是完全不同的语言，不论是概念还是设计。但是基础语法类似。



## 2.2JavaScript 引入方式

==引入方式==

1. 内部脚本  ：将JS代码定义在HTML页面中

   - 在HTML文档中可以在任意地方，放置任意数量的<script> 
   - 一般把脚本置于<body>元素的底部，可改善显示速度，因为脚本执行会拖慢显示

2. 外部脚本：将JS代码定义在外部JS文件中，然后引入到HTML页面中

   



## 2.3JavaScript基础语法

### 2.3.1书写语法

- 区分大小写: 与Java一样，变量名、函数名以及其他一切东西都是区分大小写的

- ==每行结尾的分号可有可无==

- 注释:

  - 单行注释: //注释内容

  - 多行注释:/* 注释内容 */  

- 大括号表示代码块

### 2.3.2输出语句

- 使用==windqw.alert()== ：写入警告框
- 使用==document.write()==   ：写入HTML输出
- 使用==console.log()==   ：写入浏览器控制台

### 2.3.1变量

1. 使用 var 关键字 （variable的缩写） 声明变量 
   - 可以存放不同类型的值
2. 其他的规则和Java一样

var：

1. ==作用域：全局变量==
2. 变量可以重复控制：后面的变量值会把前面同变量名的值给覆盖

let：

1. 作用域：当前的大括号
2. 变量不允许重复定义

==const 关键字  用于声明只读的常量== 常量值不能再次改变

### 2.3.1数据类型

1. 原始类型
   1. number  ：数字 （整数、小数、NaN）
   2. string  ：字符、字符串、单双引号皆可
   3. boolean  ：布尔
   4. null  ：对象为空
   5. undefined ：==声明当前变量未初始化==  默认值是underfined
2. 引用类型
   - 

### 2.3.1运算符

==typeof  运算符== 判断当前的值是什么类型的数据类型

![image-20220317224643306](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220317224643306.png)

==全等于==  ：判断类型是否一样，如果不一样，直接返回false，再去比较其值

```js
类型转换：
    * 其他类型转为number：
        1. string: 按照字符串的字面值，转为数字.如果字面值不是数字，则转为NaN。一般使用parseInt
        2. boolean: true 转为1，false转为0

    * 其他类型转为boolean：
        1. number:0和NaN转为false，其他的数字转为true
        2. string:空字符串转为false，其他的字符串转为true
        3. null:false
        4. undefined:false
```



### 2.3.1流程控制语句

- fi
- Switch
- for   使用let 定义  防止全局都是  i  的值
- while 
- do…while

### 2.3.1函数

- 是被设计为执行指定任务的代码块

==定义方式一==

- JavaScript 函数通过function关键字进行定义

  > function functionName（参数1，参数2 。。。）{
  >
  > 要执行的代码
  >
  > }

注意 ：

- ==形式参数不需要类型==。因为JavaScript是弱类型语言
- ==返回值也不需要定义类型==。可以在函数内部直接使用return返回即可

==定义方式二==

~~~js
var functionName = function(参数列表){
    执行代码
}
~~~

==函数调用可以传递任意个数参数==  只和参数的名称有关

## 2.4JavaScript常用对象

文档：https://www.w3school.com.cn/js/js_objects.asp

1. ### Array  定义数据

   ~~~js
   方式一：
   var 变量名 = new  Array (元素列表) ;
   fe:
   var a = new Array(1,2,3);
   
   方式二：
   var 变量名  = [元素列表] ;
   var arr2 = [132];
   ~~~

==JavaScript数组相当于Java中的集合 ，变长变类型==   不会出现数组下标超出

#### 属性：

1. length :长度

#### 方法

1. push:添加方法 往数组中添加元素
2. splice：删除元素  
   - 有两个参数 1（起始位置索引）， 2（结束位置索引）

### 2.String

#### 定义

~~~js
    //方式一
    var str1 = new String("abc");
    //方式二
    var str2 = "abc";
    var str3 = 'abc';

    //length
    // alert(str3.length);
    // trim():去除字符串前后两端的空白字符
    var str4 = '  abc   ';
    alert(1 + str4.trim() + 1);
~~~



### 3.自定义对象

```js
var 对象名称 = {
    属性名称1 : 属性值1,
    属性名称2 : 属性值2,
    函数名称: function (形参列表){
    }
};

var person = {
    name : "zhangsan",
    age : 23,
    eat: function (){
        alert("干饭~");
    }
};
//调用函数
    alert(person.name);
    alert(person.age);

    person.eat();

```

## 2.5BOM

### 4.Window对象

- 浏览器窗口对象

~~~js
window.alter(0);   window.可以省略
~~~

#### 方法

```js
 alert
 window.alert("abc");
 alert("bbb");

// confirm，点击确定按钮，返回true，点击取消按钮，返回false
var flag = confirm("确认删除？");

//alert(flag);

if(flag){
    //删除逻辑
}

// 定时器
/*
    setTimeout(function,毫秒值): 在一定的时间间隔后执行一个function，只执行一次

    setInterval(function,毫秒值):在一定的时间间隔后执行一个function，循环执行
 */
//zhi'hui
setTimeout(function (){
    alert("hehe");
},3000);
//每隔两秒就弹一次弹窗
setInterval(function (){
    alert("hehe");
},2000);
```

​	==弹窗==

1. alter ：弹出警告框 有一段消息，和确定按钮

2. comfirm：显示带有一段消息以及确认和取消的对话框

   ==定时器：==

3. setInterval() ：安装指定的周期来调用函数或计算表达式

4. setTimeout ：指定毫秒数后调用的函数或计算表达式

开灯案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JavaScript演示</title>
</head>
<body>



<input type="button" onclick="on()" value="开灯">
<img id="myImage" border="0" src="../imgs/off.gif" style="text-align:center;">
<input type="button" onclick="off()" value="关灯">


<script>

    function on(){
        document.getElementById('myImage').src='../imgs/on.gif';
    }

    function off(){
        document.getElementById('myImage').src='../imgs/off.gif'
    }

    //设置一个变量控制灯的开关
    var x = 0;

    // 根据一个变化的数字，产生固定个数的值； 两种可能 : x % 2    三种可能：  3   x % 3
    //定时器
    setInterval(function (){

        if(x % 2 == 0){
            on();
        }else {
            off();
        }
        x ++;
    },1000);

</script>
</body>
</html>
```

### 5.History历史记录对象

~~~js
windows.history.方法();
history.方法()
~~~

### 6.Location 地址栏对象

~~~js
windows.location.方法();
location.方法()
~~~

- href属性 获取当前地址栏的url

```js
//3秒跳转到首页
document.write("3秒跳转到首页...");
setTimeout(function (){
    location.href = "https://www.baidu.com"
},3000);
```

## 2.6DOM  文档对象模型

- Document：整个文档对象
- Element：元素对象
- AttributeL：属性对象
- Text：文本对象
- Comment：注释对象



![image-20220319213115964](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220319213115964.png)

js通过DOM，就能够对HTML进行操作

- 改变HTML元素的内容
- 改变HTML的元素样式
- 对DOM事件作出响应
- 添加和删除HTML元素

### 1.获取Element对象

1. 获取:使用Document对象的方法来获取
   1. getElement==Byld==:根据id属性值获取，返回一个Element对象
   2. getElements==ByTagName==:根据标签名称获取，返回Element对象数组
   3. getElements==ByName:==根据name属性值获取，返回Element对象数组
   4. getElements==ByClassName==:根据class属性值获取，返回Element对象数组



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<img id="light" src="../imgs/off.gif"> <br>

<div class="cls">传智教育</div>   <br>
<div class="cls">黑马程序员</div> <br>

<input type="checkbox" name="hobby"> 电影
<input type="checkbox" name="hobby"> 旅游
<input type="checkbox" name="hobby"> 游戏
<br>

<script>
    //1. getElementById：根据id属性值获取，返回一个Element对象
    var img = document.getElementById("light");
     alert(img);

    //2. getElementsByTagName：根据标签名称获取，返回Element对象数组
    var divs = document.getElementsByTagName("div");
     alert(divs.length);
    /*
        style:设置元素css样式
        innerHTML：设置元素内容
    */
    for (let i = 0; i < divs.length; i++) {
        //divs[i].style.color = 'red';
       //把div里面的文本内容全部改成以下的文本
        divs[i].innerHTML = "呵呵";
    }

    //3. getElementsByName：根据name属性值获取，返回Element对象数组
    var hobbys = document.getElementsByName("hobby");
    for (let i = 0; i < hobbys.length; i++) {
        alert(hobbys[i]);
        //复选框处于选中的状态
        hobbys[i].checked = true;
    }

    //4. getElementsByClassName：根据class属性值获取，返回Element对象数组
    var clss = document.getElementsByClassName("cls");
    for (let i = 0; i < clss.length; i++) {
        alert(clss[i]);
    }
</script>
</body>
</html>
```



## 2.7事件监听

- JavaScript可以在事件被侦听时执行

### 2.7.1.事件绑定

事件绑定的方式

#### 方式一

- 通过HTML标签中的事件属性进行绑定
- 会和html代码耦合在一起

#### 方式二（推荐）

- 通过DOM元素属性绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="点我" onclick="on()"> <br>
<input type="button" value="再点我" id="btn">
<script>
    //方式一
    function on(){
        alert("我被点了");
    }
    //方式二
    document.getElementById("btn").onclick = function (){
        alert("我被点了");
    }
</script>
</body>
</html>
```



### 2.7.2.常见事件

1. onblur ：失去焦点 ，文本输入框
2. onfocus：获得焦点
3. onchange：文本内容改变
4. onclinck：点击事件
5. onkeydown：键盘被按下
6. onmouseout：鼠标移开
7. onmouseover：鼠标移到元素上

```html
<body>
<form id="register" action="#" >
    <input type="text" name="username" />
    <input type="submit" value="提交">
</form>
<script>
    document.getElementById("register").onsubmit = function (){
        //onsubmit 返回true，则表单会被提交，返回false，则表单不提交
        return true;
    }
</script>
</body>
```

### 表单验证（案例）

1. 当输入框失去焦点时：验证输入内容是否符合要求
2. 当点击注册按钮时，判断所有输入框的内容是否都符合要求，如果不符合则阻止表单提交

![image-20220319225140827](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220319225140827.png)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>欢迎注册</title>
    <link href="../css/register.css" rel="stylesheet">
</head>
<body>

<div class="form-div">
    <div class="reg-content">
        <h1>欢迎注册</h1>
        <span>已有帐号？</span> <a href="#">登录</a>
    </div>
    <form id="reg-form" action="#" method="get">

        <table>

            <tr>
                <td>用户名</td>
                <td class="inputs">
                    <input name="username" type="text" id="username">
                    <br>
                    <span id="username_err" class="err_msg" style="display: none">请输入正确的用户名！</span>
                </td>

            </tr>

            <tr>
                <td>密码</td>
                <td class="inputs">
                    <input name="password" type="password" id="password">
                    <br>
                    <span id="password_err" class="err_msg" style="display: none">密码格式有误</span>
                </td>
            </tr>

            <tr>
                <td>手机号</td>
                <td class="inputs"><input name="tel" type="text" id="tel">
                    <br>
                    <span id="tel_err" class="err_msg" style="display: none">手机号格式有误</span>
                </td>
            </tr>

        </table>

        <div class="buttons">
            <input value="注 册" type="submit" id="reg_btn">
        </div>
        <br class="clear">
    </form>

</div>


<script>

    //1. 验证用户名是否符合规则
    //1.1 获取用户名的输入框
    var usernameInput = document.getElementById("username");

    //1.2 绑定onblur事件 失去焦点
    usernameInput.onblur = checkUsername;

    function checkUsername() {
        //1.3 获取用户输入的用户名
        var username = usernameInput.value.trim();

        //1.4 判断用户名是否符合规则：长度 6~12,单词字符组成
        var reg = /^\w{6,12}$/;
        var flag = reg.test(username);

        //var flag = username.length >= 6 && username.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("username_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("username_err").style.display = '';
        }

        return flag;
    }


    //2. 验证密码是否符合规则
    //2.1 获取密码的输入框
    var passwordInput = document.getElementById("password");

    //2.2 绑定onblur事件 失去焦点
    passwordInput.onblur = checkPassword;

    function checkPassword() {
        //2.3 获取用户输入的密码
        var password = passwordInput.value.trim();

        //2.4 判断密码是否符合规则：长度 6~12
        var reg = /^\w{6,12}$/;
        var flag = reg.test(password);

        //var flag = password.length >= 6 && password.length <= 12;
        if (flag) {
            //符合规则
            document.getElementById("password_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("password_err").style.display = '';
        }
        return flag;
    }


    //3. 验证手机号是否符合规则
    //3.1 获取手机号的输入框
    var telInput = document.getElementById("tel");

    //3.2 绑定onblur事件 失去焦点
    telInput.onblur = checkTel;

    function checkTel() {
        //3.3 获取用户输入的手机号
        var tel = telInput.value.trim();

        //3.4 判断手机号是否符合规则：长度 11，数字组成，第一位是1

        //var flag = tel.length == 11;
        //以1开头的0-9的数字并且至少有10数字
        var reg = /^[1]\d{10}$/;
        var flag = reg.test(tel);
        if (flag) {
            //符合规则
            document.getElementById("tel_err").style.display = 'none';
        } else {
            //不合符规则
            document.getElementById("tel_err").style.display = '';
        }

        return flag;
    }

    //1. 获取表单对象
    var regForm = document.getElementById("reg-form");

    //2. 绑定onsubmit 事件
    regForm.onsubmit = function () {
        //挨个判断每一个表单项是否都符合要求，如果有一个不合符，则返回false

        var flag = checkUsername() && checkPassword() && checkTel();

        return flag;
    }

</script>
</body>
</html>
```





# 3.Web核心



## JavaWeb技术栈

- ==B/S架构:== Browser/Server，浏览器/服务器架构模式，它的特点是，客户端只需要浏览器，应用程序的逻辑和数据都存储在服务器端。浏览器只需要请求服务器，获取Web资源，服务器把Web资源发送给浏览器即可
  - 好处：易于维护升级，服务器端升级后，客户端无需任何 部署就可以使用到新版本
- 静态资源：HTML，CSS ，JavaSpring 图片等
- 动态资源：Servlet、JSP等
- 数据库：存储数据

# 4.HTTP

- 概念：Hyper Text  Transfer Protocol ，超文本传输协议，规定了浏览器和服务器之间 数据传输的规则



HTTP协议特点：

1. 基于TCP协议：面向链接，安全
2. 基于请求-响应模型的：一次请求对应一次响应
3. HTTP协议是无状态的协议：对于事务处理没有记忆能力。每次请求-响应都是==独立的==  :后一次不能请求前一次数据
   - 优点：速度快
   - 缺点：多次请求间不能共享数据  。Java中使用会话技术（Cookie、Seesion）解决这个问题

## 4.1HTTP-请求数据格式

请求数据分为3部分：

1. 请求行：
   - 请求数据的第一行。其中GET表示请求方式，/  表示请求资源路径，HTTP/1.1表示协议版本
2. 请求头：第二行开始，格式为key：value形式
3. 请求体：POST请求的最后一部分，存放请求参数



常见的请求头：

- Host:表示请求的主机名
- User-Agent:浏览器版本，例如Chrome浏览器的标识类似Mozilla/5.0 ...Chrome/79，IE浏览器的标识类似Mozilla/5.o (Windows NT ...) like Gecko;
- Accept:表示浏览器能接收的资源类型，如text/*，image/*或者*/*表示所有;
- Accept-Language:表示浏览器偏好的语言，服务器可以据此返回不同语言的网页;
- Accept-Encoding:表示浏览器可以支持的压缩类型，例如gzip, deflate等。

GET和POST的区别：

1. ==GET==请求==请求参数==在==请求行==中，没有请求体。==POST==请求的==请求参数==在==请求体==中
2. GET请求请求参数大小有限制，POST没有。

## 4.2HTTP-响应数据格

响应数据分为3部分：

1. 响应行：
   - 响应数据的第一行。其中HTTP/1.1表示协议版本，200表示响应状态码，OK表示状态码描述
2. 响应头：第二行开始，格式为key：value形式
3. 响应体：最后一部分，存放响应数据

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220321210657394.png" alt="image-20220321210657394" style="zoom:80%;" />

# 5.JSP

- 概念： Java Service Pages： Java服务端页面 

- 一种动态网页技术，其中既可以定义HTML，JS，CSS等静态内容，还可以定义Java代码的动态内容
- JSP= HTMl + java
- JSP的作用：简化开发，避免了在Servlet中直接输出HTML标签



## 5.1JSP的快速入门

步骤：

1. 带入JSP做标配
2. 创建JSP 文件
3. 编写HTML标签和Java代码

## 5.2JSP原理

- ==Java本质上就是一个Servlet==
- JSP在被访问时，由JSP容器(Tomcat)将其转换为Java文件(Servlet)，在由JSP容器(Tomcat)将其编译，最终对外提供服务的其实就是这个字节码文件

## 5.3脚本

- jsp脚本用于在JSP页面内定义Java代码
- Java脚本分类
  1. ==<%...%>==:内容会直接放到==_jspService()方法====之中==
  2. _==<%=..%>:==内容会放到 out.print()中，作为==out.print()的参数==_
  3. ==<%!...%>==:内容会放到 ==jspService()方法之外==，被类直接包含

```jsp
<%@ page import="com.itheima.pojo.Brand" %>
<%@ page import="java.util.List" %>
<%@ page import="java.util.ArrayList" %>
<%@ page contentType="text/html;charset=UTF-8" language="java" %>

<%
    // 查询数据库
    List<Brand> brands = new ArrayList<Brand>();
    brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
    brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
    brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));

%>
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="新增"><br>
<hr>
<table border="1" cellspacing="0" width="800">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>
    </tr>
    
    <%
    //需要注意是<% %>  可以阶段进行写这里在中间就能写进去html代码
        for (int i = 0; i < brands.size(); i++) {
            Brand brand = brands.get(i);
    %>

    <tr align="center">
        <td><%=brand.getId()%></td>
        <td><%=brand.getBrandName()%></td>
        <td><%=brand.getCompanyName()%></td>
        <td><%=brand.getOrdered()%></td>
        <td><%=brand.getDescription()%></td>

        <%--状态逻辑判断 里面进行了代码的截断--%>
        <%
            if(brand.getStatus() == 1){
                //显示启用
        %>
            <td><%="启用"%></td>
        <%
            }else {
                // 显示禁用
        %>
            <td><%="禁用"%></td>
        <%
            }
        %>

        <td><a href="#">修改</a> <a href="#">删除</a></td>
    </tr>

    <%
        }
    %>
   
</table>
</body>
</html>
```



## 5.4JSP缺点：

- 由于JSP页面内，既可以定义HTML 标签，又可以定义Java代码，造成了以下问题:

  1.书写麻烦:特别是复杂的页面
  2.阅读麻烦
  3.复杂度高:运行需要依赖于各种环境，JRE，JSP容器，JavaEE...

  4.占内存和磁盘:JSP会自动生成.java和.class文件占磁盘，运行的是.class文件占内存

  5.调试困难:出错后，需要找到自动生成的.java文件进行调试

  6.不利于团队协作:前端人员不会Java，后端人员不精HTML

==JSP逐渐退出历史舞台。。。==

JSP 简化了Servlet代码，但是还是不便于编写代码



 ![image-20220321224135735](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220321224135735.png)

不要在JSP里面==直接==写Java代码  ：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220321224428790.png" alt="image-20220321224428790" style="zoom:80%;" />



使用EL表达式和JSTL标签替换JSP中的Java代码

==EL表达式是用来获取替换数据的代码==

==JSTL标签是用来替换循环遍历的代码==



# 6.EL表达式 

- 用于简化JSP页面内的代码

- 主要功能：获取数据

- 语法 ：${expression}

- ~~~xml
  ${brand}  //获取域中存储的key为brands的数据
  ~~~

1. 准备数据
2. 存储到request域中
3. 转发到jsp文件中

```java
@WebServlet("/demo1")
public class ServletDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 准备数据
        List<Brand> brands = new ArrayList<Brand>();
        brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
        brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
        brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));


        //2. 存储到request域中
        request.setAttribute("brands",brands);

        //3. 转发到 el-demo.jsp
        request.getRequestDispatcher("/el-demo.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```



JavaWeb中的四大域对象：

1. page：当前页面有效
2. request：当前请求有效
3. session：当前会话有效
4. application：当前应用有效

==el表达式获取数据：会依次从这四个域中寻找，直到找到为止==



# 7.JSTL-if&foreach

## 7.1JSTL 标签

- JSP标准标签库（Jsp Standarded Tag Library）, 使用标签取代JSP页面上的Java代码

## 7.2 快速入门< c:if >

1. 导入坐标

   ```xml
   <!--jstl-->
   <dependency>
       <groupId>jstl</groupId>
       <artifactId>jstl</artifactId>
       <version>1.2</version>
   </dependency>
   
   <dependency>
       <groupId>taglibs</groupId>
       <artifactId>standard</artifactId>
       <version>1.1.2</version>
   </dependency>
   ```

2. 在JSP页面上引入JSTL标签库

   ~~~jsp
   <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
   ~~~

3. 使用< c:if >

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
    <%--
        c:if：来完成逻辑判断，替换java  if else
    --%>
<%--    <c:if test="true">
        <h1> true</h1>
    </c:if>

    <c:if test="false">
        <h1> false</h1>
    </c:if>--%>
    <c:if test="${status ==1}">
        启用
    </c:if>

    <c:if test="${status ==0}">
        禁用
    </c:if>
</body>
</html>
```



## 7.3快速入门< c:foreach >

- items:被遍历的容器
- var ：遍历产生的临时变量
- varStatus:遍历状态对象

```jsp
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<input type="button" value="新增"><br>
<hr>
<table border="1" cellspacing="0" width="800">
    <tr>
        <th>序号</th>
        <th>品牌名称</th>
        <th>企业名称</th>
        <th>排序</th>
        <th>品牌介绍</th>
        <th>状态</th>
        <th>操作</th>

    </tr>
    <c:forEach items="${brands}" var="brand" varStatus="status">
        <tr align="center">
            <%--<td>${brand.id}</td>--%>
            <%--<td>${status.index}</td>--%>
                <%--status 中有两个属性：index是从0开始 count是从1开始--%>
            <td>${status.count}</td>
            <td>${brand.brandName}</td>
            <td>${brand.companyName}</td>
            <td>${brand.ordered}</td>
            <td>${brand.description}</td>
            <c:if test="${brand.status == 1}">
                <td>启用</td>
            </c:if>
            <c:if test="${brand.status != 1}">
                <td>禁用</td>
            </c:if>
            <td><a href="#">修改</a> <a href="#">删除</a></td>
        </tr>
    </c:forEach>
</table>
<hr>

<%--普通for循环
    begin：开始值
    end：结束值
    step：步长，增长的量
    var:循环变量
--%>
<c:forEach begin="1" end="10" step="1" var="i">
    <a href="#">${i}</a>
</c:forEach>
</body>
</html>
```



Servlet服务端

```Java
package com.itheima.web;

import com.itheima.pojo.Brand;
@WebServlet("/demo1")
public class ServletDemo1 extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        //1. 准备数据
        List<Brand> brands = new ArrayList<Brand>();
        brands.add(new Brand(1,"三只松鼠","三只松鼠",100,"三只松鼠，好吃不上火",1));
        brands.add(new Brand(2,"优衣库","优衣库",200,"优衣库，服适人生",0));
        brands.add(new Brand(3,"小米","小米科技有限公司",1000,"为发烧而生",1));
        //2. 存储到request域中
        request.setAttribute("brands",brands);
        request.setAttribute("status",1);

        //3. 转发到 jstl-foreach.jsp
        request.getRequestDispatcher("/jstl-foreach.jsp").forward(request,response);
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        this.doGet(request, response);
    }
}
```



# MVC模式

MVC：分层开发模式

- M：Model
- V：view
- C：controller

## MVC好处

- 职责单一，互不影响
- 有利于分工协作
- 有利于组件重用

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323155420576.png" alt="image-20220323155420576" style="zoom:80%;" />

## 三层架构

1. 表现层
   - 接受请求。封装数据，==调用业务逻辑层==，响应数据
2. 业务逻辑层
   - 对业务逻辑进行封装，==组合数据访问层层中==基本功能，形成复杂的业务逻辑功能
3. 数据访问层
   - 对数据的CRUD基本操作



![image-20220323160037472](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323160037472.png)





## MVC和三层结构的联系



![image-20220328162516485](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220328162516485.png)



# 会话跟踪技术



- 会话：用户第一次打开浏览器，访问web服务器的资源，则会话建立，直到有一方断开连接，会话就会结束。在一次会话中可以包含==多次请求和响应。==
- 会话跟踪：一种维护浏览器状态的方法，==服务器需要识别多次请求是否来自于同一浏览器==，以便在==同一次会话的多次请求间共享数据==
- HTTP协议是==无状态==的，每次浏览器向服务器请求时，服务器都会将该请求，视为新的请求，因此我们需要会话跟踪技术来实现会话内数据共享

## 实现方式:

1. ==客户端==会话跟踪技术：==Cookie==
2. ==服务端==会话跟踪技术：==Session==







# 8.cookie（客户端）

- 客户端会话技术，将数据保存到客户端，以后每次请求都携带Cookie数据进行访问

## 8.1Cookie的基本使用



发送为一个页面

接受为另一个页面

就能实现两个不同的



1. 发送Cookie

   1. 创建Cookie对象，设置数据

      ```java
      //1. 创建Cookie对象
      Cookie cookie = new Cookie("username","zs");
      ```

   2. 发送Cookie到客户端：使用response对象  response.addCookie()方法

      ~~~Java 
      //2. 发送Cookie，response
      response.addCookie(cookie);
      ~~~

      

2. 获取Cookie

   1. 获取客户端携带的所有Cookie，使用response对象

      ```java
      //1. 获取Cookie数组
      Cookie[] cookies = request.getCookies();
      ```

   2. 遍历数组，获取每一个Cookie对象：for

      ```java
      //2. 遍历数组
      for (Cookie cookie : cookies) {
          //3. 获取数据
          String name = cookie.getName();
          if("username".equals(name)){
              String value = cookie.getValue();
              System.out.println(name+":"+value);
              break;
          }
      }
      ```

   3. 使用Cookie对象方法获取数据

      - cookie.getName()
      -  cookie.getValue()



## 8.2Cookie的原理

1. Cookie的实现是基于HTTP协议
   - 响应头：set-cookie
   - 请求头：cookie

![image-20220323164721317](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323164721317.png)



浏览器会讲所有的cookie对象获取到



## 8.3Cookie的使用细节

1. Cookie存活时间

   - 默认情况下：Cookie存储在浏览器内存中，当浏览器关闭，内存释放，则Cookie被销毁
   - setMaxAge(int seconds )：设置Cookie存活时间
     1. 正数：将Cookie写入浏览器所在电脑的硬盘，==持久化存储==。到时间自动删除
     2. 负数：默认值，Cookie在当前浏览器内存中，当浏览器关闭，则Cookie被销毁
     3. 零：删除对应Cookie

2. Cookie中文设置

   ==tomcat8后的版本，支持存入中文，但是有一些特殊字符还是会不支持==

   - Cookie不能直接存储中文

   - 如需要存储，则需要转编码：URL编码

     ```java
     String value = "张三";
     //URL编码  
     value = URLEncoder.encode(value, "UTF-8");
     System.out.println("存储数据："+value);
     Cookie cookie = new Cookie("username",value);
     ```

     URL解码：因为前面存储的中文输出是URL的编码，要进行解码才会显示出中文

     ```java
     //URL解码
     value = URLDecoder.decode(value,"UTF-8");
     ```

# 9.session

- ==服务端== 会话跟踪技术：将数据保存到服务端
- Java提供==HttpServlet接口==，来实现一次会话的==多次请求间数据共享数据==  要继承HttpServlet

## 9.1session基本使用

1. 获取Session对象
2. Session对象功能
   1. void setsetAttribute(String name, Object o)：存储数据到Session域中
   2. Object getsetAttribute(String name)：根据key，获取值
   3. void removesetAttribute(String name)：根据key，删除该键值对



![image-20220323172657527](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323172657527.png)



```java
//存储到Session中
//1. 获取Session对象
HttpSession session = request.getSession();
System.out.println(session);
//2. 存储数据
session.setAttribute("username","zs");
```



```java
//获取数据，从session中
//1. 获取Session对象
HttpSession session = request.getSession();
//2. 获取数据
Object username = session.getAttribute("username");
System.out.println(username);
```





## 9.2session原理

- Session的基于Cookie实现的
- ==一次会话的多次请求之间都是获取同一个会话对象==



![image-20220323174210614](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323174210614.png)





## 9.3Session使用细节

1. Session钝化、活化

   - 服务器重启之后，Session中的数据还是保留，并不会丢失  ，当再次获取时，id会改变
   - 钝化：在服务器正常关闭后，Tomcat会自动将Session数据写入硬盘的文件中  。钝化是关闭服务器，把数据存在服务器的硬盘上
   - 活化：再次启动服务器后，从文件中加载数据到Session中

   

2. Session销毁

   1. 默认情况下，无操作，30分钟自动销毁  在web.xml配置

      ```xml
      <session-config>
          <session-timeout>30</session-timeout>
      </session-config>
      ```

   2. 调用Session对象的invalidate方法

      session.invalidate();



## 小结

- Cookie和Session都是用来完成一次会话多次请求间数据共享的
- 区别
  - 存储位置：Cookie是将数据存储在客户端，Session将数据存储在服务端
  - 安全性：Cookie不安全，Session安全
  - 数据大小：Cookie最大3km，Session无大小限制
  - 存储时间：Cookie可以长时期存储，Session默认30分钟,到时间就会重新登录
  - 服务器性能：Cookie不占服务器资源，Session占用服务器资源

cookie是保存未登录用户的数据

session是保存登录用户的数据



# 10.FIlter

- 概念:Filter表示过滤器，是JavaWeb==三大组件(Servlet、Filter、Listener)==之一
- 过滤器可以把对==资源的请求拦截==下来，从而实现一些特殊的功能。
- 过滤器一般完成一些==通用的操作==。比如:权限控制、统一编码处理、敏感字符处理等等



## 10.1Filter快速入门

步骤：

1. 定义类，实现FIlter接口，并重写其所有方法
2. 配置Filter==拦截资源==的路径：在类上定义@WebFilter注解
3. 在doFilter方法中输出一句话，并放行

```Java
@WebFilter("/*")
public class FilterDemo implements Filter {
    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
        //1. 放行前，对 request数据进行处理
        System.out.println("1.FilterDemo...");

        //放行 若是不放行 就会被拦截下来，控制台会有打印输出
        chain.doFilter(request,response);     
    }
    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
    }
    @Override
    public void destroy() {
    }
}
```



## 10.2Filter执行流程

1. 放行后访问对应资源，资源访问完成后，还会回到filter中
2. 回到了Filter中之后，是执行放行后的逻辑



~~~mermaid
graph LR 
a(执行放行前逻辑)-->b(放行)-->c(访问资源)-->d(执行后的逻辑)
~~~





![image-20220323190227826](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323190227826.png)





## 10.3Filter使用细节

1. Filter拦截路径配置  （根据需求，配置不同的拦截资源路径）
   - 拦截具体的资源：/index.jsp ：只有访问index.jsp 时才会被拦截
   - 目录拦截：/user/* ：访问/user下的所有资源，都会被拦截
   - 后缀名拦截：. jsp ：访问后缀名为jsp的资源，都会被拦截
   - 拦截所有：/*：访问所有资源，都会被拦截
2. 过滤器链
   - 一个Web应用中，可以配置多个过滤器，这些过滤器就称为过滤器

==先拦截的后执行，后拦截的先执行==   

![image-20220323192259796](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220323192259796.png)



==注解配置的Filter，优先级按照过滤器类名（字符串）的自然顺序==

# Listener

概念：Listener表示监听器，是JavaWeb三大组件(Servlet、Filter、Listener)之一。

监听器可以监听就是在application,session,request三个对象==创建、销毁==或者往其中添加、修改、删除属性时==自动执行代码==的功能组件

## Listener分类：JavaWeb中提供8个监听器

Servlet监听器的作用是监听Web容器的有效期事件，可以监听由于==Web应用中状态改变而引起的Servlet容器产生的相应事件==，然后接受并处理这些事件。

### 一.ServletContext监听器

1.**ServletContextListener**   ✔

Servlet的上下文监听，它主要实现监听ServletContext的==创建和删除 （销毁）==。提供了==2种方法==

- contextInitialized(ServletContextEvent event);   通知正在收听的对象，应用程序已经被加载和初始化。
- contextDestroyed(ServletCotextEvent event);   通知正在收听的对象，应用程序已经被载出，即关闭。

2 . **ServletContextAttributeListener**   

主要实现监听ServletContext属性的==增加==，删除和修改。提供了==3个方法==

- attributeAdded(ServletContextAttributeEvent event);   当有对象加入Application的范围时，通知正在收听的对象
- attributeReplaced(ServletContextAttributeEvent event);当在application的范围有对象取代另一个对象的时，通知正在收听的对象
- attributeRemoved(ServletContextAttributeEvent event);  当有对象从application的范围移除时，通知正在收听的对象

### 二.Session监听

**3.HttpSessionListener**    

 HTTP会话监听，该接口实现监听HTTP会话创建、销毁。提供了2种方法

- sessionCreated(HttpSessionEvent event) ；通知正在收听的对象，session已经被加载及初始化
- sessionDestoryed(HttpSessionEvent event)  ；通知正在收听的对象，session已经被载出（HttpSessionEvent类的主要方法是getSession(),可以使用该方法回传一个session对象）

**4.HttpSessionActivationListener**   

  该接口实现监听HTTP会话active和passivate。 提供了3个方法 

- attributeAdded（HttpSessionBindingEvent event）;当有对象加入session的范围时，通知正在收听的对象
- attributeReplaced（HttpSessionBindingEvent event);当在session的范围有对象取代另一个对象时，通知正在收听的对象。
- attributeRemoved(HttpSessionBindingEvent event);  当有对象从session的范围有对象取代另一个对象时，通知正在收听的对象 其中HttpSessionBindingEvent类主要有三个方法：getName()、getSession()和getValue()

**5.HttpBindingListener**

接口实现监听HTTP会话中对象的绑定信息。它是唯一不需要在web.xml中设定Listener的。提供了2个方法

- valueBound(HttpSessionBindingEvent event);   当有对象加入session的范围时会被自动调用
- valueUnBound(HttpSessionBindingEvent event);   当有对象从session的范围内移除时会被自动调用

**6.HttpSessionAttributeListener**          

该接口实现监听HTTP会话中属性的设置请求。提供了2个方法。

- sessionDidActivate（HttpSessionEvent event);    通知正在收听的对象，它的session已经变为有效状态。
- sessionWillPassivate(HttpSessionEvent event);    通知正在收听的对象，它的session已经变为无效状态

### 三 Request监听

**7.ServletRequestListener**                 

对Request对象进行监听（创建、销毁） 提供了2个方法

- requestInitalized(ServletRequestEvent event)     通知正在收听的对象，ServletRequest已经被加载及初始化
- requestDestroyed(ServletRequestEvent event)   通知正在收听的对象，ServletRequest已经被载出，即关闭

**8.ServletRequestAttributeListener**           

 对Request对象进行监听（增加改属性）  提供了3个方法

- attributeAdded（ServletRequestAttributeEvent event）；  当有对象加入request的范围时，通知正在收听的对象
- attributeReplaced(ServletRequestAttributeEvent event);        当在request的范围内有对象取代两一个对象时，通知正在收听的对象
- attributeRemoved（ServletRequestAttributeEvent event）;     当有对象从request的范围移除时，通知正在收听的对象



ServletContextListener使用

- 定义类，实现ServletContextListener接口
- 在类上添加@WebListener



# 11.Ajax

- 概念：AJAX（Asynchronous Java JavaScript And Xml ）：异步的JavaScript和Xml

AJAX作用：

1. 与服务器进行数据交换：通过AJAX可以给服务器发送请求，并获取服务器响应的数据。
   - 使用AJAX和服务器进行通信，就可以使用HTML + AJAX来替换JSP页面
2. 异步交互：可以在==不重新加载整个页面的情况下==，与服务器==交换数据并更新部分网页==的技术       比如==:搜索联想、用户名是否可用校验==等..



## 11.2AJAX快速入门



1. 编写AjaxServlet，并使用response输出字符串  服务端代码

   ```java
   @WebServlet("/ajaxServlet")
   public class AjaxServlet extends HttpServlet {
       @Override
       protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           //1. 响应数据
           response.getWriter().write("hello ajax~");
       }
   
       @Override
       protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
           this.doGet(request, response);
       }
   }
   ```

2. 创建XmlHttpRequest对象：用于和服务器交换数据   （不用自己写，在官网复制 https://www.w3school.com.cn/js/js_ajax_http.asp ）

3. 向服务器发送请求

4. 获取服务器响应数据

```html
<script>
    //以下 的代码都是w3school中复制来的
    //1. 创建核心对象
    var xhttp;
    if (window.XMLHttpRequest) {
        xhttp = new XMLHttpRequest();
    } else {
        // code for IE6, IE5
        xhttp = new ActiveXObject("Microsoft.XMLHTTP");
    }
    //2. 发送请求 路劲写全路径
    xhttp.open("GET", "http://localhost:8080/ajax-demo/ajaxServlet");
    xhttp.send();

    //3. 获取响应
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
               alert(this.responseText);
        }
    };
</script>
```





## 11.3Axios-基本使用&请求方式别名

- 对原生的Ajax进行封装 ，简化书写

### 快速入门

1. 引入axios的js文件

2. 使用axios发送请求，应获取响应结果

   ```html
   <script src="js/axios-0.18.0.js"></script>
   
   <script>
       //1. get
      /* axios({
           method:"get",
           url:"http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan"
       }).then(function (resp) {
           alert(resp.data);
       })*/
   
       //2. post
       axios({
           method:"post",
           url:"http://localhost:8080/ajax-demo/axiosServlet",
           data:"username=zhangsan" /*设置请求参数data*/
       }).then(function (resp) {
           alert(resp.data);
       })
   </script>
   ```

后台代码：

```java
@WebServlet("/axiosServlet")
public class AxiosServlet extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("get...");

        //1. 接收请求参数
        String username = request.getParameter("username");
        System.out.println(username);

        //2. 响应数据
        response.getWriter().write("hello Axios~");
    }

    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        System.out.println("post...");
        this.doGet(request, response);
    }
}
```



#### Axios请求方式别名

```html
<script src="js/axios-0.18.0.js"></script>

<script>
    //1. get
    axios.get("http://localhost:8080/ajax-demo/axiosServlet?username=zhangsan").then(function (resp) {
        alert(resp.data);
    })
    
    //2. post  方便书写 ，但是不清楚哪一个参数对应的意思
axios.post("http://localhost:8080/ajax-demo/axiosServlet","username=zhangsan").then(function (resp) {
        alert(resp.data);
    })
</script>
```





# JSON

- 概念：JavaScript Object Notation。JavaScript对象表示法
- 由于其语法简单，层次结构鲜明，易于阅读， 多用于作为数据载体，在网络中进行数据传输
- 存储和交换数据的语法。轻量级的数据交换格式



## JSON基础语法

在 JSON 中，值必须是以下数据类型之一：

- 字符串
- 数字
- 对象（JSON 对象）
- 数组 （在方括号中）
- 布尔（true或false）
- null



1. 定义格式：

   ~~~json
   var 变量名 = {
       "key1": value1,
       "key2": value2,
       "key3": value3,
       ...
   }
   ~~~

2. 示例：

   ```json
   var jsonStr = '{"name":"zhangsan","age":23,"addr":["北京","上海","西安"]}';
   ```

3. 获取数据

4. 变量名 . key

   json . name

```js
var json = {"name": "zhangsan", "age": 23, "addr": ["北京", "上海", "西安"]};

alert(json.name);
```



## JSON数据和Java对象转换  ==重点==

- JSON 的常规用途是同 web 服务器进行数据传输。

  在从 web 服务器接收数据时，数据永远是字符串。

  通过 JSON.parse() 解析数据，这些数据会成为 JavaScript 对象。



- 请求数据：JSON字符串转为Java对象
- 响应数据：Java对象转换为JSON对象



- Fastjson是阿里巴巴提供的一个Java语言编写的==高性能功能完善==的JSON库，是目前Java语言中最快的JSON库，可以实现Java对象和JSON字符串的相互转换。

使用：

1. 导入坐标
2. Java转换JSON对象
3. JSON转换Java对象

```java
public class FastJsonDemo {

    public static void main(String[] args) {
        //1. 将Java对象转为JSON字符串
        User user = new User();
        user.setId(1);
        user.setUsername("zhangsan");
        user.setPassword("123");

        String jsonString = JSON.toJSONString(user);
        System.out.println(jsonString);//{"id":1,"password":"123","username":"zhangsan"}

        //2. 将JSON字符串转为Java对象
        User u = JSON.parseObject("{\"id\":1,\"password\":\"123\",\"username\":\"zhangsan\"}", User.class);
        System.out.println(u);
        
    }
}
```

输出结果：

```json
{"id":1,"password":"123","username":"zhangsan"}
User{id=1, username='zhangsan', password='123'}
```





# 12.Vue



## 12.1 概述：

- Vue是一套前端框架，免除原生JavaScript中的DOM操作，简化书写
- 基于MVVM思想，实现数据的双向绑定，将编程的关注点放在数据上

![image-20220324220035827](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220324220035827.png)



## 12.2Vue快速入门

1. 引入Vue.js文件

   ```html
   <script src="js/vue.js"></script>
   ```

2. 在js代码区域，创建vue核心对象，进行数据绑定

   ```js
   new Vue({
       el:"#app",
       data(){
           return {
               username:""
           }
       }
   ```

   创建 Vue 对象时，需要传递一个 js 对象，而该对象中需要如下属性：

   * `el` ： 用来指定哪儿些标签受 Vue 管理。 该属性取值 `#app` 中的 `app` 需要是受管理的标签的id属性值
   * `data` ：用来定义数据模型
   * `methods` ：用来定义函数。这个我们在后面就会用到

3. 编写视图    下面的id 的值需要和上面的 el 的值 相同，才能进行联动

   ```html
   <div id="app">
   
       <input v-model="username">
       <!--插值表达式-->
       {{username}}
   
   </div>
   ```

## 12.3Vue常用指令

- **指令：**HTML 标签上带有 v- 前缀的特殊属性，不同指令具有不同含义。

| **指令**  | **作用**                                            |
| --------- | --------------------------------------------------- |
| v-bind    | 为HTML标签绑定属性值，如设置  href , css样式等      |
| v-model   | 在表单元素上创建双向数据绑定                        |
| v-on      | 为HTML标签绑定事件                                  |
| v-if      | 条件性的渲染某元素，判定为true时渲染,否则不渲染     |
| v-else    |                                                     |
| v-else-if |                                                     |
| v-show    | 根据条件展示某元素，区别在于切换的是display属性的值 |
| v-for     | 列表渲染，遍历容器的元素或者对象的属性              |

1. v-bind 

   < a v-bind:href="url">百度一下</a>

2. v-model     ==该指令可以给表单项标签绑定模型数据。这样就能实现双向绑定效果== 

   ```
   <input name="username" v-model="username">
   ```

3. v-on

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <div id="app">
       <!--<input type="button" value="一个按钮" v-on:click="show()"><br>-->
       <input type="button" value="一个按钮" @click="show()">
   
   </div>
   
   <script src="js/vue.js"></script>
   <script>
   
       //1. 创建Vue核心对象
       new Vue({
           el:"#app",
           data(){
               return {
                   username:"",
                   url:"https://www.baidu.com"
               }
           },
           methods:{
               show(){
                   alert("我被点了...");
               }
           }
       });
   </script>
   </body>
   </html>
   ```

4. v-if、v- if -else  

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <div id="app">
       <!--当下面js中的count值等于v-if的count值时就会把对应的div显示出来，因为只用使用了v-model才会把对应的div显示出来-->
       <div v-if="count == 3">div1</div>
       <div v-else-if="count == 4">div2</div>
       <div v-else>div3</div>
       <hr>
       <div v-show="count == 3">div v-show</div>
       <br>
       <input v-model="count">
   </div>
   <script src="js/vue.js"></script>
   <script>
       //1. 创建Vue核心对象
       new Vue({
           el:"#app",
           data(){
               return {
                   count:3
               }
           },
           methods:{
               show(){
                   alert("我被点了...");
               }
           }
       });
   </script>
   </body>
   </html>
   ```

5. v -for

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Title</title>
   </head>
   <body>
   <div id="app">
       <div v-for="addr in addrs">
           {{addr}} <br>
       </div>
       <hr>
       <!--添加索引值 i ,i是从0开始的。里面的addrs是下面的数组名  addr则是相当于变量名-->
       <div v-for="(addr,i) in addrs">
           {{i+1}}--{{addr}} <br>
       </div>
   </div>
   
   <script src="js/vue.js"></script>
   <script>
   
       //1. 创建Vue核心对象
       new Vue({
           el:"#app",
           data(){
               return {
                   addrs:["北京","上海","西安"]
               }
           },
       });
   </script>
   </body>
   </html>
   ```

## 12.4Vue生命周期

- 生命周期的八个阶段：每触发一个生命周期事件，会自动执行一个生命周期方法，这些生命周期方法也被称为钩子方法。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220324223825341.png" alt="image-20220324223825341" style="zoom:80%;" />



- ==mounted：==挂载完成，Vue初始化成功，HTML页面渲染成功。而以后我们会在该方法中==发送异步请求，加载数据。==

- 

- ```js
  new Vue({
      el:"#app",
      //在开发中这里是创建异步请求的代码
      mounted(){
          alert("加载完成...")
      }
  });
  ```

# Element

- 是一套基于Vue的网站组件库，用于快速构建网页
- 组件：组成网页的部件，如：超链接、按钮、图片、表格等等

## 快速入门

1. 映入Element的css、js文件和Vue.js 

   ```html
   <script src="js/vue.js"></script>
   <script src="element-ui/lib/index.js"></script>
   <link rel="stylesheet" href="element-ui/lib/theme-chalk/index.css">
   ```

2. 创建Vue核心对象

   ```html
   <script>
       new Vue({
           el:"#app"
       })
   </script>
   ```

## Element布局

在官网上查看 复制粘贴。

1. Layout布局：通过基础的24分栏，迅速简便的创建布局。一行分为24栏
2. Container布局容器：用于布局的容器组件，方便快速搭建页面的基本结构。如下图就是布局容器效果。

## Element常用组件

官网查看   https://element.eleme.cn/#/zh-CN/component/installation

# 13.代理模式

- 设计模式
  1. 装饰模式
  2. 代理模式
     - 动态代理

## 13.1概念

1. 真实对象：被代理的对象
2. 代理对象：
3. 代理模式：代理对象代理真实对象，达到增强真实对象功能的目的

## 13.2实现方式

1. 静态代理：有一个类文件描述代理模式
2. 动态代理：在内存中形成代理类
   - 实现步骤：
     1. 代理对象和真实对象实现相同的接口     代理类和目标类必须实现 同一个接口或者继承相同的父类
     2. 代理对象=Proxy.newProxyInstance();
     3. 使用代理对象调用方法
     4. 增强方法
   - 增强方式
     1. 增强参数列表
     2. 增强返回值类型
     3. 增强方法体执行逻辑



