> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# 一、Offset

## 1.1 概述

offset ==> 偏移量 ，可以动态的获取的元素的位置、大小等属性。

- 获得元素距离带有定位父元素的位置
- 获得元素自身的大小(宽度高度) ==返回的数值都不带单位==

offset常用属性：

| 属性                   | 作用                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `element.offsetParent` | 返回作为该元素带有定位的父级元素如果父级都没有定位则返回body |
| `element.offsetTop`    | 返回元素相对带有定位父元素上方的偏移                         |
| `element.offsetLeft`   | 返回元素相对带有定位父元素左边框的偏移                       |
| `element.offsetWidth`  | 返回自身包括padding 、边框、内容区的宽度，返回数值不带单位   |
| `element.offsetHeight` | 返回自身包括padding、边框、内容区的高度，返回数值不带单位    |

注意：

- `offsetLeft` 如果没有父亲或者父亲没有定位，则以 `body`为准

在案例一演示

## 1.2 offset 和 style 的区别

### 1、offset 

① offset 可以得到==任意样式表==中的样式值
② offset 系列获得的数值是==没有单位==的
③ offsetWidth、offsetHeight==包含==padding+border+width
④ offsetWidth、offsetHeight等属性是==只读属性==，只能获取不能赋值

所以，我们想要获取元素大小位置，用offset更合适。

### 2、style

① style 只能得到==行内样式表==中的样式值
② style.width 获得的是==带有单位==的字符串
③ style.width、style.height获得的是==不包含==padding和border 的值
④ style.width、style.height是==可读写属性==，可以获取也可以赋值

所以，我们想要给元素更改值，则需要用style改变。







## offset案例

### 案例一

> 获取鼠标在盒子内的坐标



1. 我们在盒子内点击， 想要得到鼠标距离盒子左右的距离。
2. 首先得到鼠标在页面中的坐标（ e.pageX, e.pageY）
3. 其次得到盒子在页面中的距离(box.offsetLeft, box.offsetTop)
4. ==用鼠标距离页面的坐标减去盒子在页面中的距离==， 得到鼠标在盒子内的坐标



```js
<head>
    <meta charset="UTF-8">
    <title>盒子坐标</title>
    <style>
        .box {
            width: 300px;
            height: 300px;
            background-color: pink;
            margin: 200px;
        }
    </style>
</head>

<body>
    <div class="box"></div>
    <script>
        var box = document.querySelector('.box');
        box.addEventListener('mousemove', function(e) {
            // offsetLeft、offsetTop 盒子与边框的距离
            var x = e.pageX - this.offsetLeft;
            var y = e.pageY - this.offsetTop;
            this.innerHTML = '鼠标坐标是(' + x + ',' + y + ')';
        })
    </script>
</body>
```

![image-20221217215131346](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221217215131346.png)

### 案例二

> 拖动的模块框



1. 点击弹出，则显示登录框 `display:block`
2. 点击关闭，则关闭登录框`display:none`
3. 拖动原理：鼠标按下并且移动，松开鼠标
4. 使用到鼠标事件：`mousedown`：鼠标按下、`mousemove`：鼠标移动 、`mouseup`：鼠标松开

```html
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .login-header {
            width: 100%;
            text-align: center;
            height: 30px;
            font-size: 24px;
            line-height: 30px;
        }

        * {
            padding: 0px;
            margin: 0px;
        }

        .login {
            display: none;
            width: 512px;
            height: 280px;
            position: fixed;
            border: #ebebeb solid 1px;
            left: 50%;
            top: 50%;
            background: #ffffff;
            box-shadow: 0px 0px 20px #ddd;
            z-index: 9999;
            transform: translate(-50%, -50%);
        }

        .login-title {
            width: 100%;
            margin: 10px 0px 0px 0px;
            text-align: center;
            line-height: 40px;
            height: 40px;
            font-size: 18px;
            position: relative;
            cursor: move;
        }

        .login-input-content {
            margin-top: 20px;
        }

        .login-button {
            width: 50%;
            margin: 30px auto 0px auto;
            line-height: 40px;
            font-size: 14px;
            border: #ebebeb 1px solid;
            text-align: center;
        }

        .login-bg {
            display: none;
            width: 100%;
            height: 100%;
            position: fixed;
            top: 0px;
            left: 0px;
            background: rgba(0, 0, 0, .3);
        }

        a {
            text-decoration: none;
            color: #000000;
        }

        .login-button a {
            display: block;
        }

        .login-input input.list-input {
            float: left;
            line-height: 35px;
            height: 35px;
            width: 350px;
            border: #ebebeb 1px solid;
            text-indent: 5px;
        }

        .login-input {
            overflow: hidden;
            margin: 0px 0px 20px 0px;
        }

        .login-input label {
            float: left;
            width: 90px;
            padding-right: 10px;
            text-align: right;
            line-height: 35px;
            height: 35px;
            font-size: 14px;
        }

        .login-title span {
            position: absolute;
            font-size: 12px;
            right: -20px;
            top: -30px;
            background: #ffffff;
            border: #ebebeb solid 1px;
            width: 40px;
            height: 40px;
            border-radius: 20px;
        }
    </style>
</head>

<body>
    <div class="login-header"><a id="link" href="javascript:;">点击，弹出登录框</a></div>
    <div id="login" class="login">
        <div id="title" class="login-title">登录会员
            <span><a id="closeBtn" href="javascript:void(0);" class="close-login">关闭</a></span>
        </div>
        <div class="login-input-content">
            <div class="login-input">
                <label>用户名：</label>
                <input type="text" placeholder="请输入用户名" name="info[username]" id="username" class="list-input">
            </div>
            <div class="login-input">
                <label>登录密码：</label>
                <input type="password" placeholder="请输入登录密码" name="info[password]" id="password" class="list-input">
            </div>
        </div>
        <div id="loginBtn" class="login-button"><a href="javascript:void(0);" id="login-button-submit">登录会员</a></div>
    </div>
    <!-- 遮盖层 -->
    <div id="bg" class="login-bg"></div>
    <script>
        // 1. 获取元素
        var login = document.querySelector('.login');
        var mask = document.querySelector('.login-bg');
        var link = document.querySelector('#link');
        var closeBtn = document.querySelector('#closeBtn');
        var title = document.querySelector('#title');
        // 2. 点击弹出层这个链接 link
        link.addEventListener('click', function () {
            mask.style.display = 'block';
            login.style.display = 'block';
        })
        // 3. 点击 closeBtn 就隐藏 mask 和 login
        closeBtn.addEventListener('click', function () {
            mask.style.display = 'none';
            login.style.display = 'none';
        })
        // 4. 开始拖拽，限制拖动的范围
        title.addEventListener('mousedown', function (e) {
            // (1)当鼠标按下，获得鼠标在盒子内的坐标
            var x = e.pageX - login.offsetLeft;
            var y = e.pageY - login.offsetTop;
            //（2）鼠标移动
            document.addEventListener('mousemove', move)
            // (3) 鼠标弹起，鼠标移除事件
            document.addEventListener('mouseup', function () {
                document.removeEventListener('mousemove', move);
            })
            // 移动鼠标事件处理：鼠标移动的时候，把鼠标在页面中的坐标，减去鼠标在盒子内的坐标就是模态框的left和top值
            function move(e) {
                login.style.left = e.pageX - x + 'px';
                login.style.top = e.pageY - y + 'px';
            }
        })
    </script>
</body>
```

