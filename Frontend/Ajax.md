> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# 1.JavaWeb - Ajax

- 概念：AJAX（Asynchronous Java JavaScript And Xml ）：异步的JavaScript和Xml

AJAX作用：

1. 与服务器进行数据交换：通过AJAX可以给服务器发送请求，并获取服务器响应的数据。
   - 使用AJAX和服务器进行通信，就可以使用HTML + AJAX来替换JSP页面
2. 异步交互：可以在==不重新加载整个页面的情况下==，与服务器==交换数据并更新部分网页==的技术       比如==:搜索联想、用户名是否可用校验==等



## 1.2 AJAX快速入门



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

## 1.3 Axios-基本使用&请求方式别名

- 对原生的Ajax进行封装 ，简化书写

### 快速入门

1. 引入axios的js文件，.

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



# 2. Ajax

## 2.1 Ajax简介

Ajax：就是JavaScript 与 服务器交互的手段



有以下几点特性

1. Ajax 全名称为： `Asynchronous JavaScript and XML`（异步的 JavaScript 和 XML）
2. 具有 ==前后台交互的能⼒== 就是： 客户端给服务端发送消息的⼯具，以及接受响应的⼯具，用于创建快速动态网页的技术
3. Ajax 不是新的编程语言，而是一种使用现有标准的新方法。
4. Ajax 最大的优点是在==不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容==。
5. Ajax 不需要任何浏览器插件，但需要用户允许 JavaScript 在浏览器上执行。
6. XMLHttpRequest 只是实现 Ajax 的一种方式。
7. 是⼀个 ==默认异步==执⾏机制的功能，Ajax 分为同步（async = false）和异步（async = true）



同步请求：（async = false）

>  同步请求是指当前发出请求后，浏览器什么都不能做，
>  必须得等到请求完成返回数据之后，才会执行后续的代码，
>  相当于生活中的排队，必须等待前一个人完成自己的事物，后一个人才能接着办。
>  也就是说，当JS代码加载到当前AJAX的时候会把页面里所有的代码停止加载，页面处于一个假死状态，
>  当这个AJAX执行完毕后才会继续运行其他代码页面解除假死状态



异步请求：（async = true）

> 默认异步：异步请求就当发出请求的同时，浏览器可以继续做任何事，
> Ajax发送请求并不会影响页面的加载与用户的操作，相当于是在两条线上，各走各的，互不影响，
>
> 相当于生活中的煮饭和洗菜，煮饭的过程当中可以同时进行洗菜。
>
> 一般默认值为true，异步。异步请求可以完全不影响用户的体验效果，
> 无论请求的时间长或者短，用户都在专心的操作页面的其他内容，并不会有等待的感觉。



## 2.2 Ajax 的应用场景

- 运用 XHTML+CSS 来表达资讯；
- 运用 JavaScript 操作 DOM（Document Object Model）来执行动态效果；
- 运用 XML 和 XSLT 操作资料;
- 运用 XMLHttpRequest 或新的 Fetch API 与网页服务器进行异步资料交换；
- **注意：**AJAX 与 Flash、Silverlight 和 Java Applet 等 RIA 技术是有区分的。



## 2.3 Ajax 优势

- 不需要插件的⽀持，原⽣ js 就可以使⽤
- ⽤户体验好（不需要刷新⻚⾯就可以更新数据）
- 减轻服务端和带宽的负担

缺点：

- 搜索引擎的⽀持度不够，因为数据都不在⻚⾯上，搜索引擎搜索不到
- 存在跨域问题，也就是不能从 `baidu.com` 向` a.com` 这个网站发送请求



## 2.3 Ajax 的执行过程

![image-20221222141034812](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221222141034812.png)

1. 首先通过PHP页面将数据库中的数据取出
2. 取出后转成Json格式的字符串，后利用 Ajax把字符串返还给前台
3. 再利用 Json.Parse解析通过循环添加到页面上
4. 那么反之，前端的数据可以利用Ajax提交到后台
5. 但是后台是没有办法直接把这些数据插入到数据库中，所以要先提交到PHP页面上
6. 最后再由PHP将数据插入到数据库中



