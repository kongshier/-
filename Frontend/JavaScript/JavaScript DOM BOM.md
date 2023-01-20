> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# JavaScript DOM

## DOM简介

（Document Object Model ）文档对象模型：通过DOM可以来任意来修改网页中各个内容



DOM模型结构化：对象树

![image-20221120214345818](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221120214345818.png)

### HTML DOM

- 是HTML标准对象模型和编程接口
- 可访问所有的HTML元素的属性、元素方法、元素事件。

1. 文档 
   - 文档指的是网页，一个网页就是一个文档 
2. 对象 
   - 对象指将网页中的每个节点都转换为对象  
   - 转换完对象后，即可纯面向对象的形式来操作网页
3. 模型  
   - 模型用来表示节点和节点之间的关系，方便操作页面  
4. 节点（Node）  
   1.  节点是构成网页的最基本的单元，网页中的每一个部分都可以称为是一个节点  
   2.  虽然都是节点，但节点类型是不同的  
5.  常用的节点  
   1. 文档节点 （Document），代表整个网页  
   2. 元素节点（Element），代表网页中的标签  
   3. 属性节点（Attribute），代表标签中的属性  
   4. 文本节点（Text），代表网页中的文本内容 

### API 与Web API

- API：应用程序编程接口，预定义的函数
- Web API：浏览器提供的一套操作浏览器功能和页面元素的API（BOM、DOM）

## DOM操作  

###  DOM查询-获取元素

网页中浏览器已提供document对象，它代表的是整个网页，它是window对象的属性，可以在页面中直接使用。 

document查询方法：  

- 根据元素的==id属性==值查询一个元素节点对象：

  - `document.getElementById("id属性值"); `

  - 返回一个元素对象

    ```js
    <body>
        <p id="demo01">通过id查找元素</p>
        <script>
          // 此时 Hello world 就会替换掉 p标签的文本
            document.getElementById("demo01").innerHTML = "Hello World!";
        </script>
    </body>
    ```

    `innerHTML` 属性：获取元素（标签）内容

    - 使用该属性可以获取或改变、替换HTML元素的内容

- 根据元素的==name、类名==值查询一组元素节点对象：	 

  - `document.getElementsByName("name属性值")；`

  - 返回的是一个元素对象集合，用伪数组类型存储内容

    ```js
    <body>
        <p name="demo">hello</p>
        <p name="demo">hello</p>
    		<p class="cdemo">hello</p>
        <p class="cdemo">hello</p>
        <script>
            var demo = document.getElementsByName("demo");
    				var cdemo = document.getElementsByName("cdemo");
            // 对第一个p标签替换内容
            demo[0].innerHTML="这是第一个p标签";
            // 对第二个p标签替换内容
            demo[1].innerHTML="这是第二个p标签";
    
    				// 通过类名				
    				// 对第一个p标签替换内容
            cdemo[0].innerHTML="这是通过类名设置的第一个p标签";
            // 对第二个p标签替换内容
            cdemo[1].innerHTML="这是通过类名设置的第二个p标签";
        </script>
    </body>
    ```

- 根据==标签名==来查询一组元素节点对象： 

  - `document.getElementsByTagName("标签名")；`

  - 返回的是一个数组类型变量，存在索引

    ```js
    <body>
        <p >hello</p>
        <p >hello</p>
        <p id="demo"></p>
        <script>
            var demo1 = document.getElementsByTagName("p");
            // 对第一个p标签替换内容
            demo1[0].innerHTML="这是第一个p标签";
            // 对第二个p标签替换内容
            demo1[1].innerHTML="这是第二个p标签";
            // 将getElementsByTagName的文本 赋值给getElementById 显示
            document.getElementById("demo").innerHTML="这个是通过获取到一个新的p标签的id显示的结果&nbsp;&nbsp;&nbsp"+demo1[0].innerHTML;
    
    				// 遍历的形式
    				for (var i = 0;i<demo1.length;i++){
              console.log(demo1[i]);  
            }
    
        </script>
    </body>
    ```
    
  - 通过父元素获取指定的子元素，不包括父元素

    ```js
    <body>
        <ol id="ol">
            <li>li</li>
            <li>li</li>
            <li>li</li>
            <li>li</li>
        </ol>
        <script>
            var list = document.getElementsByTagName("ol");
            var ol = document.getElementById("ol");
            list[1].getElementsByTagName("li");
            ol.getElementsByTagName("li");
        </script>
    </body>
    ```

- 通过 CSS 选择器查找 HTML 元素

  - 使用 `querySelectorAll()` 方法，返回所有的元素

  - `querySelector()` 获取第一个选择器元素
  
  - `class` 选择器：`.` 
  
  - `id  ` 选择器：`#`
  
    ```js
    <body>
        <p>Hello World!</p>
        <p class="intro">DOM很有用</p>
        <p class="intro">DOM！！！！</p>
        <p id="demo"></p>
        <script>
            var x = document.querySelectorAll(".intro");
            document.getElementById("demo").innerHTML = 'class ="intro" 的第一段（索引 0）：' + x[0].innerHTML;
        </script>
    </body>
    ```

元素的属性：  **读取元素的属性：**  

​		语法：`元素.属性名`    

- 获取body元素
  - `document.body` 

- 获取html 元素
  - `document.documentElement`

- `ele.id`   
- `ele.value`   
- `ele.className`   

注意：class属性不能采用这种方式读取class属性时需要使用 `元素.className`	   

修改元素的属性： 
	语法：`元素.属性名 = 属性值`  



###  DOM修改  

- `element.innerText`
  - 起始位置到终止位置的内容，会去除html标签，同时空格和换行也会去除
- `element.innerHTML`
  - 起始位置到终止位置的内容，保留html标签、空格和换行
- `innerHTML`和`innerText`区别
  - 不同点：`innerHTML`会获取到html标签，而innerText会自动去除标签
  - 设置标签内部的内容时，没有任何区别的，都可读取标签内部的文本内容


| 方法                                      | 说明                                                         |
| ----------------------------------------- | ------------------------------------------------------------ |
| `document.createElement("TagName")`       | 创建元素节点对象， 它需要标签名作为参数，将会根据该标签名创建元素节点对象，并将创建好的对象作为返回值返回 |
| `document.createTextNode("textContent") ` | 根据文本内容创建文本节点对象                                 |
| `父节点.appendChild(子节点)`              | 向父节点中添加指定的子节点                                   |
| `父节点.insertBefore(新节点,旧节点)`      | 将新的节点插入到旧节点的前边                                 |
| `父节点.replaceChild(新节点,旧节点)`      | 新的节点去替换旧节点                                         |
| `父节点.removeChild(子节点)`              | 删除指定的子节点                                             |
| `子节点.parentNode.removeChild(子节点)`   | 改变了相应元素（标签）的innerHTML的值                        |

### 操作元素

#### DOM修改元素属性

点击按钮修改显示的图片

```js
<body>
    <button id="img1">1</button>
    <button id="img2">2</button>
    <img src="../../Images/1.jpeg" alt="">
    <script>
        // 1. 获取元素
        var img1 = document.getElementById("img1");
        var img2 = document.getElementById("img2");
        var showImg = document.querySelector("img");
        // 2.绑定监听事件
        img1.onclick = function () {
            showImg.src = "../../Images/1.jpeg";
            showImg.title="1";
        }
        img2.onclick = function () {
            showImg.src="../../Images/2.jpeg"
           // 还可以修改其他的元素 
            showImg.title="2";
        }
    </script>
</body>
```



分时问候案例

```js
<body>
    <div>上午好</div>
    <img src="../../Images/10.jpeg" alt="">
    <script>
        // 获取元素
        var div = document.querySelector("div"); // 获取到div这个标签
        var changeImg = document.querySelector("img") // 获取img元素
        // 获取时间
        var date = new Date();
        var hours = date.getHours();
        //比较系统时间
        if (hours > 0 && hours < 8) {
            changeImg.src = "../../Images/cool.jpg";
            div.innerHTML = "走开，还没有到点起床";
        } else if (hours >= 8 && hours < 12) {
            changeImg.src = "../../Images/girls.jpeg";
            div.innerHTML = "码农开始上班了😎";
        } else if (hours >= 12 && hours < 14) {
            changeImg.src = "../../Images/meinv1.jpg";
            div.innerHTML = "午休时间";
        } else if (hours >= 14 && hours < 18) {
            changeImg.src = "../../Images/sun.jpeg";
            div.innerHTML = "继续敲代码嘀嘀嘀❤️‍🔥";
        } else if (hours >= 18 && hours < 20) {
            changeImg.src = "../../Images/guinv.jpg";
            div.innerHTML = "加班时间😭";
        } else if (hours >= 20) {
            changeImg.src = "../../Images/25.jpeg";
            div.innerHTML = "回家睡觉❤️";
        }
    </script>
</body>
```

#### 修改表单属性值

- 使用`value` 修改
- 禁用点击后的按钮 ：`disable`属性

```js
<body>
    <button>修改</button>
    <input type="text" value="输入文本">
    <script>
        // 获取元素
        var button = document.querySelector("button");
        var input = document.querySelector("input");
        // 绑定点击按钮事件
        button.onclick = function(){
            // 设置表单属性使用innerHTMl是不能修改内容的，使用value进行修改值
            input.value = "按钮被点击了"
            // 当点击了按钮，将按钮禁用
            // button.disabled = true;
            // this 指向当前事件的调用者
            this.disabled = true;
        }
    </script>
</body>
```

显示 / 隐藏密码 案例

```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>显示隐藏密码</title>
    <style>
        .box {
            position: relative;
            width: 400px;
            height: 25px;
            margin: 100px auto;
            border-bottom: 1px solid #ccc;
        }
        .box input {
            width: 380px;
            height: 20px;
            border: 0;
            outline: none;
        }
        .box img {
            position: absolute;
            width: 24px;
            top: 2px;
            right: 0px;
        }
        p {
            float: left;
            margin-left: 270px;
            margin-top: -1px;
        }
    </style>
</head>

<body>
    <p>密码：</p>
    <div class="box">
        <label for="">
            <img src="../../Images/closeeye.png" alt="" id="eye">
        </label>
        <input type="password" id="passwd">
    </div>
    <script>
        // 获取元素
        var eyeImg = document.getElementById("eye");
        var pwd = document.getElementById("passwd");
        // 控制遍历
        var flag = 0;
        //绑定事件
        eyeImg.onclick = function () {
            if (flag == 0) {
                pwd.type = "text";
                flag = 1;
                eyeImg.src = "../../Images/openeys.png";
            } else {
                pwd.type = "password";
                flag = 0;
                eyeImg.src = "../../Images/closeeye.png";
            }
        }
    </script>
</body>
</html>
```

#### 修改样式属性

- 样式采用驼峰命名
- 使用Style样式修改

```js
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        div{
            width: 500px;
            height: 500px;
            background-color: green;
        }        
    </style>
</head>
<body>
    <div id="div1" ></div>
    <script>
        // 获取点击事件
        var div = document.getElementById("div1");
        div.onclick = function(){
            div.style.backgroundColor = "red";
            div.style.width = "100%";
        }
    </script>
</body>
</html>
```



#### 显示隐藏文本框内容

表单需要两个事件

- 获得焦点 `onfocus`
- 失去焦点 `onblur`