### mouseenter 与 mouseover 区别

`mouseenter`事件

- 只会经过自身盒子触发，通常与`mouselevel`搭配使用，不会存在冒泡行为

`mouseover`事件

- 鼠标经过自身盒子就会触发，经过子盒子还会触发



# 二、Client

## 1.1 client 介绍

client 字面意思就是客户端，client的相关属性可以动态获取到元素的边框大小、元素大小等。

### client的属性

| client相关属性         | 作用                                                         |
| ---------------------- | ------------------------------------------------------------ |
| `element.clientTop`    | 返回元素上边框的大小                                         |
| `element.clientLeft`   | 返回元素左边框的大小                                         |
| `element.clientWidth`  | 返回自身包括padding、内容区的宽度、不含边框,返回数值不带单位 |
| `element.clientHeight` | 返回自身包括padding、内容区的高度、不含边框,返回数值不带单位 |



client 的宽度和 offsetWidth 最大的区别就是 不包含边框





## 立即执行函数

> 立即执行函数最大的作用就是独立创建了一个作用域, 里面所有的变量都是局部变量不会有命名冲突的情况



```js
<body>
    <script>
        // 1.立即执行函数: 不需要调用，立马能够自己执行的函数
        function fn() {
            console.log(1);
        }
        fn();
        // 2. 写法也可以传递参数进来
        // 1.(function() {})();
        (function(a, b) {
            console.log(a + b);
            var num = 10;
        })(1, 2); // 第二个小括号可以看做是调用函数
				
				// 2. (function(){}());
        (function sum(a, b) {
            console.log(a + b);
            var num = 10; // 局部变量
        }(2, 3));
        
    </script>
</body>
```

## flexible分许

```js
/**
 * 立即执行函数
 */
(function flexible(window, document) {
    // 获取的html 的根元素
    var docEl = document.documentElement
    // dpr 物理像素比，若是浏览器没有物理像素比，则为1
    var dpr = window.devicePixelRatio || 1
    
    // adjust body font size  设置body的字体大小
    function setBodyFontSize() {
        // 如果页面中有body这个元素就设置body的字体大小
        if (document.body) {
            document.body.style.fontSize = (12 * dpr) + 'px'
        } else {
            // 如果页面中没有body这个元素，则等着页面主要的DOM元素加载完毕再去设置body的字体大小
            document.addEventListener('DOMContentLoaded', setBodyFontSize)
        }
    }
    setBodyFontSize();
    
    // set 1rem = viewWidth / 10  设置html元素的文字大小
    function setRemUnit() {
        var rem = docEl.clientWidth / 10
        docEl.style.fontSize = rem + 'px'
    }
    setRemUnit();
    
    // reset rem unit on page resize  当页面尺寸大小发生变化的时候，要重新设置下rem的大小
    window.addEventListener('resize', setRemUnit)
    // pageshow 是重新加载页面触发的事件，load是每次进入都会触发，具有缓存则不触发
    window.addEventListener('pageshow', function (e) {
        // e.persisted 返回的是true 就是说如果这个页面是从缓存取过来的页面，也需要从新计算一下rem的大小
        if (e.persisted) {
            setRemUnit()
        }
    });

    // detect 0.5px supports  有些移动端的浏览器不支持0.5像素的写法
    if (dpr >= 2) {
        var fakeBody = document.createElement('body')
        var testElement = document.createElement('div')
        testElement.style.border = '.5px solid transparent'
        fakeBody.appendChild(testElement)
        docEl.appendChild(fakeBody)
        if (testElement.offsetHeight === 1) {
            docEl.classList.add('hairlines')
        }
        docEl.removeChild(fakeBody)
    }
}(window, document))
```



# 三、scroll



> 使用scroll系列相关属性可以动态获取该元素的大小、滚动距离等。



| scroll系列属性         | 作用                                   |
| ---------------------- | -------------------------------------- |
| `element.scrollTop`    | 返回被滚动上去的上侧距离，不带单位     |
| `element.scrollLeft`   | 返回被滚动到左侧的距离，不带单位       |
| `element.scrollWidth`  | 返回自身实际的宽度，不含边框，不带单位 |
| `element.scrollHeight` | 返回自身实际的高度，不含边框，不带单位 |

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221218215505925.png" alt="image-20221218215505925" style="zoom: 67%;" />

```js
// scroll滚动事件当我们滚动条发生变化会触发的事件
div.addEventListener('scroll', function() {
    console.log(div.scrollTop);
})
```





`scrollWidth`和`scrollHeight`指的返回自身实际宽和高的意思是，如果box盒子的宽和高都是200px，但是里面的内容已经超过了box盒子，溢出来了，那么`scrollWidth`和`scrollHeight`的返回自身的宽和高就是实际内容的宽和高。

```js
<!-- box盒子的宽和高都是200px -->
<div class="box"></div>
<script>
	var box = document.querySelector(".box");
	console.log(box.scrollHeight); // 200
	console.log(box.scrollWidth); // 200
</script>
```

`pageYOffset`可以获取页面被滚动上去的部分，`pageXOffset`可以获取被滚动到左侧的部分。

```js
<div class="box"></div>
<script>
	var box = document.querySelector(".box");
    // scroll滚动事件在滚动条发生变化时会被触发
    box.addEventListener("scroll",function(){
        console.log(box.scrollTop);
    })
</script>
```



## 案例

> 固定左侧侧边栏

1. 原先侧边栏为绝对定位
2. 页面滚动到一定的位置时，改变成固定定位
3. 继续滚动页面，显示出回到顶部