## 2.4 Ajax 实际使用过程

- 在 JS 中有内置的构造函数来创建 Ajax对象

- 创建 Ajax 对象以后，我们就使⽤ Ajax对象的⽅法去发送请求和接受响应

- Ajax 的一个最大的特点是==无需刷新页面便可向服务器传输或读写数据==(又称无刷新更新页面)，这一特点主要得益于 `XMLHTTP `组件 `XMLHTTPRequest `对象。

XMLHttpRequest 对象方法描述：

![20200315104357831](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20200315104357831.png)



### 2.4.1 创建Ajax对象

~~~js
// IE9及以上
const xhr = new XMLHttpRequest()
// IE9以下
const xhr = new ActiveXObject('Mricosoft.XMLHTTP')
~~~

创建的Ajax对象 xhr 用来发送ajax请求



### 2.4.2 配置链接信息

XMLHttpRequest 对象属性描述（用于和服务器交互数据）

![2](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2.png)



~~~js
//现在的浏览器（IE7+、Firefox、Chrome、Safari 以及 Opera）均内建 XMLHttpRequest 对象。
const xhr = new XMLHttpRequest()
// xhr 对象中的 open ⽅法是来配置请求信息的
// 第⼀个参数是本次请求的请求⽅式 get / post / put / ...
// 第⼆个参数是本次请求的 url 
// 第三个参数是本次请求是否异步，默认 true 表示异步，false 表示同步
// xhr.open('请求⽅式', '请求地址', 是否异步)
xhr.open('get', './data.php')
~~~

上⾯的代码执⾏完毕以后，本次请求的基本配置信息就写完了

### 2.4.3 发送请求

~~~js
//如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：
const xhr = new XMLHttpRequest()
xhr.open('get', './data.php')
// 使⽤ xhr 对象中的 send ⽅法来发送请求
xhr.send()
~~~

将配置好的Ajax对象信息发送至服务端



 一个最基本的 ajax 请求就是上面三步 但是光有上面的三个步骤，我们确实能把请求发送到服务端 

如果服务端正常的话，响应也能回到客户端 但是我们拿不到响应
如果想要拿到响应，我们需要有两个前提条件

 1. 本次 HTTP 请求是成功的，也就是我们下面要说的 http 状态码为 200 ~ 299
 2. ajax 对象也有自己的状态码，用来表示本次 ajax 请求中各个阶段



## 2.5 状态码

Ajax 状态码 :`Ajax对象.readyState`  用来表示一个Ajax请求的全过程中的某一个状态

主要有以下几个状态：

>  readyState `===` 0 : 表示未初始化完成，也就是 open 方法还没有执行 
>  readyState `===` 1 : 表示配置信息已经完成，也就是执行完 open 之后 
>  readyState `===  ` 2 : 表示 send 方法已经执行完成
>  readyState `===` 3 : 表示正在解析响应内容
>  readyState `===` 4 : 表示响应内容已经解析完毕，可以在客户端使用了

由此一来，只有当readyState === 4 的时候，我们才可以正常使用服务端给我们的数据

因此，需要配合我们的HTTP状态码 （200~299）

- 一个Ajax对象中的一个成员为 `xhr.status` （用来记录本次请求的 HTTP状态码）

当`readState === 4` 这个条件 和HTTP 的状态码在 200~299 之间才是正常的完成本次的请求



### 2.5.1 监听Ajax状态值

**readyStatueChange** 

- 这个事件，是专门用来Ajax的状态值的，当readyState的值发生改变时，它就能监听到发生改变的值。也就说当状态值改变才会触发此事件

如此一来就能用这个来监听readyStatue 是否为 4 