```js
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        input{
            color: #999;
            margin: 100px auto;
        }
    </style>
</head>
<body>
    <input type="text" value="显示内容">
    <script>
        // 1.获取元素
        var inputInfo = document.querySelector("input");
        // 2.注册事件，获得焦点事件 onfocus
        inputInfo.onfocus= function(){
            if(this.value == "显示内容"){
                this.value ="";
            }
            // 获得焦点时，设置文本样式
            this.style.color = "black";
        }
        // 3.注册事件，失去焦点 onblur
        inputInfo.onblur = function(){
            if(this.value == ""){
                this.value ="显示内容";
            }
            this.style.color = "#999";
        }
    </script>
</body>
</html>
```



#### `className` 修改样式

- 事先定义好 css 类，在需要的地方调用类名
- 多类名选择器：

```js
// 保留旧的类名
element.className ="旧类名 新类名"
```



输入密码案例提示信息

```js
  <style>
      div {
          width: 600px;
          margin: 100px auto;
          line-height: 25px;
      }
      /*提示信息*/
      .msg {
          /*行内式*/
          display: inline-block;
          font-size: 25px;
          color: #999999;
          background: url("../../Images/info.png") no-repeat left center;
          padding-left: 30px;
      }
      /*错误类*/
      .wrong {
          color: red;
          background-image: url("../../Images/error.png");
      }

      /* 正确类*/
      .right {
          color: green;
          background-image: url("../../Images/right.png");
      }
  </style>
</head>
<body>
  <div class="register">
    <input type="password" class="ipt">
    <p class="msg">请输入6~10位密码</p>
  </div>
  <script>
    // 获取元素对象
    var inputs = document.querySelector("input");
    var meg = document.querySelector(".msg");
    // 注册事件 失去焦点
    inputs.onblur = function () {
      // 根据长度判断
      if (this.value.length < 6 || this.value.length > 10) {
        meg.className = "msg wrong";
        meg.innerHTML = "您输入密码长度不符合要求";
      }else {
        meg.className = "msg right";
        meg.innerHTML = "正确";
      }
    }
  </script>
</body>
```

#### HTML5自定义属性

```js
    <div getTime="20" data-index="2" data-list-name="andy"></div>
    <script>
        var div = document.querySelector('div');
        // console.log(div.getTime);
        console.log(div.getAttribute('getTime'));
        div.setAttribute('data-time', 20);
        console.log(div.getAttribute('data-index'));
        console.log(div.getAttribute('data-list-name'));

        // h5新增的获取自定义属性的方法 它只能获取data-开头的
        // dataset 是一个集合里面存放了所有以data开头的自定义属性，在IE11以上可以兼容，IE10以下不兼容
        console.log(div.dataset);
        console.log(div.dataset.index);
        console.log(div.dataset['index']);

        // 自定义属性里面有多个-链接的单词，获取的时候采取:驼峰命名法
        console.log(div.dataset.listName);
        console.log(div.dataset['listName']);
    </script>
```





<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221127221637531.png" alt="image-20221127221637531" style="zoom:67%;" />

### 节点操作

利用节点层级关系获取元素

- 利用父子结点关系获取元素
- 逻辑性强，但兼容性差



节点至少拥有三个基本属性

- nodeType（节点类型）
- nodeName（节点名称）
- nodeValue（节点值）



- 元素节点`nodeType`为1
- 属性节点`nodeType`为2
- 文本节点nodeType为3（文本节点包含文字、空格、换行等）

#### 父级节点

`node.parentNode`

```
// 得到的是离元素最近的父级节点(亲爸爸)如果找不到父节点就返回为null
erweima.parentNode;
```

- parentNode属性可返回某节点的最近父节点
- 如果指定的节点没有父节点则返回null

#### 子节点

1. `parentNode.childNodes`
   - `parentNode.childNodes`返回包含指定节点的子节点的集合，为即时更新的集合
   - 如果只想要获得里面的元素节点，需要专门处理。一般不提倡使用childNodes

```js
 console.log(ul.childNodes); // 获取ul节点里面的所以孩子节点、元素节点、属性节点等节点
```



2. `parentNode.children`==重点==
   - `parentNode.children`是一个只读属性，获取==所有的子元素节点==它只返回子元素节点，其余节点不返回

```js
console.log(ul.children);
```



3. `parentNode.firstChild`
   - 返回第一个子节点

```js
console.log(ol.firstChild);
```



4. `parentNode.lastChild`
   - 返回最后一个子节点

```js
console.log(ol.lastChild);
```



5. `parentNode.firstElementChild`
   - 返回第一个子元素节点

```js
console.log(ol.firstElementChild);
```

6. `parentNode.lastElementChild`
   - 返回最后一个子元素节点

```js
console.log(ol.lastElementChild);
```

注意：这两个方法有兼容性问题，IE9以上才支持，实际开发的写法 既没有兼容性问题又返回

```js
console.log(ol.children[0]); // 第一孩子节点
console.log(ol.children[ol.children.length - 1]);
```
下拉菜单案例

```js
    <script>
        // 1. 获取元素
        var nav = document.querySelector('.nav');
        var lis = nav.children; // 得到4个小li
        // 2.循环注册事件
        for (var i = 0; i < lis.length; i++) {
            lis[i].onmouseover = function() {
                this.children[1].style.display = 'block';
            }
            lis[i].onmouseout = function() {
                this.children[1].style.display = 'none';
            }
        }
    </script>
```

![xialacaidan](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/xialacaidan.gif)

#### 兄弟节点

1. `node.nextSibling` 
   - 返回当前元素的下一个兄弟节点，包含所有的节点。

```js
console.log(div.nextSibling);
```



2.`node.previousSibling`

- 当前元素上一个兄弟节点，找不到则返回null，包含所有的节点

```js
console.log(div.previousSibling);
```



3.`node.nextElementSibling`

- 当前元素下一个兄弟节点

```js
console.log(div.nextElementSibling);
```



4.`node.previousElementSibling`

- 返回当前元素上一个兄弟节点

```js
console.log(div.previousElementSibling);
```

有兼容性问题，IE9以上才支持

        function getNextElementSibling(element) {
            var el = element;
            while (el = el.nextsibling) {
                if (el.nodeType === 1) {
                    return el;
                }
            }
            return null;
        }
#### 创建、添加节点

`document.createElement（‘tagName’）`

`document.createElement（）`方法创建由tagName指定的HTML元素。因为这些元素原先不存在，是根据我们的需求动态生成的，所以我们也称为动态创建元素节点。



1. `node.appendChild（child）`
   - 将一个节点添加到指定父节点列表末尾，类似于css里面的after伪元素

2. `node.insertBefore（child，指定元素）`
   - 将一个节点添加到父节点的指定子节点前面。类似于css里面的before伪元素

```js
// 创建节点元素
var li = document.createElement('li');
var ul = document.querySelector('ul');
// 添加节点node.appendChild(child) node:父级, child:子级, 后面追加元素,类似于数组中的push
ul.appendChild(li);
// 3.添加节点node.insertBefore(child,指定元素);
var lili = document.createElement('li')
ul.insertBefore(lili,ul.children[0]);// 在第一个元素前面添加入节点
```
发布内容案例

```js
<body>
    <textarea  name="" id="">默认内容</textarea>
    <button>发布</button>
    <ul>

    </ul>
    <script>
        // 1. 获取元素
        var btn = document.querySelector('button');
        var text = document.querySelector('textarea');
        var ul = document.querySelector('ul');
        // 2. 注册事件
        btn.onclick = function () {
            if (text.value == '') {
                alert('您没有输入内容');
                return false;
            } else {
                // (1) 创建元素
                var li = document.createElement('li');
                // 先有li 才能赋值
                li.innerHTML = text.value + "<a href='javascript:;'>删除</a>";
                // (2) 添加元素
                // ul.appendChild(li); 追加
                ul.insertBefore(li, ul.children[0]);
                // 点击发布之后就会清空
                text.value = "";
                // (3) 删除元素 删除的是当前链接的li
                var as = document.querySelectorAll('a');
                for (var i = 0; i < as.length; i++) {
                    as[i].onclick = function() {
                        // 删除的是 li 当前a所在的li
                        ul.removeChild(this.parentNode);
                    }
                }
            }
        }
        // 焦点事件
        text.onfocus= function(){
            if(this.value == "默认内容"){
                this.value ="";
            }
        }
        // 3.注册事件，失去焦点 onblur
        text.onblur = function(){
            if(this.value == ""){
                this.value ="默认内容";
            }

        }
    </script>
</body>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/fabu.gif" alt="fabu" style="zoom: 50%;" />



#### 删除节点

`node.removeChild（child）`

- 从DOM中删除一个子节点，返回删除的节点


```js
ul.removeChild(ul.children[0])
阻止链接跳转添加JavaScript：void（0）；或者JavaScript;

