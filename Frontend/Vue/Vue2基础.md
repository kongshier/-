> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

[学习视频](https://www.bilibili.com/video/BV1Zy4y1K7SH/)



# 1、Vue简介

[Vue2中文官网](https://v2.cn.vuejs.org/)

## 1.1 Vue 介绍

一套用于构建用户界面的渐进式JavaScript框架

- 构建用户界面：把数据通过某种办法变成用户界面
- 渐进式：可以自底向上逐层的应用，简单应用只需要一个轻量小巧的核心库，复杂应用可以引入各式各样的

尤雨溪为Vue开发



## 1.2 Vue 特点

1. 采用组件化模式，提高代码复用率、代码更好维护。

2. 声明式编码，无需直接操作DOM，提高开发效率

   - 命令式编码：发出一个指令就执行一步
   - 声明式编码：通过指令一步完成

3. 使用虚拟DOM+DIff算法，复用DOM节点

   新数据与原始数据进行对比：有新增的数据则添加进来

   ![image-20230106123059660](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230106123059660.png)

4. 编码简单、体积小、运行效率高



##  Vue库

- vue-cli： vue脚手架
- vue-resource(axios)： ajax 请求
- vue-router：路由
- vuex：状态管理(它是 vue 的插件但是没有用vue-xxx的命名规则)
- vue-lazyload：图片懒加载
- vue-scroller：页面滑动相关
- mint-ui：基于vue的U组件库(移动端)
- element-ui：基于vue的U组件库(PC端)



# 2、Vue核心

## 2.1 初识Vue

1. 创建Vue实例，引入js对象
2. 容器中的代码依然符合html代码的规范，加入了Vue语法
3. 容器中的代码称为 ==Vue模板==
4. Vue实例与容器是==一一对应==的
5. 真实开发中只有一个Vue实例，并且会配合着组件一起使用
6. `{{xxx}}`中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性
   - 表达式：表达式会返回一个值（结果），供其他地方调用
   - 代码（语句）：不会返回一个值
7. 一旦data中的数据发生变化，那么模板中用到该数据的地方也会自动更新



```vue
<head>
    <meta charset="UTF-8">
    <title>初始Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
</head>
<body>
    <!--div容器-->
    <div id="root">
        <h1>初始Vue,{{ name }}</h1>   <!---->
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        // 创建Vue对象
        new Vue({
            el: '#root', // el用于讲当前的Vue实例，绑定的指定的容器中，此处指定了root容器
            data: {  // 用于存储数据 给el中指定的容器使用
                name: 'Shier'  // 讲name指定到容器中的name，实现数据的互传
            }
        })
    </script>
</body>
```



## 2.2 模板语法

Vue模板语法有2大类：

* 插值语法：

  功能：用于解析==标签体内容==

  写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性

* 指令语法：

  功能：用于==解析标签==（包括：标签属性、标签体内容、绑定事件.....）

  举例：`v-bind:href="xxx"` 或  简写为 `:href="xxx"`，xxx同样要写js表达式，且可以直接读取到data中的所有属性



```vue
<head>
    <meta charset="UTF-8">
    <title>初始Vue</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
</head>
<body>
    <!--div容器-->
    <div id="root">
        <h1>插值语法</h1>
        <h3>Hello {{ name }}</h3>
        <hr>
        <h1>指令语法</h1>
        <a v-bind:href="go.url"> {{ go.name }} </a>  <!--方式一 -->
        <a :href="go.url"> {{ go.name }} </a>    <!--方式二-->
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        // 创建Vue对象
        new Vue({
            el: '#root',
            data: { 
                name: 'Vue',
                go: {
                    name: 'B站大学',
                    url: 'https://www.bilibili.com/'
                },
            }
        })
    </script>
</body>
```



## 2.3 数据绑定

数据绑定的两种形式

1. 单向绑定(`v-bind`)：数据只能从data流向页面（也就是通过代码修改页面）

2. 双向绑定(`v-model)`：数据不仅能从data流向页面，还可以从页面流向data （代码修改页面内容、页面内容也可以修改指定的值）
   - 双向绑定一般都应用在表单类元素上（如：input、select等）
   - `v-model:value` 可以简写为 `v-model`，因为v-model默认收集的就是value值


```vue
<head>
    <meta charset="UTF-8">
    <title>数据绑定</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
</head>
<body>
    <!--div容器-->
    <div id="box">
        <h1>数据绑定</h1>
        单向数据绑定：<input type="text" v-bind:value="name">
        双向数据绑定：<input type="text" v-model:value="name">
        <hr>
        <!--简写形式-->
        单向数据绑定：<input type="text" :value="name">
        双向数据绑定：<input type="text" v-model="name">
        <hr>
        错误的使用v-model 数据绑定：<input type="text" v-model:aa="name">
        <hr>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        // 创建Vue对象
        new Vue({
            el: '#box',
            data: {
                name: '学习vue',
            }
        })
    </script>
</body>
```



示例结果如下：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230106185049921.png" alt="image-20230106185049921" style="zoom: 80%;" />



## 2.4 el与data的两种形式

### el有2种写法

1. new Vue时候配置el属性

2. 先创建Vue实例，随后再通过`v.$mount('#box')`指定el的值



```vue
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        const v = new Vue({
            el:'#box', // 第一种选择容器的方法
            data: {  // 第一种data 方法形式
                name: 'Shier',
                age: '18',
            }
        })
        // 第二种选择容器使用$mount 讲内容挂载到页面
        v.$mount('#box')
    </script>
```



### data的两种写法

1. data对象形式
2. 函数形式（不能使用箭头函数，因为this执行的是Vue实例）



```vue
<head>
    <meta charset="UTF-8">
    <title>el与data的两种写法</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
</head>
<body>
    <!--div容器-->
    <div id="box">
        <h1>{{ name }} 学习Vue </h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        const v = new Vue({
            el:'#box', // 第一种选择容器的方法
          
            /*data: {  // 第一种data 方法形式
                name: 'Shier',
                age: '18',
            }*/
          
            data:function (){ // 第二种 data 方法形式 普通函数时
                return{}
            },
            //简写形式
            data(){  
                return{
                    name: 'Shier',
                    age: '18',
                }
            }
        })
        // 第二种选择容器使用$mount 讲内容挂载到页面
        v.$mount('#box')
    </script>
</body>
```



## 2.5 MVVM模型

- M：模型（Model）：对应data中的数据
- V：视图（View）：模板
- VM：视图模型（ViewModel）：Vue实例对象

MVVM框图

![image-20230106192621837](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230106192621837.png)

```js
<head>
    <meta charset="UTF-8">
    <title>MVVM模型</title>
    <script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
</head>
<body>
    <!--div容器-->
    <div id="box">
        <h1>{{ name }}</h1>
        <h1>{{ address }}</h1>
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        // 创建Vue对象
        const vm = new Vue({
            el: '#box',
            data: {
                name: '最佳Vue学习地方',
                address: 'B站大学',
            }
        })
        console.log(vm)
    </script>
</body>
```



- `vm` 所有的属性 及 Vue原型上所有属性，还有data的属性，都可以写在 `{{xxx}}` 里面





## 2.6 数据代理

### 2.6.1 Object.defineProperty() 设置属性

Object.defineProperty(obj, prop, descriptor)

1. obj：要定义属性的对象。

2. prop：要定义或修改的属性的名称

3. descriptor：要定义或修改的属性描述符

```vue
<script>
    let age = 18
    // 定义一个person对象
    let person = {
        name: 'Shier',
        sex: '男'
        // age 通过 defineProperty进行设置
    }
    Object.defineProperty(person, 'age', {
        // value: 18, // 设置age值为18
        // enumerable: true, // 属性是否可以枚举，默认为false 不可以
        // writable: true, // 属性是否可以修改，默认false 不可以
        // configurable: true, // 属性是否可以删除
        // get方法，读取person的age属性时，就会执行getter,且返回age值
        get() {
            console.log('读取了age:', age)
            return age
        },
        // set方法 ，修改person的age属性, 就会执行 setter 访问器，且修改age值
        set(value) {
            console.log('value修改为', value)
            age = value // 将修改的值赋值给age
        }
    })
</script>
```

执行结果：

![image-20230107115756071](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107115756071.png)

### 2.6.2 数据代理

数据代理：通过一个对象代理对另一个对象中属性的操作（读/写）

```js
<script>
    let va1 = {
        x:1
    }
    let va2 = {
        y:2
    }
    Object.defineProperty(va2,'x',{
        get(){
            return va1.x
        },
        set(value){
            va1.x = value
        }
    })
</script>
```

执行结果：

![image-20230107120520082](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107120520082.png)



### 2.6.2 Vue中的数据代理

* Vue中的数据代理：通过vm对象来代理data对象中属性的操作（读/写）
* Vue中数据代理的好处：更加方便的操作data中的数据
* 基本原理：
  * 通过Object.defineProperty()把data对象中所有属性添加到vm上。
  * 为每一个添加到vm上的属性，都指定一个getter/setter。
  * 在getter/setter内部去操作（读/写）data中对应的属性。

```js
<!-- 准备好一个容器-->
<div id="root">
    <h2>名称：{{ name }}</h2>
    <h2>地址：{{ address }}</h2>
</div>

<script>
    Vue.config.productionTip = false
    const vm = new Vue({
        el: '#root',
        data: {
            name: 'Shier',
            address: '广西'
        }
    })
</script>
```

将vm对象在控制台打印，可以看到，写在配置项中的 data 数据被绑定到了 vm 对象上，结果是 Vue 将 _data 中的 name，address 数据代理到 vm 本身上。

![image-20230107122425594](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107122425594.png)

`_data` 在上图的 红色框下来一点 ，`_data `是 vm的属性。

new Vue 时，Vue 通过一系列处理， 将匹配项上的 data 数据赋值给 _data 这个属性上，并对这个属性进行了处理（数据劫持），但这个属性就是来源于配置项中的 data。



> 数据劫持：将要修改的数据的值，将会被set方法获取（劫持）的修改的内容

数据代理上来，将 **vm._data** 中的值，再代理到 vm 本身上来，用vm.name 代替 **vm._data.name**。这就是 Vue 的数据代理

![image-20230107122945669](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107122945669.png)

以上的都是通过 Object.defineProperty() 来完成数据代理的。

~~~js
Object.defineProperty(vm, 'name', {
    get() {
        return vm._data.name;
    },
    set(value) {
        vm._data.name = value
    }
})
~~~

在插值语法中，{{ name }} 取到的值就相当于 {{ vm.name }}，不用数据代理的话，在插值语法就要这样去写了。

{{ _data. name }} 这不符合直觉。vue 这样设计更利于开发者开发，我们在研究原理会觉得有些复杂。



视频中的数据代理图解

![image-20230107123623994](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107123623994.png)



## 2.7 事件处理

事件的基本使用：

* 使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名
* 事件的回调需要配置在methods对象中，最终会在vm上
* methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象
* methods中配置的函数，不能使用箭头函数，否则this对象不再是vm
* `@click = "functionName"` 和 `@click="functionName($event)"`效果一直，但是后者可以传递参数

```vue
<body>
    <!--div容器-->
    <div id="root">
       <h1>{{name}}学习记录</h1>
        <input type="button" value="提示信息1(不传参)" v-on:click="showInfo1">
        <!--简介v-on -->
        <input type="button" value="提示信息2(传参)" @click="showInfo2($event,668)">
    </div>
    <script type="text/javascript">
        Vue.config.productionTip = false // 阻止vue在启动时生成生产提示
        // 创建Vue对象
        new Vue({
            el: '#root',
            data: {
                name: 'Shier',
            },
            methods:{
                showInfo1(event){
                    alert('欢迎监督学习1')
                },
                showInfo2(event,number){
                    console.log(event,number)
                    alert('欢迎监督学习2')
                }
            }
        })
    </script>
</body>
```



### 2.7.1 Vue中的事件修饰符

* prevent：阻止默认事件（常用）
* stop：阻止事件冒泡（常用）
* once：事件只触发一次（常用）
* captrue：使用事件的捕获模式
* self：只有`event.target` 是当前操作元素菜触发事件
* passive：事件的默认行为立即执行，无需等待事件回调执行完毕。

> 修饰符可以连续写，比如可以这么用：`@click.prevent.stop="showInfo"`



~~~vue
<div id="root">
    <h2>欢迎来到{{name}}学习</h2>
    <!-- 阻止默认事件（常用） -->
	<a href="http://www.baidu.com" @click.prevent="showInfo">点我提示信息</a>
    <!-- 阻止事件冒泡（常用） -->
    <div class="demo1" @click="showInfo">
        <button @click.stop="showInfo">点我提示信息</button>
        <!-- 修饰符可以连续写 -->
        <!-- <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
    </div>
    <!-- 事件只触发一次（常用） -->
    <button @click.once="showInfo">点我提示信息</button>
</div>
~~~



### 2.7.2 键盘事件

键盘事件语法：`@keydown`，`@keyup`

Vue中常用的按键别名：

* 回车 => enter
* 删除 => delete
* 退出 => esc
* 空格 => space
* 换行 => tab (特殊，必须配合keydown去使用)
* 上 => up
* 下 => down
* 左 => left
* 右 => right



系统修饰键（用法特殊）：ctrl、alt、shift、meta

- 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发
- 配合keydown使用：正常触发事件



```js
<body>
    <!-- 创建一个容器-->
    <div id = 'app'>
        <h2>欢迎来到{{name}}</h2>
        <!--限制按下enter键才会触发事件-->
        <input type="text" placeholder="请输入提示内容" @keyup.enter="showInfo">
    </div>

    <script>
        Vue.config.productionTip = false
        new Vue({
            el:'#app',
            data: {
                name:'Shier',
            },
            methods:{
                showInfo(e) {
                    console.log('你按下了',e.key,'对应编码为',e.keyCode)
                }
            }
        })
    </script>
</body>
```



## 2.8 计算属性

* 定义：要用的属性不存在，要通过==已有属性计算得来==（data里面的属性），使用 `computed` 来定义计算属性
* 原理：底层借助了`Objcet.defineProperty`方法提供的getter和setter
* get函数什么时候执行？
  1. 初次读取时会执行一次
  2. 当依赖的数据发生改变时会被再次调用
* 优势：与methods实现相比，内部有缓存机制（复用），效率更高，调试方便
* 注意3点：
  1. 计算属性最终会出现在vm上，直接读取使用即可
  2. 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变
  3. 如果计算属性确定不考虑修改，可以使用计算属性的简写形式



姓名案例-methods方法实现

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        姓：<input type="text" placeholder="请输入姓" v-model="firstName"><br><br>
        名：<input type="text" placeholder="请输入名" v-model="lastName"><br><br>
        全名：<strong><span>{{ fullName() }}</span></strong>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示

        new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                firstName: '张',
                lastName: '三',
            },
            methods: {
                fullName() {
                    return this.firstName + this.lastName
                },
            }
        })
    </script>
</body>
```



姓名案例-计算属性实现

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        姓：<input type="text" placeholder="请输入姓" v-model="firstName"><br><br>
        名：<input type="text" placeholder="请输入名" v-model="lastName"><br><br>
        全名：<strong><span>{{ fullName }}</span></strong>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                firstName: '张',
                lastName: '三',
            },
            computed: {
                fullName: {
                    // 读取时调用
                    get() {
                        console.log('get被调用了')
                        return this.firstName + '-' + this.lastName
                    },
                    // fullName 修改时调用
                    set(value) {
                        console.log('修改成', value)
                        const arr = value.split('-')
                        this.firstName = arr[0]
                        this.lastName = arr[1]
                    }
                }

            }
        })
    </script>
</body>
```

执行结果如下：

![image-20230107153247279](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230107153247279.png)

计算属性简写：没有修改，只有读取形式

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        姓：<input type="text" placeholder="请输入姓" v-model="firstName"><br><br>
        名：<input type="text" placeholder="请输入名" v-model="lastName"><br><br>
        全名：<strong><span>{{ fullName }}</span></strong>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                firstName: '张',
                lastName: '三',
            },
            // 简写形式
            computed: {
                fullName(){
                    return this.firstName + '-' + this.lastName
                }
            }
        })
    </script>
</body>
```



## 2.9 监视属性-watch

监视属性watch：

* 当被监视的属性变化时, 回调函数自动调用, 进行相关操作
* 监视的属性必须存在，才能进行监视
* 监视的两种写法：
  1. new Vue时传入watch配置
  2. 通过`vm.$watch`监视



通过一个天气案例说明监视属性

方式一：

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        <h2>今天天气{{ weather }}</h2>
        <button @click="changeWeather">切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                isSunny: true
            },
            computed: {
                weather() {
                    return this.isSunny ? '晴天' : '下雨'
                }
            },
            methods: {
                changeWeather() {
                    this.isSunny = !this.isSunny
                },
            },
            // 监视配置对象
            watch: {
                isSunny: {
                    immediate: true, // 初始化时，让handler调用一下
                    handler(newValue, oldValue) {
                        console.log('isSunny修改了', oldValue, '=>', newValue)
                    }
                }
            }
        })
    </script>
</body>
```