~~~js
   const xhr = new XMLHttpRequest() xhr.open('get', './data.php')
	xhr.send()
	xhr.onreadyStateChange = function () {
	// 每次 readyState 改变的时候都会触发该事件
	// 我们就在这里判断 readyState 的值是不是到 4
	// 并且 http 的状态码是不是 200 ~ 299
	if (xhr.readyState === 4 && /^2\d{2|$/.test(xhr.status)) {
	// 这里表示验证通过
	// 我们就可以获取服务端给我们响应的内容了 }
}
~~~



## 2.6 使用Ajax发送请求时携带参数

- 参数就是与后台交互时传递的信息
- 携带的参数有两个方式 `get` 、`post` 

下面来讲解以下 `get `和 `post `携带参数的区别

### 2.6.1 两种请求方式的优缺点以及比较

- 首先两方请求方式，==GET请求比POST请求要简单而且更加快== ，并且GET在大部分情况下都是能用的。
- POST的使用情况，有以下几种
  1. 无法使用缓存文件（更新服务器上的文件或数据库）
  2. 向服务器发送大量数据（POST 没有数据量限制）
  3. 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠



### 2.6.2 发送一个 GET 请求

> GET请求的参数就是 在URL后面拼接

~~~js
// 直接在地址后面加一个 ?，然后以 key=value 的形式传递 // 两个数据之间以 & 分割
xhr.open('get', './data.php?a=100&b=200')
xhr.send()
~~~

如此一来，服务端拿到的参数和值为`a=100` `b=200`



### 2.6.3 发送一个 POST 请求

> post 请求的参数是携带在请求体中的，所以不需要再 url 后面拼接

~~~js
	const xhr = new XMLHttpRequest() xhr.open('post', './data.php')
	// 如果是用 ajax 对象发送 post 请求，必须要先设置一下请求头中的 content- type
	// 告诉一下服务端我给你的是一个什么样子的数据格式 xhr.setRequestHeader('content-type', 'application/x-www-form- urlencoded')
	// 请求体直接再 send 的时候写在 () 里面就行
	// 不需要问号，直接就是 'key=value&key=value' 的形式 xhr.send('a=100&b=200')
~~~

~~~js
// 1. 创建 ajax 对象
let xhr = new XMLHttpRequest()
// 2. 配置请求信息 xhr.open(‘GET’, ‘./test.php’, true)
// 3. 发送请求 xhr.send()
// 4. 接受响应 xhr.onload = function () {
console.log(xhr.responseText) }
~~~



## 2.7 Ajax 封装

~~~html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Document</title>
        <script>
            /*
                type 代表 请求方式
                url  代表 请求url路径
                data 代表 发送数据
                success 代表 下载数据成功以后执行的函数
                error   代表 下载数据失败以后执行的函数
            */
            function $ajax({type = "get", url, data, success, error}){
                var xhr = null;
                try{
                    xhr = new XMLHttpRequest();
                }catch(error){
                    xhr = new ActiveXObject("Microsoft.XMLHTTP")
                }
                
                if(type == "get" && data){
                    url += "?" + querystring(data);
                }

                xhr.open(type, url, true);

                if(type == "get"){
                    xhr.send();
                }else{
                     //设置提交数据格式
                    xhr.setRequestHeader("content-type", "application/x-www-form-urlencoded");
                    data ? xhr.send(querystring(data)) : xhr.send();
                }
                xhr.onreadystatechange = function(){
                    if(xhr.readyState == 4){
                        if(xhr.status == 200){
                            if(success){
                                success(xhr.responseText);
                            }
                        }else{
                            if(error){
                                error("Error：" + xhr.status);
                            }
                        }
                    }
                }
            }
            function querystring(obj){
                var str = '';
                for(var attr in obj){
                    str += attr + "=" + obj[attr] + "&";
                }
                return str.substring(0, str.length - 1);
            }

            window.onload = function(){
                var aBtns = document.getElementsByTagName("button");
                /*
                    当我们下载完数据以后需要对数据的处理方式不一样
                    【注】$ajax，我们需要按照传参的顺序，依次传入我们的参数。
                */

                aBtns[0].onclick = function(){
                    $ajax({
                        url: "code14/1.get.php",
                        data: {
                            username: "小明",
                            age: 18,
                            password: "123abc"
                        },
                        success: function(result){
                            alert("GET请求到的数据：" + result);
                        },
                        error: function(msg){
                            alert("GET请求数据错误：" + msg);
                        }
                    })
                }

                aBtns[1].onclick = function(){
                    $ajax({
                        type: "post",
                        url: "code14/2.post.php",
                        data: {
                            username: "小花",
                            age: 18,
                            password: "123abc"
                        },
                        success: function(result){
                            alert("POST请求到的数据：" + result);
                        },
                        error: function(msg){
                            alert("POST请求数据错误：" + msg);
                        }
                    })
                }
            }

        </script>
    </head>
    <body>
        <button>GET请求</button>
        <button>POST请求</button>
    </body>
</html>
~~~



# 3. Ajax - 原生Ajax



## 3..1 Ajax - HTTP 协议

http协议（超文本传输协议），协议详细规定了浏览器和万维网服务器之间互相通信的规则。

请求报文：参数格式

~~~js
行   GET/s?ie=utf-8 HTTP/1.1
头   Host:atguigu.com
     Cookie:name=guigu
     Content-type:application/x-www-form-urlencoded
     User-Agent:chrome 83
空行
体    username=admin&password=admin 
~~~

- GET请求可以不存在请求体
- POST存在请求体



响应报文

~~~js
行    HTTP/1.1  200  OK
头    Content-Type:text/html;charset=utf-8
      Content-length:2048
      Content-encoding:gzip 
空行   
体     <html> 
   				<head>
   				</head>
   				<body>
   						xxx
   				</body>
       </html>
~~~



### 3.1.1 Chrome 查看通信报文

![image-20221223104454195](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223104454195.png)

## 3.2 Express 框架使用

1. 初始化npm  npm init --yes

2. 安装express  npm install express

~~~js
// 1.引入express框架
const express = require('express');
// 2.创建网站服务器
const app = express();

// 3.创建路由规则
app.get('/', (request, response) => {
    response.setHeader('response:', '*');
    //send()
    //1.send方法内部会检测响应内容的类型
    //2.send方法会自动设置http状态码
    //3.send方法会自动设置响应的内容类型及编码
    response.send('Hello, world');
});
//监听端口
app.listen(8000,() => {
    console.log('网站服务器启动成功...');
});
~~~

![image-20221223113347578](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223113347578.png)



## 3.3 Ajax 发送请求

### 3.3.1 Ajax 发送GET请求

HTML执行代码

~~~js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ajax-GET请求</title>
    <style>
        #result {
            width: 200px;
            height: 100px;
            border: solid 1px pink;
        }
    </style>