// 获取元素
var ul = document.querySelector('ul');
var btn = document.querySelector('button');
// 点击按钮依次删除里面的孩子
btn.onclick = function() {
    if (ul.children.length == 0) {
       // 没有孩子节点，则禁用按钮
        this.disabled = true;
    } else {
        // 永远删除第一个孩子节点
        ul.removeChild(ul.children[0]);
    }

```


#### 复制节点（克隆节点）

`node.cloneNode()`方法返回调用该方法的节点的一个副本

```js
var ul = document.querySelector('ul')
 
var lili = ul.children[0].cloneNode();
 
var lili = ul.children[0].cloneNode(true);
 
ul.appendChild(lili); // 将克隆的节点追加
```
==注意：==



1. 括号为空或者里面是`false`浅拷贝，只复制标签不复制里面的内容，即只克隆复制节点本省，不克隆里面的子节点。
2. 如果括号参数为true，则是深度拷贝，会复制节点本身以及里面所有的子节点。

#### 动态生成表单

```js
<body>
    <table cellspacing="0">
        <thead>
            <tr>
                <th>姓名</th>
                <th>科目</th>
                <th>成绩</th>
                <th>操作</th>
            </tr>
        </thead>
        <tbody>
        </tbody>
    </table>
    <script>
        // 1.对象存储数据，数组存储对象
        var datas = [{
            name: '魏璎珞',
            subject: 'JavaScript',
            score: 100
        }, {
            name: '弘历',
            subject: 'JavaScript',
            score: 98
        }, {
            name: '傅恒',
            subject: 'JavaScript',
            score: 99
        }, {
            name: '明玉',
            subject: 'JavaScript',
            score: 88
        }, {
            name: 'nnnnn',
            subject: 'JavaScript',
            score: 0
        }, {
            name: "kkkong",
            subject: "java",
            score: 87
        }];
        // 2. 往tbody 里面创建行： 有几个人（通过数组的长度）就创建几行
        var tbody = document.querySelector('tbody');
        for (var i = 0; i < datas.length; i++) { // 外面的for循环管行 tr
            // 1. 创建 tr行
            var tr = document.createElement('tr');
            tbody.appendChild(tr);
            // 2. 行里面创建单元格(跟数据有关系的3个单元格) td 单元格的数量取决于每个对象里面的属性个数  for循环遍历对象 datas[i]
            for (var k in datas[i]) { // 里面的for循环管列 td
                // 创建单元格 
                var td = document.createElement('td');
                // 把对象里面的属性值 datas[i][k] 给 td
                td.innerHTML = datas[i][k];
                tr.appendChild(td);
            }
            // 3. 创建有删除2个字的单元格 
            var td = document.createElement('td');
            td.innerHTML = '<a href="javascript:;">删除 </a>';
            tr.appendChild(td);
        }
        // 4. 删除操作 开始 
        var as = document.querySelectorAll('a');
        for (var i = 0; i < as.length; i++) {
            as[i].onclick = function () {
                // 点击a 删除 当前a 所在的行  node.removeChild(child)  
                tbody.removeChild(this.parentNode.parentNode)
            }
        }
    </script>
</body>
```





#### 表格隔行变色

`js`代码

```js
    <script>
        // 1.获取元素 获取的是 tbody 里面所有的行
        var trs = document.querySelector('tbody').querySelectorAll('tr');
        // 2. 利用循环绑定注册事件
        for (var i = 0; i < trs.length; i++) {
            // 3. 鼠标经过事件 onmouseover
            trs[i].onmouseover = function() {
                    // 选中类
                    this.className = 'bg';
                }
                // 4. 鼠标离开事件 onmouseout
            trs[i].onmouseout = function() {
                this.className = '';
            }
        }
    </script>
```

#### 表达全选

```js
    <script>
        // 1. 全选和取消全选做法：  让下面所有复选框的checked属性（选中状态） 跟随全选按钮
        // 获取元素
        var j_cbAll = document.getElementById('j_cbAll'); // 全选按钮
        var j_tbs = document.getElementById('j_tb').getElementsByTagName('input'); // 下面所有的复选框
        // 全选按钮注册事件
        j_cbAll.onclick = function () {
            // this.checked 获得当前checkbox的选中状态
            console.log(this.checked);
            // 获取到表内容的复选框选中状态
            for (var i = 0; i < j_tbs.length; i++) {
                j_tbs[i].checked = this.checked;
            }
        }
        // 2.给下面所有复选框绑定点击事件，每次点击，都要循环查看下面所有的复选框是否有没选中的，如果有一个没选中的，上面全选就不选中。
        for (var i = 0; i < j_tbs.length; i++) {
            j_tbs[i].onclick = function () {
                // flag 控制全选按钮是否选中
                var flag = true;
                // 每次点击下面的复选框都要循环检查者4个小按钮是否全被选中
                for (var i = 0; i < j_tbs.length; i++) {
                    if (!j_tbs[i].checked) {
                        flag = false;
                        break; // 退出for循环 只要有一个没有选中，则无需循环判断
                    }
                }
                j_cbAll.checked = flag;
            }
        }
    </script>
```



![image-20221128163516046](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221128163516046.png)



### 排他算法

> 同一组元素，需要给某一个元素实现某种样式，需要使用循环排他算法

1. 清除全部元素的样式
2. 给当前元素设置样式

```js
<body>
    <button>按钮1</button>
    <button>按钮2</button>
    <button>按钮3</button>
    <button>按钮4</button>
    <button>按钮5</button>
    <script>
        // 1.获取所有同样元素
        var btns = document.getElementsByTagName("button");
        // 2.循环遍历得到每个元素
        for (let i = 0; i < btns.length; i++) {
            // 2.1给每个按钮创建一个点击事件
            btns[i].onclick = function () {
                // 2.2清除所有按钮的样式 里外循环遍历都要一致
                for (let i = 0; i< btns.length; i++) {
                    btns[i].style.backgroundColor = "";
                }
                // 2.3设置当前元素的样式
                this.style.backgroundColor = "green";
            }
        }
    </script>
</body>
```

修改背景图片案例

- 给同一组元素注册事件
- 利用循环点击事件
- 点击当前图片即可切换背景图片
- 核心算法：获取到图片背景图路径

```js
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background: url("../../Images/10.jpeg") no-repeat center top;
        }

        li {
            /*不显示列表前的点*/
            list-style: none;
        }

        .img {
            overflow: hidden;
            margin: 100px auto;
            background-color: #ffffff;
            width: 510px;
            padding-top: 3px;
        }

        .img li {
            float: left;
            margin: 0 1px;
            cursor: pointer;
        }

        .img img {
            width: 100px;
        }
    </style>
</head>
<body>
    <ul class="img">
        <li><img src="../../Images/10.jpeg"></li>
        <li><img src="../../Images/11.jpeg"></li>
        <li><img src="../../Images/12.jpeg"></li>
        <li><img src="../../Images/13.jpeg"></li>
        <li><img src="../../Images/14.jpeg"></li>
    </ul>
    <script>
        // 1. 获取所有的图片元素
        var imgs = document.querySelector(".img").querySelectorAll("img");
        // 循环注册事件
        for (let i = 0; i < imgs.length; i++) {
            // 每个图片设置点击事件
            imgs[i].onclick = function () {
                // 获取到当前图片的路径 this.src 就是当前图片的路径
                document.body.style.backgroundImage = "url(" + this.src + ")";
            }
        }
    </script>
</body>
```

#### 获取自定义属性

```js
<body>
    <div id="demo" index="1" class="nav"></div>
    <script>
        var div = document.querySelector('div');
        // 1. 获取元素的属性值
        // (1) element.属性
        console.log(div.id);
        //(2) element.getAttribute('属性')  get得到获取 attribute 属性的意思，自定义属性：index
        console.log(div.getAttribute('id'));
        console.log(div.getAttribute('index'));

        // 2. 设置元素属性值
        // (1) element.属性= '值'
        div.id = 'test';
        div.className = 'navs';
        // (2) element.setAttribute('属性', '值');  主要针对于自定义属性
        div.setAttribute('index', 2);
        div.setAttribute('class', 'footer'); // class特殊，这里面写的是class 不是className

        // 3 移除属性 removeAttribute(属性) 
        div.removeAttribute('index');

    </script>
</body>
```

#### tab栏切换

```js
<head>
    <meta charset="UTF-8">
    <title>tab栏切换</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        .tab {
            width: 978px;
            margin: 100px auto;
        }
        
        .tab_list {
            height: 39px;
            border: 1px solid #ccc;
            background-color: #f1f1f1;
        }
        
        .tab_list li {
            float: left;
            height: 39px;
            line-height: 39px;
            padding: 0 20px;
            text-align: center;
            cursor: pointer;
        }
        .tab_list .current {
            background-color: #c81623;
            color: #fff;
        }
        
        .item_info {
            padding: 20px 0 0 20px;
        }
        /*隐藏item内容*/
        .item {
            display: none;
        }
    </style>
</head>

<body>
    <div class="tab">
        <div class="tab_list">
            <ul>
                <li class="current">商品介绍</li>
                <li>规格与包装</li>
                <li>售后保障</li>
                <li>商品评价（50000）</li>
                <li>手机社区</li>
            </ul>
        </div>
        <div class="tab_con">
            <!-- -->
            <div class="item" style="display: block;">
                商品介绍模块内容
            </div>
            <div class="item">
                规格与包装模块内容
            </div>
            <div class="item">
                售后保障模块内容
            </div>
            <div class="item">
                商品评价（50000）模块内容
            </div>
            <div class="item">
                手机社区模块内容
            </div>
        </div>
    </div>
    <script>
        // 1.获取元素
        var tab_list = document.querySelector('.tab_list');
        var lis = tab_list.querySelectorAll('li');
        var items = document.querySelectorAll('.item');
        // 2.for循环绑定点击事件
        for (var i = 0; i < lis.length; i++) {
            // 开始给5个小li 设置索引号 
            lis[i].setAttribute('index', i);
            lis[i].onclick = function() {
                // 2.1. 上的模块选项卡，点击某一个，当前这一个底色会是红色，其余不变（排他思想） 修改类名的方式
                // 其余的li清除 class 这个类
                for (var i = 0; i < lis.length; i++) {
                    // 清空所有选项的样式
                    lis[i].className = '';
                }
                // 清除之后，设置当前点中选项的样式
                this.className = 'current';
                
                // 2.2下面的显示内容模块
                var index = this.getAttribute('index');
                console.log(index);
                // 所有的item的div隐藏
                for (var i = 0; i < items.length; i++) {
                    items[i].style.display = 'none';
                }
                // 让对应的item显示出来
                items[index].style.display = 'block';
            }
        }
    </script>