方式二：

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        <h2>今天天气{{ weather }}</h2>
        <button @click="changeWeather">切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                isSunny: true
            },
            computed: {
                weather() {
                    return this.isSunny ? '晴天' : '下雨'
                }
            },
            methods: {
                changeWeather() {
                    this.isSunny = !this.isSunny
                },
            },
        })
        // 创建了Vue实例之后
        vm.$watch('isSunny',{
            immediate: true, // 初始化时，让handler调用一下
            handler(newValue, oldValue) {
                console.log('isSunny修改了', oldValue, '=>', newValue)
            }
        })
    </script>
</body>
```



### 2.9.1 深度监视

1. Vue中的watch默认不监测对象内部值的改变（一层）
2. 配置`deep:true`可以监测对象内部值改变（多层）



注意：

- Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以

- 使用watch时根据数据的具体结构，决定是否采用深度监视



```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        <h3>a值:{{ numbers.a }}</h3>
        <button @click="numbers.a++">a+1</button>
        <h3>b值:{{ numbers.b }}</h3>
        <button @click="numbers.b++">b+1</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                numbers: {
                    a: 1,
                    b: 2
                }
            },
            // 监视配置对象
            watch: {
               // 多层监视，属性里面的单个值变化
                'numbers.a':{
                    handler(){
                        console.log('a++了')
                    }
                },
                // 监视属性内部的改变情况
                numbers:{
                    deep:true, // 开启检测对象内部值的改变（检测多层）
                    handler() {
                        console.log('numbers改变了')
                    }
                }
            }
        })
    </script>
</body>
```

执行结果如下：

![image-20230108111620728](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230108111620728.png)

### 2.9.2 监视属性简写

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        <h2>今天天气{{ weather }}</h2>
        <button @click="changeWeather">切换天气</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                isSunny: true
            },
            computed: {
                weather() {
                    return this.isSunny ? '晴天' : '下雨'
                }
            },
            methods: {
                changeWeather() {
                    this.isSunny = !this.isSunny
                },
            },
            // 监视配置对象
            watch: {
                // 完整写法 
                /*weather: {
                    immediate: true, // 初始化时，让handler调用一下
                    handler(newValue, oldValue) {
                        console.log('weather修改了', oldValue, '=>', newValue)
                    }
                }*/
                // 简写写法，不需要设置其他的，只需要响应handler既可以简写
                weather: {
                    handler(newValue, oldValue) {
                        console.log('weather修改了', oldValue, '=>', newValue)
                    }
                }
            }
        })
        // $watch简写形式
        vm.$watch('weather',function (newValue, oldValue){
            console.log('weather修改了', oldValue, '=>', newValue)
        })
    </script>
</body>
```



### 2.9.3 computed和watch之间的区别

* computed能完成的功能，watch都可以完成
* watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作

函数的两个重要小原则：

1. 所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm 或 组件实例对象

2. 所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数、Promise的回调函数等）最好写成箭头函数，这样this的指向才是vm 或 组件实例对象

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}</h2>
        姓：<input type="text" placeholder="请输入姓" v-model="firstName"><br><br>
        名：<input type="text" placeholder="请输入名" v-model="lastName"><br><br>
        全名：<strong><span>{{ fullName}}</span></strong>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                firstName: '张',
                lastName: '三',
                fullName:'张 三'
            },
            watch:{
                // watch 监视器里可以写 异步函数
                firstName(value){
                    setTimeout(()=>{
                        this.fullName = value + ' ' + this.lastName
                    },500);
                },
                lastName(value){
                    setTimeout(()=>{
                        this.fullName = this.firstName + ' ' + value
                    },500);
                }
            }
        })
    </script>
</body>
```



## 2.10 绑定样式

1. class样式：
   - 写法：`class="xxx"`，xxx可以是字符串、对象、数组
   - 字符串写法适用于：类名不确定，要动态获取
   - 对象写法适用于：要绑定多个样式，个数不确定，名字也不确定
   - 数组写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用
2. style样式
   - `:style="{fontSize: xxx}"`其中xxx是动态值
   - `:style="[a,b]"`其中a、b是样式对象



使用到的Style

~~~css
<style>
    .basic{
        width: 400px;
        height: 100px;
        border: 1px solid black;
    }
    .happy{
        border: 4px solid red;;
        background-color: rgba(255, 255, 0, 0.644);
        background: linear-gradient(30deg,yellow,pink,orange,yellow);
    }
    .sad{
        border: 4px dashed rgb(2, 197, 2);
        background-color: gray;
    }
    .normal{
        background-color: skyblue;
    }

    .atguigu1{
        background-color: yellowgreen;
    }
    .atguigu2{
        font-size: 30px;
        text-shadow:2px 2px 10px red;
    }
    .atguigu3{
        border-radius: 20px;
    }
</style>
~~~



class样式类型写法：

- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定
- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定
- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用

style样式类型写法

- 对象写法
- 数组写法

~~~html
<div id="root">
    <!-- 绑定class样式--字符串写法，适用于：样式的类名不确定，需要动态指定 -->
    <div class="basic" :class="mood" @click="changeMood">{{name}}</div> <br/><br/>

    <!-- 绑定class样式--数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
    <div class="basic" :class="classArr">{{name}}</div> <br/><br/>

    <!-- 绑定class样式--对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
    <div class="basic" :class="classObj">{{name}}</div> <br/><br/>

    <!-- 绑定style样式--对象写法 -->
    <div class="basic" :style="styleObj">{{name}}</div> <br/><br/>

    <!-- 绑定style样式--数组写法 -->
    <div class="basic" :style="styleArr">{{name}}</div>
</div>
~~~

script 中的Vue实例

~~~vue
<script type="text/javascript">
	Vue.config.productionTip = false
    const vm = new Vue({
        el:'#root',
        data:{
            name:'Shier',
            mood:'normal',
            classArr:['atguigu1','atguigu2','atguigu3'],
            classObj:{
                atguigu1:false,
                atguigu2:false,
            },
          // style 对象写法
            styleObj:{
                fontSize: '40px',
                color:'red',
            },
          // style 对象写法
            styleObj2:{
                backgroundColor:'orange'
            },
           // style数组写法
            styleArr:[
                {
                    fontSize: '40px',
                    color:'blue',
                },
                {
                    backgroundColor:'gray'
                }
            ]
        },
       // class的字符串的样式
        methods: {
            changeMood(){
                const arr = ['happy','sad','normal']
                const index = Math.floor(Math.random()*3)
                this.mood = arr[index]
            }
        },
    })
</script>
~~~

执行效果总体如下：

![image-20230108123828879](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230108123828879.png)





## 2.11 条件渲染

### 2.11.1 v-if

* 写法：

  1. `v-if="表达式" `

  2. `v-else-if="表达式"`

  3. `v-else="表达式"`

* 适用于：切换频率较低的场景

* 特点：不展示的DOM元素直接被移除

* 注意：`v-if`可以和 `:v-else-if`、`v-else`一起使用，但要求结构不能被“打断”

### 2.11.2 v-show

- 写法：`v-show="表达式"`
- 适用于：切换频率较高的场景
- 特点：不展示的DOM元素未被移除，仅仅是使用样式隐藏掉



> 使用`v-if`的时，元素可能无法获取到，而使用`v-show`一定可以获取到
>
> v-if 是实打实地改变dom元素，v-show 是隐藏或显示dom元素



```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <!--v-show条件渲染-->
        <h2 v-show="isShow">v-show欢迎来到{{ name }}</h2>
        <h2 v-show=" 1===1">v-show欢迎来到{{ name }}</h2>

        <!--v-if条件渲染-->
        <h2 v-if="isShow">v-if欢迎来到{{ name }}</h2>
        <h2 v-if="1===1">v-if欢迎来到{{ name }}</h2>

        <!--v-else-if、v-else-->
        <h2>number++:{{ number }}</h2>
        <button @click="number++">修改number</button>
        <div v-if="number === 1">1</div>
        <div v-else-if="number === 2">2</div>
        <div v-else-if="number === 3">3</div>
        <div v-else>number:(1-3)</div>

        <!-- v-if与template配合使用-->
        <template v-if="number===3">
            <h3>学习</h3>
            <h3>Vue</h3>
            <h3>看禹老师</h3>
        </template>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                isShow: true,
                number: 0
            },
        })
    </script>
</body>
```



## 2.12 列表渲染

### 2.12.1 v-for指令

* 用于遍历列表数据
* 语法：`v-for="(item, index) in xxx" :key="index"` ，xxx为一下几种的对象
* 可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）



~~~vue
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>基本列表</title>
		<script src="https://cdn.jsdelivr.net/npm/vue@2.7.14/dist/vue.js"></script>
	</head>
	<body>
		<div id="root">
      <h2>欢迎来到{{name}}学习笔记</h2>
        <!-- 遍历数组 -->
			<h2>人员列表（遍历数组）</h2>
			<ul>
				<li v-for="(p,index) in persons" :key="index">
					{{p.name}}-{{p.age}}
				</li>
			</ul>
      
      <!-- 遍历对象 -->
			<h2>汽车信息（遍历对象）</h2>
			<ul>
				<li v-for="(value,k) in car" :key="k">
					{{k}}-{{value}}
				</li>
			</ul>
      
			 <!-- 遍历字符串（用的少） -->
			<h2>遍历字符串（用的少）</h2>
			<ul>
				<li v-for="(char,index) in str" :key="index">
					{{char}}-{{index}}
				</li>
			</ul>
			<!-- 遍历指定次数（用的少） -->
			<h2>遍历指定次数（用的少）</h2>
			<ul>
				<li v-for="(number,index) in 5" :key="index">
					{{index}}-{{number}}
				</li>
			</ul>
		</div>

		<script type="text/javascript">
			Vue.config.productionTip = false
			new Vue({
				el:'#root',
         name：'Shier'
				data:{
					persons:[
						{id:'001',name:'张三',age:18},
						{id:'002',name:'李四',age:19},
						{id:'003',name:'王五',age:20}
					],
					car:{
						name:'奥迪A8',
						price:'70万',
						color:'黑色'
					},
					str:'hello'
				}
			})
		</script>
    </body>
</html>
~~~



### 2.12.2 key原理



vue中的key有什么作用？（key的内部原理）



就是vue的虚拟dom，vue会根据 data 中的数据生成虚拟dom，如果是第一次生成页面，就将虚拟dom转成真实dom，在页面展示出来。

虚拟dom有啥用？每次`vm._data` 中的数据更改，都会触发生成新的虚拟dom，新的虚拟dom会跟旧的虚拟dom进行比较，如果有相同的，在生成真实dom时，这部分相同的就不需要重新生成，只需要将两者之间不同的dom转换成真实dom，再与原来的真实dom进行拼接。我的理解是虚拟dom就是起到了一个dom复用的作用，还有避免重复多余的操作。



而key有啥用？

key是虚拟dom的标识。



参考：[Vue中虚拟的DOM](https://juejin.cn/post/6844903895467032589)



key一般为两种值（ index 或 id ），这两种的优缺点下面介绍：



用index作为key可能会引发的问题：

- 若对数据进行：逆序添加、逆序删除等破坏顺序操作：

- 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。




```html
<!-- 准备好一个容器-->
<div id="root">
    <!-- 遍历数组 -->
    <h2>人员列表（遍历数组）</h2>
    <button @click.once="add">添加一个老刘</button>
    <ul>
        <li v-for="(p,index) of persons" :key="index">
            {{p.name}}-{{p.age}}
            <input type="text">
        </li>
    </ul>
</div>

<script type="text/javascript">
	Vue.config.productionTip = false

	new Vue({
		el: '#root',
		data: {
			persons: [
				{ id: '001', name: '张三', age: 18 },
				{ id: '002', name: '李四', age: 19 },
				{ id: '003', name: '王五', age: 20 }
			]
		},
		methods: {
			add() {
				const p = { id: '004', name: '老刘', age: 40 }
				this.persons.unshift(p) // 在第一个位置添加
			}
		},
	});
</script>
```

#### index 作为key 图解

![image-20230108211244103](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230108211244103.png)



用index作为key可能会引发的问题：

1. 若对数据进行逆序添加、逆序删除等破坏顺序操作：
   - 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低
2. 若结构中还包含输入类的DOM：
   - 会产生错误DOM更新 ==> 界面有问题



#### id 作为key的示意图解

![image-20230108211620632](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230108211620632.png)



### 总结Key的作用

1. 虚拟DOM中key的作用：
   - key是虚拟DOM中对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】，随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：

2. 对比规则：

   1. 旧虚拟DOM中找到了与新虚拟DOM相同的key：

      - 若虚拟DOM中内容没变, 直接使用之前的真实DOM

      - 若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM

   2. 旧虚拟DOM中未找到与新虚拟DOM相同的key：

      - 创建新的真实DOM，随后渲染到到页面

3. 开发中如何选择key?

   - 最好使用每条==数据的唯一标识作为key==，比如id、手机号、身份证号、学号等唯一值

   - 如果不存在对数据的逆序添加、逆序删除等破坏顺序的操作，仅用于渲染列表，使用index作为key是没有问题的





### 2.12.3 列表过滤

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <!-- 遍历数组 -->
        <h2>人员列表</h2>
        <input type="text" placeholder="输入搜索内容" v-model="searchKeyWord">
        <ul>
            <li v-for="(p,index) of filterPersons">
                {{ p.name }}-{{ p.age }}-{{ p.address }}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                persons: [
                    {id: '001', name: '马冬梅', age: 18, address: '北京'},
                    {id: '002', name: '周冬雨', age: 19, address: '上海'},
                    {id: '003', name: '周杰伦', age: 20, address: '天津'},
                    {id: '004', name: '艾伦', age: 22, address: '重庆'}
                ],
                searchKeyWord: '',
                filterPersons: [], // 获取过滤后的内容
            },
            watch: {
                searchKeyWord: {
                    immediate: true,// 初始化一次
                    handler(value) {
                        this.filterPersons = this.persons.filter((p) => {
                            return p.name.indexOf(value) !== -1 // 输入的内容是否在name中，indexOf返回索引
                        })
                    }
                }
            },
          // 使用计算属性实现
          	computed:{
							 filterPersons(){
							 		return this.persons.filter((p)=>{
										return p.name.indexOf(this.searchKeyWord) !== -1
							 		})
							}
					 }
        })
    </script>
</body>
```



> 当 computed 和 watch 都能实现功能时，优先使用computed实现
>



### 2.12.4 列表排序

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <!-- 遍历数组 -->
        <h2>人员列表</h2>
        <input type="text" placeholder="输入搜索内容" v-model="searchKeyWord">
        <button @click="sortType = 2">年龄升序</button>
        <button @click="sortType = 1">年龄降序</button>
        <button @click="sortType = 0">原序</button>
        <ul>
            <li v-for="(p,index) of filterPersons" :key="index">
                {{ p.name }}-{{ p.age }}-{{ p.address }}
            </li>
        </ul>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                searchKeyWord: '',
                sortType: 0, // 0：原序，1：降序，2；升序
                persons: [
                    {id: '001', name: '马冬梅', age: 19, address: '北京'},
                    {id: '002', name: '周冬雨', age: 33, address: '上海'},
                    {id: '003', name: '周杰伦', age: 20, address: '天津'},
                    {id: '004', name: '艾伦', age: 10, address: '重庆'}
                ],
            },
            computed: {
                filterPersons() {
                    // 先过滤
                    const arr = this.persons.filter((p) => {
                        return p.name.indexOf(this.searchKeyWord) !== -1
                    })
                    // 再排序，判断是否需要排序
                    if (this.sortType) {
                        arr.sort((p1, p2) => {
                            return this.sortType === 1 ? p2.age - p1.age : p1.age - p2.age
                        })
                    }
                    return arr
                }
            }
        })
    </script>