</head>

<body>
    <button id="btn">点击发送请求</button>
    <div id="result"></div>
    <script>
        // 获取对象
        const btn = document.querySelector("#btn");
        const result = document.querySelector("#result");
        btn.onclick = function() {
            //1.创建对象
            const xhr = new XMLHttpRequest();
            //2.初始化，设置请求方式和url
            xhr.open('GET', 'http://localhost:9000/server');
            //3.发送
            xhr.send();
            //4.事件绑定 处理服务器端返回的结果。当事件状态改变时进行以下操作：
            xhr.onreadystatechange = function() {
                //判断
                if (xhr.readyState == 4) {
                    //判断响应状态码 200 404 403 401 500   2xx都是成功
                    if (xhr.status >= 200 && xhr.status < 300) {
                        //处理结果 行 头 空行 体
                        //响应 行
                        console.log(xhr.status); //状态码
                        console.log(xhr.statusText); //状态字符串
                        console.log(xhr.getAllResponseHeaders()); //所有响应头
                        console.log(xhr.response); //响应体
                        result.innerHTML = xhr.response; // 将服务端发送的内容显示到div里面
                    }
                }
            }
        }
    </script>
</body>
~~~

服务端JS代码

~~~js
//引入express框架
const express = require('express');
//创建网站服务器
const app = express();

app.get('/server', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    //send()
    //1.send方法内部会检测响应内容的类型
    //2.send方法会自动设置http状态码
    //3.send方法会自动设置响应的内容类型及编码
    res.send('Express Hello World');
});
//监听端口
app.listen(9000,()=>{
    console.log('网站服务器端口：9000，启动成功');
});
~~~

![image-20221223120348511](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223120348511.png)

![image-20221223120206830](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223120206830.png)

### 3.3.2 Ajax 设置请求参数