</body>
```

![tab切换](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/tab%E5%88%87%E6%8D%A2.gif)









### 创建元素

三种方式区别：

1. `documen.write()` 如果页面文档加载完毕，会覆盖掉前面HTML界面
2. `documen.createElement()` 
3. `document.innerHTml` 拼接字符串的方式花费的时间比较长，执行效率较低；通过数组追加，最后一次渲染出来，花费的时间较少，执行效率更高





### DOM操作总结

> 主要是增删改查、属性操作

#### 创建

1. `document.write`
2. `innerHTML`
3. `createElement`

#### 增加元素

1. `appendChild` ：在后面增加
2. `insertBefore`：在前面插入

#### 删除

1. `removeChild` ：移除指定的元素

#### 修改

1. 修改元素属性：src ，href 等
2. 修改普通元素的内容：innerHTML、innerText
3. 修改表单元素：value、type、disable等
4. 修改元素样式：style、className

#### 查

1. 获取DOMAPI元素：获取元素ID（`getElementByID`）、标签名（`getElementByTagName`）
2. HTML5提供新查询的方法：`querySeletor`、`querySelectorAll`等
3. 节点获取元素：父（`parentNode`），子（`Children`）、兄（`previousElementSibling`、`nextElementSibling`）







# Document 对象

## 查找HTML元素

| 方法                                    | 描述                                                         |
| :-------------------------------------- | :----------------------------------------------------------- |
| `document.getElementById(id)`           | 通过元素 id 来查找元素                                       |
| `document.getElementsByTagName(name)`   | 通过标签名来查找元素                                         |
| `document.getElementsByClassName(name)` | 通过类名来查找元素                                           |
| `document.querySelector()`              | 根据CSS选择器去页面中查询一个元素，如果匹配到的元素有多个，则返回查询到的第一个元素 |
| `document.querySelectorAll()`           | 根据CSS选择器去页面中查询一组元素，会将匹配到所有元素封装到一个数组中返回，即使只匹配到一个 |

## 改变HTML元素

| 方法                                    | 描述                   |
| :-------------------------------------- | :--------------------- |
| `element.innerHTML = new html content`  | 改变元素的 inner HTML  |
| `element.attribute = new value`         | 改变 HTML 元素的属性值 |
| `element.setAttribute(attribute,value)` | 改变 HTML 元素的属性值 |
| `element.style.property = new style`    | 改变 HTML 元素的样式   |

## 添加和删除元素

| 方法                              | 描述             |
| :-------------------------------- | :--------------- |
| `document.createElement(element)` | 创建 HTML 元素   |
| `document.removeChild(element)`   | 删除 HTML 元素   |
| `document.appendChild(element)`   | 添加 HTML 元素   |
| `document.replaceChild(element)`  | 替换 HTML 元素   |
| `document.write(text)`            | 写入 HTML 输出流 |

## 添加事件处理程序对象

| 方法                                                     | 描述                            |
| :------------------------------------------------------- | :------------------------------ |
| `document.getElementById(id).onclick = function(){code}` | 向 onclick 事件添加事件处理程序 |

## 查找HTML对象

| 属性                           | 描述                                                         | DOM  |
| :----------------------------- | :----------------------------------------------------------- | :--- |
| `document.anchors`             | 返回拥有 name 属性的所有 <a> 元素。                          | 1    |
| `document.applets`             | 返回所有 <applet> 元素（HTML5 不建议使用）                   | 1    |
| `document.baseURI`             | 返回文档的绝对基准 URI                                       | 3    |
| `document.body`                | 返回 <body> 元素                                             | 1    |
| `document.cookie`              | 返回文档的 cookie                                            | 1    |
| `document.doctype`             | 返回文档的 doctype                                           | 3    |
| `document.documentElement`     | 返回 <html> 元素                                             | 3    |
| `document.documentMode`        | 返回浏览器使用的模式                                         | 3    |
| `document.documentURI`         | 返回文档的 URI                                               | 3    |
| `document.domain`              | 返回文档服务器的域名                                         | 1    |
| `document.domConfig`           | 废弃。返回 DOM 配置                                          | 3    |
| `document.embeds`              | 返回所有 <embed> 元素                                        | 3    |
| `document.forms`               | 返回所有 <form> 元素                                         | 1    |
| `document.head`                | 返回 <head> 元素                                             | 3    |
| `document.images`              | 返回所有 <img> 元素                                          | 1    |
| `document.implementation`      | 返回 DOM 实现                                                | 3    |
| `document.inputEncoding`       | 返回文档的编码（字符集）                                     | 3    |
| `document.lastModified`        | 返回文档更新的日期和时间                                     | 3    |
| `document.links`               | 返回拥有 href 属性的所有 <area> 和 <a> 元素                  | 1    |
| `document.readyState`          | 返回文档的（加载）状态                                       | 3    |
| `document.referrer`            | 返回引用的 URI（链接文档）                                   | 1    |
| `document.scripts`             | 返回所有 <script> 元素                                       | 3    |
| `document.strictErrorChecking` | 返回是否强制执行错误检查                                     | 3    |
| `document.title`               | 返回 <title> 元素                                            | 1    |
| `document.URL`                 | 返回文档的完整 URL                                           | 1    |
| `元素.childNodes `             | 获取当前元素的所有子节点，会获取到空白的文本子节点  <br />在IE8及以下的浏览器中，不会将空白文本当成子节点，所以该属性在IE8中会返回4个子元素而其他浏览器是9个 |      |
| `元素.children`                | 获取当前元素的所有子元素                                     |      |
| `元素.firstChild `             | 获取当前元素的第一个子节点，会获取到空白的文本子节点         |      |
| `元素.lastChild`               | 获取当前元素的最后一个子节点                                 |      |
| `元素.parentNode`              | 获取当前元素的父元素                                         |      |
| `元素.previousSibling`         | 获取当前元素的前一个兄弟节点，IE8及以下不支持                |      |
| `元素.nextSibling`             | 获取当前元素的后一个兄弟节点                                 |      |
| `元素.firstElementChild`       | 获取当前元素的第一个子元素，不支持IE8及以下的浏览器<br />如果需要兼容他们尽量不要使用 |      |
| `元素.firstChild.nodeValue `   | 获取第一个子元素的文本值                                     |      |

## 其他属性、方法

| 属性、方法                          | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| `document.all()`                    | 获取页面中的所有元素，相当于`document.getElementsByTagName("*");` |
| `document.documentElement() `       | 获取页面中html根元素                                         |
| `document.body()`                   | 获取页面中的body元素                                         |
| `document.getElementsByClassName()` | 根据元素的class属性值查询一组元素节点对象（IE8及以下的浏览器不支持） |





# DOM对CSS的操作

### 读取和修改内联样式  

1. 使用style属性操作元素的内联样式 
   	读取内联样式： `元素.style.样式名 `

```js
	元素.style.width 
	元素.style.height 
	注意：如果样式名中带有-，则需要将样式名修改为驼峰命名法将-去掉，然后后的字母改大写 
	比如：backgroundcolor > backgroundColor 、borderwidth > borderWidth 
```

2. 修改内联样式： 

   ```js
   元素.style.样式名 = 样式值 
   ```

   - 通过style修改和读取的样式都是内联样式，由于内联样式的优先级比较高，所以通过JS来修改的样式，往往会立即生效， 如果样式中设置了 `!important`，则内联样式将不会生效。	  

### 读取元素的当前样式

正常浏览器

```js
使用getComputedStyle()，属于window对象的方法，可以返回一个对象，这个对象中保存着当前元素生效样式  
参数：  
	1.要获取样式的元素  
	2.可以传递一个伪元素，一般传null  
例子：  
获取元素的宽度  
	getComputedStyle(box , null)["width"];  
  通过该方法读取到样式都是只读的不能修改  
```

IE8

```
使用currentStyle  
语法：  
	元素.currentStyle.样式名  
例子：  
	box.currentStyle["width"]  
  这个属性读取到的样式是只读的不能修改
```

实现兼容性

```javascript  
/*  
* 对象.属性不存在，不会报错，如果直接寻找对象，（当前作用域到全局作用域）找不到会报错  
* 定义一个函数，用来获取指定元素的当前的样式  
* 参数：  
* 		obj 要获取样式的元素  
* 		name 要获取的样式名  
*/  
function getStyle(obj , name){  
//对象.属性不存在，不会报错，如果直接寻找对象，（当前作用域到全局作用域）找不到会报错  
    if(window.getComputedStyle){  
        //正常浏览器的方式，具有getComputedStyle()方法  
        return getComputedStyle(obj , null)[name];  
    }else{  
        //IE8的方式，没有getComputedStyle()方法  
        return obj.currentStyle[name];  
    }  
    //return window.getComputedStyle?getComputedStyle(obj , null)[name]:obj.currentStyle[name];			  
}  
```

### 其他的样式相关的属性

==以下样式都是只读的,未指明偏移量都是相对于当前窗口左上角== 

| 属性                                     | 说明                                                         |
| ---------------------------------------- | ------------------------------------------------------------ |
| `clientHeight `                          | 元素的可见高度，包括元素的内容区和内边距的高度               |
| `clientWidth  `                          | 元素的可见宽度，包括元素的内容区和内边距的宽度               |
| `offsetHeight  `                         | 整个元素的高度，包括内容区、内边距、边框                     |
| `offfsetWidth`                           | 整个元素的宽度，包括内容区、内边距、边框                     |
| `offsetParent  `                         | 当前元素的定位父元素，离他最近的开启了定位的祖先元素，如果所有的元素都没有开启定位，则返回body |
| `offsetLeft  `、`offsetTop`              | 当前元素和定位父元素之间的偏移量，`ffsetLeft`水平偏移量  `offsetTop`垂直偏移量 |
| `scrollHeight  `、`scrollWidth  `        | 获取元素滚动区域的高度和宽度                                 |
| `scrollTop  `、`scrollLeft`              | 获取元素垂直和水平滚动条滚动的距离  ，判断滚动条是否滚动到底 |
| `scrollHeight -scrollTop = clientHeight` | 垂直滚动条                                                   |
| `scrollWidth -scrollLeft = clientWidth`  | 水平滚动条                                                   |



# DOM事件（Event）  

## DOM事件简介

事件三要素

1. 事件源：被触发的对象
2. 事件类型：怎么触发？
3. 事件处理程序：通过函数完成赋值



事件指的是用户和浏览器之间的交互行为。比如：点击按钮、关闭窗口、鼠标移动等，可以为事件绑定回调函数来响应事件。 

## 注册事件

### 传统注册事件方式： 

- 利用on开头的事件，创建事件，如下所示
- 特点：注册事件单一性，后面的给相同的元素注册事件会覆盖掉前面的注册事件，也就是同一个元素只能注册一个事件

1.在标签事件属性中设置相应的JS代码

```javascript  
<button onclick="点击执行的事件">按钮</button>
```

2.通过为对象的指定事件属性，设置回调函数的形式来处理事件 

```javascript  
<button id="btn">按钮</button>
<script> 
    var btn = document.getElementById("btn");  
    btn.onclick = function(){  
      alert("点击了我");
    };  
</script>  
```

### 方法监听注册方式：

#### addEventListener()

- 使用 `addEventListener(type,listenner,[UseCaptrue])` 方法
- 可以将同一个元素绑定多个监听事件

```js
<body>
    <button>方法监听注册事件</button>
    <script>
        var btns = document.querySelectorAll('button');
          // 里面的事件类型是字符串 必定加引号 而且不带on
         // 同一个元素 同一个事件可以添加多个侦听器（事件处理程序）
        btns[1].addEventListener('click', function() {
            alert(22);
        })
        btns[1].addEventListener('click', function() {
                alert(33);
            })
    </script>
</body>

// 最后弹窗内容是：先22 后 33
```

该方法的三个参数类型：

1. `type` ：事件类型字符串
2. `listener` ：事件处理程序，一般使用创建一个函数将处理的程序放在这个函数里面
3. `UseCaptrue`：可选参数，选择DOM事件流进行的阶段，返回布尔值。`true`则是处于捕获阶段，`false`则是处于冒泡阶段



#### attachEvent()  

在IE8以下浏览器使用
参数： 

- 事件的字符串，要on 
- 回调函数  

可以同时为一个事件绑定多个处理函数。不同点：==后绑定先执行==，执行顺序和addEventListener()相反  



```j
btn01.attachEvent("onclick",function(){  
alert(1);  
});  
  
btn01.attachEvent("onclick",function(){  
alert(2);  
});	  
```



### 文档的加载

浏览器在加载一个页面时，是按照自上向下的顺序加载的，加载一行执行一行。如果将js代码编写到页面的上边，当代码执行时，页面中的DOM对象还没有加载，此时将会无法正常获取到DOM对象，导致DOM操作失败。 

1. 解决方式一：  
   - 可以将js代码编写到body的下边  	  

```javascript  
<body>  
		<button id="btn">按钮</button>  
  
		<script>  
			var btn = document.getElementById("btn");  
			btn.onclick = function(){  
		  
			};  
	</script>  
</body>  
```

2. 解决方式二： 
   - 将js代码编写到`window.onload = function(){}`中，`window.onload` 对应的回调函数会在整个页面加载完毕以后才执行， 所以可以确保代码执行时,DOM对象已经加载完毕

```javascript  
<script>  
    window.onload = function(){  
        var btn = document.getElementById("btn");  
        btn.onclick = function(){  
        };  
    };  
</script>	    
```

## 删除对象

> 也有两种方式删除对象
>
> 1. 传统的删除对象
>    - `divs[0].onclick = null`
> 2. 方法监听删除对象
>    - `addEventListener(type, function名)` 

```js
<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <button> 1</button>
    <button> 2</button>
    <button> 3</button>
    <button> 4</button>
    <script>
        // 获取的元素对象
        var divs = document.querySelectorAll('div');
        // 获取按钮对象
        let buttonElement = document.querySelectorAll('button'); // 获取所有的button 在下面才会有索引的对应第几个button

        // 第一种：传统方式删除事件
        divs[0].onclick = function () {
            alert(11);
            divs[0].onclick = null; // 对元素进行解绑，只能点击触发事件
        }
        // 第二种：removeEventListener 删除事件
        divs[1].addEventListener('click', fn) // fn为函数名，里面的fn函数不需要调用加小括号
        function fn() {
            alert(22);
            divs[1].removeEventListener('click', fn); // 删除第二关div事件，让其在界面刷新之后只触发一次
        }
				// 点击按钮 触发删除事件，而且指挥触发一次
        // 按钮对象删除事件
        buttonElement[0].addEventListener('click', btnfn);
        buttonElement[1].addEventListener('click', btnfn);
        buttonElement[2].addEventListener('click', btnfn);
        buttonElement[3].addEventListener('click', btnfn);
        function btnfn() {
            alert("已删除该按钮事件");
            buttonElement[0].removeEventListener('click', btnfn);
        }

        // 第三种：detachEvent
        divs[2].attachEvent('onclick', fn1);

        function fn1() {
            alert(33);
            divs[2].detachEvent('onclick', fn1);
        }
    </script>