</body>
```



效果如下

![image-20230108222444759](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230108222444759.png)



### 2.12.5 Vue数据监视

解析模板后面的操作---》调用 set 方法时，就会去解析模板----->生成新的虚拟DOM----->新旧DOM 对比 -----> 更新页面



模拟Vue中数据监视

~~~vue
<script type="text/javascript" >

    let data = {
        name:'尚硅谷',
        address:'北京',
    }

    //创建一个监视的实例对象，用于监视data中属性的变化
    const obs = new Observer(data)		
    console.log(obs)	

    //准备一个vm实例对象
    let vm = {}
    vm._data = data = obs

    function Observer(obj){
        //汇总对象中所有的属性形成一个数组
        const keys = Object.keys(obj)
        //遍历
        keys.forEach((k) => {
            Object.defineProperty(this, k, {
                get() {
                    return obj[k]
                },
                set(val) {
                    console.log('${k}被改了，我要去解析模板，生成虚拟DOM.....我要开始忙了')
                    obj[k] = val
                }
            })
        })
    }
</script>
~~~



`Vue.set`使用

![image-20230109114934385](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230109114934385.png)

`Vue.$set` 

![image-20230109123628650](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230109123628650.png)



> Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象 添加属性！！！



~~~vue
<!-- 准备好一个容器-->
<div id="root">
    <h1>学生信息</h1>
    <button @click="addSex">添加性别属性，默认值：男</button> <br/>
</div>

<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el:'#root',
        data:{
            student:{
                name:'tom',
                age:18,
                hobby:['抽烟','喝酒','烫头'],
                friends:[
                    {name:'jerry',age:35},
                    {name:'tony',age:36}
                ]
            }
        },
        methods: {
            addSex(){
                // Vue.set(this.student,'sex','男')
                this.$set(this.student,'sex','男')
            }
        }
    })
</script>
~~~



#### Vue检测数组的数据

~~~vue
<!-- 准备好一个容器-->
<div id="root">
    <h2>爱好</h2>
    <ul>
        <li v-for="(h,index) in student.hobby" :key="index">
            {{h}}
        </li>
    </ul>
    <h2>朋友们</h2>
    <ul>
        <li v-for="(f,index) in student.friends" :key="index">
            {{f.name}}--{{f.age}}
        </li>
    </ul>
</div>

<script type="text/javascript">
    Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

    const vm = new Vue({
        el:'#root',
        data:{
            student:{
                name:'tom',
                age:{
                    rAge:40,
                    sAge:29,
                },
                hobby:['抽烟','喝酒','烫头'],
                friends:[
                    {name:'jerry',age:35},
                    {name:'tony',age:36}
                ]
            }
        },
    })
</script>
~~~

如图，是无法修改hobby中的值，就算修改了Vue也是无法监视到修改之后的值，也就无法更新页面内容。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230109125316946.png" alt="image-20230109125316946" style="zoom:80%;" />

官网对数组变更的解释：

![image-20230109131727143](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230109131727143.png)

Vue监视数据

~~~html
    <!-- 准备好一个容器-->
    <div id="root">
        <h1>学生信息</h1>
        <button @click="student.age++">年龄+1岁</button><br/>
        <button @click="addSex">添加性别属性，默认值：男</button> <br/>
        <button @click="student.sex = '女'">修改性别</button> <br/>
        <button @click="addFriend">在列表首位添加一个朋友</button> <br/>
        <button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button><br/>
        <button @click="addHobby">添加一个爱好</button> <br/>
        <button @click="updateHobby">修改第一个爱好为：开车</button><br/>
        <button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br/>
        <h3>姓名：{{student.name}}</h3>
        <h3>年龄：{{student.age}}</h3>
        <h3 v-if="student.sex">性别：{{student.sex}}</h3>
        <h3>爱好：</h3>
        <ul>
            <li v-for="(h,index) in student.hobby" :key="index">
                {{ h }}
            </li>
        </ul>
        <h2>朋友们</h2>
        <ul>
            <li v-for="(f,index) in student.friends" :key="index">
                {{ f.name }}--{{ f.age }}
            </li>
        </ul>
    </div>

    <script type="text/javascript">
        Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。
        const vm = new Vue({
            el: '#root',
            data: {
                student: {
                    name: 'Shier',
                    age: {
                        rAge: 40,
                        sAge: 29,
                    },
                    hobby: ['抽烟', '喝酒', '烫头'],
                    friends: [
                        {name: 'jerry', age: 35},
                        {name: 'tony', age: 36}
                    ]
                }
            },
            methods:{
                addSex(){
                    // vm.$set(this.student,'sex','男')
                    Vue.set(this.student,'sex','男')
                },
                addFriend(){
                    this.student.friends.unshift({name:'Shier1',age:22})
                },
                updateFirstFriendName(){
                    this.student.friends[0].name = '张三'
                },
                addHobby(){
                    this.student.hobby.unshift('学习')
                },
                updateHobby(){
                  	// 三种写法
                    // this.student.hobby.splice(0,1,'ctr')
                    // Vue.set(this.student.hobby,0,'开车玩')
                    vm.$set(this.student.hobby,0,'开车玩')
                },
                removeSmoke(){
                  // 直接将新的数组替换掉旧的数组
                    this.student.hobby = this.student.hobby.filter((p)=>{
                        return p !== '抽烟'
                    })
                },
            }
        })
    </script>
~~~

显示如下：

![image-20230109134030591](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230109134030591.png)



#### Vue监视数据的原理

* vue会监视data中所有层次的数据

* 如何监测对象中的数据？

  通过setter实现监视，且要在new Vue时就传入要监测的数据。

  * 对象中后追加的属性，Vue默认不做响应式处理

  * 如需给后添加的属性做响应式，请使用如下API：

    `Vue.set(target，propertyName/index，value)` 或 `vm.$set(target，propertyName/index，value)`

* 如何监测数组中的数据？

  通过包裹数组更新元素的方法实现，本质就是做了两件事：

  * 调用原生对应的方法对数组进行更新
  * 重新解析模板，进而更新页面

* 在Vue修改数组中的某个元素一定要用如下方法：

  * 使用这些API：push()、pop()、shift()、unshift()、splice()、sort()、reverse()
  * Vue.set() 或 vm.$set()



## 2.13 收集表单数据

1. 若：`<input type="text"/>`，则v-model收集的是value值，用户输入的就是value值。

2. 若：`<input type="radio"/>`，则v-model收集的是value值，且要给标签配置value值。

3. 若：`<input type="checkbox"/>`

   * 没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）

   * 配置input的value属性:
     * v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
     * v-model的初始值是数组，那么收集的的就是value组成的数组


v-model的三个修饰符：

1. lazy：失去焦点再收集数据

2. number：输入字符串转为有效的数字

3. trim：不收集输入的空格

视频中案例：

```vue
<body>
    <!-- 创建一个容器-->
    <div id = 'app'>
        <h2>欢迎来到{{name}}学习笔记</h2>
        <form @submit.prevent="demo" >
            账号：<input type="text" v-model.trim="userInfo.account"> <br/><br/>
            密码：<input type="password" v-model="userInfo.password"> <br/><br/>
            年龄：<input type="number" v-model.number="userInfo.age"> <br/><br/>
            性别：
            男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
            女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> <br/><br/>
            爱好：
            学习<input type="checkbox" v-model="userInfo.hobby" value="study">
            打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
            吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
            <br/><br/>
            所属校区：
            <select v-model="userInfo.city">
                <option value="">请选择校区</option>
                <option value="beijing">北京</option>
                <option value="shanghai">上海</option>
                <option value="shenzhen">深圳</option>
                <option value="wuhan">武汉</option>
            </select>
            <br/><br/>
            其他信息：
            <textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
            <input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.baidu.com">《用户协议》</a><br/><br/>
            <button>提交</button>
        </form>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el:'#app',
            data: {
                name:'Shier',
                userInfo:{
                    account:'',
                    password:'',
                    sex:'male',
                    hobby:[],
                    city:'shenzhen',
                    other:'',
                    agree:'',
                }
            },
            methods:{
                demo(){
                    console.log(JSON.stringify(this.userInfo))
                },
            }
        })
    </script>
</body>
```



## 2.14 过滤器

定义：对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。

**语法：**

* 注册过滤器：`Vue.filter(name,callback) `或 `new Vue{filters:{}}`
* 使用过滤器：=={{ xxx | 过滤器名}}==  或  ==v-bind:属性 = "xxx | 过滤器名"==

注意：

1. 过滤器也可以接收额外参数、多个过滤器也可以串联

2. 并没有改变原本的数据, 是产生新的对应的数据



```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2>显示格式化后的时间</h2>
        <!-- 计算属性实现 -->
        <h3>计算属性实现,现在是：{{ fmtTime }}</h3>
        <!-- methods实现 -->
        <h3>methods实现,现在是：{{ getFmtTime() }}</h3>
        <!-- 过滤器实现 -->
        <h3>过滤器实现,现在是：{{ time | timeFormater }}</h3>
        <!-- 过滤器实现（传参） -->
        <h3>过滤器实现（传参）,现在是：{{ time | timeFormater('YYYY/MM/DD') | mySlice }} 年</h3>

        <h3 :x="msg | mySlice">尚硅谷</h3>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示

        //全局过滤器
        Vue.filter('mySlice',function(value){
            return value.slice(0,4) // 将时间的前四位保留
        })
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                time: 1673245892084,
                msg:'学习3333445',
            },
            computed: {
                fmtTime() {
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss')
                },
            },
            methods: {
                getFmtTime() {
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss')
                },
            },
            // 局部过滤器写法,过滤器本质就是函数
            filters: {
                timeFormater(value, srt= 'YYYY-MM-DD HH:mm:ss' ) {
                    return dayjs(value).format(srt)
                },
            }
        })
    </script>
</body>
```



## 2.15 内置指令

### 2.15.1 v-text指令：(使用的比较少)

作用：向其所在的节点中渲染（插入）文本内容。

与插值语法的区别：

- v-text会替换掉节点中的内容，{{xx}}（插值语法）则不会。

```vue
<body>
    <!-- 创建一个容器-->
    <div id = 'app'>
        <h2>欢迎来到{{name}}学习笔记</h2>
        <h2 v-text="name"></h2>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el:'#app',
            data: {
                name:'Shier',
            }
        })
    </script>
</body>
```



### 2.15.2 v-html指令：(使用的很少)

作用：向指定节点中渲染包含html结构的内容。

与插值语法的区别：

* v-html会替换掉节点中所有的内容，{{xx}}则不会。
* v-html可以识别html结构。
* `{{}}`双大括号和`v-text`都是输出纯文文本，不会进行转换成html格式，那如果想输出为html，则使用`v-html` 进行渲染

```vue
<body>
    <!-- 创建一个容器-->
    <div id = 'app'>
        <h2>欢迎来到{{name}}学习笔记</h2>
        <h2 v-html="str"></h2>

    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el:'#app',
            data: {
                name:'Shier',
                str:'<h3>欢迎来学习</h3>'
            }
        })
    </script>
</body>
```

严重注意：v-html有安全性问题！！！！

* 在网站上动态渲染任意HTML是非常危险的，容易导致XSS（跨站脚本攻击）攻击。
* 一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！



### 2.15.3 v-cloak指令（没有值）

* 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
* 使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}的问题。



### 2.15.4 v-once指令：(用的少)

* v-once所在节点在初次动态渲染后，只会执行一次渲染，当数据发生改变时，不会再变化，就视为静态内容（只渲染一次）了。
* 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2 v-once>初始化number值：{{ number }}</h2>
        <h2>初始化number值：{{ number }}</h2>
        <button @click="number++">number+1</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                number: 1
            }
        })
    </script>
</body>
```



### 2.15.5 v-pre指令：

* 跳过其所在节点的编译过程
* 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>初始化number值：{{ number }}</h2>
        <h2 v-pre>你好吗，网不好</h2>
        <button @click="number++">number+1</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                number: 1
            }
        })
    </script>
</body>
```



### 2.15.6 前面学习过的指令

1. `v-bind`：将标签内的属性值解析成js代码，在标签的属性中使用v-bind，双引号里的内容会被当作js解析（只能解析变量或三元表达式），还可以单向绑定该数据
2. `v-model` : 用于双向绑定数据，限制在`<input>、<select>、<textarea>`、components中使用
3. `v-show`：接受一个表达式或一个布尔值。相当于给元素添加一个`display`属性
4. `v-if、v-else、v-else-if`：
   1. `v-if`和`v-show`有同样的效果，不同在于`v-if`是重新渲染，而`v-show`使用`display`属性来控制显示隐藏。频繁切换的话使用`v-show`减少渲染带来的开销。
   2. `v-if`可以单独使用，而`v-else-if`,`v-else`必须与`v-if`组合使用
   3. `v-if、v-else-if`都是接受一个条件或布尔值，`v-else`不需要参数
5. `v-for` ：用来遍历数组、对象、字符串
6. `v-on` ：事件绑定，简写为 @
7. v-solt：[参考](https://v2.cn.vuejs.org/v2/api/#v-slot)



## 2.16 自定义指令



### 2.16.1 自定义函数式指令

需求：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2>当前n:{{ n }}</h2>
        <h2>放大后的n:<span v-big="n">{{ n }}</span></h2>
        <button @click="n++">n++</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                n: 1
            },
            // 自定义指令函数式
            directives: {
                // 1.指令与元素成功绑定时被调用
                // 2.指令所在的模板被重新解析时，就被调用
                big(el, binding) {
                    el.innerHTML = binding.value * 10
                }
            }
        })
    </script>
</body>
```



自定义函数式指令何时调用？

1. 指令与元素成功绑定时被调用
2. 指令所在的模板被重新解析时，就被调用

#### 定义全局函数式指令

~~~js
// 定义全局指令-函数形式
Vue.directive('big', function (el, binding) {
    el.innerHTML = binding.value * 10
})
~~~



### 2.16.2 自定义对象式指令

需求：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。



```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2>当前n:{{ n }}</h2>
        <h2>放大后的n:<span v-big="n">{{ n }}</span></h2>
        <button @click="n++">n++</button>
        <br>
        <input type="text" v-fbind:value="n">
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                n: 1
            },
            // 自定义指令函数式
            directives: {
                // 1.指令与元素成功绑定时被调用
                // 2.指令所在的模板被重新解析时，就被调用
                big(el, binding) {
                    el.innerHTML = binding.value * 10
                },
                fbind:{
                    // 指令与元素成功绑定时调用。
                    bind(el, binding){
                        el.value = binding.value
                    },
                    // 指令所在元素被插入页面时调用。
                    inserted(el, binding){
                        el.focus()
                    },
                    // 指令所在模板结构被重新解析时调用。
                    update(el, binding){
                        el.value = binding.value
                    },
                }
            }
        })
    </script>
</body>
```

配置对象中常用的3个回调：

* bind：指令与元素成功绑定时调用。
* inserted：指令所在元素被插入页面时调用。
* update：指令所在模板结构被重新解析时调用。

#### 定义全局指令-对象形式

```js
// 定义全局指令-对象形式
Vue.directive('fbind', {
    // 指令与元素成功绑定时调用。
    bind(el, binding) {
        el.value = binding.value
    },
    // 指令所在元素被插入页面时调用。
    inserted(el, binding) {
        el.focus()
    },
    // 指令所在模板结构被重新解析时调用。
    update(el, binding) {
        el.value = binding.value
    },
})
```



### 总结

自定义指令定义语法：

1. 局部指令：

   对象形式

   ~~~js
    new Vue({															
    	directives:{指令名:配置对象}   
    }) 		
   ~~~

   函数形式：

   ~~~js
    new Vue({															
    	directives:{指令名:回调函数}   
    }) 
   ~~~

2. 全局指令

   1. `Vue.directive(指令名,配置对象)`
   2. `Vue.directive(指令名,回调函数)`

   如同以下形式：

   ```js
   // 定义全局指令-对象形式
   Vue.directive('fbind', {
       // 指令与元素成功绑定时调用。
       bind(el, binding) {
           el.value = binding.value
       },
       // 指令所在元素被插入页面时调用。
       inserted(el, binding) {
           el.focus()
       },
       // 指令所在模板结构被重新解析时调用。
       update(el, binding) {
           el.value = binding.value
       },
   })
   // 定义全局指令-函数形式
   Vue.directive('big', function (el, binding) {
       el.innerHTML = binding.value * 10
   })
   ```



创建对象自定义指令中常用的3个回调函数：

1. `bind(element,binding)`：指令与元素成功绑定时调用
2. `inserted(element,binding)`：指令所在元素被插入页面时调用
3. `update(element,binding)`：指令所在模板结构被重新解析时调用



注意：

1. 指令定义时不加`“v-”`，但使用时要加`“v-”`
2. 指令名如果是多个单词，要使用`kebab-case`命名方式，不要用`camelCase`命名
   - kebab-case：就是使用 `-` 进行单词之间的链接
   - camelCase：就是驼峰命名规则



## 2.17 Vue生命周期

Vue生命周期：Vue 实例有⼀个完整的⽣命周期，也就是从new Vue()、初始化事件(.once事件)和生命周期、编译模版、挂载Dom -> 渲染、更新 -> 渲染、卸载 等⼀系列过程。