~~~js
xhr.open('GET', 'http://localhost:9000/server?var1=100&var2=200');
~~~



### 3.3.3 Ajax 发送POST请求

```js
xhr.open('POST','http://127.0.0.1:9000/server');
```

服务端的修改为POST请求方式

```js
app.post('/server', (req, res) => {
    res.setHeader('POST response:', '*');
    res.send('POST Express Hello World');
});
```



![image-20221223130431211](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223130431211.png)

POST设置参数（URL参数）

~~~js
xhr.send('a=100&b=200');
~~~

### 3.3.4 Ajax 设置请求头信息

使用 `setRequestHeader` 设置请求头信息

~~~js
xhr.setRequestHeader('Content-type','application/x-www-form-lencoded')；
// 自定义请求头
xhr.setRequestHeader('header',' response header');
~~~

接收所有的请求方式：并设置自定义请求头

```js
app.all('/server', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    // 响应自定义的请求头
    res.setHeader('Access-Control-Allow-Header', '*');
    res.send('POST Express Hello World');
});
```

## 3.4 服务端响应JSON

用到的JSON的两种方法：

- 将对象转化为JSON格式：JSON.stringify()
- 将JSON格式转化为对象：JSON.parse()

服务端设置：

```js
// JSON
app.all('/jsonServer', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    // 创建JSON对象
    const obj = {
        name: 'kcs',
        age: 21
    }
    // 将对象进行字符串转换
    let str = JSON.stringify(obj);
    // 发送响应体
    res.send(str);
});
```

客户端设置：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>JSON</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            border: solid 2px pink;
        }
    </style>
</head>
<body>
    <div></div>
    <script>
        // 获取元素
        let divElement = document.querySelector('div');
        divElement.addEventListener('mouseover', function () {
            // 创建对象 const:定义常量
            const xhr = new XMLHttpRequest();
            // 自动转换json格式
            xhr.responseType = 'json';
            // 初始化URL
            xhr.open('POST', 'http://127.0.0.1:9000/jsonServer');
            // 发送请求
            xhr.send();
            // 事件绑定
            xhr.onreadystatechange = function () {
                // 判断状态
                if (xhr.readyState === 4) {
                    // 响应状态
                    if (xhr.status >= 200 && xhr.status < 300) {
                        // 将数据显示在div中
                        divElement.innerHTML = '当前的操作者<br>' + '姓名:' + xhr.response.name + '<br>年龄:' + xhr.response.age;

                    }
                }
            }
        })
    </script>
</body>
</html>
```

当鼠标移动到框内时就会发送请求给服务端，服务端就会将数据响应给客户端

![image-20221223140925153](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223140925153.png)



自动重启服务端工具下载 `nodemon`

~~~nginx
npm install -g nodemon
~~~

启动脚本

~~~
nodemon 脚本名称
~~~



## 3.5 请求超时或网络异常请求

客户端设置

```js
<head>
    <meta charset="UTF-8">
    <title>超时链接</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            border: solid 2px pink;
        }
    </style>
</head>
<body>
    <button>发送请求</button>
    <div></div>
    <script>
        // 获取元素
        let btnElement = document.querySelector('button');
        let divElement = document.querySelector('div');
        btnElement.addEventListener('click',function () {
            // 创建对象 const:定义常量
            const  xhr = new XMLHttpRequest();
            // 超时设置 2秒
            xhr.timeout = 2000;
            // 超时的提醒设置
            xhr.ontimeout = function () {
                alert('网络链接超时，请稍后重试！');
            }
            // 网络原因
            xhr.onerror = function (e) {
                alert('当前没有链接网络！');
            }
            // 初始化URL
            xhr.open('GET','http://127.0.0.1:9000/timer');
            // 发送请求
            xhr.send();
            // 事件绑定
            xhr.onreadystatechange = function () {
                // 判断状态
                if (xhr.readyState === 4 ){
                    // 响应状态
                    if (xhr.status >= 200 && xhr.status < 300) {
                        divElement.innerHTML = xhr.response;
                    }
                }
            }
        })
    </script>