</body>
```



注意事项

> 1. 在使用`removeEventListener` 删除事件时，要先对元素进行添加事件，并且给定事件类型 (type)，以及（创建）函数名 ，而函数名不要带括号，就是不要进行函数调用，移除事件时的时候也不能带括号。



## DOM事件流

### DOM事件流介绍

- 事件流：描述的是从页面中接收事件的顺序。

- DOM事件流过程：事件发生时会在元素节点之间按照特定的顺序传播。

- DOM事件流分为3个阶段：==三个一次只能处于一个阶段==

  1. 捕获阶段：文档（Document）== >  元素HTML（Element HTML）== > 元素body == > 目标对象元素 （从最外层的元素往目标元素阶段进去。如果希望在捕获阶段就触发事件，可以将addEventListener()的第三个参数设置为`true`，

  2. 当前进行阶段 ：目标对象元素执行

  3. 冒泡阶段：与捕获阶段相反进行 （从目标元素往外层元素出去）

  ~~~mermaid
  graph LR
  a(1.捕获阶段)-->b(2.当前元素执行阶段)
  
  b(2.当前元素执行阶段)-->c(冒泡阶段)
  ~~~

三个阶段执行过程

![image-20221204152254722](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221204152254722.png)

捕获阶段：

```js
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // 捕获阶段 如果addEventListener 第三个参数true则为捕获阶段，元素执行顺序: document -> html -> body -> father -> son
        var son = document.querySelector('.son');
        son.addEventListener('click', function() {
            alert('son');
        }, true);
				document.addEventListener('click', function() {
            alert('document');
        }, true)
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, true);
    </script>
</body>

// 弹窗顺序：document -> father -> son
```

冒泡阶段：

```js
<body>
    <div class="father">
        <div class="son">son盒子</div>
    </div>
    <script>
        // 冒泡阶段 如果addEventListener 第三个参数是false或者省略,则处于冒泡阶段，元素执行顺序  son -> father ->body -> html -> document
        var son = document.querySelector('.son');
        document.addEventListener('click', function() {
            alert('document');
        })
        son.addEventListener('click', function() {
            alert('son');
        }, false);
        var father = document.querySelector('.father');
        father.addEventListener('click', function() {
            alert('father');
        }, false);
    </script>
</body>
// 弹窗顺序：son -> father -> document
```

> 注意：
> JS 代码中只能执行捕获或者冒泡其中的一个阶段。
> onclick 和 attachEvent（ie） 只能得到冒泡阶段。
>
> 有些事件是没有冒泡的，比如 onblur, onfocus, onmouseenter, onmouseleave



## 事件对象

### 事件介绍

- 事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象event。
- 当响应函数被调用时，浏览器每次都会将一个事件对象作为实参传递进响应函数中，这个事件对象中封装了当前事件的相关信息，比如：鼠标的坐标，键盘的按键，鼠标的按键，滚轮的方向等 

- 可以在响应函数中定义一个形参，来使用事件对象，但是在IE8以下浏览器中事件对象没有做完实参传递，而是作为window对象的属性保存  


例子说明：  

```javascript  
元素.事件 = function(event){  
    event = event || window.event;  
};  
  
元素.事件 = function(e){  
	e = e || event;  
	  
};  
```

获取到鼠标的坐标` clientX和clientY` 用于获取鼠标在当前的可见窗口的坐标，div的偏移量，是相对于整个页面的`pageX和pageY` 可以获取鼠标相对于当前页面的坐标 但是这个两个属性在IE8中不支持，所以如果需要兼容IE8，则不要使用  

```js
var left = event.clientX;
var　top = event.clientY;
```





```js
<body>
    <div>123</div>
    <script>
        // div事件对象
        var div = document.querySelector('div');
        div.onclick = function (e) {
            // console.log(e);
            // console.log(window.event); // 不兼容下：ie678中的事件对象
            // e = e || window.event;  // 兼容处理
            console.log(e);
        }
        // div.addEventListener('click', function(e) {
        //         console.log(e);
        //     })
    </script>
</body>
```

> 1. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看
> 2. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数
> 3. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键
> 4. 这个事件对象我们可以自己命名 比如 event 、 evt、 e
> 5. 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法  e = e || window.event;



### 事件属性和方法

![image-20221204155952991](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221204155952991.png)

1. `e.target` 返回的是==触发事件==的对象（元素）
2. `this `返回的是==绑定事件==的对象（元素）

 区别 ： 

- `e.target` 点击了那个元素，就返回那个元素
- `this `那个元素绑定了这个点击事件，那么就返回谁

```js
<body>
    <div>123</div>
    <ul>
        <li>abc</li>
        <li>abc</li>
        <li>abc</li>
    </ul>
    <script>
        // 常见事件对象的属性和方法
        // 1. e.target 返回的是触发事件的对象（元素）  this 返回的是绑定事件的对象（元素）
        // 区别 ： e.target 点击了那个元素，就返回那个元素 this 那个元素绑定了这个点击事件，那么就返回谁
        var div = document.querySelector('div');
        div.addEventListener('click', function (e) {
            console.log(e.target);
            console.log(this);
        })
        // 获取 ul 元素
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function (e) {
            // 给ul绑定了事件  那么this 返回ul
            console.log(this);  // 指向ul
            console.log(e.currentTarget); // 返回的是绑定事件，与this一样返回结果
            // e.target 指向我们点击的那个对象，谁触发了这个事件 我们点击的是li，e.target就指向li
            console.log(e.target);// 指向li
        })
    </script>
</body>
```

其他事件属性

```js
<body>
    <div>123</div>
    <a href="http://www.baidu.com">百度</a>
    <form action="http://www.baidu.com">
        <input type="submit" value="提交" name="sub">
    </form>
    <script>
        // 常见事件对象的属性和方法
        // 1. 返回事件类型
        var div = document.querySelector('div');
        div.addEventListener('click', fn);
        div.addEventListener('mouseover', fn);
        div.addEventListener('mouseout', fn);
        function fn(e) {
            console.log(e.type);

        }

        // 2. 阻止默认行为（事件） 让链接不跳转 或者让提交按钮不提交
        var a = document.querySelector('a');
        a.addEventListener('click', function (e) {
            e.preventDefault(); // 阻止跳转，标准写法
        })
        // 3. 传统的注册方式
        a.onclick = function (e) {
            // 普通浏览器 e.preventDefault();  方法
            // e.preventDefault();
            // 低版本浏览器 ie678  returnValue  属性
            // e.returnValue;
            // 我们可以利用return false 也能阻止默认行为 没有兼容性问题 特点： return 后面的代码不执行了， 而且只限于传统的注册方式
            return false;
            alert(11);// 无法弹出11 ，return 执行之后就会退出函数
        }
    </script>
</body>
```



## 事件的冒泡（Bubble）  

事件的冒泡指的是事件向上传导，当后代元素上的事件被触发时，将会导致其祖先元素上的同类事件也会触发。 
事件的冒泡大部分情况下都是有益的，如果需要取消冒泡，则需要使用事件对象来取消，可以将事件对象的cancelBubble设置为true，即可取消冒泡
 例子：  

```javascript  
元素.事件 = function(event){  
    event = event || window.event;  
    event.cancelBubble = true;// 低版本浏览器
};  
```

### 阻止冒泡

```js
<body>
    <div class="father">
        <div class="son">son儿子</div>
    </div>
    <script>
        var son = document.querySelector('.son');
        son.addEventListener('click', function(e) {
            alert('son');
            e.stopPropagation(); // 停止传播冒泡，不会向上进行冒泡，所以后面的father、document就不会弹出
            e.cancelBubble = true; // 非标准 cancel 取消 bubble 泡泡
        }, false); //false 进行DOM事件流的冒泡阶段

        var father = document.querySelector('.father');
        father.addEventListener('click', function(e) {
            alert('father');
          	e.stopPropagation();// 停止传播冒泡,但是点击了father区域还是会向上冒泡所以在father的也添加一个stopPropagation阻止冒泡
        }, false);
        document.addEventListener('click', function(e) {
            alert('document');
          	e.stopPropagation();
        })
    </script>
</body>

```

## 事件委派  

==将事件统一绑定给元素的共同的祖先元素，这样当后代元素上的事件触发时，会一直冒泡到祖先元素，从而通过祖先元素的响应函数来处理事件。==  



事件委派是利用了冒泡阶段，通过委派可以减少事件绑定的次数，提高程序的性能，希望只绑定一次事件，即可应用到多个的元素上，即使元素是后添加的，可以尝试将其绑定给元素的共同的祖先元素.。

`target : event`中的 target 表示的触发事件的对象



```js
<body>
    <ul>
        <li>li1！</li>
        <li>li2！</li>
        <li>li3！</li>
        <li>li4！</li>
        <li>li5！</li>
    </ul>
    <script>
        // 事件委托的核心原理：给父节点添加监听器， 利用事件冒泡影响每一个子节点
        // 获取父节点 ul
        var ul = document.querySelector('ul');
        ul.addEventListener('click', function(e) {
            // 点击li的元素，修改背景颜色
            e.target.style.backgroundColor = 'pink';
        })
    </script>