### 2.17.1 引出生命周期案例

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2 :style="{opacity}">引出Vue生命周期</h2>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                opacity: 1
            },
            // 完成挂载：Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂在完毕）调用mounted
            mounted() {
                setInterval(() => {
                    console.log(this.opacity)
                    this.opacity -= 0.01
                    if (this.opacity <= 0) {
                        this.opacity = 1
                    }
                }, 50)
            },
        })
    </script>
</body>
```



 生命周期

1. 又名：生命周期回调函数、生命周期函数、生命周期钩子
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的函数
3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的
4. 生命周期函数中的this指向是vm 或 组件实例对象



### 2.17.2 Vue执行流程

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2>当前的number：{{ number }}</h2>
        <button @click="add">number+1</button>
        <button @click="bye">结束生命周期</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            // template:`
            //     <div>
            //        <h2>当前的n值是：{{n}}</h2>
            //        <button @click="add">点我n+1</button>
            //     </div>
            // `, // 会替换掉上面整个容器
            data: {
                name: 'Shier',
                number: 1
            },
            methods: {
                add() {
                    this.number++
                },
                bye(){
                    console.log('bye')
                }
            },
            watch:{
                n(){
                    console.log('n变了')
                }
            },
            // 以下是生命周期函数
            beforeCreate() {
                console.log('beforeCreate')
            },
            created() {
                console.log('created')
            },
            beforeMount() {
                console.log('beforeMount')
            },
            mounted() {
                console.log('mounted')
            },
            beforeUpdate() {
                console.log('beforeUpdate')
            },
            updated() {
                console.log('updated')
            },
            beforeDestroy() {
                console.log('beforeDestroy')
            },
            destroyed() {
                console.log('destroyed')
            },
        })
    </script>
</body>
```



Vue生命周期执行流程图：

![Vue生命周期](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/Vue%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F.png)



**Vue生命周期执行流程解析：**

1. **beforeCreate（创建前）**：数据监测(getter和setter)和初始化事件还未开始，此时 data 的响应式追踪、event/watcher 都还没有被设置，也就是说不能访问到data、computed、watch、methods上的方法和数据。
2. **created（创建后）**：实例创建完成，实例上配置的 options 包括 data、computed、watch、methods 等都配置完成，但是此时渲染得节点还未挂载到 DOM，所以不能访问到 `$el`属性。
3. **beforeMount（挂载前）**：在挂载开始之前被调用，相关的render函数首次被调用。此阶段Vue开始解析模板，生成虚拟DOM存在内存中，还没有把虚拟DOM转换成真实DOM，插入页面中。所以网页不能显示解析好的内容。
4. **mounted（挂载后）**：在el被新创建的 vm.$el（就是真实DOM的拷贝）替换，并挂载到实例上去之后调用（将内存中的虚拟DOM转为真实DOM，真实DOM插入页面）。此时页面中呈现的是经过Vue编译的DOM，这时在这个钩子函数中对DOM的操作可以有效，但要尽量避免。一般在这个阶段进行：开启定时器，发送网络请求，订阅消息，绑定自定义事件等等
5. **beforeUpdate（更新前）**：响应式数据更新时调用，此时虽然响应式数据更新了，但是对应的真实 DOM 还没有被渲染（数据是新的，但页面是旧的，页面和数据没保持同步呢）。
6. **updated（更新后）** ：在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。此时 DOM 已经根据响应式数据的变化更新了。调用时，组件 DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。
7. **beforeDestroy（销毁前）**：实例销毁之前调用。这一步，实例仍然完全可用，`this` 仍能获取到实例。在这个阶段一般进行关闭定时器，取消订阅消息，解绑自定义事件。
8. **destroyed（销毁后）**：实例销毁后调用，调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务端渲染期间不被调用。



### 总结：

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
        <h2 :style="{opacity}">引出Vue生命周期</h2>
        <button @click="stop">停止变化</button>
    </div>

    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
                opacity: 1
            },
            methods: {
                stop() {
                    // 销毁
                    this.$destroy()
                }
            },
            // 完成挂载：Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂在完毕）调用mounted
            mounted() {
                this.timer = setInterval(() => {
                    console.log(this.opacity)
                    this.opacity -= 0.03
                    if (this.opacity <= 0) {
                        this.opacity = 1
                    }
                }, 50)
            },
            // 销毁之前停止定时器
            beforeDestroy() {
                clearInterval(this.timer)
            }
        })
    </script>
</body>
```



常用的生命周期钩子：

1. `mounted`：发送ajax请求、启动定时器、绑定自定义事件、订阅消息等【初始化操作】
2. `beforeDestroy`：清除定时器、解绑自定义事件、取消订阅消息等收尾工作



关于销毁Vue实例：

1. 销毁后借助Vue开发者工具看不到任何信息
2. ==销毁后自定义事件会失效==，但原生DOM事件依然有效
3. 一般不会在`beforeDestroy`操作数据，因为即便操作数据，也不会再触发更新流程了





# 3、Vue组件化编程



## 3.1 组件介绍

- 定义：用来实现==局部功能==的代码和资源的集合（html/css/js/image…）
- 为什么：一个界面的功能很复杂，简化页面编码
- 作用：代码复用率高，简化项目编码，提高运行效率



通过传统编写应用方法 与 组件方式编写应用方法对比，突出组件编码的优势：

传统的形式：

![传统编写应用](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E4%BC%A0%E7%BB%9F%E7%BC%96%E5%86%99%E5%BA%94%E7%94%A8.png)



组件编写形式：

- 将同一部分的文件进行封装

![组件编写应用](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E7%BB%84%E4%BB%B6%E7%BC%96%E5%86%99%E5%BA%94%E7%94%A8.png)



对页面进行组件形式管理（不断嵌套）

![image-20230110110017241](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230110110017241.png)



### 3.1.1 组件化

当应用中的功能都是多组件的方式来编写的，那这个应用就是一个组件化的应用



## 3.2 模块

- 理解：向外提供特定功能的 js 程序，一般就是一个 js 文件
- 为什么：js 文件很多很复杂
- 作用： 提高 js 的复用，简化 js 的编写，提高 js 运行效率



### 3.2.1 模块化

当应用中的 js 都以模块（按照不同的功能来拆分，但是都还是在同一个组件中）来编写的，那这个应用就是一个模块化的应用



## 3.3 非单文件组件

### 3.3.1 非单文件组件介绍

> 一个文件中包含有 n 个组件



### 3.3.2 非单文件组件基本使用

组件的使用步骤：

1. 创建组件
2. 注册组件
3. 使用（调用）组件

如何定义一个组件？

使用Vue.extend(options)创建，其中options和new Vue(options)时传入的options几乎一样，但也有点区别：

1. el不要写，为什么？

   - 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器

2. data必须写成函数，为什么？

   - 避免组件被复用时，数据存在引用关系

3. 如何注册组件？

   - 局部注册：`new Vue`的时候传入`components`选项

   - 全局注册：`Vue.component('组件名',组件)`

4. 使用组件标签：`<component1></component1>`

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
        <h2>欢迎来到{{ name }}学习笔记</h2>
    <!--3.使用组件-->
        <component1></component1>
        <component2></component2>
        <hr>
    </div>
    <div id="root">
        <!--全局组件-->
        <component2></component2>
    </div>
    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        // 1.创建组件标签
        const component1 = Vue.extend({
            template: `
              <div>
                <h2>学习笔记地址：{{ address }}</h2>
              </div>
            `,
            // data 必须写成一个函数形式
            data() {
                return{
                    address:'局部地址',
                }
            }
        })
        // 创建全局组件
        const component2 = Vue.extend({
            template: `
              <div>
                <h2>学习笔记地址：{{ address }}</h2>
              </div>
            `,
            // data 必须写成一个函数形式
            data() {
                return{
                    address:'全局地址',
                }
            }
        })
        // 注册全局组件
        Vue.component('component2',component2)
        const vm = new Vue({
            el: '#app',
            data: {
                name: 'Shier',
            },
            // 2. 局部注册组件
            components:{
                component1
            }
        })
        new Vue({
            el:'#root',
            data:{
            }
        })
    </script>
</body>
```



### 3.3.3 非单文件组件注意事项

关于组件名：

1. 一个单词组成：

   - 第一种写法（首字母小写）：school

   - 第二种写法（首字母大写）：School

2. 多个单词组成：

   - 第一种写法（kebab-case命名）：my-school

   - 第二种写法（CamelCase命名）：MySchool （需要Vue脚手架支持）

   备注：

   - 组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行

   - 可以使用name配置项指定组件在开发者工具中呈现的名字

关于组件标签：

- 第一种写法：`<school></school>`
- 第二种写法：`<school/>`

- 备注：不使用脚手架时，<school/>会导致后续组件不能渲染
  - 一个简写方式：const school = Vue.extend(options)可简写为：const school = options

```vue
<body>
    <!-- 创建一个容器-->
    <div id = 'app'>
        <h2>欢迎来到{{name}}学习笔记</h2>
        <school></school>
        <hr>
        <school1></school1>
    </div>
    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示
        const school = Vue.extend({
            name:'school',
            template:`
            <div>
               <h2>学校名称：{{name}}</h2>
               <h2>学校地址：{{address}}</h2>
            </div>
         `,
            data(){
                return {
                    name:'尚硅谷',
                    address:'北京'
                }
            }
        })
        // 简写形式
        const school1 ={
            name:'school',
            template:`
            <div>
               <h2>学校名称：{{name}}</h2>
               <h2>学校地址：{{address}}</h2>
            </div>
         `,
            data(){
                return {
                    name:'尚硅谷1',
                    address:'北京1'
                }
            }
        }
        new Vue({
            el:'#app',
            data:{
                name:'Shier',
            },
            components:{
                school,
                school1
            }
        })
    </script>
</body>
```



### 3.3.4 组件的嵌套

```vue
<body>
    <!-- 创建一个容器-->
    <div id='app'>
    </div>
    <script>
        Vue.config.productionTip = false // 阻止Vue启动时生产提示


        // 定义子组件
        const student = Vue.extend({
            name: 'student',
            template: `
              <div>
              <h2>学生名称：{{ name }}</h2>
              <h2>学生班级：{{ address }}</h2>
              <hr>
              </div>
            `,
            data() {
                return {
                    name: 'Shier',
                    address: '2033'
                }
            }
        })

        // 定义父组件标签
        const school = Vue.extend({
            name: 'school',
            template: `
              <div>
              <h2>学校名称：{{ name }}</h2>
              <h2>学校地址：{{ address }}</h2>
              <hr>
              <!--使用子student组件标签-->
              <student></student>
              </div>
            `,
            data() {
                return {
                    name: '尚硅谷',
                    address: '北京'
                }
            },
            // 在父组件中注册子组件标签
            components: {
                student
            }
        })

        // 定义组件
        const come = Vue.extend({
            name: 'come',
            template: `
              <div>
              <h2>欢迎来到{{ name }}学习笔记</h2>
              <hr>
              </div>
            `,
            data() {
                return {
                    name: 'Shier',
                }
            }
        })

        // 定义app组件
        const app = Vue.extend({
            name: 'app',
            template: `
              <div>
              <come></come>
              <school></school>
              </div>
            `,
          // 注册其他的子组件
            components: {
                come,
                school
            }
        })

        new Vue({
            template:`<app></app>`,
            el: '#app',
            // 注册组件
            components: {app}
        })
    </script>
</body>
```

### 3.3.5 VueComponent

1. school组件本质是一个名为VueComponent的构造函数，且不是程序员定义的，是Vue.extend生成的。
2. 我们只需要写`<school/>`或`<school></school>`，Vue解析时会帮我们创建school组件的实例对象，即Vue帮我们执行的：new VueComponent(options)。
3. 特别注意：==每次调用`Vue.extend`，返回的都是一个全新的`VueComponent` ! (这个VueComponent可不是实例对象)== (分配了不同的内存空间)
4. 关于this指向：
   * 组件配置中的this：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是 VueComponent实例对象vc。
   * new Vue(options)配置中的this：data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是 Vue实例对象vm。
5. `VueComponent`的实例对象，以后简称vc（也可称之为：组件实例对象）。Vue的实例对象，以后简称vm。



VueComponent管理的内容：

![image-20230110154816839](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230110154816839.png)

- 一个children就是一个组件



### 3.3.6 Vue实例与组件实例



Vue实例对象 ViewModel 【vm】

- new Vue出来的
- vm能指定容器，通过`el` 配置项指定容器



组件实例对象VueComponent 【vc】

- vc不能指定容器 ，也就是不能写 `el` 配置项



> vm 不能完全等同于vc



### 3.3.7 重要的内置关系

* 一个重要的内置关系：`VueComponent.prototype.__proto__ === Vue.prototype` (VueComponent的原型对象的原型就是Vue的原型)
* 为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

![重要关系](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E9%87%8D%E8%A6%81%E5%85%B3%E7%B3%BB.png)





## 3.4 单文件组件

### 3.4.1 单文件组件介绍

> 一个文件中只包含有 1 个组件



将一个组件的代码写在 .vue 这种格式的文件中，webpack 会将 .vue 文件解析成 html,css,js这些形式。





School.vue

```html
<template>
	<div class="demo">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
		<button @click="showName">点我提示学校名</button>	
	</div>
</template>

<script>
	 export default {
		name:'School',
		data(){
			return {
				name:'尚硅谷',
				address:'北京昌平'
			}
		},
		methods: {
			showName(){
				alert(this.name)
			}
		},
	}
</script>

<style>
	.demo{
		background-color: orange;
	}
</style>
```

Student.vue

```html
<template>
	<div>
		<h2>学生姓名：{{name}}</h2>
		<h2>学生年龄：{{age}}</h2>
	</div>
</template>

<script>
	 export default {
		name:'Student',
		data(){
			return {
				name:'张三',
				age:18
			}
		}
	}
</script>
```

App.vue

用来汇总所有的组件  (管理所有的组件)

```html
<template>
	<div>
		<School></School>
		<Student></Student>
	</div>
</template>

<script>
	//引入组件
	import School from './School.vue'
	import Student from './Student.vue'

	export default {
		name:'App',
		components:{
			School,
			Student
		}
	}
</script>
```

main.js

在这个文件里面创建 vue 实例

```js
import App from './App.vue'

new Vue({
	el:'#root',
	template:`<App></App>`,
	components:{App},
})
```

index.html

在这写 vue 要绑定的容器

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>练习一下单文件组件的语法</title>
	</head>
	<body>
		<!-- 准备一个容器 -->
		<div id="root"></div>
        <script type="text/javascript" src="../js/vue.js"></script>
		<script type="text/javascript" src="./main.js"></script>
	</body>
</html>
```



# 4、Vue脚手架（Vue-CLI）