</body>
```

服务端设置接口：

```js
// 延迟规定
app.get('/timer', (req, res) => {
    res.setHeader('Access-Control-Allow-Origin', '*');
    // 延迟设置 2秒
    setTimeout(() => {
        res.send('REQUEST Timer Out');
    },2000)
});
```



### 3.5.1  手动取消请求

```html
<head>
    <meta charset="UTF-8">
    <title>超时链接</title>
</head>
<body>
    <button class="send">发送请求</button>
    <button class="cancel">取消请求</button>
    <div></div>
    <script>
        // 获取元素
        let send = document.querySelector('.send');
        let cancel = document.querySelector('.cancel');
        let xhr = null;
        // 发送
        send.addEventListener('click', function () {
            // 创建对象 const:定义常量
            xhr = new XMLHttpRequest();
            // 初始化URL
            xhr.open('GET', 'http://127.0.0.1:9000/timer');
            // 发送请求
            xhr.send();
        })
        //取消
        cancel.addEventListener('click', function () {
            xhr.abort();
        })
    </script>
</body>
```



![image-20221223144303416](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223144303416.png)



## 3.6 重复请求问题

不断点击请求，给服务器发送相同的请求会 给服务器带来很大的压力

解决办法

1. 首先判断前面是否存在相同的请求在进行，有则关闭前面的请求



```js
<head>
    <meta charset="UTF-8">
    <title>重复请求</title>
</head>
<body>
    <button class="send">发送请求</button>
    <script>
        // 获取元素
        let send = document.querySelector('.send');
        let xhr = null;
        // 标识 是否正在发送Ajax请求
        let isSending = false;
        // 发送
        send.addEventListener('click', function () {
            // 如果前一个在发送请求就取消掉
            if (isSending) {
                xhr.abort();
            }
            // 创建对象 const:定义常量
            xhr = new XMLHttpRequest();
            // 正在发送修改成true
            isSending = true;
            // 初始化URL
            xhr.open('GET', 'http://127.0.0.1:9000/server');
            // 发送请求
            xhr.send();
            xhr.onreadystatechange = function () {
                // 发送状态为 4 则修改标识
                if (xhr.readyState === 4) {
                    isSending = false;
                }
            }
        })
    </script>
</body>
```

由于电脑的响应速度比较快，总之就是每次点击发送请求就会把前一个请求给取消

![image-20221223145339391](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221223145339391.png)



# 4. Ajax - axios请求 

[中文官网](https://www.axios-http.cn/)



## 4.1 axios 发送 GET、POST、Ajax 请求 

服务端配置

```js
app.get('/axios-server', (request, response) =>{
    response.setHeader('Access-Control-Allow-Headers', '*');// 设置允许自定义请求头
    response.setHeader('Access-Control-Allow-Origin', '*');// 设置允许跨域
    response.end();
});

app.options('/axios-server', (request, response) =>{
    response.setHeader('Access-Control-Allow-Headers', '*');// 设置允许自定义请求头
    response.setHeader('Access-Control-Allow-Origin', '*');// 设置允许跨域
    response.end();
});

app.post('/axios-server', (request, response) =>{
    response.setHeader('Access-Control-Allow-Headers', '*');// 设置允许自定义请求头
    response.setHeader('Access-Control-Allow-Origin', '*');// 设置允许跨域
    console.log('axios-server 接口接收到请求');
    response.send('HELLO Axios');
});
```

客户端的GET配置

```js
<head>
    <meta charset="UTF-8">
    <title>Axios</title>
    <script crossorigin="anonymous" src="https://cdn.bootcdn.net/ajax/libs/axios/1.2.1/axios.js"></script>