</body>
```



## 常用事件  

### 鼠标事件

| 事件          | 说明                         |
| ------------- | ---------------------------- |
| `onclick`     | 点击鼠标右键触发             |
| `onfocus`     | 获得光标焦点触发             |
| `onblur`      | 失去光标焦点触发             |
| `onmouseover` | 光标经过触发                 |
| `onmouseout`  | 光标离开触发                 |
| `onmousedown` | 按下任意鼠标键触发           |
| `onmouseup`   | 释放任意鼠标键触发           |
| `onmousemove` | 在元素内当光标移动时持续触发 |

### 鼠标坐标事件

| 属性                                                         | 描述                                                         | DOM  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :--- |
| [altKey](https://www.runoob.com/jsref/event-altkey.html)     | 返回当事件被触发时，"ALT" 是否被按下。                       | 2    |
| [button](https://www.runoob.com/jsref/event-button.html)     | 返回当事件被触发时，哪个鼠标按钮被点击。                     | 2    |
| [clientX](https://www.runoob.com/jsref/event-clientx.html)   | 返回当事件被触发时，鼠标指针的水平坐标。                     | 2    |
| [clientY](https://www.runoob.com/jsref/event-clienty.html)   | 返回当事件被触发时，鼠标指针的垂直坐标。                     | 2    |
| [ctrlKey](https://www.runoob.com/jsref/event-ctrlkey.html)   | 返回当事件被触发时，"CTRL" 键是否被按下。                    | 2    |
| [Location](https://www.runoob.com/jsref/event-key-location.html) | 返回按键在设备上的位置                                       | 3    |
| [charCode](https://www.runoob.com/jsref/event-key-charcode.html) | 返回onkeypress事件触发键值的字母代码。                       | 2    |
| [key](https://www.runoob.com/jsref/event-key-key.html)       | 在按下按键时返回按键的标识符。                               | 3    |
| [keyCode](https://www.runoob.com/jsref/event-key-keycode.html) | 返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码。 | 2    |
| [which](https://www.runoob.com/jsref/event-key-which.html)   | 返回onkeypress事件触发的键的值的字符代码，或者 onkeydown 或 onkeyup 事件的键的代码。 | 2    |
| [metaKey](https://www.runoob.com/jsref/event-metakey.html)   | 返回当事件被触发时，"meta" 键是否被按下。                    | 2    |
| [relatedTarget](https://www.runoob.com/jsref/event-relatedtarget.html) | 返回与事件的目标节点相关的节点。                             | 2    |
| [screenX](https://www.runoob.com/jsref/event-screenx.html)   | 返回当某个事件被触发时，鼠标指针的水平坐标。                 | 2    |
| [screenY](https://www.runoob.com/jsref/event-screeny.html)   | 返回当某个事件被触发时，鼠标指针的垂直坐标。                 | 2    |
| [shiftKey](https://www.runoob.com/jsref/event-shiftkey.html) | 返回当事件被触发时，"SHIFT" 键是否被按下。                   | 2    |

| 方法                | 描述                   | W3C  |
| :------------------ | :--------------------- | :--- |
| initMouseEvent()    | 初始化鼠标事件对象的值 | 2    |
| initKeyboardEvent() | 初始化键盘事件对象的值 | 3    |

#### 案例

```js
<body>
    不可复制文本
    <script>
        // 1. contextmenu 我们可以禁用右键菜单
        document.addEventListener('contextmenu', function (e) {
            e.preventDefault();
        })
        // 2. 禁止选中文字 selectstart
        document.addEventListener('selectstart', function (e) {
            e.preventDefault();// 阻止行为
        })
    </script>
</body>

```

鼠标基本事件

```js
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>鼠标事件</title>
    <style>
        * {
            margin: 0;
            padding: 0;

        }

        div {
            margin: 100px auto;
            position: relative;
            width: 400px;
            height: 400px;
            background-color: red;
        }

        p {
            margin: 100px 100px;
            width: 200px;
            height: 200px;
            position: absolute;
            background-color: blue;
        }
    </style>
</head>
<body>
    <div>
        <p></p>
    </div>
    <script>
        // 获取到div、p 元素
        var div = document.querySelector('div');
        var p = document.querySelector('p');
        // 1, 单击事件 click
        p.onclick = function () {
            alert("单击")
        }
        // 2, 双击事件 dblclick
        p.ondblclick = function () {
            alert("双击")
        }
        // 3, 鼠标按下  mousedown
        p.onmousedown = function () {
            alert('鼠标按下')
        }
        // 4, 鼠标抬起  mouseup
        p.onmouseup = function () {
            alert('鼠标抬起')
        }
        // 5, 鼠标移动  mousemove
        p.onmousemove = function () {
            alert("鼠标在这个div内部正在移动ing")
        }
        // 6, 右键菜单  contextmenu
        p.oncontextmenu = function () {
            alert("调出右键菜单")
        }
        // 7, 滑轮滚动  wheel
        p.onwheel = function () {
            alert("滑轮滚动")
        }
        // 8, 鼠标移入移出 mouseenter/mouseleave  不继承,鼠标在子标签上不会触发事件
        div.onmouseenter = function () {
            console.log("鼠标移入");
            p.style.backgroundColor = "green";
        }
        div.onmouseleave = function () {
            console.log("鼠标移出");
            p.style.backgroundColor = "black";
        }
        // 简单来说就是鼠标进入div区域会显示移入，出div就会显示移出

        // 9, 鼠标悬停离开  mouseover/mouseout 会继承, 鼠标在子标签上也会触发事件
        div.onmouseover = function () {
            console.log("鼠标悬停");
            p.style.backgroundColor = "pink";
        }
        div.onmouseout = function () {
            console.log("鼠标离开");
        }
        // 而悬停离开的话，就是鼠标进入div区域会提示悬停，然后鼠标进入p标签区域会先显示 离开 再悬停，最后移出显示离开
    </script>
</body>
</html>
```

设置图片随着光标移动案例

```js
<head>
    <meta charset="UTF-8">
    <title>鼠标背景随着移动</title>
    <style>
        img {
            /*对图像鼠标进行绝对定位*/
            position: absolute;
            top: 2px;
        }
    </style>
</head>

<body>
    <img src="../../Images/mouse.png" alt="">
    <script>
        // 获取到图片元素
        var img = document.querySelector('img');

        // mousemove 鼠标移动坐标
        document.addEventListener('mousemove', function (e) {
            //获取鼠标移动的坐标,将图片的top赋值给y left赋值给x 图片就会随着鼠标光标移动
            var x = e.pageX;
            var y = e.pageY;
            console.log("当前坐标为：" + "(" + x + "," + y + ")");
            // 给图片位置赋值 必须添加单位
          	// 可以理解为：X、Y为一个二维坐标。top方向是上下的，所以对应的是获取光标的Y值，left的方向是左右的，所以获取的光标的X值
            img.style.top = y-5 + "px"; // 向上移动5，减去5 
            img.style.left = x-10 + "px"; // 向左移动10，减去10 
        });
    </script>
</body>
```



### 键盘事件  

- 键盘事件一般会绑定获取到焦点的对象或者是document对象

| 键盘事件                         | 说明                                                         |
| -------------------------------- | ------------------------------------------------------------ |
| `onkeydown  `                    | 按下键盘触发，一直按一直触发                                 |
| `onkeyup`                        | 按键松开触发                                                 |
| `keyCode `                       | 通过`keyCode`来获取按键ASCII编码，可以判断哪个按键被按下。还有其他属性判断按键状态。==已经被弃用== |
| `altKey `、`ctrlKey`、`shiftKey` | 判断alt ctrl 和 shift是否被按下，按下则返回true，否则返回false |
| `onkeypress`                     | 某个键盘按键被按下并松开。不能识别功能键 Shift 、Ctrl 、Alt、 |

**关于keyCode 被弃用处理：**

> keyCode=“键盘的ASCLL码值”，例 keyCode=“80”、keyCode="76"等
> 改为
> key=“键盘的字母内容”，例 key=“a”、key=“Alt”、key="Enter"等



键盘事件案例：

```js
<body>
    <script>
        // 常用的键盘事件
        document.addEventListener('keyup', function () {
            console.log('我弹起了');
        })
        // keypress 按键按下的时候触发  不能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keypress', function () {
            console.log('我按下了press');
        })
        // keydown 按键按下的时候触发  能识别功能键 比如 ctrl shift 左右箭头啊
        document.addEventListener('keydown', function () {
            console.log('我按下了down');
        })
        // 三个事件的执行顺序  keydown -- keypress -- keyup
    </script>
</body>
```

输出结果：

![image-20221204213852138](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221204213852138.png)



**按下指定的按键触发** 

```javascript  
//判断y和ctrl是否同时被按下  
if(event.keyCode === 89 && event.ctrlKey){  
	console.log("ctrl和y都被按下了");  
}  
// 将keyCode 改成key使用
if(event.key == 'c' && event.ctrlKey){  
	console.log("ctrl和y都被按下了");  
} 
```

```javascript  
input.onkeydown = function(event) {  
    event = event || window.event;  
    //数字 48 - 57  
    //使文本框中不能输入数字  
    if(event.keyCode >= 48 && event.keyCode <= 57) { //0~9
        //在文本框中输入内容，属于onkeydown的默认行为  
        //如果在onkeydown中取消了默认行为，则输入的内容，不会出现在文本框中  
        return false;  
    }  
};  
```

```js
<body>
    <script>
        // keyup 和keydown事件不区分字母大小写  a 和 A 得到的都是65
        
        document.addEventListener('keyup', function (e) {
            // console.log(e);
            console.log('up:' + e.keyCode);
            // 利用keycode返回的ASCII码值来判断用户按下了那个键
            // if (e.keyCode === 65) {
  					 // key 是判断 a 字符
            if (e.key == 'a') {
                alert('您按下的a键');
            } else {
                alert('您没有按下a键')
            }
        })
				// keypress 事件区分字母大小写  a=97 和 A=65
        document.addEventListener('keypress', function (e) {
            // console.log(e);
            console.log('press:' + e.keyCode);
        })
    </script>
</body>
```

#### 按键输入内容案例

- 检测用户是否按下 s 键 ，按下 s 键，则将光标定位到输入框内
- 使用KeyCode属性，判断是否为 s 键
- 搜索框获得焦点，focus() 方法

```js
<body>
    <input type="text">
    <script>
        // 获取输入框的元素
        var search = document.querySelector('input');
        // 创建按下按钮事件 使用keyup 按下s键提起之后才会获得交代呢
        document.addEventListener('keyup', function (e) {
            // 判断是否为 s 键
            if (e.keyCode === 83) { // 三个等号，严格控制类型和值都要相等
                search.focus();
            }
        })
    </script>
</body>
```



#### 输入文本时方法字体案例

- 快递单号输入内容时， 上面的大号字体盒子（con）显示(这里面的字号更大）
- 表单检测用户输入： 给表单添加键盘事件
- 同时把快递单号里面的值（value）获取过来赋值给 con盒子（innerText）做为内容
- 如果快递单号里面内容为空，则隐藏大号字体盒子(con)盒子



```js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>输入内容放大</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        .search {
            position: relative;
            width: 178px;
            margin: 100px;
        }

        /*一开始是隐藏*/
        .con {
            display: none;
            position: absolute;
            top: -40px;
            width: 171px;
            border: 1px solid rgba(0, 0, 0, .2);
            box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
            padding: 5px 0;
            font-size: 18px;
            line-height: 20px;
            color: #333;
        }

        /*输入文本之后*/
        .con::before {
            content: '';
            width: 0;
            height: 0;
            position: absolute;
            top: 28px;
            left: 18px;
            border: 8px solid #000;
            border-style: solid dashed dashed;
            border-color: #fff transparent transparent;
        }
    </style>
</head>

<body>
    <div class="search">
        <div class="con">123</div>
        <input type="text" placeholder="请输入您的快递单号" class="jd">
    </div>
    <script>
        // 获取元素
        var con = document.querySelector('.con');
        var jd_input = document.querySelector('.jd');
        // 使用keyup原因 是让其按下抬起之后，再触发事件
        jd_input.addEventListener('keyup', function () {
            // 判断当前输入的文本内容是否为空
            if (this.value == '') {
                // 没有内容输入则一直隐藏
                con.style.display = 'none';
            } else {
                // 有内容输入则显示放大框
                con.style.display = 'block';
                con.innerText = this.value;
            }
        })
        // 当我们失去焦点，就隐藏这个con盒子
        jd_input.addEventListener('blur', function () {
            con.style.display = 'none';
        })
        // 当我们获得焦点，就显示这个con盒子
        jd_input.addEventListener('focus', function () {
            if (this.value !== '') {
                con.style.display = 'block';
            }
        })
    </script>