[中文官网](https://cli.vuejs.org/zh/) 

Vue-CLI全称：==command line interface==

Vue.js 开发的标准工具



## 4.1 创建Vue脚手架

### 4.1.1 安装Vue-cli

如果下载缓慢请配置 npm 淘宝镜像：`npm config set registry http://registry.npm.taobao.org`



第一步(没有安装过的执行)：全局安装 @vue/cli

~~~bash
npm install -g @vue/cli
# OR
yarn global add @vue/cli
~~~

第二步：切换到要创建项目的目录，然后使用命令创建项目

~~~vue
vue create xxxxx
~~~

第三步：启动项目

~~~bash
npm run serve
~~~

第四步：选择使用vue的版本

第五步：启动项目：`npm run serve`

- 暂停项目：Ctrl+C



### 4.1.2 脚手架目录结构

~~~git
.文件目录
├── node_modules 
├── public
│   ├── favicon.ico: 页签图标
│   └── index.html: 主页面
├── src
│   ├── assets: 存放静态资源
│   │   └── logo.png
│   │── component: 存放组件
│   │   └── HelloWorld.vue
│   │── App.vue: 汇总所有组件
│   └── main.js: 入口文件
├── .gitignore: git版本管制忽略的配置
├── babel.config.js: babel的配置文件
├── package.json: 应用包配置文件 
├── README.md: 应用描述文件
└── package-lock.json: 包版本控制文件
~~~



![image-20230110193940172](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230110193940172.png)



## 4.2 main.js中的 rander 函数

之前的写法是这样：

```js
import App from './App.vue'

new Vue({
	el:'#root',
	template:`<App></App>`,
	components:{App},
})
```

如果这样子写，运行的话会引发如下的报错

![image-20230110204543640](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230110204543640.png)

报错的意思是，是在使用运行版本的 vue ，没有模板解析器。

从上面的小知识可以知道，我们引入的 vue 不是完整版的，是残缺的（为了减小vue的大小）。所以残缺的vue.js 只有通过 render 函数才能把项目给跑起来。

来解析一下render

~~~js
// render最原始写的方式
// render是个函数，还能接收到参数a
// 这个 createElement 很关键，是个回调函数
new Vue({
  render(createElement) {
      console.log(typeof createElement);
      // 这个 createElement 回调函数能创建元素
      // 因为残缺的vue 不能解析 template，所以render就来帮忙解决这个问题
      // createElement 能创建具体的元素
      return createElement('h1', 'hello')
  }
}).$mount('#app')
~~~

![image-20230110204628258](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230110204628258.png)



 render 函数内并没有用到 this，所以可以简写成箭头函数。

```js
new Vue({
  render: (createElement) => {
    return createElement(App)
  }
}).$mount('#app')
```

再简写：

```js
new Vue({
  // render: h => h(App),
  render: createElement => createElement(App)
}).$mount('#app')

```

最后把 createElement 换成 h 就完事了。

~~~js
new Vue({
    el: '#app',
    radar: h => h(App)
})
~~~



#### 理解 render 函数的简写方式

对象内写方法最原始的：

```js
let obj = {
    name: 'aaa',
    work: function (salary) {
        return '工资' + salary;
    }
}
```

ES6 简化版：

```js
let obj = {
    name: 'aaa',
    work(salary) {
        return '工资' + salary;
    }
}
```

箭头函数简化版:

```js
let obj = {
    name: 'aaa',
    work: (salary) => {
        return '工资' + salary;
    }
}
```

箭头函数再简化（最终版）：

```js
// 只有一个参数就可以把圆括号去了，函数体内部只有一个 return 就可以把大括号去掉，return去掉
let obj = {
    name: 'aaa',
    work: salary => '工资' + salary;
}
```



来个不同版本 vue 的区别

* `vue.js`与`vue.runtime.xxx.js`的区别：
  * `vue.js`是完整版的Vue，包含：核心功能+模板解析器。（体积大）
  * `vue.runtime.xxx.js`是运行版的Vue，只包含：核心功能；没有模板解析器。(体积小)
* 因为`vue.runtime.xxx.js`没有模板解析器，所以不能使用template配置项，需要使用render函数接收到的createElement函数去指定具体内容。

### 修改脚手架的默认配置

* 使用`vue inspect > output.js`可以查看到Vue脚手架的默认配置。
* 使用`vue.config.js`可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh



创建工程出来的脚手架中index.html

~~~html
<!DOCTYPE html>
<html lang="">
  <head>
    <meta charset="utf-8">
	<!-- 针对IE浏览器的一个特殊配置，含义是让IE浏览器以最高的渲染级别渲染页面 -->
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
	<!-- 开启移动端的理想视口 -->
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
	<!-- 配置页签图标 -->
    <link rel="icon" href="<%= BASE_URL %>favicon.ico">
	<!-- 引入第三方样式 -->
	<link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css">
	<!-- 配置网页标题 -->
    <title></title>
  </head>
  <body>
		<!-- 当浏览器不支持js时noscript中的元素就会被渲染 -->
    <noscript>
      <strong>We're sorry but <%= htmlWebpackPlugin.options.title %> doesn't work properly without JavaScript enabled. Please enable it to continue.</strong>
    </noscript>
		<!-- 容器 -->
    <div id="app"></div>
    <!-- built files will be auto injected -->
  </body>
</html>
~~~



## 4.3 ref属性



* 被用来给元素或子组件注册引用信息（id的替代者）
* 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
* 使用方式：
  * 打标识：```<h1 ref="xxx">.....</h1>```或 ```<School ref="xxx"></School>```
  * 获取：```this.$refs.xxx```

~~~vue
<template>
	<div>
		<h1 v-text="msg" ref="title"></h1>
		<button ref="btn" @click="showDOM">点我输出上方的DOM元素</button>
		<School ref="sch"/>
	</div>
</template>

<script>
	//引入School组件
	import School from './components/School'

	export default {
		name:'App',
		components:{School},
		data() {
			return {
				msg:'欢迎学习Vue！'
			}
		},
		methods: {
			showDOM(){
				console.log(this.$refs.title) //真实DOM元素
				console.log(this.$refs.btn) //真实DOM元素
				console.log(this.$refs.sch) //School组件的实例对象（vc）
			}
		},
	}
</script>
~~~



## 4.4 props配置

1. 功能：让组件接收外部传过来的数据

2. 传递数据：```<Demo name="xxx"/>```

3. 接收数据：

   1. 第一种方式（只接收）：`props:['name'] `

   2. 第二种方式（限制类型）：`props:{name:String}`

   3. 第三种方式（限制类型、限制必要性、指定默认值）：

      ```js
      props:{
      	name:{
              type:String, //类型
              required:true, //必要性
              default:'Vue' //默认值
      	}
      }
      ```

   

> ==备注==：
>
> 1. props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。
> 2. 必要性和默认值不会同时出现的，因为都必须填写了，默认值就不会起作用，简单理解一下



通过案例说明：

`Student.vue`

~~~vue
<template>
  <div>
    <h1>{{ msg }}</h1>
    <h2>学生姓名：{{ Name }}</h2>
    <h2>学生年龄：{{ age }}</h2>
    <h2>学生性别：{{ sex }}</h2>
    <button @click="ageAdd">年龄+1</button>
  </div>
</template>

<script>
export default {
  name: "School",
  data() {
    return {
      msg: '欢迎Shier学习Vue！！'
    }
  },
  methods: {
    ageAdd() {
      this.age++
    }
  },
  // 第一种形式 props 只接受数据
  // props:['name','age','sex'],

  // 第二种形式 props 接收数据且限定接收的类型
  /*  props:{
      name:String,
      age:Number,
      sex:String
    },*/
  // 第二种形式 props 接收数据且限定类型+必要性+默认值
  props: {
    name: {
      type: String,
      required: true
    },
    age: {
      type: Number,
      default: 20
    },
    sex: {
      type: String,
      required: true
    }
  }
}
</script>
~~~

`App.vue`

```vue
<template>
  <div>
    <Student name="Shier" :age="18" sex="男"/>
  </div>
</template>

<script>
//引入School组件
import Student from './components/Student'

export default {
  name:'App',
  components:{Student},
}
</script>
```

运行效果如下：

![image-20230111123649736](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230111123649736.png)



## 4.5 mixin （混入）

混入 (mixin) 提供了一种非常灵活的方式，来分发 Vue 组件中的可复用功能。一个混入对象可以包含任意组件选项。当组件使用混入对象时，所有混入对象的选项将被“混合”进入该组件本身的选项。



功能：可以把多个组件共用的配置提取成一个混入对象

定义混入：

~~~js
const mixin = {
    data(){....},
    methods:{....}
    ....
}
~~~

使用混入：

1. 全局混入：Vue.mixin(xxx)
2. 局部混入：mixins:['xxx']



注意：

1. 当组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”。
2. 数据对象在内部会进行递归合并，并在发生冲突时以组件数据优先。
3. 值为对象的选项，例如 `methods`、`components` 和 `directives`，将被合并为同一个对象。两个对象键名冲突时，取组件对象的键值对。
4. 同名生命周期钩子将合并为一个数组，因此都将被调用。另外，混入对象的钩子将在组件自身钩子之前调用。
5. 组件和混入对象含有同名选项时，这些选项将以恰当的方式进行“合并”，在发生冲突时以组件优先。



`School.vue`

```vue
<template>
  <div>
    <h2 @click="ShowName">学校姓名：{{ name }}</h2>
    <h2>学校地址：{{ address }}</h2>
    <hr>
  </div>
</template>

<script>
// 引入 mixin 混合
import {mixin} from '../mixin'
export default {
  name: "School",
  data() {
    return {
      name:'B站大学',
      address:'https://www.bilibili.com/',
    }
  },
  // mixins
  mixins:[mixin]
}
</script>
```



`Student.vue`

```vue
<template>
  <div>
    <h2 @click="ShowName">学生姓名：{{ Name }}</h2>
    <h2>学生年龄：{{ age }}</h2>
    <hr>
  </div>
</template>

<script>
// 引入mixin混合
import {mixin} from '../mixin'
export default {
  name: "School",
  data() {
    return {
      Name:'Shier',
      age:18,
    }
  },
  // mixin配置项
  mixins:[mixin]
}
</script>
```



`mixin.js`

```js
/**
 * Author:Shier
 * createTime:13:13
 */

export const mixin = {
    methods:{
        ShowName(){
            alert(this.Name)
        }
    }
}
```



全局引入混合：在`main.js`中

```js
// 全局配置mixin
import {mixin} from './mixin'
Vue.mixin(mixin)
```

> 不推荐全局引入混合



## 4.6 插件

插件通常用来为 Vue 添加全局功能。插件的功能范围没有严格的限制。

通过全局方法 `Vue.use()` 使用插件。在项目入口中调用插件`main.js` ：使用插件：`Vue.use(文件名,[参数1,参数2,....参数n])`

```js
// 使用插件
Vue.use(plugin)

new Vue({
  // ...组件选项
})
```

本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是插件使用者传递的数据。

### 4.6.1 定义插件

~~~js
对象.install = function (Vue, options) {
    // 1. 添加全局过滤器
    Vue.filter(....)

    // 2. 添加全局指令
    Vue.directive(....)

    // 3. 配置全局混入(合)
    Vue.mixin(....)

    // 4. 添加实例方法
    Vue.prototype.$myMethod = function () {...}
    Vue.prototype.$myProperty = xxxx
}
~~~



实现案例：

1. 定义插件(`plugins.js`)：

   ```js
   /**
    * Author:Shier
    * createTime:13:43
    */
   export default {
       install(Vue, x, y, z) {
           console.log(x, y, z)
           //全局过滤器
           Vue.filter('mySlice', function (value) {
               return value.slice(0, 4)
           })
   
           //定义全局指令
           Vue.directive('fbind', {
               //指令与元素成功绑定时（一上来）
               bind(element, binding) {
                   element.value = binding.value
               },
               //指令所在元素被插入页面时
               inserted(element, binding) {
                   element.focus()
               },
               //指令所在的模板被重新解析时
               update(element, binding) {
                   element.value = binding.value
               }
           })
   
           //定义混入
           Vue.mixin({
               data() {
                   return {
                       x: 100,
                       y: 200
                   }
               },
           })
           //给Vue原型上添加一个方法（vm和vc就都能用了）
           Vue.prototype.hello = () => {
               alert('你好啊1111')
           }
       }
   }
   ```

2. 全局定义插件`main.js`

   ```js
   // 引入插件文件
   import plugin from "./plugins";
   // 使用插件
   Vue.use(plugin)
   ```

3. 使用插件：

   在需要的地方调用插件里面功能的名字



## 4.7 scoped样式

1. 作用：让样式在局部生效，防止冲突。
2. 写法：`<style scoped>`

```vue
<template>
  <div class="school">
    <h2>学校姓名：{{ name }}</h2>
    <h2 class="fontSize">学校地址：{{ address }}</h2>
    <hr>
  </div>
</template>

<script>
export default {
  name: "School",
  data() {
    return {
      name: 'B站大学sdddddsd',
      address: 'https://www.bilibili.com/',
    }
  },
}
</script>
<style lang="less" scoped>
  /* lang="" 指定样式的格式*/
  .school{
    background: red;
    .fontSize{
      font-size: 50px;
    }
  }
</style>
```

执行效果：

![image-20230111141457115](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230111141457115.png)



## 4.8 Todo-list案例

1. 组件化编码流程：

   拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。

   实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   1. 一个组件在用：放在组件自身即可。

   2. 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

   实现交互：从绑定事件开始。

2. props适用于：

   1. 父组件 ==> 子组件 通信

   2. 子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！

4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。



### 具体实现

`App.vue`

```vue
<template>
  <div id="root">
    <div class="todo-container">
      <div class="todo-wrap">
        <HeaderTodo :addTodo="addTodo"/>
        <ListTodo :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo"/>
        <FooterTodo :todos="todos" :checkAllTodo="checkAllTodo" :clearAllTodo="clearAllTodo"/>
      </div>
    </div>
  </div>
</template>

<script>
  import HeaderTodo from './components/HeaderTodo.vue'
  import ListTodo from './components/ListTodo.vue'
  import FooterTodo from './components/FooterTodo.vue'

  export default {
    name: 'App',
    components: {HeaderTodo, ListTodo, FooterTodo},
    data() {
      return {
        todos: [
          {id: '001', title: '吃饭', done: false},
          {id: '002', title: '睡觉', done: false},
          {id: '003', title: '学习', done: false},
        ]
      }
    },
    methods: {
      //添加一个todo
      addTodo(todoObj) {
        // 回车就会在列表中添加显示
        this.todos.unshift(todoObj)
      },
      // 勾选or取消勾选一个todo
      checkTodo(id) {
        this.todos.forEach((todo) => {
          if (todo.id === id) {
            todo.done = !todo.done
          }
        })
      },
      //删除一个todo
      deleteTodo(id) {
        this.todos = this.todos.filter(todo => todo.id !== id)
      },
      //全选or取消勾选
      checkAllTodo(done) {
        this.todos.forEach(todo => todo.done = done)
      },
      //删除已完成的todo
      clearAllTodo() {
        this.todos = this.todos.filter(todo => !todo.done)
      }
    }
  }
</script>

<style>
  body {
    background: #fff;
  }

  .btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
    border-radius: 4px;
  }

  .btn-danger {
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
  }

  .btn-danger:hover {
    color: #fff;
    background-color: #bd362f;
  }

  .btn:focus {
    outline: none;
  }

  .todo-container {
    width: 600px;
    margin: 0 auto;
  }

  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
```

`FooterTodo.vue`

```vue
<!--
User:Shier
CreateTime:14:35
-->
<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll"/>
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
  export default {
    name: 'FooterTodo',
    props: ['todos', 'checkAllTodo', 'clearAllTodo'],
    computed: {
      doneTotal() {
        return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0)
      },
      total() {
        return this.todos.length
      },
      isAll: {
        get() {
          return this.total === this.doneTotal && this.total > 0
        },
        set(value) {
          this.checkAllTodo(value)
        }
      }
    },
    methods: {
      clearAll() {
        this.clearAllTodo()
      }
    }
  }
</script>

<style scoped>
  .todo-footer {
    height: 40px;
    line-height: 40px;
    padding-left: 6px;
    margin-top: 5px;
  }

  .todo-footer label {
    display: inline-block;
    margin-right: 20px;
    cursor: pointer;
  }

  .todo-footer label input {
    position: relative;
    top: -1px;
    vertical-align: middle;
    margin-right: 5px;
  }

  .todo-footer button {
    float: right;
    margin-top: 5px;
  }
</style>
```



`ItemTodo.vue`

```vue
<!--
User:Shier
CreateTime:14:35
-->
<template>
  <li>
    <label>
      <input type="checkbox" :checked="todo.done" @click="handleCheck(todo.id)"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" @click="handleDelete(todo.id,todo.title)">删除</button>
  </li>
</template>

<script>
  export default {
    name:'ItemTodo',
    props:['todo','checkTodo','deleteTodo'],
    methods:{
      handleCheck(id){
        // 通过id进行勾选
        this.checkTodo(id)
      },
      handleDelete(id,title){
        if(confirm("确定删除任务："+title+"吗？")){
          this.deleteTodo(id)
        }
      }
    }
  }
</script>

<style scoped>
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }

  li label {
    float: left;
    cursor: pointer;
  }

  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }

  li button {
    float: right;
    display: none;
    margin-top: 3px;
  }

  li:before {
    content: initial;
  }

  li:last-child {
    border-bottom: none;
  }

  li:hover {
    background-color: #eee;
  }

  li:hover button{
    display: block;
  }
</style>
```

`HeaderTodo.vue`

```vue
<!--
User:Shier
CreateTime:14:25
-->
<template>
  <div class="todo-header">
    <input type="text" placeholder="请输入你的任务名称，按回车键确认" @keydown.enter="add" v-model="title"/>
  </div>
</template>

<script>
  import {nanoid} from 'nanoid'
  export default {
    name:'HeaderTodo',
    data() {
      return {
        // 绑定数据
        title:''
      }
    },
    methods:{
      add(){
        // 校验数据
        if(!this.title.trim()) return
        const todoObj = {id:nanoid(),title:this.title,done:false}
        // App组件添加一个todo对象
        this.addTodo(todoObj)
        // 清空输入
        this.title = ''
      }
    },
    props:['addTodo']
  }
</script>

<style scoped>
  .todo-header input {
    width: 560px;
    height: 28px;
    font-size: 14px;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 4px 7px;
  }

  .todo-header input:focus {
    outline: none;
    border-color: rgba(82, 168, 236, 0.8);
    box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
  }
</style>
```

`ListTodo.vue`

```vue
<!--
User:Shier
CreateTime:14:35
-->
<template>
  <ul class="todo-main">
    <itemTodo
        v-for="todo in todos"
        :key="todo.id"
        :todo="todo"
        :checkTodo="checkTodo"
        :deleteTodo="deleteTodo"
    />
  </ul>
</template>

<script>
  import itemTodo from './ItemTodo.vue'
  export default {
    name:'ItemTodo',
    components:{itemTodo},
    props:['todos','checkTodo','deleteTodo']
  }
</script>

<style scoped>
  .todo-main {
    margin-left: 0px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding: 0px;
  }

  .todo-empty {
    height: 40px;
    line-height: 40px;
    border: 1px solid #ddd;
    border-radius: 2px;
    padding-left: 5px;
    margin-top: 10px;
  }
</style>
```



## 4.9 浏览器本地存储



### 4.9.1 Cookie

Cookie是最早被提出来的本地存储方式，在此之前，服务端是无法判断网络中的两个请求是否是同一用户发起的，为解决这个问题，Cookie就出现了。Cookie 是存储在用户浏览器中的一段不超过 4 KB 的字符串。它由一个名称（Name）、一个值（Value）和其它几个用 于控制 Cookie 有效期、安全性、使用范围的可选属性组成。不同域名下的 Cookie 各自独立，每当客户端发起请求时，会自动把当前域名下所有未过期的 Cookie 一同发送到服务器。



**Cookie的特性：**

- Cookie一旦创建成功，名称就无法修改
- Cookie是无法跨域名的，也就是说a域名和b域名下的cookie是无法共享的，这也是由Cookie的隐私安全性决定的，这样就能够阻止非法获取其他网站的Cookie
- 每个域名下Cookie的数量不能超过20个，每个Cookie的大小不能超过4kb
- 有安全问题，如果Cookie被拦截了，那就可获得session的所有信息，即使加密也于事无补，无需知道cookie的意义，只要转发cookie就能达到目的
- Cookie在请求一个新的页面的时候都会被发送过去



**Cookie 在身份认证中的作用**

客户端第一次请求服务器的时候，服务器通过响应头的形式，向客户端发送一个身份认证的 Cookie，客户端会自动 将 Cookie 保存在浏览器中。

随后，当客户端浏览器每次请求服务器的时候，浏览器会自动将身份认证相关的 Cookie，通过请求头的形式发送给 服务器，服务器即可验明客户端的身份。


![在这里插入图片描述](https://img-blog.csdnimg.cn/e29b7e0bef784bc5b6b8ed50b0d8a509.png)



**Cookie 不具有安全性**

由于 Cookie 是存储在浏览器中的，而且浏览器也提供了读写 Cookie 的 API，因此 Cookie 很容易被伪造，不具有安全性。因此不建议服务器将重要的隐私数据，通过 Cookie 的形式发送给浏览器。

> 注意：千万不要使用 Cookie 存储重要且隐私的数据！比如用户的身份信息、密码等。



### 4.9.2 Session

Session是另一种记录客户状态的机制，不同的是Cookie保存在客户端浏览器中，而Session保存在服务器上。客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了session是一种特殊的cookie。cookie是保存在客户端的，而session是保存在服务端。

为什么要用session

> 由于cookie 是存在用户端，而且它本身存储的尺寸大小也有限，最关键是用户可以是可见的，并可以随意的修改，很不安全。那如何又要安全，又可以方
>
> 便的全局读取信息呢？于是，这个时候，一种新的存储会话机制：session 诞生了

**session原理**
当客户端第一次请求服务器的时候，服务器生成一份session保存在服务端，将该数据(session)的id以cookie的形式传递给客户端；以后的每次请求，浏览器都会自动的携带cookie来访问服务器(session数据id)。

>图示：

![image-20221229132346113](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221229132346113.png)

>session可以简单理解为一个表，根据cookie传来的值查询表中的内容

**session 标准工作流程**

![session](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/Session.c66d5499.png)



### 4.9.3 LocalStorage

LocalStorage是HTML5新引入的特性，由于有的时候我们存储的信息较大，Cookie就不能满足我们的需求，这时候LocalStorage就派上用场了。



**LocalStorage的优点：**

- 在大小方面，LocalStorage的大小一般为5MB，可以储存更多的信息
- LocalStorage是持久储存，并不会随着页面的关闭而消失，除非主动清理，不然会永久存在
- 仅储存在本地，不像Cookie那样每次HTTP请求都会被携带



**LocalStorage的缺点：**

- 存在浏览器兼容问题，IE8以下版本的浏览器不支持
- 如果浏览器设置为隐私模式，那我们将无法读取到LocalStorage
- LocalStorage受到同源策略的限制，即端口、协议、主机地址有任何一个不相同，都不会访问



**LocalStorage的常用API：**

```js
// 保存数据到 localStorage
localStorage.setItem('key', 'value');

// 从 localStorage 获取数据
let data = localStorage.getItem('key');

// 从 localStorage 删除保存的数据
localStorage.removeItem('key');

// 从 localStorage 删除所有保存的数据
localStorage.clear();

// 获取某个索引的Key
localStorage.key(index)
```



**LocalStorage的使用场景:**

- 有些网站有换肤的功能，这时候就可以将换肤的信息存储在本地的LocalStorage中，当需要换肤的时候，直接操作LocalStorage即可
- 在网站中的用户浏览信息也会存储在LocalStorage中，还有网站的一些不常变动的个人信息等也可以存储在本地的LocalStorage中



### 4.9.4 SessionStorage

SessionStorage和LocalStorage都是在HTML5才提出来的存储方案，SessionStorage 主要用于临时保存同一窗口(或标签页)的数据，刷新页面时不会删除，关闭窗口或标签页之后将会删除这些数据。



**SessionStorage与LocalStorage对比：**

- SessionStorage和LocalStorage都在**本地进行数据存储**；
- SessionStorage也有同源策略的限制，但是SessionStorage有一条更加严格的限制，SessionStorage**只有在同一浏览器的同一窗口下才能够共享**；
- LocalStorage和SessionStorage**都不能被爬虫爬取**；



**SessionStorage的常用API：**

```js
// 保存数据到 sessionStorage
sessionStorage.setItem('key', 'value');

// 从 sessionStorage 获取数据
let data = sessionStorage.getItem('key');

// 从 sessionStorage 删除保存的数据
sessionStorage.removeItem('key');

// 从 sessionStorage 删除所有保存的数据
sessionStorage.clear();

// 获取某个索引的Key
sessionStorage.key(index)
```



**SessionStorage的使用场景**

由于SessionStorage具有时效性，所以可以用来存储一些网站的游客登录的信息，还有临时的浏览记录的信息。当关闭网站之后，这些信息也就随之消除了。



**localStorage**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>localStorage</title>
	</head>
	<body>
		<h2>localStorage</h2>
		<button onclick="saveData()">点我保存一个数据</button>
		<button onclick="readData()">点我读取一个数据</button>
		<button onclick="deleteData()">点我删除一个数据</button>
		<button onclick="deleteAllData()">点我清空一个数据</button>

		<script type="text/javascript" >
			let p = {name:'张三',age:18}

			function saveData(){
				localStorage.setItem('msg','hello!!!')
				localStorage.setItem('msg2',666)
        // 转成 JSON 对象存进去
				localStorage.setItem('person',JSON.stringify(p))
			}
			function readData(){
				console.log(localStorage.getItem('msg'))
				console.log(localStorage.getItem('msg2'))

				const result = localStorage.getItem('person')
				console.log(JSON.parse(result))

				// console.log(localStorage.getItem('msg3'))
			}
			function deleteData(){
				localStorage.removeItem('msg2')
			}
			function deleteAllData(){
				localStorage.clear()
			}
		</script>
	</body>
</html>
```

**sessionStorage**

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8" />
		<title>sessionStorage</title>
	</head>
	<body>
		<h2>sessionStorage</h2>
		<button onclick="saveData()">点我保存一个数据</button>
		<button onclick="readData()">点我读取一个数据</button>
		<button onclick="deleteData()">点我删除一个数据</button>
		<button onclick="deleteAllData()">点我清空一个数据</button>

		<script type="text/javascript" >
			let p = {name:'张三',age:18}

			function saveData(){
				sessionStorage.setItem('msg','hello!!!')
				sessionStorage.setItem('msg2',666)
        // 转换成JSON 字符串存进去
				sessionStorage.setItem('person',JSON.stringify(p))
			}
			function readData(){
				console.log(sessionStorage.getItem('msg'))
				console.log(sessionStorage.getItem('msg2'))

				const result = sessionStorage.getItem('person')
				console.log(JSON.parse(result))

				// console.log(sessionStorage.getItem('msg3'))
			}
			function deleteData(){
				sessionStorage.removeItem('msg2')
			}
			function deleteAllData(){
				sessionStorage.clear()
			}
		</script>
	</body>
</html>
```



### 4.9.5 总结

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）
2. 浏览器端通过`Window.sessionStorage`和`Window.localStorage`属性来实现本地存储机制
3. `xxxStorage.setItem('key', 'value')`：该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值
4. `xxxStorage.getItem('key')`：该方法接受一个键名作为参数，返回键名对应的值
5. `xxxStorage.removeItem('key')`：该方法接受一个键名作为参数，并把该键名从存储中删除
6. `xxxStorage.clear()`：该方法会清空存储中的所有数据

注意：

- SessionStorage存储的内容会随着浏览器窗口关闭而消失
- LocalStorage存储的内容，需要手动清除才会消失
- `xxxStorage.getItem(xxx)`如果 xxx 对应的 value 获取不到，那么getItem()的返回值是null
- `JSON.parse(null)`的结果依然是null，为JSON格式



## 4.10 组件自定义事件

组件自定义事件是一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>

**使用场景**

A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。



### 4.10.1 绑定自定义事件：

第一种方式，在父组件中：`<Student@atguigu="test"/>`或 `<Student v-on:atguigu="test"/>`

> 具体代码

App.vue

```html
<template>
	<div class="app">
		<!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第一种写法，使用@或v-on） -->
		<Student @atguigu="getStudentName"/> 
	</div>*
</template>

<script>
	import Student from './components/Student'

	export default {
		name:'App',
		components:{Student},
		data() {
			return {
				msg:'你好啊！',
				studentName:''
			}
		},
		methods: {
			getStudentName(name,...params){
				console.log('App收到了学生名：',name,params)
				this.studentName = name
			}
		}
	}
</script>

<style scoped>
	.app{
		background-color: gray;
		padding: 5px;
	}
</style>

```

Student.vue

```html
<template>
	<div class="student">
		<button @click="sendStudentlName">把学生名给App</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			return {
				name:'张三',
			}
		},
		methods: {
			sendStudentlName(){
				// 触发Student组件实例身上的atguigu事件
				this.$emit('atguigu',this.name,666,888,900)
			}
		},
	}
</script>

<style lang="less" scoped>
	.student{
		background-color: pink;
		padding: 5px;
		margin-top: 30px;
	}
</style>

```



第二种方式，在父组件中：

使用 `this.$refs.xxx.$on()` 这样写起来更灵活，比如可以加定时器啥的。

> 具体代码

App.vue

```html
<template>
	<div class="app">
		<!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第二种写法，使用ref） -->
		<Student ref="student"/>
	</div>
</template>

<script>
	import Student from './components/Student'

	export default {
		name:'App',
		components:{Student},
		data() {
			return {
				studentName:''
			}
		},
		methods: {
			getStudentName(name,...params){
				console.log('App收到了学生名：',name,params)
				this.studentName = name
			},
		},
		mounted() {
			this.$refs.student.$on('atguigu',this.getStudentName) //绑定自定义事件
			// this.$refs.student.$once('atguigu',this.getStudentName) //绑定自定义事件（一次性）
		},
	}
</script>

<style scoped>
	.app{
		background-color: gray;
		padding: 5px;
	}
</style>
```

Student.vue

```html
<template>
	<div class="student">
		<button @click="sendStudentlName">把学生名给App</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			return {
				name:'张三',
			}
		},
		methods: {
			sendStudentlName(){
				//触发Student组件实例身上的atguigu事件
				this.$emit('atguigu',this.name,666,888,900)
			}
		},
	}
</script>

<style lang="less" scoped>
	.student{
		background-color: pink;
		padding: 5px;
		margin-top: 30px;
	}
</style>

```

> 1. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。
>
> 2. 触发自定义事件：```this.$emit('atguigu',数据)```		
>
>    使用 this.$emit() 子组件就可以向父组件传数据



### 4.10.2 解绑自定义事件

`this.$off('atguigu')`

```js
this.$off('atguigu') //解绑一个自定义事件
// this.$off(['atguigu','demo']) //解绑多个自定义事件
// this.$off() //解绑所有的自定义事件
```

`App.vue`

~~~js
<template>
    <div class="app">
        <Student @shier="getStudentName"/>
    </div>
</template>

<script>
    import Student from './components/Student.vue'

    export default {
        name:'App',
        components: { Student },
        methods:{
            getStudentName(name){
                console.log("已收到学生的姓名："+name)      
            }
        }
    }
</script>

<style scoped>
	.app{
		background-color: gray;
		padding: 5px;
	}
</style>
~~~

`Student.vue`

~~~js
<template>
    <div class="student">
        <h2>学生姓名：{{name}}</h2>
        <h2>学生性别：{{sex}}</h2>
        <button @click="sendStudentName">点我传递学生姓名</button> 
        <button @click="unbind">解绑自定义事件</button> 
    </div>
</template>

<script>
    export default {
        name:'Student',
        data() {
            return {
                name:'Shier',
								sex:'男'
            }
        },
        methods:{
            sendStudentName(){
                this.$emit('shier',this.name)
            },
            unbind(){
                // 解绑一个自定义事件
                // this.$off('shier')
                // 解绑多个自定义事件
                // this.$off(['shier'])
                // 解绑所有自定义事件
                this.$off()
            }
        }
    }
</script>

<style scoped>
    .student{
        background-color: chartreuse;
        padding: 5px;
		margin-top: 30px;
    }
</style>
~~~



**组件上也可以绑定原生DOM事件，需要使用```native```修饰符。**

```vue
<!-- 通过父组件给子组件绑定一个自定义事件实现：子给父传递数据（第二种写法，使用ref） --> 
<Student ref="student" @click.native="show"/>
```



> 注意：通过`this.$refs.xxx.$on('atguigu',回调)`绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！



## 4.11 全局事件总线

> 全局事件总线是一种可以在任意组件间通信的方式，本质上就是一个对象。它必须满足以下条件：1. 所有的组件对象都必须能看见他 2. 这个对象必须能够使用`$on`、`$emit`和`$off`方法去绑定、触发和解绑事件

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 安装全局事件总线：

   ```js
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

   2. 提供数据：```this.$bus.$emit('xxxx',数据)```

4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。



代码实现：

`School.vue`

```html
<template>
	<div class="school">
		<h2>学校名称：{{name}}</h2>
		<h2>学校地址：{{address}}</h2>
	</div>
</template>

<script>
	export default {
		name:'School',
		data() {
			return {
				name:'尚硅谷',
				address:'北京',
			}
		},
    methods: {
       demo(data) {
         console.log('我是School组件，收到了数据',data)
       }
    }
		mounted() {
			this.$bus.$on('hello',this.demo)
		},
		beforeDestroy() {
			this.$bus.$off('hello')
		},
	}
</script>

<style scoped>
	.school{
		background-color: skyblue;
		padding: 5px;
	}
</style>
```

`Student.vue`

```html
<template>
	<div class="student">
		<h2>学生姓名：{{name}}</h2>
		<h2>学生性别：{{sex}}</h2>
		<button @click="sendStudentName">把学生名给School组件</button>
	</div>
</template>

<script>
	export default {
		name:'Student',
		data() {
			return {
				name:'张三',
				sex:'男',
			}
		},
		mounted() {
			// console.log('Student',this.x)
		},
		methods: {
			sendStudentName(){
				this.$bus.$emit('hello',this.name)
			}
		},
	}
</script>

<style lang="less" scoped>
	.student{
		background-color: pink;
		padding: 5px;
		margin-top: 30px;
	}
</style>

```




## 4.12 消息订阅与发布

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：`npm i pubsub-js`

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods:{
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：```pubsub.publish('xxx',数据)```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>

订阅消息

`School.vue`

```html
<template>
  <div class="school">
    <h2>学校名称：{{name}}</h2>
    <h2>学校地址：{{address}}</h2>
  </div>
</template>

<script>
  import pubsub from 'pubsub-js'
  export default {
    name:'School',
    data() {
      return {
        name:'尚硅谷',
        address:'北京',
      }
    },
    mounted() {
      // 接收信息
      this.pubId = pubsub.subscribe('hello',(msgName,data)=>{
        console.log('接收到消息,信息内容为：',data)
      })
    },
    beforeDestroy() {
      pubsub.unsubscribe(this.pubId)
    },
  }
</script>

<style scoped>
  .school{
    background-color: skyblue;
    padding: 5px;
  }
</style>
```

发布消息

`Student.vue`

```html
<template>
  <div class="student">
    <h2>学生姓名：{{name}}</h2>
    <h2>学生性别：{{sex}}</h2>
    <button @click="sendStudentName">把学生名给School组件</button>
  </div>
</template>

<script>
  import pubsub from 'pubsub-js'
  export default {
    name:'Student',
    data() {
      return {
        name:'张三',
        sex:'男',
      }
    },
    mounted() {
    },
    methods: {
      sendStudentName(){
        pubsub.publish('hello',666)
      }
    },
  }
</script>

<style lang="less" scoped>
  .student{
    background-color: pink;
    padding: 5px;
    margin-top: 30px;
  }
</style>
```



### 4.12.1 nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在`nextTick`所指定的回调函数中执行。

```js
this.$nextTick(function(）{
	this.$refs.inputTitle.focus()
}
```



## 4.13 Vue封装的过度与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

   图解：

   ![image-20230117222348361](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230117222348361.png)

2. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点


   2. 使用```<transition>```包裹要过渡的元素，并配置name属性：

      ```html
      <transition name="hello">
      	<h1 v-show="isShow">xxx</h1>
      </transition>
      ```


备注：若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。



案例-单个元素过渡

> name 的作用可以让不同的元素有不同的动画效果

```html
<!--
User:Shier
CreateTime:21:13
-->
<template>
  <div>
    <button @click="isShow = !isShow">显示/隐藏</button>
    <transition name="demo" appear>
      <h1 v-show="isShow">左右过度显示隐藏</h1>
    </transition>
  </div>
</template>

<script>
  export default {
    name:'Test',
    data() {
      return {
        isShow:true
      }
    },
  }
</script>

<style scoped>
  h1{
    background-color: orange;
  }

  .demo-enter-active{
    animation: move 0.5s linear;
  }

  .demo-leave-active{
    animation: move 0.5s linear reverse;
  }

  @keyframes move {
    from{
      transform: translateX(-100%);
    }
    to{
      transform: translateX(0px);
    }
  }
</style>
```


案例-多个元素过渡

```html
<!--
User:Shier
CreateTime:21:13
-->
<template>
  <div>
    <button @click="isShow = !isShow">切换</button>
    <transition-group name="demo" appear>
      <h1 v-show="!isShow" key="1">1来了</h1>
      <h1 v-show="isShow" key="2">2来了</h1>
    </transition-group>
  </div>
</template>

<script>
  export default {
    name: 'Test2',
    data() {
      return {
        isShow: true
      }
    },
  }
</script>

<style scoped>
  h1 {
    background-color: orange;
  }

  /* 进入的起点、离开的终点 */
  .demo-enter, .demo-leave-to {
    transform: translateX(-100%);
  }

  /* 整个进入过程、整个离开过程 */
  .demo-enter-active, .demo-leave-active {
    transition: 0.5s linear;
  }

  /* 进入的终点、离开的起点 */
  .demo-enter-to, .demo-leave {
    transform: translateX(0);
  }
</style>
```

### 4.13.1 第三库样式

库的名称：Animate.css
安装：`npm i animate.css`
引入：`import 'animate.css'`

```html
<template>
	<div>
		<button @click="isShow = !isShow">显示/隐藏</button>
		<transition-group 
			appear
			name="animate__animated animate__bounce" 
			enter-active-class="animate__swing"
			leave-active-class="animate__backOutUp"
		>
			<h1 v-show="!isShow" key="1">你好啊！</h1>
			<h1 v-show="isShow" key="2">尚硅谷！</h1>
		</transition-group>
	</div>
</template>

<script>
	import 'animate.css'
	export default {
		name:'Test',
		data() {
			return {
				isShow:true
			}
		},
	}
</script>

<style scoped>
	h1{
		background-color: orange;
	}
</style>
```



## 4.14 Vue脚手架配置代理

Vue的配置代理主要用于解决跨域的问题

跨域的问题

1. 主机名不一致
2. 协议名不一致
3. 端口号不一致

图解示意：

![image-20230117223929828](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230117223929828.png)

> ajax 是前端技术，你得有浏览器，才有window对象，才有xhr，才能发ajax请求，服务器之间通信就用传统的http请求就行了。



### 方法一：单个代理

vue.config.js中添加如下配置：

```js
devServer:{
  proxy:"http://localhost:5000"
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）

### 方法二：多个代理

vue.config.js配置具体代理规则：

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}//代理服务器将请求地址转给真实服务器时会将 /api1 去掉
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
2. 缺点：配置略微繁琐，请求资源时必须加前缀。



## 4.15 slot插槽

1. 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 <strong style="color:red">父组件 ===> 子组件</strong> 。
2. 分类：默认插槽、具名插槽、作用域插槽

默认插槽：

```html
父组件中：
        <Category>
           <div>html结构1</div>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot>插槽默认内容...</slot>
            </div>
        </template>
```

案例代码

`App.vue`

```vue
<template>
  <div class="container">
    <Category title="美食">
      <img src="https://s3.ax1x.com/2021/01/16/srJlq0.jpg" alt="">
    </Category>

    <Category title="游戏">
      <ul>
        <li v-for="(g,index) in games" :key="index">{{ g }}</li>
      </ul>
    </Category>

    <Category title="电影">
      <video controls src="http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4"></video>
    </Category>
  </div>
</template>

<script>
  import Category from './components/Category'

  export default {
    name: 'App',
    components: {Category},
    data() {
      return {
        games: ['植物大战僵尸', '红色警戒', '空洞骑士', '王国']
      }
    },
  }
</script>

<style scoped>
  .container {
    display: flex;
    justify-content: space-around;
  }
</style>
```

`Category.vue`

```vue
<template>
 <div class="category">
  <h3>{{title}}分类</h3>
  <!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
  <slot>我是一些默认值，当使用者没有传递具体结构时，我会出现</slot>
 </div>
</template>

<script>
 export default {
  name:'Category',
  props:['title']
 }
</script>

<style scoped>
 .category{
  background-color: skyblue;
  width: 200px;
  height: 300px;
 }
 h3{
  text-align: center;
  background-color: orange;
 }
 video{
  width: 100%;
 }
 img{
  width: 100%;
 }
</style>
```



具名插槽：

```html
父组件中：
        <Category>
            <template slot="center">
              <div>html结构1</div>
            </template>

            <template v-slot:footer>
               <div>html结构2</div>
            </template>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot name="center">插槽默认内容...</slot>
               <slot name="footer">插槽默认内容...</slot>
            </div>
        </template>
```



作用域插槽：

1. 理解：<span style="color:red">数据在组件的自身（子组件），但根据数据生成的结构需要组件的使用者（父组件）来决定。</span>（games数据在Category（子）组件中，但使用数据所遍历出来的结构由App（父）组件决定）

2. 具体编码：

   ```html
   父组件中：
   		<Category>
   			<template scope="scopeData">
   				<!-- 生成的是ul列表 -->
   				<ul>
   					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
   				</ul>
   			</template>
   		</Category>
   
   		<Category>
   			<template slot-scope="scopeData">
   				<!-- 生成的是h4标题 -->
   				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
   			</template>
   		</Category>
   子组件中：
           <template>
               <div>
               <!-- 通过数据绑定就可以把子组件的数据传到父组件 -->
                   <slot :games="games"></slot>
               </div>
           </template>
   		
           <script>
               export default {
                   name:'Category',
                   props:['title'],
                   //数据在子组件自身
                   data() {
                       return {
                           games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                       }
                   },
               }
           </script>
   ```

案例实现：

`App.vue`

~~~vue
<template>
	<div class="container">
		<Category title="游戏" >
			<template scope="jojo">
				<ul>
					<li v-for="(g,index) in jojo.games" :key="index">{{g}}</li>
				</ul>
			</template>
		</Category>

		<Category title="游戏" >
			<template scope="jojo">
				<ol>
					<li v-for="(g,index) in jojo.games" :key="index">{{g}}</li>
				</ol>
			</template>
		</Category>

		<Category title="游戏" >
			<template scope="jojo">
				<h4 v-for="(g,index) in jojo.games" :key="index">{{g}}</h4>
			</template>
		</Category>
	</div>
</template>

<script>
	import Category from './components/Category'
	export default {
		name:'App',
		components:{Category}
	}
</script>

<style>
	.container,.foot{
		display: flex;
		justify-content: space-around;
	}
	h4{
		text-align: center;
	}
</style>
~~~

`Category.vue`

~~~vue
<template>
	<div class="category">
		<h3>{{title}}分类</h3>
		<!-- 定义一个插槽（挖个坑，等着组件的使用者进行填充） -->
		<slot :games="games">我是一些默认值，当使用者没有传递具体结构时，我会出现1</slot>
	</div>
</template>

<script>
	export default {
		name:'Category',
		props:['title'],
        data() {
			return {
				games:['植物大战僵尸','红色警戒','空洞骑士','王国']
			}
		},
	}
</script>

<style scoped>
	.category{
		background-color: skyblue;
		width: 200px;
		height: 300px;
	}
	h3{
		text-align: center;
		background-color: orange;
	}
	video{
		width: 100%;
	}
	img{
		width: 100%;
	}
</style>
~~~



# 5、Vuex

## 5.1 概念

> 在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。
>
> 1. 集中式说明：老师讲课，只讲了一次，但全班人都有不同的理解方式
> 2. 分布式说明：类似一对一辅导教学，内容重复
>
> 

## 5.2 何时使用

1. 多个组件依赖于同一状态
2. 来自不同组件的行为需要该变为同一行为（共享）

> 多个组件需要共享数据时-全局事件总线实现
>
> 红色线：读取数据A中的值
>
> 绿色线：修改A中的属性值

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230118150116529.png" alt="image-20230118150116529" style="zoom:80%;" />

> 多个组件需要共享数据时-vuex实现

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230118150135411.png" alt="image-20230118150135411" style="zoom:80%;" />

## 5.3 Vuex原理图

![image-20230118152109412](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230118152109412.png)

> 以下的存在Store中
>
> - Actions：行为
> - Mutations：修改state
> - State：状态==数据，对象



### 5.2.1  搭建vuex环境

安装vuex中，因为是在vue2的项目中，只能使用Vuex3的版本

~~~
npm i vuex@3
~~~

1. 创建文件：```src/store/index.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //应用Vuex插件
   Vue.use(Vuex)
   
   //准备actions对象——响应组件中用户的动作
   const actions = {}
   //准备mutations对象——修改state中的数据
   const mutations = {}
   //准备state对象——保存具体的数据
   const state = {}
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state
   })
   
   // import是首先执行（会全部置顶到最前方）的，才会去执行其他代码 
   ```

2. 在```main.js```中创建vm时传入```store```配置项

   ```js
   ......
   //引入store
   import store from './store'
   ......
   
   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

###    5.2.1 基本使用

1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)
   
   const actions = {
       //响应组件中加的动作
   	jia(context,value){
   		// console.log('actions中的jia被调用了',miniStore,value)
   		context.commit('JIA',value)
   	},
   }
   
   const mutations = {
       //执行加
   	JIA(state,value){
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }
   
   //初始化数据
   const state = {
      sum:0
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取vuex中的数据：```$store.state.sum```

3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)```或 ```$store.commit('mutations中的方法名',数据)```

   >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```



具体案例：

`./store/index.js`

```js
/**
 * Author:Shier
 * createTime:15:51
 */

//引入Vue核心库
import Vue from 'vue'

//引入Vuex
import Vuex from 'vuex'

//应用Vuex插件,Vuex需要使用在Store之前
Vue.use(Vuex)

//准备actions对象——响应组件中用户的动作
const actions = {
  //  响应组件中奇数加的动作
  odd(context, value) {
    console.log('actions中的add被调用了')
    if (context.state.sum % 2) {
      context.commit('ADD', value)
    }
  },
  //  响应组件中等一会加的动作
  jiaWait(context, value) {
    console.log('actions中的jiaWait被调用了')
    setTimeout(() => {
      context.commit('ADD', value)
    }, 300)
  }

}
//准备mutations对象——修改state中的数据
const mutations = {
  // 加法函数
  ADD(state, value) {
    console.log('mutations中的ADD被调用了')
    state.sum += value
  },
  // 减法函数
  JIAN(state, value) {
    console.log('mutations中的JIAN被调用了')
    state.sum -= value
  }
}
//准备state对象——保存具体的数据
const state = {
  sum: 0 //当前的和
}

//创建并暴露store
export default new Vuex.Store({
  actions,
  mutations,
  state
})
```

`Count.vue`

```html
<template>
  <div>
    <h1>当前求和为：{{$store.state.sum}}</h1>
    <!--双向绑定-->
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementOdd">当前求和为奇数再加</button>
    <button @click="incrementWait">等一等再加</button>
  </div>
</template>

<script>
  export default {
    name:'Count',
    data() {
      return {
        n:1, //用户选择的数字
      }
    },
    methods: {
      // 加
      increment(){
        this.$store.commit('ADD',this.n)
      },
      // 减
      decrement(){
        this.$store.commit('JIAN',this.n)
      },
      // 奇数
      incrementOdd(){
        this.$store.dispatch('odd',this.n)
      },
      // 等一等再加
      incrementWait(){
        this.$store.dispatch('jiaWait',this.n)
      },
    },
  }
</script>

<style>
  button{
    margin-left: 5px;
  }
</style>
```

## 5.4 getters的使用

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。

2. 在```store.js```中追加```getters```配置

   ```js
   const getters = {
   	bigSum(state){
   		return state.sum * 10
   	}
   }
   
   // 创建并暴露store
   export default new Vuex.Store({
   	getters
   })
   ```
   
3. 组件中读取数据：```$store.getters.bigSum```



## 5.5 四个map方法的使用

导入map方法

```js
import {mapState, mapGetters, mapActions, mapMutations} from 'vuex'
```

1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性

   ```js
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}),
            
       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

   ```js
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),
   
       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

3. <strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：incrementOdd、incrementWait（对象形式）
       ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   
       //靠mapActions生成：incrementOdd、incrementWait（数组形式）
       ...mapActions(['jiaOdd','jiaWait'])
   }
   ```

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则传的参数是事件对象(event)。

优化计数案例：

`Count.vue`

```html
<template>
  <div>
    <h1>当前求和为：{{ sum }}</h1>
    <h3>当前求和放大10倍为：{{ bigSum }}</h3>
    <h3>年龄：{{ age }}</h3>
    <h3>姓名：{{ name }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <!-- 用了mapActions 和 mapMutations 的话要主动传参 -->
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>

<script>
  import {mapState, mapGetters, mapActions, mapMutations} from 'vuex'

  export default {
    name: "Count",
    data() {
      return {
        n: 1, //用户选择的数字
      };
    },
    computed: {
      ...mapState(['sum', 'age', 'name']),
      ...mapGetters(['bigSum'])
    },
    methods: {
      ...mapActions({incrementOdd: 'odd', incrementWait: 'jiaWait'}),
      ...mapMutations({increment: 'ADD', decrement: 'JIAN'})
    },
    mounted() {
      console.log("Count", this);
    },
  };
</script>

<style lang="css">
  button {
    margin-left: 5px;
  }
</style>
```

`index.js`

```js
/**
 * Author:Shier
 * createTime:15:51
 */

//引入Vue核心库
import Vue from 'vue'

//引入Vuex
import Vuex from 'vuex'

//应用Vuex插件,Vuex需要使用在Store之前
Vue.use(Vuex)

//准备actions对象——响应组件中用户的动作
const actions = {
  //  响应组件中奇数加的动作
  odd(context, value) {
    console.log('actions中的add被调用了')
    if (context.state.sum % 2) {
      context.commit('ADD', value)
    }
  },
  //  响应组件中等一会加的动作
  jiaWait(context, value) {
    console.log('actions中的jiaWait被调用了')
    setTimeout(() => {
      context.commit('ADD', value)
    }, 300)
  }

}
//准备mutations对象——修改state中的数据
const mutations = {
  // 加法函数
  ADD(state, value) {
    console.log('mutations中的ADD被调用了')
    state.sum += value
  },
  // 减法函数
  JIAN(state, value) {
    console.log('mutations中的JIAN被调用了')
    state.sum -= value
  }
}
//准备state对象——保存具体的数据
const state = {
  sum: 0, //当前的和
  name:'Shier',
  school:'BBGU',
  age:'18'
}

const getters = {
  bigSum(state){
    return state.sum * 10
  }
}

//创建并暴露store
export default new Vuex.Store({
  actions,
  mutations,
  state,
  getters
})
```



## 5.6 模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改`store.js` 

   ```javascript
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{},
     mutations: {},
     actions: {},
     getters: {}
   
   const personAbout = {
     namespaced:true,//开启命名空间
     state:{},
     mutations: {},
     actions: {}
   }
   
   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ```

3. 开启命名空间后，组件中读取state数据：

   ```js
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   // 用 mapState 取 countAbout 中的state 必须加上 'countAbout'
   ...mapState('countAbout',['sum','school','subject']),
   ```

4. 开启命名空间后，组件中读取getters数据：

   ```js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

5. 开启命名空间后，组件中调用dispatch

   ```js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

6. 开启命名空间后，组件中调用commit

   ```js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```

案例演示：
`count.js`

```js
/**
 * Author:Shier
 * createTime:22:14
 */

// 计数相关模块
export default  {
  namespaced:true, // 开启命名空间
  actions:{
    //  响应组件中奇数加的动作
    odd(context, value) {
      console.log('actions中的add被调用了')
      if (context.state.sum % 2) {
        context.commit('ADD', value)
      }
    },
    //  响应组件中等一会加的动作
    jiaWait(context, value) {
      console.log('actions中的jiaWait被调用了')
      setTimeout(() => {
        context.commit('ADD', value)
      }, 300)
    }
  },
  state:{
    sum: 0, //当前的和
    name:'Shier',
    school:'BBGU',
    age:'18',
  },
  mutations:{
    // 加法函数
    ADD(state, value) {
      console.log('mutations中的ADD被调用了')
      state.sum += value
    },
    // 减法函数
    JIAN(state, value) {
      console.log('mutations中的JIAN被调用了')
      state.sum -= value
    },
    ADD_PERSON(state,value){
      console.log('mutations中的ADD_PERSON被调用了')
      state.personList.unshift(value)
    }
  },
  getters:{
    bigSum(state){
      return state.sum * 10
    }
  }
}
```

`person.js`

```js
/**
 * Author:Shier
 * createTime:22:15
 */
import axios from 'axios'
import {nanoid} from "nanoid";

// 人员相关模块
export default {
  namespaced: true, // 开启命名空间
  actions: {
    addPersonKong(context, value) {
      if (value.name.indexOf('孔') === 0) {
        context.commit('ADD_PERSON', value)
      } else {
        alert('此人应姓孔！')
      }
    },
    // person服务
    addPersonServer(context) {
      axios.get('https://api.uixsj.cn/hitokoto/get?type=social').then(
          response => {
            context.commit('ADD_PERSON', {id: nanoid(), name: response.data})
          },
          error => {
            alert(error.message)
          }
      )
    },
  },
  state: {
    personList: [
      {id: '001', name: 'Shier1'}
    ]
  },
  mutations: {
    ADD_PERSON(state, value) {
      console.log('mutations中的ADD_PERSON被调用了')
      state.personList.unshift(value)
    }
  },
  getters: {
    firstName(state) {
      return state.personList[0].name
    }
  }
}
```

`index.js`

```js
/**
 * Author:Shier
 * createTime:15:51
 */

//引入Vue核心库
import Vue from 'vue'

//引入Vuex
import Vuex from 'vuex'

//应用Vuex插件,Vuex需要使用在Store之前
Vue.use(Vuex)
import countOptions from './count'
import personOptions from './person'

//创建并暴露store
export default new Vuex.Store({
  modules:{
    countOptions,
    personOptions
  }
})
```

`Count.vue`

```html
<template>
  <div>
    <h1>当前求和为：{{ sum }}</h1>
    <h3>当前求和放大10倍为：{{ bigSum }}</h3>
    <h3>年龄：{{ age }}</h3>
    <h3>姓名：{{ name }}</h3>
    <select v-model.number="n">
      <option value="1">1</option>
      <option value="2">2</option>
      <option value="3">3</option>
    </select>
    <!-- 用了mapActions 和 mapMutations 的话要主动传参 -->
    <button @click="increment(n)">+</button>
    <button @click="decrement(n)">-</button>
    <button @click="incrementOdd(n)">当前求和为奇数再加</button>
    <button @click="incrementWait(n)">等一等再加</button>
  </div>
</template>

<script>
  import {mapState, mapGetters, mapActions, mapMutations} from 'vuex'
  export default {
    name: "Count",
    data() {
      return {
        n: 1, //用户选择的数字
      };
    },
    computed: {
      // 第一个参数为模块名
      ...mapState('countOptions',['sum', 'age', 'name']),
      ...mapGetters('countOptions',['bigSum'])
    },
    methods: {
      ...mapActions('countOptions',{incrementOdd: 'odd', incrementWait: 'jiaWait'}),
      ...mapMutations('countOptions',{increment: 'ADD', decrement: 'JIAN'})
    },
    mounted() {
      console.log(this.$store);
    },
  };
</script>

<style lang="css">
  button {
    margin-left: 5px;
  }
</style>
```

`Person.vue`

```html
<template>
  <div>
    <h1>人员列表</h1>
    <h3 style="color:red">Count组件求和为：{{ sum }}</h3>
    <input type="text" placeholder="请输入名字" v-model="name">
    <button @click="add">添加</button>
    <button @click="addKong">添加孔氏族人</button>
    <button @click="addPersonServer">添加随机人</button>
    <ul>
      <li v-for="p in personList" :key="p.id">{{ p.name }}</li>
    </ul>
  </div>
</template>

<script>
  import {nanoid} from 'nanoid'

  export default {
    name: 'Person',
    data() {
      return {
        name: ''
      }
    },
    computed: {
      personList() {
        return this.$store.state.personOptions.personList
      },
      sum() {
        return this.$store.state.countOptions.sum
      }
    },
    methods: {
      add() {
        // person对象 id name
        const personObj = {id: nanoid(), name: this.name}
        this.$store.commit('personOptions/ADD_PERSON', personObj)
        this.name = ''
      },
      addKong() {
        const personObj = {id: nanoid(), name: this.name}
        this.$store.dispatch('personOptions/addPersonKong', personObj)
        this.name = ''
      },
      addPersonServer(){
        this.$store.dispatch('personOptions/addPersonServer')
      }
    }
  }
</script>
```

`App.vue`

```vue
<template>
  <div>
    <Count/>
    <hr style="border-bottom: 2px solid blue">
    <Person/>
  </div>
</template>

<script>
  import Count from "./components/Count";
  import Person from "./components/Person";

  export default {
    name: 'App',
    components: {Count,Person},
    mounted() {
      console.log(this)
    }
  }
</script>
```



# 6、路由

## 6.1 路由概念

1.  一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. vue-router 插件库，用来实现SPA（single page web application）应用。
3. 整个应用只在一个页面呈现，不会出现多个页面跳转，只会局部页面更新
4. 前端路由：key是路径，value是组件。

### 6.1.1 路由分类

1. 后端路由：

   - 理解：value 是 function，用于处理客户端提交的请求

   - 工作过程：服务器接收到一个请求时，根据请求路径找到匹配的函数来处理请求，返回响应数据

2. 前端路由：

   - 理解：value 是 component，用于展示页面内容

   - 工作过程：当浏览器的路径改变时，对应的组件就会显示



## 6.2 路由基本使用

1. 安装vue-router，命令：`npm i vue-router`

2. 应用插件：`Vue.use(VueRouter)`

3. 编写router配置项：

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
   	routes:[
   		{
   			path:'/about',
   			component:About
   		},
   		{
   			path:'/home',
   			component:Home
   		}
   	]
   })
   
   //暴露router
   export default router
   ```

4. 实现切换（active-class可配置高亮样式）

   ```html
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```html
   <router-view></router-view>
   ```