</head>
<body>
    <button class="get">GET</button>
    <button class="post">POST</button>
    <button class="ajax">AJAX</button>

    <script>
        var get = document.querySelector('.get');
        var post = document.querySelector('.post');
        var ajax = document.querySelector('.ajax');
        //配置baseURL
        axios.defaults.baseURL = 'http://localhost:9000';
        get.addEventListener('click', function () {
            //get请求
            axios.get('/axios-server', {
                //url参数
                params: {
                    id: 100,
                    vip: 7
                },
                // 请求头
                headers: {
                    name: "kcs",
                    age: 20
                }
            }).then(value => {
                console.log(value);
            });
        })
        // post请求
        post.onclick = function () {
            //get请求
            axios.post('/axios-server', {
                //url参数
                params: {
                    id: 200,
                    vip: 9
                },
                // 请求头
                headers: {
                    name: "kcs",
                    age: 20
                },
                data: {
                    username: 'kcs',
                    password: 123456
                }
            })
        }
        // ajax请求
        ajax.onclick = function () {
            axios({
                //请求方法
                method: 'POST',
                //url
                url: '/axios-server',
                //url参数
                params: {
                    vip: 10,
                    level: 30
                },
                //头信息
                headers: {
                    a: 100,
                    b: 200
                },
                //请求体参数
                data: {
                    user: 'admin',
                    pass: 'admin'
                }
            })
        }
    </script>

</body>
```



# 5. 通过 全局对象的fetch()方法 进行AJAX操作

[GitHub 地址](https://github.com/github/fetch)

fetch()返回的是promise对象，通过fetch()发送AJAX请求

~~~js
fetch(url,[{可选配置项}])
~~~

客户端设置：

```js
<body>
    <button>AJAX</button>
    <script>
        const btn = document.querySelector("button");
        btn.onclick = function () {
            fetch('http://localhost:9000/axios-server', {
                //请求方法
                method: 'POST',

                //url参数
                params: {
                    vip: 10,
                    level: 30
                },
                //头信息
                headers: {
                    a: 100,
                    b: 200
                },
                //请求体参数
                data: {
                    user: 'admin',
                    pass: 'admin'
                }
            }).then(value => {
                return value.text();
            }).then(value => {
                console.log(value);
            })
        }
    </script>
</body>
```



服务端设置：

```js
app.post('/axios-server', (request, response) => {
    response.setHeader('Access-Control-Allow-Headers', '*');// 设置允许自定义请求头
    response.setHeader('Access-Control-Allow-Origin', '*');// 设置允许跨域
    console.log('axios-server 接口接收到请求');
    const data = {
        name: 'kcs',
        age: 21
    }
    response.send(JSON.stringify(data));
});
```



# 6. 跨域

## 6.1 同源策略

> 同源策略是浏览器的一种安全策略
>
> 同源：协议、域名、端口号必须完全相同
>
> ==违背同源策略就是跨域==
>
> AJAX请求默认遵循同源策略



### 同源策略案例

客户端

```html
<body>
    <button>data</button>
    <script>
        const btn = document.querySelector('button');
        btn.onclick = function () {
            const x = new XMLHttpRequest();
            //这里因为是满足同源策略的，所以url可以简写，省略不写就会自动添加上
            x.open("GET",'/data');
            //发送
            x.send()
            x.onreadystatechange = function () {
                if (x.readyState === 4) {
                    if (x.status >= 200 && x.status < 300) {
                        console.log(x.response);
                    }
                }
            }
        }
    </script>
</body>
```



服务端

```js
//引入express框架
const express = require('express');
//创建网站服务器
const app = express();

app.get('/home', (request, response) => {
    response.sendFile(__dirname + '/index.html');
});

app.all('/data', (request, response) => {
    response.send('用户数据');
});

//监听端口
app.listen(8000, () => {
    console.log('网站服务器端口：8000，启动成功');
});
```



## 6.1 解决跨域问题 - JSONP

- SONP（JSON with Padding）是一个非官方的跨域解决方案，只支持get请求
- 如何工作：在网页有一些标签天生具有跨域能力，比如：`img link iframe script`，JSONP就是利用script标签的跨域能力来发送请求的





## 6.2 解决跨域问题 - CORS



- CORS（Cross-Origin-Resource-Sharing），跨域资源共享。CORS是官方的跨域解决方案
- 特点是不需要在客户端做任何特殊的操作，完全在服务器端中处理，支持get和post请求。跨域资源共享标准新增了一组http首部字段，允许服务器声明哪些源站通过浏览器有权限访问哪些资源
- 工作原理：通过设置一个响应头来告诉浏览器，该请求允许跨域，浏览器收到该响应后就会对响应放行

HTML创建Ajax对象：

```html
<head>
    <meta charset="UTF-8">
    <title>Ajax跨域</title>
    <style>
        .div {
            width: 200px;
            height: 200px;
            border: solid 1px pink;
        }
    </style>