</body>
</html>
```

### 传统的ON开头HTML事件

- 不常用

| 事件          | 描述                         |
| :------------ | :--------------------------- |
| `onchange`    | HTML 元素已被改变            |
| `onclick`     | 用户点击了 HTML 元素         |
| `onmouseover` | 用户把鼠标移动到 HTML 元素上 |
| `onmouseout`  | 用户把鼠标移开 HTML 元素     |
| `onkeydown`   | 用户按下键盘按键             |
| `onload`      | 浏览器已经完成页面加载       |





# JavaScript BOM

## BOM简介

浏览器对象模型(`Browser Object Mode`) ，BOM通过JS来操作浏览器，在BOM中为提供了一组对象，用来完成对浏览器的操作BOM对象，允许 JavaScript 与浏览器对话



### BOM的构造

BOM 比 DOM 作用范围更加大

~~~mermaid
graph TB
A(JavaScript)-->a(BOM)
A(JavaScript)-->a1(DOM)
a(BOM)-->b(Window)
b(Window)-->a2(Document)
b(Window)-->c(Navigator)
b(Window)-->d(Location)
b(Window)-->e(History)
b(Window)-->f(Screen)
~~~





Window。

- 代表的是整个浏览器的窗口，同时window也是网页中的==顶级对象==。访问浏览器的接口，同时也是 Window 的全局变量，BOM对象在浏览器中作为window对象的属性保存，可以通过window对象来使用，也可以直接使用该属性，但是我们一般情况下会省略掉`Window.xxx方法()`  

Navigator

- 代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器

Location

-  代表当前浏览器的地址栏信息，通过Location可以获取地址栏信息，或者操作浏览器跳转页面

History

- 代表浏览器的历史记录，可以通过该对象来操作浏览器的历史记录，由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页，而且该操作只在当次访问时有效

Screen

- 代表用户的屏幕的信息，通过该对象可以获取到用户的显示器的相关的信息  



## Window

### Window 常见事件

| 事件                      | 事件说明                                         |
| ------------------------- | ------------------------------------------------ |
| `window.innerHeight`      | 浏览器窗口的内部高度(包括滚动条)                 |
| `window.innerWidth`       | 浏览器窗口的内部宽度(包括滚动条)                 |
| `window.open() `          | 打开新窗口                                       |
| `window.close()`          | 关闭窗口                                         |
| `window.moveTo()`         | 移动当前窗口                                     |
| `window.resizeTo() `      | 调整当前窗口的尺寸                               |
| `window.load()`           | 当文档内容加载完毕再触发该事件，旧的注册事件方式 |
| `window.DOMContentLoaded` | DOM加载完毕即可执行                              |

代码案例：

```js
<head>
    <meta charset="UTF-8">
    <title>Window点击触发事件</title>
    <script>
        window.addEventListener('load', function () {
            var btn = document.querySelector('button');
            btn.addEventListener('click', function () {
                alert('点击我');
            })
        })
        // load 等页面内容全部加载完毕，包含页面dom元素 图片 flash  css 等等
        window.addEventListener('load', function () {
            alert(22);
        })
        // DOMContentLoaded 是DOM加载完毕就执行，不包含图片 falsh css 等就可以执行 加载速度比 load更快一些
        document.addEventListener('DOMContentLoaded', function () {
            alert(33);
        })
				// 最后的弹出效果：33 --> 22 --> 点击我
    </script>
</head>

<body>
    <button>点击</button>
</body>
```



```js
<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        // resize 调整窗口大小的事件
        window.addEventListener('resize', function () {
            console.log(window.innerWidth);
            console.log('变化了');
            // innerWidth 当前屏幕的宽度 小于 800 就隐藏该颜色
            if (window.innerWidth <= 800) {
                div.style.display = 'none';
            } else {
                div.style.display = 'block';
            }
        })
    </script>
</body>
```

![windowWidth](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/windowWidth.gif)



###  定时器 setInterval()

定时调用：可以将一个函数，每隔一段时间执行一次 

- 每隔一定的时间就回去重复调用这个函数

```js
参数：
	1.回调函数，该函数会每隔一段时间被调用一次  
	2.每次调用间隔的时间，单位是毫秒  
返回值：  
	返回一个Number类型的数据  
	这个数字用来作为定时器的唯一标识
```

```js
<body>
    <script>
        // 语法规范：  window.setInterval(调用函数, 延时时间);
        var count1 = 0;
        var count2 = 0;
        setInterval(function () {
            count1++;
            console.log("第一种第 " + count1 + " 次执行setInterval");

        }, 2000);
        setInterval(intervalFun,2000);
        function intervalFun(){
            count2++;
            console.log("第2种第 " + count2 + " 次执行setInterval");
        }
        // setTimeout  延时时间到了，就去调用这个回调函数，只调用一次 就结束了这个定时器
        // setInterval  每隔这个延时时间，就去调用这个回调函数，会调用很多次，重复调用这个函数
    </script>
</body>
```

倒计时效果：

```js
<head>
    <meta charset="UTF-8">
    <title>倒计时案例</title>
    <style>
        div {
            margin: 200px;
        }

        span {
            display: inline-block;
            width: 40px;
            height: 40px;
            background-color: #333;
            font-size: 20px;
            color: #fff;
            text-align: center;
            line-height: 40px;
        }
    </style>
</head>

<body>
    <div>
        <span class="hour">1</span>
        <span class="minute">2</span>
        <span class="second">3</span>
    </div>
    <script>
        // 1. 获取元素 
        var hour = document.querySelector('.hour'); // 小时的黑色盒子
        var minute = document.querySelector('.minute'); // 分钟的黑色盒子
        var second = document.querySelector('.second'); // 秒数的黑色盒子
        var inputTime = +new Date('2022-12-6 16:00:00'); // 返回的是用户输入时间总的毫秒数
        countDown(); // 我们先调用一次这个函数，防止第一次刷新页面有空白
        
        // 2. 开启定时器
        setInterval(countDown, 1000);
        function countDown() {
            var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
            var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
            var h = parseInt(times / 60 / 60 % 24); //时
            h = h < 10 ? '0' + h : h;
            hour.innerHTML = h; // 把剩余的小时给 小时黑色盒子  
            // 分
            var m = parseInt(times / 60 % 60); 
            m = m < 10 ? '0' + m : m;
            minute.innerHTML = m;

            var s = parseInt(times % 60); // 当前的秒
            s = s < 10 ? '0' + s : s;
            second.innerHTML = s;
        }
    </script>
</body>
```

![image-20221205160342128](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205160342128.png)









**clearInterval()** 清除定时器 



可以用来关闭一个定时器方法中需要一个定时器的标识作为参数，这样将关闭标识对应的定时器，可以接收任意参数，如果参数是一个有效的定时器的标识，则停止对应的定时器，如果参数不是一个有效的标识，则什么也不做  

```javascript  
var num = 1;  
var timer = setInterval(function() {  
	count.innerHTML = num++;  
	if(num == 11) {  
		//关闭定时器  
		clearInterval(timer);  
	}  
}, 1000);  
```



```js
<body>
    <button class="begin">开启定时器</button>
    <button class="stop">停止定时器</button>
    <p class="showData"></p>
    <script>
        var begin = document.querySelector('.begin');
        var stop = document.querySelector('.stop');
        var show = document.querySelector('.showData');

        var timer = null; // 全局变量 定时器名称  null是一个空对象
        var count = 0; // 计数

        begin.addEventListener('click', function () {
            timer = setInterval(function () {
                count++;
                show.innerHTML = "打印计数:" + count;
            }, 1000);
        })
        stop.addEventListener('click', function () {
            clearInterval(timer);
            show.innerHTML = "总共计数:" + count + "次";
        })
    </script>
</body>
```

由于时间原因后面在打印了5次， 所以总共打印了9次

![image-20221205161059706](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205161059706.png) ![image-20221205161158288](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205161158288.png)





发送短信案例

> 按钮点击之后，会禁用 disabled 为true 
> 同时按钮里面的内容会变化， 注意 button 里面的内容通过 innerHTML修改
> 里面秒数是有变化的，因此需要用到定时器 `setInterval`
> 定义一个变量，在定时器里面，不断递减  ：`time`
> 如果变量为0 说明到了时间，我们需要停止定时器，并且复原按钮初始状态



```js
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        p{
            /* 一开始先隐藏 */
            display: none;
        }
    </style>
</head>

<body>
    手机号码： <input type="number">
    <button>发送</button>
    <p> 无法接受?? </p>
    <script>
        var btn = document.querySelector('button');
        var input = document.querySelector('input');
        var p = document.querySelector('p');
        var time = 5; // 定义剩下的秒数
        btn.addEventListener('click', function () {
            btn.disabled = true; // 倒计时期间,禁用按钮
            var timer = setInterval(function () {
                if (time == 0 ) {
                    // 清除定时器和复原按钮
                    clearInterval(timer);
                    btn.disabled = false; // 启用按钮
                    p.style.display = "block"; // 显示提示文字
                    btn.innerHTML = '发送';
                } else if (input.value !== "") { // 输入有内容就结束倒计时
                    clearInterval(timer); // 清除倒计时
                    btn.disabled = false; // 启动按钮
                    btn.innerHTML = '验证';
                } else {
                    btn.innerHTML = '剩余有效时间' + time + '秒';
                    time--;
                }
            }, 1000);
        })
    </script>
</body>
```



### 延时调用 setTimeout

```js
declare function setTimeout(functionName,delayTime);
参数1：调用的函数
参数2：延迟的时间 单位为ms
```

延时调用函数不马上执行，而是隔一段时间以后在执行，且只执行一次 

- 延时调用和定时调用的区别：定时调用会执行多次，==而延时调用只会执行一次== 
- 延时调用和定时调用实际上是可以互相代替的，在开发中可以根据自己需要去选择  

```js
var timer = setTimeout(function(){ 
	console.log(num++); 
},3000);  

<body>
    <script>
        function delayTimer() {
            alert("3秒后~~~");
        }

        // 调用函数
        setTimeout(delayTimer, 3000);
    </script>
</body>
```

#### 回调函数 callback

```js
<body>
    <img src="../../Images/meinv1.jpg" alt="" class="ad">
    <script>
        var ad = document.querySelector('.ad');
        // 两秒后隐藏 图片
        setTimeout(function() {
            ad.style.display = 'none';
        }, 2000);
    </script>
</body>
```

#### 停止定时器

使用`clearTimeout(timerId)`来关闭一个延时调用`setTimeout()  ` 



`timerId` ：就是定时器的名称。

```js
<body>
    <button>点击停止定时器</button>
    <script>
        var btn = document.querySelector('button');
        var timer = setTimeout(function() {
            console.log('爆炸了');
        }, 2000);
        // 在定时器出发前点击按钮，就不会看到输出的日志
        btn.addEventListener('click', function() {
            clearTimeout(timer);
        })
    </script>