案例实现

`router/index.js`

```js
/**
 * Author:Shier
 * createTime:13:59
 */

//该文件专门用于创建整个应用的路由器
import VueRouter from "vue-router";
//引入组件
import Home from '../components/Home'
import About from '../components/About'

//创建并暴露一个路由器
export default new VueRouter({
  routes:[
    {
      path:'/about',
      component:About
    },
    {
      path:'/home',
      component:Home
    }
  ]
})
```

`main.js`

```js
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'
import router from './router'

Vue.config.productionTip = false
Vue.use(VueRouter)

new Vue({
    el:"#app",
    render: h => h(App),
    router
})
```

`App.js`

```vue
<!--
User:Shier
CreateTime:14:00
-->
<template>
  <div>
    <div class="row">
      <div class="col-xs-offset-2 col-xs-8">
        <div class="page-header"><h2>Vue Router Demo</h2></div>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-2 col-xs-offset-2">
        <div class="list-group">
          <!-- 原始html中我们使用a标签实现页面跳转 -->
          <!-- <a class="list-group-item active" href="./about.html">About</a>
          <a class="list-group-item" href="./home.html">Home</a> -->

          <!-- Vue中借助router-link标签实现路由的切换 -->
          <router-link class="list-group-item" active-class="active" to="/about">About
          </router-link><br>
          <router-link class="list-group-item" active-class="active" to="/home">Home
          </router-link>
        </div>
      </div>
      <div class="col-xs-6">
        <div class="panel">
          <div class="panel-body">
            <!-- 指定组件的呈现位置 -->
            <router-view></router-view>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'App',
  }
</script>
```