```html
<head>
    <meta charset="UTF-8">
    <title>固定侧边栏</title>
    <style>
        .slider-bar {
            position: absolute;
            left: 50%;
            top: 300px;
            margin-left: 600px;
            width: 45px;
            height: 50px;
            background-color: gray;
        }

        .w {
            width: 1200px;
            margin: 10px auto;
        }

        .header {
            text-align: center;
            height: 150px;
            background-color: purple;
        }

        .banner {
            text-align: center;
            height: 250px;
            background-color: skyblue;
        }

        .main {
            text-align: center;
            height: 1000px;
            background-color: yellowgreen;
        }

        span {
            display: none;
            position: absolute;
            bottom: 0;
        }
    </style>
</head>

<body>
    <div class="slider-bar">
        <span class="goBack">返回顶部</span>
    </div>
    <div class="header w">头部区域</div>
    <div class="banner w">banner区域</div>
    <div class="main w">主体部分</div>
    <script>
        // 获取元素
        var sliderBar = document.querySelector('.slider-bar');
        var banner = document.querySelector('.banner');
        var main = document.querySelector('.main');
        var goBack = document.querySelector('.goBack');

        // 获取到banner的顶部值
        var bannerTop = banner.offsetTop;
        // 侧边栏固定定位变化的数值
        var sliderbarTop = sliderBar.offsetTop - bannerTop;
        // 获取到mainTop距离
        var mainTop = main.offsetTop;
        // 页面滚动滚动事件 scroll
        document.addEventListener('scroll', function () {
            // 当页面向下滚动达到某个数值，则改成固定定位
            if (window.pageYOffset >= bannerTop) {
                sliderBar.style.position = 'fixed';
                sliderBar.style.top = sliderbarTop + 'px';
            } else {
                sliderBar.style.position = 'absolute';
                sliderBar.style.top = '300px';
            }
            // 滚动到main位置显示出文本内容
            if (window.pageYOffset >= mainTop) {
                goBack.style.display = 'block';
            } else {
                goBack.style.display = 'none';
            }
        });
    </script>
</body>
```



## 三大系列总结

![image-20221218223015284](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221218223015284.png)

### 主要应用场景：

1. offset系列 通常应用于获得元素的位置， `offsetLeft `、`offsetTop`。
2. client系列 通常应用于获得元素的大小 ，`clientWidth `、`clientHeight`。

3. scroll系列 通常应用于获取元素的滚动距离， `scrollTop`、 `scrollLeft `。

4. 页面的滚动距离通过 `window.pageYOffset` 和 `window.pageXOffset `获得。

5. 都有一个共同点，返回值都是数字且不带单位。

6. 获取页面在Y轴上的滚动距离，可以通过`window.pageYOffset、`、`document.documentElement.scrollTop`、`document.body.scrollTop` 三种方式



# 四、动画特效

## 4.1 动画原理

1. 获得盒子当前位置
2. 让盒子在当前位置加上1个移动距离
3. 利用定时器不断重复这个操作
4. 加一个结束定时器的条件 
5. 注意该元素需要添加定位，才能使用element.style.left



```html
<head>
    <meta charset="UTF-8">
    <title>动画原理</title>
    <style>
        div {
            /*设置定位*/
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        // 获取元素
        var d = document.querySelector('div');
        // 设置定时器
        var timer = setInterval(function () {
            // 设置结束条件
            if (d.offsetLeft >= 500){
                // 清除定时器
                clearInterval(timer);
            }
          // 移动后位置
            d.style.left = d.offsetLeft + 2 + 'px';
        }, 50)
    </script>
</body>
```

效果如下：

<video controls autoplay name="donghua">
	<source src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/动画特效 - Trim.mp4" type="video/mp4">
</video>

## 4.2 封装动画对象

- 封装动画函数对象，可以使不同的对象进行相同的操作，方便调用达到相同的效果
- 不同的对象添加不同的定时器，就不会出现迭代动画效果，比如下面的按钮事件，多次点击它不会出现移动的速度越来越快的效果

```html
<head>
    <meta charset="UTF-8">
    <style>
        div {
            position: absolute;
            left: 0;
            width: 100px;
            height: 100px;
            background-color: pink;
        }

        span {
            position: absolute;
            left: 0;
            top: 150px;
            display: block;
            width: 150px;
            height: 150px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <button>点击夏雨荷才走</button>
    <div></div>
    <span>夏雨荷</span>
    <script>
        // 获取对象
        var buttonElement = document.querySelector('button');
        var divElement = document.querySelector('div');
        var spanElement = document.querySelector('span');
        // 封装定时器
        function animate(obj, stopPosition) {
            // 将上一次的定时器清除掉，就不会出现迭代效果,点击按钮就不会，越点击，移动速度越快的效果
            clearInterval(obj.timer);
            // 定时器
            obj.timer = setInterval(function () {
                // 元素停止限制
                if (obj.offsetLeft >= stopPosition) {
                    // 清除定时器
                    clearInterval(obj.timer);
                } else {
                    // 不断移动，距离左侧越来越远
                    obj.style.left = obj.offsetLeft + 1 + 'px';
                }
            }, 40)
        }
        // 不同的对象调用同一个函数
        animate(divElement,100);
        // span点了按钮才会开始动
        buttonElement.addEventListener('click',function (){
            animate(spanElement,150);
        });
    </script>
</body>
```

实现的效果如下所示：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E5%B0%81%E8%A3%85%E5%8A%A8%E7%94%BB.gif" alt="封装动画" style="zoom:67%;" />



## 4.3 缓冲动画

### 4.3.1 缓冲动画原理

元素运动的速度有所变化，停止的移动的距离慢慢减小



具体思路如下

1. 盒子每次移动的距离越来越小，相当于速度越来越小
2. 每次移动距离的步长：使用缓冲动画公式==（目标值 - 当前的位置）/ 10==
3. 停止条件：当前盒子的位置等于目标位置，定时器停止

之前的是匀速动画，现在是缓冲动画，两者之间的区别：

- 匀速动画就是盒子是当前的位置 +  固定的值 10
- 缓动动画就是盒子当前的位置 + 变化的值(目标值 - 现在的位置) / 10）



一个目标元素来回移动：

```html
<body>
    <button class="btn500">点击夏雨荷到500</button>
    <button class="btn800">点击夏雨荷到800</button>
    <span>夏雨荷</span>
    <script>
        function animate(obj, target) {
            // 先清除以前的定时器，只保留当前的一个定时器执行
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                // 把我们步长值改为整数 不要出现小数的问题 步长公式：(目标值 - 现在的位置) / 10
                var step = (target - obj.offsetLeft) / 10;
                // ceil 向上取整，floor向下取整
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                }
                obj.style.left = obj.offsetLeft + step + 'px';

            }, 15);
        }
        var span = document.querySelector('span');
        var btn500 = document.querySelector('.btn500');
        var btn800 = document.querySelector('.btn800');

        btn500.addEventListener('click', function () {
            animate(span, 500);
        })
        btn800.addEventListener('click', function () {
            animate(span, 800);
        })
    </script>
</body>
```