</head>
<body>
    <button>发送请求</button>
    <div class="div"></div>
    <script>
        // 获取对象
        let buttonElement = document.querySelector('button');
        let divElement = document.querySelector('div');
        buttonElement.addEventListener('click',function () {
            // 1. 创建对象
            const x = new XMLHttpRequest();
            // 2.初始化对象
            x.open("GET", 'http://127.0.0.1:8000/cors-server');
            // 3.发送请求
            x.send()
            // 绑定事件
            x.onreadystatechange = function () {
                if (x.readyState === 4) {
                    if (x.status >= 200 && x.status < 300) {
                        divElement.innerHTML = x.response;
                    }
                }
            }
        })
    </script>
</body>
```



服务端设置GET请求

```js
app.get('/cors-server', (request, response) => {
    // 设置响应头
    response.setHeader('Access-Control-Allow-Origin','*');
    response.setHeader('Access-Control-Allow-Methods','*');
    response.setHeader('Access-Control-Allow-Headers','*');
    response.send('Ajax跨域解决CROS');
});
```





### 规范定义的响应首部字段：

[响应头首部](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Credentials)

- `Access-Control-Allow-Origin`：其中，origin 参数的值指定了允许访问该资源的外域 URI。对于不需要携带身份凭证的请求，服务器可以指定该字段的值为通配符，表示允许来自所有域的请求.
- `Access-Control-Allow-Credentials`：头指定了当浏览器的credentials设置为true时是否允许浏览器读取response的内容。当用在对preflight预检测请求的响应中时，它指定了实际的请求是否可以使用credentials。请注意：简单 GET 请求不会被预检；如果对此类请求的响应中不包含该字段，这个响应将被忽略掉，并且浏览器也不会将相应内容返回给网页。
- `Access-Control-Allow-Methods`： 默认情况下，CORS 仅支持客户端发起 GET、POST、HEAD 请求。如果客户端希望通过 PUT、DELETE 等方式请求服务器的资源，则需要在服务器端，通过 `Access-Control-Alow-Methods` 来指明实际请求所允许使用的 HTTP 方法
- `Access-Control-Allow-Headers`： 首部字段用于预检请求的响应。其指明了实际请求中允许携带的首部字段。
- `Access-Control-Expose-Headers`：在跨源访问时，XMLHttpRequest对象的getResponseHeader()方法只能拿到一些最基本的响应头，Cache-Control、Content-Language、Content-Type、Expires、Last-Modified、Pragma，如果要访问其他头，则需要服务器设置本响应头。Access-Control-Expose-Headers 头让服务器把允许浏览器访问的头放入白名单
- `Access-Control-Max-Age`： 头指定了preflight请求的结果能够被缓存多久



[更多的跨域解决方案](https://blog.csdn.net/itcats_cn/article/details/82318092?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522167178653716800225544511%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=167178653716800225544511&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~hot_rank-1-82318092-null-null.142^v68^control,201^v4^add_ask,213^v2^t3_control1&utm_term=Ajax%E8%B7%A8%E5%9F%9F&spm=1018.2226.3001.4187)



#### 简单请求

- 请求方式：GET、POST、HEAD 三者之一
- HTTP 头部信息不超过以下几种字段：无自定义头部字段、Accept、Accept-Language、Content-Language、DPR、Downlink、Save-Data、Viewport-Width、Width 、Content-Type（只有三个值 application/x-www-formurlencoded、multipart/form-data、text/plain）

#### 预检请求

- 请求方式为 GET、POST、HEAD 之外的请求 Method 类型
- 请求头中包含自定义头部字段
- 向服务器发送了 application/json 格式的数据

在浏览器与服务器正式通信之前，浏览器会先发送 OPTION 请求进行预检，以获知服务器是否允许该实际请求，所以这一次的 OPTION 请求称为“预检请求”。服务器成功响应预检请求后，才会发送真正的请求，并且携带真实数据