`About.vue`

```vue
<!--
User:Shier
CreateTime:14:01
-->
<template>
  <h2>我是About组件的内容</h2>
</template>

<script>
  export default {
    name:'About'
  }
</script>
```

`Home.vue`

```vue
<!--
User:Shier
CreateTime:14:01
-->
<template>
  <h2>我是Home组件的内容</h2>
</template>

<script>
  export default {
    name:'Home'
  }
</script>
```



## 6.3 Vue路由注意项

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在`components`文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。



## 6.4 多级路由

1. 配置路由规则，使用children配置项

   ```js
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径，把前面级别的路径写上）：

   ```html
   <router-link to="/home/news">News</router-link>
   ```

3. 指定展示位置

   ```html
   <router-view></router-view>
   ```




## 6.5 路由的query参数

1. 传递参数

   ```html
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">{{m.title}}</router-link>
   
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link 
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		   id:666,
          title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```html
   <template>
     <ul>
       <li>消息编号：{{$route.query.id}}</li>
       <li>消息标题：{{$route.query.title}}</li>
     </ul>
   </template>
   ```

## 6.6 命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```html
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>
      
      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>
      
      <!--简化写法配合传递参数 -->
      <router-link 
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
             title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```

## 6.7 路由的params参数

1. 配置路由，声明接收params参数

   ```js
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```html
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   特别注意：==路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！==

3. 接收参数：

   ```js
   $route.params.id
   $route.params.title
   ```

## 6.8 路由的props配置

作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数以props形式传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props($route) {
		return {
		  id: $route.query.id,
		  title:$route.query.title,
		  a: 1,
		  b: 2
		}
	}
}
```