### 4.3.2 缓冲动画的回调函数

回调函数：

```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        span {
            position: absolute;
            left: 0;
            top: 40px;
            display: block;
            text-align: center;
            width: 150px;
            height: 150px;
            background-color: #b2dba1;
        }
    </style>
</head>

<body>
    <button class="start">起点位置</button>
    <button class="mid">中点位置</button>
    <button class="end">终点位置</button>
    <span>开始位置</span>
    <script>
      // callback 为形参，作为回调函数
        function animate(obj, target, callback) {
            clearInterval(obj.timer);
            obj.timer = setInterval(function () {
                var step = (target - obj.offsetLeft) / 10;
                step = step > 0 ? Math.ceil(step) : Math.floor(step);
                if (obj.offsetLeft == target) {
                    // 停止动画 本质是停止定时器
                    clearInterval(obj.timer);
                    // 回调函数写到定时器结束里面
                    if (callback) {
                        // 调用函数
                        callback();
                    }
                }
                obj.style.left = obj.offsetLeft + step + 'px';
            }, 15);
        }
				// 获取元素
        var span = document.querySelector('span');
        var start = document.querySelector('.start');
        var mid = document.querySelector('.mid');
        var end = document.querySelector('.end');
        //回到起始位置
        start.addEventListener('click', function () {
            animate(span, 0, function () {
                span.style.backgroundColor = 'grey';
                span.innerHTML = '起点位置';
            })
        })
        // 移动到中间
        mid.addEventListener('click', function () {
            animate(span, 500, function () {
                span.style.backgroundColor = 'blue';
                span.innerHTML = '中点位置';
            });
        })
        // 移动到末端
        end.addEventListener('click', function () {
            animate(span, 800, function () {
                span.style.backgroundColor = 'red';
                span.innerHTML = '终点位置';
            });
        })
    </script>
</body>
```

#### 动画函数的使用

将函数单独写道一个 JS 文件当中，在需要的的 html 中引用进来



用一个列子说明：

> 鼠标经过 / 离开侧边栏时的弹出，隐藏的效果

`animate.js`

```js
function animate(obj, target, callback) {
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
        var step = (target - obj.offsetLeft) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            callback && callback();
        }
        obj.style.left = obj.offsetLeft + step + 'px';

    }, 15);
}
```

`html` 设置

```js
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .sliderbar {
            position: fixed;
            right: 0;
            bottom: 100px;
            width: 32px;
            height: 32px;
            text-align: center;
            line-height: 32px;
            cursor: pointer;
            color: blue;
        }

        .con {
            position: absolute;
            left: 0;
            top: 0;
            width: 200px;
            height: 32px;
            background-color: gray;
            z-index: -1;
        }
    </style>
		
    <script src="animate.js"></script>
</head>

<body>
    <div class="sliderbar">
        <span><img src="../../Images/questionback.png"></span>
        <div class="con">问题反馈</div>
    </div>

    <script>
        // 1. 获取元素
        var sliderbar = document.querySelector('.sliderbar');
        var con = document.querySelector('.con');
        // 当鼠标经过 sliderbar 就会让 con这个盒子滑动到左侧
        sliderbar.addEventListener('mouseenter', function () {
            animate(con, -160, function () {
                // 当动画执行完毕,显示回图片
                sliderbar.children[0].innerHTML = '<img src="../../Images/outquestion.png">';
            });
        })
        // 当鼠标离开 sliderbar 就会让 con这个盒子滑动到右侧
        sliderbar.addEventListener('mouseleave', function () {
            animate(con, 0, function () {
                sliderbar.children[0].innerHTML = '<img src="../../Images/questionback.png">';
            });
        })
    </script>
</body>
```









# 五、网页特效案例



## 5.1 轮播图功能需求

- 鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮。
- 点击右侧按钮一次，图片往左播放一张，以此类推， 左侧按钮同理。
- 图片播放的同时，下面小圆圈模块跟随一起变化。
- 点击小圆圈，可以播放相应图片。
- 鼠标不经过轮播图， 轮播图也会自动播放图片。
- 鼠标经过，轮播图模块， 自动播放停止。



![image-20221219135656761](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221219135656761.png)



## 5.2 轮播图实现过程

1. 给定一个大盒子，为了方便后面盒子的定位操作，再给它一个相对定位，把图片通过无序列表的形式添加进大盒子中，
2. 因为我们要实现的轮播图效果是横向的，所以我们可以给图片添加`float：left`属性，
3. 又因为图片所在的`ul`不够大，所以其他的图片会被挤到下面，所以我们可以手动修改图片所在的`ul`的大小，
4. 接下来写一个无序列表用于放置小圆圈，通过绝对定位的方式将其定位到大盒子的下面，在将小圆圈加进去，方便我们实现点击对应的小圆圈，就跳转到相应图片的效果。
5. 然后将左右箭头通过绝对定位分别定到大盒子两侧合适位置。最后，我们再将大盒子外面的内容隐藏掉。



## 5.3 轮播图代码实现

### 5.3.1 创建HTML代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>轮播图</title>
    <!--引入js，css-->
    <link rel="stylesheet" href="css/lunbotu.css">
    <script src="js/lunbotu.js"></script>
    <script src="js/animate.js"></script>
</head>
<body>
    <div class="main">
        <div class="focus">
            <!-- 左侧按钮 -->
            <a href="javascript:;" class="prev">&lt;</a>
            <!-- 右侧按钮 -->
            <a href="javascript:;" class="next">&gt;</a>
            <!-- 核心滚动区 -->
            <ul>
                <li>
                    <a href="javascript:;"><img src="Images/1.jpeg" alt=""></a>
                </li>
                <li>
                    <a href="javascript:;"><img src="Images/3.jpeg" alt=""></a>
                </li>
                <li>
                    <a href="javascript:;"><img src="Images/5.jpeg" alt=""></a>
                </li>
                <li>
                    <a href="javascript:;"><img src="Images/37.jpeg" alt=""></a>
                </li>
                <li>
                    <a href="javascript:;"><img src="Images/38.jpeg" alt=""></a>
                </li>
                <li>
                    <a href="javascript:;"><img src="Images/39.jpeg" alt=""> </a>
                </li>
            </ul>
            <!-- 小圆点 -->
            <ol class="circle">
            </ol>
        </div>
    </div>
</body>
</html>
```

### 5.3.2 编写CSS代码

> css在开发过程中尽量不要写在html文件中
>

`lunbotu.css`

```css
* {
    margin: 0;
    padding: 0;
}