</body>
```



### 定时器中`this` 

> 定时器 的 this 指向 Window ，若是嵌套在多个对象中，最里面的 this 调用的是距离它最近的 对象

```js
<body>
    <button>点击</button>
    <script>
        // 1. 全局作用域或者普通函数中this指向全局对象window
        console.log(this);

        function fn() {
            console.log(this);
        }
        window.fn();
        // 创建定时器 定时器里面的this指向window
        window.setTimeout(function () {
            console.log(this);
        }, 1000);

        // 2. 方法调用中谁调用this指向谁
        // 创建 o 对象
        var o = {
            // sayHi 为 o 的函数
            sayHi: function () {
                console.log(this); // this指向的是 o 这个对象
            }
        }
        o.sayHi();
        var btn = document.querySelector('button');
        btn.addEventListener('click', function () {
            console.log(this); // this指向的是btn这个按钮对象
        })

        // 3. 构造函数中this指向构造函数的实例
        function Fun() {
            console.log(this); // this 指向的是fun 实例对象
        }
        new Fun();
    </script>
</body>
```

## Navigator

代表的当前浏览器的信息，通过该对象可以来识别不同的浏览器，由于历史原因，Navigator对象中的大部分属性已经不能帮助识别浏览器，一般只会使用userAgent来判断浏览器的信息，`userAgent`是一个字符串，这个字符串中包含有用来描述浏览器信息的内容，不同的浏览器会有不同的`userAgent  `



火狐的userAgent 

```
Mozilla5.0 (Windows NT 6.1; WOW64; rv:50.0) Gecko20100101 Firefox50.0  
```

Chrome的userAgent 

```
Mozilla5.0 (Windows NT 6.1; Win64; x64) AppleWebKit537.36 (KHTML, like Gecko) Chrome52.0.2743.82 Safari537.36  
```

IE8  

```
Mozilla4.0 (compatible; MSIE 8.0; Windows NT 6.1; WOW64; Trident7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E) 
```

IE9  

```
Mozilla5.0 (compatible; MSIE 9.0; Windows NT 6.1; WOW64; Trident7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)  
```

IE10  

```
Mozilla5.0 (compatible; MSIE 10.0; Windows NT 6.1; WOW64; Trident7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E)  
```

IE11 

```
Mozilla5.0 (Windows NT 6.1; WOW64; Trident7.0; SLCC2; .NET CLR 2.0.50727; .NET CLR 3.5.30729; .NET CLR 3.0.30729; Media Center PC 6.0; .NET4.0C; .NET4.0E; rv:11.0) like Gecko  
```

==IE11中已经将微软和IE相关的标识已经去除了，目前基本已经不能通过UserAgent来识别一个浏览器是否是IE==

```javascript  
alert(navigator.appName);  
  
var ua = navigator.userAgent;  
  
console.log(ua);  
  
if(firefoxi.test(ua)){  
alert("你是火狐！！！");  
}else if(chromei.test(ua)){  
alert("你是Chrome");  
}else if(msiei.test(ua)){  
alert("你是IE浏览器~~~");  
}else if("ActiveXObject" in window){  
alert("你是IE11，枪毙了你~~~");  
}  
```



## History  

- `history`对象可以用来操作浏览器向前或向后翻页，主要是与历史记录进行交互操作

| length 属性 | 获取到当成访问的链接数量                                     |
| ----------- | ------------------------------------------------------------ |
| back()      | 回退到上一个页面，作用和浏览器的回退按钮一样                 |
| forward()   | 跳转下一个页面，作用和浏览器的前进按钮一样                   |
| go()        | 跳转到指定的页面<br />需要一个整数作为参数  <br/>	1：向前跳转一个页面 相当于forward()  <br/>	2：向前跳转两个页面  <br/>   -1：向后跳转一个页面  <br/>   -2：向后跳转两个页面 |

```js
<body>
    <a href="list.html">点击我去往列表页</a>
    <button>前进</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // history.forward(); // 前进
            history.go(1); // 到下页
        })
    </script>
</body>


<body>
    <a href="index.html">点击我去往首页</a>
    <button>后退</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // history.back(); // 回退上一页
            history.go(-1); // 回到上一页
        })
    </script>
</body>
```

## Location

- `location`该对象中封装了浏览器的地址栏的信息（URL）
- URL：统一资源定位符
- Location 对象是 window 对象的一部分，可通过 window.location.xxx 格式的相关属性对其进行访问。



URL的一般语法格式：

![image-20221205212019938](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205212019938.png)

- protocol：通信协议（http，dtp 等等）
- host：主机，域名（www.baidu.com）
- port：端口号
- path：路径（表示主机的目录或文件地址）
- query：参数（以键值对的形式用&隔开）
- fradment：片段（#后面接链接 或 锚点）



### Location 属性和方法

| 属性       | 描述                                  |
| :--------- | :------------------------------------ |
| hash       | 返回一个URL的锚部分                   |
| host       | 返回一个URL的主机名和端口             |
| hostname   | 返回URL的主机名                       |
| **href**   | 返回完整的URL（==重点==）             |
| pathname   | 返回的URL路径名。                     |
| port       | 返回一个URL服务器使用的端口号         |
| protocol   | 返回一个URL协议                       |
| **search** | 返回一个URL的查询部分（参数）==重点== |

### Location 方法

| 打印location | 获取到地址栏的信息，当前页面的完整路径                       |
| ------------ | ------------------------------------------------------------ |
| assign()     | 用来跳转到其他的页面，作用和直接修改location一样             |
| reload()     | 用于重新加载当前页面，作用和刷新按钮一样，在方法中传递一个`true`作为参数，则会强制清空缓存刷新页面`location.reload(true);` |
| replace()    | 可以使用一个新的页面替换当前页面，调用完毕也会跳转页面，不会生成历史记录，不能使用回退按钮回退 |

```js
<body>
    <button>点击</button>
    <script>
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            // 记录浏览历史，所以可以实现后退功能
            location.assign('https://shier-blog.vercel.app/');
            // 不记录浏览历史，所以不可以实现后退功能
            location.replace('https://shier-blog.vercel.app/');
            // 刷新
            location.reload(true);
        })
    </script>
</body>
```







如果直接将location属性修改为一个完整的路径，或相对路径，则页面会自动跳转到该路径，并且会生成相应的历史记录  

```js
location = "http:www.baidu.com";  
location = "01.BOM.html";  
```

 

倒计时完成页面跳转

```js
<body>
    <div></div>
    <script>
        var div = document.querySelector('div');
        var timer = 5;
        setInterval(function () {
            if (timer == 0) {
                location.href = 'https://shier-blog.vercel.app/';
            } else {
                div.innerHTML = '您将在' + timer + '秒钟之后跳转到首页';
                timer--;
            }
        }, 1000);
    </script>
</body>
```



案例：在第一个页面中输入数据登录跳转到第二个页面，在第二个页面显示出第一个页面输入的数据

```js
<body>
    <form action="index2.html"> <!--跳转到的页面-->
        用户名:<input type="text" name="username">
        <input type="submit" value="首页">
    </form>
</body>
```

第二个页面：

```js
<body>
    <div></div>
    <script>
        // 输出获取到的参数
        console.log(location.search);
        // 去掉问好 substr('起始的位置'，截取几个字符); 弃用了 ,使用slice方法一样的截取字符串
        // var params = location.search.substr(1);
        var params = location.search.slice(1);
        console.log(params);
        // 获取到输入的名字 使用 split 进行分割字符串 返回的是一个数组
        var username = location.search.split("=");

        // 将获取到文本显示
        var showName = document.querySelector('div');
        showName.innerHTML = username[1] + "你好呀!!!";
    </script>
</body>
```

输入Shier



输出的结果：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205215312425.png" alt="image-20221205215312425" style="zoom: 80%;" />







#### 类的操作  

通过`style`属性来修改元素的样式，每修改一个样式，浏览器就需要重新渲染一次页面，执行性能差。



修改元素的`class`属性间接的修改样式，只需修改一次，即可同时修改多个样式，浏览器只需要重新渲染页面一次，性能提高，使表现和行为进一步分离  。

```javascript  
box.className += " b2";	//注意有空格，添加class属性  
```

```javascript  
//定义一个函数，用来向一个元素中添加指定的class属性值  
/*  
 * 参数:  
 * 	obj 要添加class属性的元素  
 *  cn 要添加的class值  
 * 	  
 */  
function addClass(obj, cn) {  
	if (!hasClass(obj, cn)) {  
		obj.className += " " + cn;  
	}  
}  
/*  
 * 判断一个元素中是否含有指定的class属性值  
 * 	如果有该class，则返回true，没有则返回false  
 * 	  
 */  
function hasClass(obj, cn) {  
	var reg = new RegExp("\\b" + cn + "\\b");  
	return reg.test(obj.className);  
}  
/*  
 * 删除一个元素中的指定的class属性  
 */  
function removeClass(obj, cn) {  
	//创建一个正则表达式  
	var reg = new RegExp("\\b" + cn + "\\b");  
	//删除class  
	obj.className = obj.className.replace(reg, "");  
}  
/*  
 * toggleClass可以用来切换一个类  
 * 	如果元素中具有该类，则删除  
 * 	如果元素中没有该类，则添加  
 */  
function toggleClass(obj , cn){	  
	//判断obj中是否含有cn  
	if(hasClass(obj , cn)){  
		//有，则删除  
		removeClass(obj , cn);  
	}else{  
		//没有，则添加  
		addClass(obj , cn);  
	}  
}  
```



## JS执行队列

JS是属于单线程进行操作，同一时间只能执行一个任务，这样子会消耗大量的时间，执行效率比较低。



### JS同步和异步

> HTML5提出了 Web Worker 标准，允许JavaScript进行创建多线程

#### 同步

- 依次排队的完成任务，完成一个任务之后再去做另一个任务，前一个任务不完成，下一个任务就不会开始，任务依次进行执行效率低。多任务单线程

**同步任务**：同步任务都在主线程上执行，形成一个执行栈

#### 异步

- 同一时间进行多个任务，就不需要依次排队等候完成了一个任务之后再去下一个任务。任务同时进行提高效率。多任务多线程

**异步任务**：JS的异步都是通过回调函数实现的，异步任务放到任务队列（消息队列）中



常见的异步任务：

1. 普通事件：如click 、resize等

2. 资源加载：如load、error等

3. 定时器：包括setInterval 、setTimeout、ajax等



### 执行机制

1. 先执行执行栈中的同步任务

2. 异步任务（回调函数）放入任务队列（相当于一个候车室）中
3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈开始执行；

```js
console.log(1);
setTimeout(function() {
    console.log(3);
}, 0);
console.log(2);
```

解析上诉执行的代码：此代码首先会创建一个执行栈，判断是否有回调函数，由此可得如下的表格（一个执行栈、一个回调函数），由JS的执行机制可知（先创建执行栈先执行里面的内容、判断是否执行完执行栈中的内容，执行完毕之后才回去执行回调函数的内容），==由此可知先输出的是 1 再到 2，才会去执行回调函数，最后才输出 3== 

|             执行栈             |           回调函数            |
| :----------------------------: | :---------------------------: |
|        console.log(1);         | function1() {console.log(3);} |
| setTimeout(function1() {}, 0); |                               |
|        console.log(2);         |                               |



多异步任务时

```js
console.log(1);
document.onclick = function () { //此异步任务 只有点击了被异步处理进程才会放入任务队列
    console.log('click');
}
console.log(2);
setTimeout(function () { // 此异步任务 等到了 3 秒 就会被步进程处理放入任务队列
    console.log(3)
}, 3000)
```



#### 事件循环

- 主线程不断重复获得任务队列的任务，执行任务，再获取任务队列任务，再执行任务。



![image-20221205174322745](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221205174322745.png)