> 方便在要接收数据的组件里更简便的写法


接收数据的组件：

```html
<template>
  <ul>
      <h1>Detail</h1>
      <li>消息编号：{{id}}</li>
      <li>消息标题：{{title}}</li>
      <li>a:{{a}}</li>
      <li>b:{{b}}</li>
  </ul>
</template>

<script>
export default {
    name: 'Detail',
    props: ['id', 'title', 'a', 'b'],
    mounted () {
        console.log(this.$route);
    }
}
</script>
```



## 6.9 router-link的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式

2. 浏览器的历史记录有两种写入方式：分别为```push```和```replace```，```push```是追加历史记录，```replace```是替换当前记录。路由跳转时候默认为```push```

3. 开启`replace` 

   在`router-link` 中添加 replace 属性

   模式：`<router-link replace .......>News</router-link>`



## 6.10 编程式路由导航

1. 作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
   this.$router.push({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   
   this.$router.replace({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //正数：前进，负数：后退
   ```



## 6.11 缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码： ==include 指的是组件名==

   ```html
   <!--缓存单个组件-->
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   
   <!--缓存多个组件：使用数组形式-->
   <keep-alive :include="['News','Message']"> 
       <router-view></router-view>
   </keep-alive>
   ```



## 6.12 两个新的生命周期钩子

作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
具体名字：

*  ```activated```路由组件被激活时触发。
*  ```deactivated```路由组件失活时触发。

> 这两个生命周期钩子需要配合前面的缓存路由组件使用（没有缓存路由组件不起效果）



## 6.13 路由守卫

1. 作用：对路由进行权限控制
2. 分类：全局守卫、独享守卫、组件内守卫

### 6.13.1 全局守卫:

1. 全局前置守卫
2. 全局后置守卫

```js
//全局前置守卫：初始化时执行、每次路由切换前执行
router.beforeEach((to,from,next)=>{
	console.log('beforeEach',to,from)
	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'zhejiang'){ //权限控制的具体规则
			next() //放行
		}else{
			alert('暂无权限查看')
			// next({name:'guanyu'})
		}
	}else{
		next() //放行
	}
})

//全局后置守卫：初始化时执行、每次路由切换后执行
router.afterEach((to,from)=>{
	console.log('afterEach',to,from)
	if(to.meta.title){ 
		document.title = to.meta.title //修改网页的title
	}else{
		document.title = 'vue_test'
	}
})
```

完整实现代码：

```js
// 这个文件专门用于创建整个应用的路由器
import VueRouter from 'vue-router'
// 引入组件
import About from '../page/About.vue'
import Home from '../page/Home.vue'
import Message from '../page/Message.vue'
import News from '../page/News.vue'
import Detail from '../page/Detail.vue'
// 创建并暴露一个路由器
const router = new VueRouter({
  routes: [
    {
      path: '/home',
      component: Home,
      meta: {title: '主页'},
      children: [
        {
          path: 'news',
          component: News,
          meta: {isAuth: true, title: '新闻'}
        },
        {
          path: 'message',
          name: 'mess',
          component: Message,
          meta: {isAuth: true, title: '消息'},
          children: [
            {
              path: 'detail/:id/:title',
              name: 'xiangqing',
              component: Detail,
              meta: {isAuth: true, title: '详情'},
              props($route) {
                return {
                  id: $route.query.id,
                  title: $route.query.title,
                  a: 1,
                  b: 'hello'
                }
              }
            }
          ]
        }
      ]
    },
    {
      path: '/about',
      component: About,
      meta: {title: '关于'}
    }
  ]
})

// 全局前置路由守卫————初始化的时候被调用、每次路由切换之前被调用
router.beforeEach((to, from, next) => {
  console.log('前置路由守卫', to, from);
  if (to.meta.isAuth) {
    if (localStorage.getItem('school') === 'bbgu') {
      // 放行
      next()
    } else {
      alert('学校名不对，无权查看')
    }
  } else {
    next()
  }
})

// 全局后置路由守卫————初始化的时候被调用、每次路由切换之后被调用
router.afterEach((to, from) => {
  console.log('后置路由守卫', to, from)
  document.title = to.meta.title || '路由系统'
})

export default router
```

### 6.13.2 独享守卫:

在 route子路由内写守卫

- 只有前置守卫，没有后置守卫

```js
beforeEnter(to,from,next){
	console.log('beforeEnter',to,from)
	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
		if(localStorage.getItem('school') === 'atguigu'){
			next()
		}else{
			alert('暂无权限查看')
			// next({name:'guanyu'})
		}
	}else{
		next()
	}
}
```



### 6.13.3 组件内守卫：

在具体组件内写守卫

```js
//进入守卫：通过路由规则，进入该组件时被调用
beforeRouteEnter (to, from, next) {
  next()
}, 
//离开守卫：通过路由规则，离开该组件时被调用
beforeRouteLeave (to, from, next) {
  next() // 放行
}
```





## 6.14 路由器的两种工作模式

1. 对于一个url来说，什么是hash值？—— ==#及其后面的内容==就是hash值。

2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。

3. hash模式：

   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。

4. history模式：

   1. 地址干净，美观 。
   2. 兼容性和hash模式相比略差。
   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

    ![image-20230120132556970](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230120132556970.png)



# 7、Vue UI组件库



## 7.1 移动端UI组件库

1. [Vant](https://youzan.github.io/vant)
2. [Cube UI](https://didi.github.io/cube-ui)
3. [Mint UI](http://mint-ui.github.io/)

## 7.2 PC端UI组件库

1. [Element UI](https://element.eleme.cn/)
2. [IView UI](https://www.iviewui.com/)



