li {
    list-style: none;
}
img {
    width: 1920px;
    height: 1020px;
    border: 0;
    vertical-align: middle;
}

.main {
    width: 1920px;
    height: 1020px;
}

.focus {
    position: relative;
    width: 1920px;
    height: 1020px;
    background-color: pink;
    /*隐藏其他的图片*/
    overflow: hidden;
}

.prev,
.next {
    /*隐藏按钮*/
    display: none;
    position: absolute;
    /* 绝对定位的盒子垂直居中 */
    top: 50%;
    margin-top: -10px;
    /* 加了绝对定位的盒子可以直接设置高度和宽度 */
    width: 50px;
    height: 60px;
    background-color: rgb(0, 0, 0, .3);
    text-align: center;
    line-height: 60px;
    color: #fff;
    font-size: 50px;
    text-decoration: none;
}

.prev {
    left: 0;
    border-top-right-radius: 15px;
    border-bottom-right-radius: 15px;
    z-index: 2;
}

.next {
    /* 如果一个盒子既有left属性又有right属性，则默认会执行left属性 同理 top bottom  会执行top  */
    right: 0;
    /* 绝对定位的盒子垂直居中 */
    border-top-left-radius: 15px;
    border-bottom-left-radius: 15px;
    z-index: 2;
}

.focus ul {
    position: absolute;
    top: 0;
    left: 0;
    width: 700%;
}

.focus ul li {
    float: left
}

.circle {
    position: absolute;
    bottom: 120px;
    left: 960px;
}

.circle li {
    float: left;
    width: 18px;
    height: 18px;
    /*background-color: #fff;*/
    border: 5px solid rgba(255, 255, 255, 0.5);
    margin: 0 5px;
    border-radius: 50%;
    /*鼠标经过显示小手*/
    cursor: pointer;
}

.current {
    background-color: deepskyblue;
}
```

### 5.3.3 动画封装

```js
function animate(obj, target, callback) {
    clearInterval(obj.timer);
    obj.timer = setInterval(function () {
        var step = (target - obj.offsetLeft) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            callback && callback();// 如果为真，就执行callback（），否则不执行
        }
        obj.style.left = obj.offsetLeft + step + 'px';
    }, 15);
}
```



### 5.3.4 编写JS代码

1. 当鼠标经过轮播图模块，左右按钮显示，离开隐藏左右按钮。
2. 点击右侧按钮一次，图片往左播放一张，以此类推， 左侧按钮同理。
3. 图片播放的同时，下面小圆圈模块跟随一起变化。
4. 点击小圆圈，可以播放相应图片。
5. 鼠标不经过轮播图， 轮播图也会自动播放图片。
6. 鼠标经过，轮播图模块， 自动播放停止。



```js
window.addEventListener('load', function () {
    // 1. 获取元素
    // 左侧按钮
    var prev = document.querySelector('.prev');
    // 右侧按钮
    var next = document.querySelector('.next');
    // 轮播图
    var focus = document.querySelector('.focus');
    // 获取图片的宽度
    var focusWidth = focus.offsetWidth;
    // 2. 鼠标经过focus就显示左右按钮
    focus.addEventListener('mouseenter', function () {
        prev.style.display = 'block';
        next.style.display = 'block';
        clearInterval(timer);
        // 清除定时器变量
        timer = null;
    })
    // 鼠标离开则隐藏按钮
    focus.addEventListener('mouseleave', function () {
        prev.style.display = 'none';
        next.style.display = 'none';
        timer = setInterval(function () {
            // 手动调用右侧按钮点击事件
            next.click();
        }, 2000)
    })
    // 3.动态生成小圆圈：根据图片的数量创建对应个数的小圆圈
    var ul = focus.querySelector('ul');// 根据ul里面的图片的数量
    var ol = focus.querySelector('.circle'); // 创建对应个数的ol的li
    for (var i = 0; i < ul.children.length; i++) {
        // 创建一个小 li
        var li = document.createElement('li');
        // 记录当前小圆圈的索引号 通过自定义属性来做
        li.setAttribute('index', i);
        // 把li 追加到 ol 里面
        ol.appendChild(li);
        // 4. 小圆圈的排他思想 可以直接在生成小圆圈的同时直接绑定点击事件
        li.addEventListener('click', function () {
            // 把所有的小 li 清除 current 类名
            for (var i = 0; i < ol.children.length; i++) {
                ol.children[i].className = '';
            }
            // 当前的小 li 设置 current 类名
            this.className = 'current';
            // 5. 点击小圆圈，移动图片，当然移动的是 ul
            // ul 的移动距离 = 小圆圈的索引号 乘以 图片的宽度 注意是负值。 当点击了某个小 li 就拿到当前小 li 的索引号
            var index = this.getAttribute('index');
            // 当点击了某个小 li 就要把这个 li 的索引号给 num 和 circle
            num = circle = index;
            // console.log(focusWidth);
            animate(ul, -index * focusWidth);
        })
    }
    // 把 ol 里面的第一个小 li 设置类名为 current
    ol.children[0].className = 'current';
    // 6. 克隆第一张图片（li）放到最后面
    var first = ul.children[0].cloneNode(true);
    ul.appendChild(first);
    // 7. 点击右侧按钮，图片滚动一张
    var num = 0;
    // 声明一个变量 circle 控制小圆圈的播放
    var circle = 0;
    // flag 节流阀
    var flag = true;
    next.addEventListener('click', function () {
        // 如果走到了最后复制的一张图片，此时 ul 要快速复原 left 改为 0
        if (flag) {
            flag = false;//关闭节流阀
            if (num == ul.children.length - 1) {
                ul.style.left = 0 + 'px';
                num = 0;
            }
            num++;
            animate(ul, -num * focusWidth, function () {
                flag = true;//打开节流阀
            });
            // 8. 点击右侧按钮，小圆圈跟随一起变化，可以再声明一个变量控制小圆圈的播放
            circle++;
            // circle走到最后克隆的这张图片 我们就复原为0
            if (circle == ol.children.length) {
                circle = 0;
            }
            //调用函数
            circleChange();
        }
    })

    // 9. 左侧按钮做法
    prev.addEventListener('click', function () {
        if (flag) {
            if (num == 0) {
                num = ul.children.length - 1;
                ul.style.left = -num * focusWidth + 'px';
            }
            num--;
            animate(ul, -num * focusWidth, function () {
                flag = true;
            });
            circle--;
            // 如果circle < 0 说明第一张图片 则小圆圈要改为第6个小圆圈
            if (circle < 0) {
                circle = ol.children.length - 1;
            }
            circleChange();
        }
    })

    // 优化代码，封装函数
    function circleChange() {
        for (var i = 0; i < ol.children.length; i++) {
            ol.children[i].className = '';
        }
        // 留下当前的小圆圈的current类名
        ol.children[circle].className = 'current';
    }

    // 10. 自动播放轮播图
    var timer = setInterval(function () {
        // 手动调用右侧按钮点击事件
        next.click();
    }, 2000)
})
```



## 5.4 筋斗云特效

HTML编写



```html
<body>
    <div id="c_nav" class="c-nav">
        <span class="cloud"></span>
        <ul>
            <li class="current"><a href="#">首页新闻</a></li>
            <li><a href="#">八卦新闻</a></li>
            <li><a href="#">娱乐新闻</a></li>
            <li><a href="#">军事新闻</a></li>
            <li><a href="#">校园新闻</a></li>
            <li><a href="#">企业新闻</a></li>
            <li><a href="#">腾讯新闻</a></li>
            <li><a href="#">新浪新闻</a></li>
        </ul>
    </div>
</body>
```

移动效果：

`animate.js` 

```js
function animate(obj, target, callback) {
    clearInterval(obj.timer);
    obj.timer = setInterval(function() {
        var step = (target - obj.offsetLeft) / 10;
        step = step > 0 ? Math.ceil(step) : Math.floor(step);
        if (obj.offsetLeft == target) {
            // 停止动画 本质是停止定时器
            clearInterval(obj.timer);
            callback && callback();
        }
        // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
        obj.style.left = obj.offsetLeft + step + 'px';

    }, 15);
}
```

css实现

```css
* {
    margin: 0;
    padding: 0
}

ul {
    list-style: none;
}

body {
    background-color: black;
}

.c-nav {
    width: 900px;
    height: 42px;
    background: #fff url(images/rss.png) no-repeat right center;
    margin: 100px auto;
    border-radius: 5px;
    position: relative;
}

.c-nav ul {
    position: absolute;
}

.c-nav li {
    float: left;
    width: 83px;
    text-align: center;
    line-height: 42px;
}

.c-nav li a {
    color: #333;
    text-decoration: none;
    display: inline-block;
    height: 42px;
}

.c-nav li a:hover {
    color: white;
}

.c-nav li.current a {
    color: #0dff1d;
}

.cloud {
    position: absolute;
    left: 0;
    top: 0;
    width: 83px;
    height: 42px;
    background: url(images/cloud.gif) no-repeat;
}
```



主JS实现



```js
    window.addEventListener('load', function () {
        // 1. 获取元素
        var cloud = document.querySelector('.cloud');
        var c_nav = document.querySelector('.c-nav');
        var lis = c_nav.querySelectorAll('li');
        // 2. 给所有的小li绑定事件 
        // 这个current 做为筋斗云的起始位置
        var current = 0;
        for (var i = 0; i < lis.length; i++) {
            // (1) 鼠标经过把当前小li 的位置做为目标值
            lis[i].addEventListener('mouseenter', function () {
                animate(cloud, this.offsetLeft);
            });
            // (2) 鼠标离开就回到起始的位置 
            lis[i].addEventListener('mouseleave', function () {
                animate(cloud, current);
            });
            // (3) 当我们鼠标点击，就把当前位置做为目标值
            lis[i].addEventListener('click', function () {
                current = this.offsetLeft;
            });
        }
    })
```



![筋斗云](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E7%AD%8B%E6%96%97%E4%BA%91.gif)



# 六、移动端特效



## 6.1 触屏事件

移动端浏览器的兼容性较好，不需要考虑JS的兼容新问题。



### 6.1.1 常见的触屏事件

| 触屏事件     | 事件说明                    |
| ------------ | --------------------------- |
| `touchstart` | 手指`触摸DOM`元素事件       |
| `touchmove`  | 手指在`DOM元素身上移动`事件 |
| `touchend`   | 手指`离开DOM`元素事件       |

```js
// 手指触摸DOM元素事件
var div = document.querySelector('div');
div.addEventListener('touchstart', function() {
    console.log('我摸了你');

});
// 手指在DOM元素身上移动事件
div.addEventListener('touchmove', function() {
    console.log('我继续摸');

});
// 手指离开DOM元素事件
div.addEventListener('touchend', function() {
    console.log('轻轻的我走了');
});
```

### 6.1.2 触摸事件对象（TouchEvent）

触摸事件常用事件对象列表

| 触摸列表       | 说明                                               |
| -------------- | -------------------------------------------------- |
| touches        | 正在触摸屏幕的所有手指的一个列表                   |
| targeTouches   | 正在触摸当前DOM元素上的手指的一个列表（常用）      |
| changedTouches | 手指状态发生了改变的列表，从无到有，从有到无的变化 |



### 6.1.3 移动端拖动元素

1. 使用到以上的三种触摸事件

2. 拖动元素需要获取到手指的坐标值： `targetTouches[0]` 的`pageX`和`pageY`
3. 原理：手指移动中，计算出手指移动的距离，然后用盒子原来的位置 + 手指移动的距离
4. 手指移动的距离：手指滑动中的位置 减去 手指刚开始触摸的位置坐标



主要就是三步骤：

1. 触摸元素 `touchstart`： 获取手指初始坐标，同时获得盒子原来的位置
2. 移动手指 `touchmove`：计算手指的滑动距离，并且移动盒子
3. 离开手指 `touchend`：

> 手指移动也会触发滚动屏幕，阻止默认的屏幕滚动 `e.preventDefault()`

```html
<body>
    <div></div>
    <script>
        // 1.获取元素
        var div = document.querySelector('div');
        // 2.获取手指、盒子初始位置坐标
        var fingerX = 0;
        var fingerY = 0;
        var boxX = 0;
        var boxY = 0;
        // 3.手指开始触摸事件
        div.addEventListener('touchstart', function (e) {
            // 获取到初始值坐标
            fingerX = e.targetTouches[0].pageX;
            fingerY = e.targetTouches[0].pageY;
            boxX = this.offsetLeft;
            boxY = this.offsetTop;
        })
        // 4. 手指移动事件
        div.addEventListener('touchmove', function (e) {
            // 手指移动的距离计算，移动后的坐标减去初始值的坐标
            var moveX = e.targetTouches[0].pageX - fingerX;
            var moveY = e.targetTouches[0].pageY - fingerY;
            // 盒子的移动距离，盒子原来的坐标加上手指移动的距离
            this.style.left = boxX + moveX + 'px';
            this.style.top = boxY + moveY + 'px';
            // 阻止屏幕的滚动行为
            e.preventDefault();
        })
    </script>
</body>
```



## 6.2 移动端特效

### 移动端轮播图

`HTML` 

```html
<!-- 焦点图模块 -->
<div class="focus">
    <ul class="total">
        <li><img src="upload/focus3.jpg" alt=""></li>
        <li><img src="upload/focus1.jpg" alt=""></li>
        <li><img src="upload/focus2.jpg" alt=""></li>
        <li><img src="upload/focus3.jpg" alt=""></li>
        <li><img src="upload/focus1.jpg" alt=""></li>
    </ul>
    <!-- 小圆点 -->
    <ol>
        <li class="current"></li>
        <li></li>
        <li></li>
    </ol>
</div>
```

`CSS`

```css
.focus {
    position: relative;
    padding-top: 44px;
    overflow: hidden;
}

.focus img {
    width: 100%;
}

.focus ul {
    overflow: hidden;
    width: 500%;
    margin-left: -100%;
}

.focus ul li {
    float: left;
    width: 20%;
}

.focus ol {
    position: absolute;
    bottom: 5px;
    right: 5px;
    margin: 0;
}

.focus ol li {
    display: inline-block;
    width: 5px;
    height: 5px;
    background-color: #fff;
    list-style: none;
    border-radius: 2px;
    transition: all .3s;
}

.focus ol li.current {
    width: 15px;
}
```

`JS`

```js
window.addEventListener('load', function () {
    // 1. 获取元素
    var focus = document.querySelector('.focus');
    var total = document.querySelector('.total');
    var ul = focus.children[0];
    // 获得focus的宽度
    var w = focus.offsetWidth;
    var ol = focus.children[1];
    // 2. 利用定时器自动轮播图图片
    var index = 0;
    var timer = setInterval(function () {
        index++;
        // 左移动 为负值
        var translatex = -index * w;
        // 过度效果
        ul.style.transition = 'all .3s';
        ul.style.transform = 'translateX(' + translatex + 'px)';
    }, 2000);
    // 等过渡完成之后，再去判断 监听过渡完成的事件 transitionend
    ul.addEventListener('transitionend', function () {
        // 无缝滚动
        if (index >= total.children.length - 2) {
            index = 0;
            // 去掉过渡效果 这样让我们的ul 快速的跳到目标位置
            ul.style.transition = 'none';
            // 利用最新的索引号乘以宽度 去滚动图片
            var translatex = -index * w;
            ul.style.transform = 'translateX(' + translatex + 'px)';
        } else if (index < 0) {
            index = 2;
            ul.style.transition = 'none';
            // 利用最新的索引号乘以宽度 去滚动图片
            var translatex = -index * w;
            ul.style.transform = 'translateX(' + translatex + 'px)';
        }
        // 3. 小圆点跟随变化
        // 把ol里面li带有current类名的选出来去掉类名 remove
        ol.querySelector('.current').classList.remove('current');
        // 让当前索引号的小li加上 current   add
        ol.children[index].classList.add('current');
    });

    // 4. 手指滑动轮播图
    var startX = 0;
    var moveX = 0; // 后面我们会使用这个移动距离所以要定义一个全局变量
    var flag = false;
    // 触摸元素 touchstart： 获取手指初始坐标
    ul.addEventListener('touchstart', function (e) {
        startX = e.targetTouches[0].pageX;
        // 手指触摸的时候就停止定时器
        clearInterval(timer);
    });
    // 移动手指 touchmove： 计算手指的滑动距离， 并且移动盒子
    ul.addEventListener('touchmove', function (e) {
        // 计算手指移动距离
        moveX = e.targetTouches[0].pageX - startX;
        // 移动盒子：  盒子原来的位置 + 手指移动的距离 
        var translatex = -index * w + moveX;
        // 手指拖动的时候，不需要动画效果所以要取消过渡效果
        ul.style.transition = 'none';
        ul.style.transform = 'translateX(' + translatex + 'px)';
        flag = true; // 如果用户手指移动过再去判断否则不做判断效果
        e.preventDefault(); // 阻止滚动屏幕的行为
    });
    // 手指离开 根据移动距离去判断是回弹还是播放上一张下一张
    ul.addEventListener('touchend', function (e) {
        if (flag) {
            // (1) 如果移动距离大于50像素我们就播放上一张或者下一张
            if (Math.abs(moveX) > 50) {
                // 如果是右滑就是 播放上一张 moveX 是正值
                if (moveX > 0) {
                    index--;
                } else {
                    // 如果是左滑就是 播放下一张 moveX 是负值
                    index++;
                }
                var translatex = -index * w;
                ul.style.transition = 'all .3s';
                ul.style.transform = 'translateX(' + translatex + 'px)';
            } else {
                // (2) 如果移动距离小于50像素我们就回弹
                var translatex = -index * w;
                ul.style.transition = 'all .1s';
                ul.style.transform = 'translateX(' + translatex + 'px)';
            }
        }
        // 手指离开的时候就重新开启定时器
        clearInterval(timer);
        timer = setInterval(function () {
            index++;
            var translatex = -index * w;
            ul.style.transition = 'all .3s';
            ul.style.transform = 'translateX(' + translatex + 'px)';
        }, 2000);
    });

    // 返回顶部模块制作
    var goBack = document.querySelector('.goBack');
    var localNav = document.querySelector('.local-nav');
    window.addEventListener('scroll', function () {
        if (window.pageYOffset >= localNav.offsetTop) {
            goBack.style.display = 'block';
        } else {
            goBack.style.display = 'none';
        }
    });
    goBack.addEventListener('click', function () {
        window.scroll(0, 0);
    })
})
```

### classList 

返回元素的类名

```js
<body>
    <div class="one two"></div>
    <button> 开关灯</button>
    <script>
        // classList 返回元素的类名
        var div = document.querySelector('div');
        console.log(div.classList[1]);// 获取类名
        // 1. 添加类名  是在后面追加类名不会覆盖以前的类名 注意前面不需要加.
        div.classList.add('three');
        // 2. 删除类名
        div.classList.remove('one');
        // 3. 切换类
        var btn = document.querySelector('button');
        btn.addEventListener('click', function() {
            document.body.classList.toggle('bg');
        })
    </script>
</body>
```



### click 延时事件



移动端click事件会有300ms的延时,原因是移动端屏幕双击会缩放(`double tap to zoom`)页面。

解决方案:

1. 禁用缩放。浏览器禁用默认的双击缩放行为并且去掉300ms的点击延迟。

```html
<meta name="viewport" content="user-scalable=no">
```

2. 利用`touch`事件自己封装这个事件解决300ms延迟。


​	原理就是：

    1.当我们手指触摸屏幕,记录当前触摸时间
    
    2.当我们手指离开屏幕,用离开的时间减去触摸的时间
    
    3.如果时间小于150ms ,并且没有滑动过屏幕,那么我们就定义为点击
    
    封装tap,解决click 300ms延时
## 6.3 移动端开发插件开发移动端特效

### 6.3.1  使用插件。fastclick 插件解决300ms延迟。



[fastclick官网地址](https://gitcode.net/mirrors/ftlabs/fastclick/-/blob/master/lib/fastclick.js)



```js
<body>
    <div></div>
    <script>
        if ('addEventListener' in document) {
            document.addEventListener('DOMContentLoaded', function() {
                FastClick.attach(document.body);
            }, false);
        }
        var div = document.querySelector('div');
        div.addEventListener('click', function() {
            console.log('这个div');
        })
    </script>
</body>
```

点击 pink 正方形：

![image-20221220134052301](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220134052301.png)



### 6.3.2 swiper 插件

[swiper 官网](https://www.swiper.com.cn/index.html)



[swiper 使用演示](https://blog.csdn.net/weixin_72322475/article/details/127052620)



[swiper官网教程](https://www.swiper.com.cn/usage/index.html)



### 6.3.3 superslide 插件

[官网](http://www.superslide2.com/)





### 6.3.4 iscroll 插件

[官网](https://github.com/cubiq/iscroll)



### 插件使用总结

1. 确认插件的功能
2. 官网查看插件说明
3. 下载插件
4. 查看demo实例文件，查看需要引入的相关文件，（JS、CSS），并且引入到 `index.html` 中
5. 复制demo的中代码到对应的 js、html、css中

### 6.3.5 视频插件

[官网](https://github.com/ireaderlab/zyMedia)

## 6.4 移动端开发框架开发移动端特效

[前端开发框架](https://www.bootcss.com/)

![image-20221220142154650](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220142154650.png)





Vue



React



Angular









# 七、本地存储

## 本地存储特性

1. 数据存储的浏览器中
2. 设置、读取方便、页面刷新不丢失数据
3. 容量较大、`sessionStorage`约5M，`localStorage`约为20M
4. 只能存储字符串、可以将`JSON.stringify()` 编码后存储



## 7.1 sessionStorage

### 介绍

1. 生命周期为关闭浏览器窗口
2. 在同一个窗口（页面）下数据可以共享
3. 以键值对的形式存储



### 存储数据

```js
sessionStorage.setItem(key,value)
```

```html
<body>
    <input type="text">
    <button class="set">存储数据</button>
    <script>
        var ipt = document.querySelector('input');
        var set = document.querySelector('.set');
        // 存储数据
        set.addEventListener('click',function (){
            var value = ipt.value;
            sessionStorage.setItem('username',value);
        })
    </script>
</body>
```

![image-20221220144935593](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220144935593.png)

### 获取数据

```js
sessionStorage.getItem(key)
```

### 删除数据

```js
sessionStorage.removeItem(key)
```

### 删除所有数据

```js
sessionStorage.clear()
```



```js
<body>
    <input type="text">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空所有数据</button>
    <script>
        var ipt = document.querySelector('input');
        var set = document.querySelector('.set');
        // 存储数据
        set.addEventListener('click', function () {
            var value = ipt.value;
            sessionStorage.setItem('username', value);
            sessionStorage.setItem('pwd', value);
        })
        // 获取数据
        get.addEventListener('click', function () {
            sessionStorage.getItem('username');
        })
        // 删除单个数据
        remove.addEventListener('click', function () {
            sessionStorage.removeItem('username');
            sessionStorage.removeItem('pwd');
        })
        // 清除所有的
        del.addEventListener('click', function () {
            sessionStorage.clear();
        })
    </script>
</body>
```

## 7.2 localStorage

1. 生命周期永久生效，除非处于手动删除，否则关闭页面也会存在
2. 可以多窗口（页面）共享，同一浏览器可以共享
3. 以键值对形式存储使用

### 获取数据

```js
localStorage.setItem(key,value);
```

### 获取数据

```js
localStorage.getItem(key)
```

### 删除数据

```js
localStorage.removeItem(key)
```

### 删除所有数据

```js
localStorage.clear()
```

```js
<body>
    <input type="text">
    <button class="set">存储数据</button>
    <button class="get">获取数据</button>
    <button class="remove">删除数据</button>
    <button class="del">清空所有数据</button>
    <script>
        var ipt = document.querySelector('input');
        var set = document.querySelector('.set');
        var get = document.querySelector('.get');
        var remove = document.querySelector('.remove');
        var del = document.querySelector('.del');
        set.addEventListener('click', function() {
            var val = ipt.value;
            localStorage.setItem('username', val);
        })
        get.addEventListener('click', function() {
            console.log(localStorage.getItem('username'));

        })
        remove.addEventListener('click', function() {
            localStorage.removeItem('username');
        })
        del.addEventListener('click', function() {
            localStorage.clear();
        })
    </script>
</body>
```



![image-20221220150945227](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220150945227.png)



## 案例

> 记住账号密码案例，方便下次进来可以直接使用，不用再次输入



```js
<body>
    <input type="text" id="username"> <input type="checkbox" name="" id="remember"> 记住用户名
    <br>
    <input type="text" id="password"> <input type="checkbox" name="" id="rememberpwd"> 记住密码
    <script>
        // 获取元素事件
        var username = document.querySelector('#username');
        var reusername = document.querySelector('#remember');
        var inputPwd = document.querySelector('#password');
        var repwd = document.querySelector('#rememberpwd');
        // 在本次存储中获取用户名，密码
        if (localStorage.getItem('username') || localStorage.getItem('passwd')) {
            username.value = localStorage.getItem('username');
            reusername.checked = true;
            inputPwd.value = localStorage.getItem('passwd');
            repwd.checked = true;
        }
        // 记住用户名的复选框
        reusername.addEventListener('change', function () {
            if (this.checked) {
                localStorage.setItem('username', username.value)
            } else {
                localStorage.removeItem('username');
            }
        })
        // 记住密码的复选框
        repwd.addEventListener('change', function () {
            if (this.checked) {
                localStorage.setItem('password', inputPwd.value);
            } else {
                localStorage.removeItem('password');
            }
        })
    </script>
</body>
```

当复选框都够选上时：数据存储到本地

![image-20221220152557290](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220152557290.png)





取消勾选，数据将不会保存的本地



![image-20221220152621424](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221220152621424.png)







到此学习JS 的BOM、DOM学习完毕，其中还有许多的还没有掌握，还需要多敲代码，加油码农！！❤️❤️‍🔥













