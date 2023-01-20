

# 一、关于DOM

## 1、复制到剪切板

>在Web应用程序中，复制到剪贴板因其对用户的便利性而迅速流行起来。
>
>```js
>const copyToClipboard = (text) =>
>navigator.clipboard?.writeText && navigator.clipboard.writeText（text）。
>// 测试
>copyToClipboard("复制的内容!")
>```
>
>注意：必须检查用户的浏览器是否支持该API .为了支持所有用户，你可以使用一个输入并复制其内容

## 2、检测黑暗模式

>随着黑暗模式的普及，如果用户在他们的设备中启用了黑暗模式，那么将你的应用程序切换到黑暗模式是非常理想的。幸运的是，可以利用媒体查询来使这项任务变得简单。
>
>```js
>const isDarkMode = () =>
>window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches。
>// 测试
>console.log(isDarkMode())
>```

## 3、滚动到顶部

>初学者经常发现自己在正确滚动元素的过程中遇到困难。最简单的滚动元素的方法是使用scrollIntoView方法。添加行为。"smooth "来实现平滑的滚动动画。
>
>```js
>const scrollToTop = (element) => element.scrollIntoView({ behavior: "smooth", block: "start" })
>```

## 4、滚动到底部

>就像scrollToTop方法一样，scrollToBottom方法也可以用scrollIntoView方法轻松实现，只需将块值切换为结束即可
>
>```js
>const scrollToBottom = (element) =>  element.scrollIntoView({ behavior: "smooth", block: "end" })
>```

## 5、生成随机颜色

>```js
>const generateRandomHexColor = () => `#${Math.floor(Math.random() * 0xffffff) .toString(16)}`;
>```

# 二、数组操作

## 1、数组乱序

>在使用需要某种程度的随机化的算法时，你会经常发现洗牌数组是一个相当必要的技能。下面的片段以O(n log n)的复杂度对一个数组进行就地洗牌。
>
>```js
>const shuffleArray = (arr) => arr.sort(() => Math.random() - 0.5) 。
>// 测试
>const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
>console.log(shuffleArray(arr))
>```

## 2、数组去重

>利用ES6的set结构的唯一性特性，可以很快的实现数组去重
>
>```js
>const getUnique = (arr) => [...new Set(arr)]。
>// 测试
>const arr = [1, 1, 2, 3, 3, 4, 4, 5, 5];
>console.log(getUnique(arr))
>```





# 三、new关键字原理

>new 运算符创建一个用户定义的对象类型的实例 或者 具有构造函数的内置对象的实例
>
>1. 创建一个空的对象作为将要返回的对象实例
>2. 构造函数的prototype属性对象 指向 这个空的对象(原型对象)
>3. 将这个实例对象的值 赋值给 函数内部的this关键字
>4. 执行构造函数内的代码
>5. 如果该函数没有返回对象,则返回this

### JS继承

#### Ⅰ - 继承是什么?

>继承是面向对象软件技术中的一个概念:
>
>>如果一个类别B 继承自 另一个类别A ,那么就把这个B称为 'A的子类'; 而把A成为B的父类或者超类
>
>###### 继承的优点:
>
>>* 继承可以使得子类具有父类别的各种属性和方法,而不需要再次编写相同的代码
>>* 子类继承父类的同时,也能重新定义某些属性或者重写某些方法,即覆盖父类的原有属性与方法,使其获得与父类不同的功能
>
>常用的几个继承实现方式
>
>>1. ###### 组合继承
>
>>   - 原型链继承: `Child.prototype = new Panent()`  -->修改一个实例,另外一个实例也会变化
>>   - 构造函数继承: `Panent.call(this) `  -->只能继承父类属性与方法,而不能继承父类的原型上的
>>   - 组合继承: 结合上面两个写法,同时需要手动挂上构造器(Child),指向自己的构造函数 `Child.prototype.constructor = Child`
>
>>2. ###### 寄生组合式继承
>
>>   - 原型继承 : 利用解决普通对象继承问题的 `Object.create()`方法进行实现
>>   - 寄生式继承: 优化上面原型继承的写法,实际上也不好
>>   - 寄生组合式继承:在前面所有继承方式的基础上进行优化,**是最优解决方案**

#### Ⅱ - 组合继承

##### ① 原型链实现继承 (`bad`)

>原型链继承是比较常见的继承方式之一, 其中涉及的构造函数、原型和实例,三者之间存在着一定关系,即前方提到的:1. 每个构造函数都有一个原型对象,原型对象又包含一个指向构造函数的指针,而实例则包含一个原型对象的指针
>
>###### 举个栗子
>
>```js
>//父类原型对象
>function Parent() {
>this.name = 'parent1';
>this.play = [1, 2, 3]
>}
>//构造函数
>function Child() {
>this.type = 'child';
>}
>//将Child 的原型指向 Parent 的实例
>Child.prototype = new Parent();
>console.log(new Child())
>//实例化两个对象
>let s1 = new Child();
>let s2 = new Child();
>console.log(s1.play,s2.play) //[1, 2, 3]    [1, 2, 3]
>
>//修改其中一个的原型
>s1.play.push(4)
>console.log(s1.play,s2.play) //[1, 2, 3, 4]   [1, 2, 3, 4]
>```
>
>我们发现:当我们改变S1的属性时,另外一个实例也发生了改变,这是因为这两个实例使用的是同一个原型对象,**他们的内存空间是共享的**

##### ② 构造函数继承(`bad`)

>借助 `call` 调用`Parent` 函数
>
>```js
>function Parent(){
>this.name='努力学习的汪'
>}
>Parent.prototype.getName=function(){return this.name}
>
>//定义构造函数
>function Child(){
>Parent.call(this);
>this.type='child'
>}
>
>let child= new Child()
>let child1=new Child()
>
>console.log(child,child1)
>//Child {name: '努力学习的汪', type: 'child'} Child {name: '努力学习的汪', type: 'child'}
>
>child.name='hong'
>//Child {name: 'hong', type: 'child'} Child {name: '努力学习的汪', type: 'child'}
>child.getName() //报错
>```
>
>可以看到,父类原型对象中一旦存在父类之前自己已经定义的方法,那么子类将无法继承这些方法
>
>* 相比第一种原型链继承方式,父类的引用属性不会被共享,但他优化了第一种继承方式的弊端
>* 只能继承父类的实例属性和方法,不能继承其原型属性或方法

##### **组合继承**

>前面我们讲到两种继承方式,各有优缺点.组合继承则是将这两种方式结合起来:  **原型链继承+构造函数继承**
>
>* 利用原型链实现对父类对象的方法继承
>* 利用`super()`(实际上你只要写了constructor,那么默认就会给你调用一次super())接用父类构造函数初始化相同属性
>
>```js
>function Parent() {
>  this.name = '努力学习的汪';
>  this.play = [1,2,3]; 
>}
>Parent.prototype.getName = function(){return this.name}
>function Child(){
>  //实际上这里运行后是第二次调用Parent
>	Parent.call(this);
>  this.type = 'child' 
>}
>//第一次调用Parent()
>Child.prototype = new Parent();
>//手动挂上构造器(Child),指向自己的构造函数
>Child.prototype.constructor = Child;
>//实例化两个对象
>let s1 = new Child();
>let s2 = new Child();
>console.log(s1.play,s2.play) //[1, 2, 3]    [1, 2, 3]
>
>//修改其中一个的原型
>s1.play.push(4)
>console.log(s1.play,s2.play) ///[1, 2, 3, 4]    [1, 2, 3]  -->互不影响
>console.log(s1.getName(),s2.getName()) //正常调用
>```
>
>这种方式看起来没什么问题,但实际上 `Parent` 执行了两次,造成了多构造一次的性能开销

#### Ⅲ - **寄生组合式继承**

##### ① 原型继承(`bad`)

>这里主要借助`Object.create`的方法实现普通对象的继承
>
>* 因为`Object.create()`方法式浅拷贝,多个实例的引用类型属性指向相同的内存,存在篡改的可能
>
>```js
>let Parent ={
>  name:'努力学习的汪',
>  arr: ['1','2','3'],
>  getName: function(){return this.name}
>}
>//Object.create()方法创建一个新对象，使用现有的对象来提供新创建的对象的 __proto__
>let child = Object.create(Parent);
>child.name = 'hong';
>child.arr.push('4');
>//声明第二个实例
>let child1 = Object.create(Parent);
>child1.name='jilin';
>child1.arr.push('5')
>
>//调用
>console.log(child.name); //hong
>console.log(child1.name === child1.getName()); //true -->方法调用正常
>console.log(child1.name); // jilin -->名字这种属性修改正常且不会互相影响
>
>console.log(child.arr);  //['1', '2', '3', '4', '5']  -->被篡改了
>console.log(child1.arr); //['1', '2', '3', '4', '5']
>```

##### ② 寄生式继承(`bad`)

>寄生式继承在上面继承基础上进行优化,利用浅拷贝的能力再次进行加强,添加一些方法,但仍然存在一样的问题
>
>```js
>const Parent = {
>name:'努力学习的汪',
>arr: ['1','2','3'],
>getName:function(){return this.name}
>}
>
>//对浅拷贝进行优化增强
>function clone(preObj){
>let clone = Object.create(preObj);
>clone.getArr = function(){return this.arr};
>return clone;
>}
>
>let child = clone(Parent);
>child.name = 'hong';
>child.arr.push('4');
>let child1 = clone(Parent);
>child1.name='jilin';
>child1.arr.push('5');
>
>//调用
>console.log(child.name); //hong
>console.log(child1.name === child1.getName()); //true -->方法调用正常
>console.log(child1.name); // jilin -->名字这种属性修改正常且不会互相影响
>
>console.log(child.getArr());  //['1', '2', '3', '4', '5']  -->被篡改了
>console.log(child1.getArr()); //['1', '2', '3', '4', '5']
>```

##### 寄生组合式继承

>寄生组合式继承,借助解决普通对象继承问题的`Object.create()`方法,结合前面全部继承方法的优缺点的基础上进行改造,这也是所有继承方式里面相对最优的继承方式
>
>* 组合继承: 缺陷是 多调用了一次构造函数,存在性能问题
>* 寄生式继承: 缺陷是 引用类型属性指向相同内存,存在篡改问题
>
>```js
>//1. 定义父类
>function Parent(){
>  this.name = '努力学习的汪';
>  this.play = [1,2,3];
>}
>//在父类原型上定义一个方法或者属性
>Parent.prototype.getName = function(){return this.name}
>
>//2. 定义子类
>function Child(){
>  //构造函数继承部分  --> 这里会使得子类获得父类本身带有的属性与方法
>  Parent.call(this);
>  this.arr = [9, 8, 7];
>}
>
>//3. 定义一个寄生式继承方法
>function clone(parent,child){
>  //这里改用 Object.create 可以减少组合继承中那多余的一次构造过程
>  child.prototype = Object.create(parent.prototype) //将父类的原型赋给子类的原型
>  //组合继承中的,需要手动挂载构造函数给自身
>  child.prototype.constructor = child; 
>}
>
>//4. 调用一下寄生式继承方法,Parent与Child关联起来,到这步为止,实现了继承
>clone(Parent,Child)
>
>//5.注意:如果要在子类原型上添加属性或者方法,需要等步骤 4 运行完,因为 clone 有覆盖原型的步骤
>Child.prototype.getArr = function(){return this.arr}
>
>//调用
>let child = new Child();
>console.log(child);  //Child {name: '努力学习的汪', play: Array(3), arr: Array(3)}
>console.log(child.getName()); //努力学习的汪
>console.log(child.getArr()); //[9, 8, 7]
>```

#### Ⅳ - ES6的  `extends` 关键字直接实现

>实际上,如果通过转换我们会发现 `extends` 实际采用的也是寄生组合式继承



# 四、JS原型、原型链、构造函数等

### 1、原型与原型链

>本人JS进阶部分有详细分析 -->[点我跳转](https://gitee.com/hongjilin/hongs-study-notes/blob/master/%E7%BC%96%E7%A8%8B_%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/HTML+CSS+JS%E5%9F%BA%E7%A1%80%E7%AC%94%E8%AE%B0/JavaScript%E7%AC%94%E8%AE%B0/A_JavaScript%E8%BF%9B%E9%98%B6%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.md#1%E5%8E%9F%E5%9E%8B%E4%B8%8E%E5%8E%9F%E5%9E%8B%E9%93%BE)
>
>###### 什么是原型呢?
>
>>你可以这么理解: 每一个JS对象(除了Null) 在创建时就会与之关联的另一个对象,这个对象就是我们所说的原型,每一个对象都会从自己的 '原型对象' 中继承属性
>
>>* 每个函数都有一个 prototype 属性,它默认指向一个 Object 空对象(即成为原型对象)
>>* Prototype 对象默认有两个属性: constructor 属性 和 `_proto_`属性
>>* prototype上的 constructor 属性包含了一个指针,指回原函数(`fun.prototype.constructor-->fun`)
>
>###### prototype属性的作用?
>
>>* 给原型对象添加属性(一般都是方法): 函数的所有 实例对象 自动拥有原型中的属性(方法)
>>* 所以说,JS的继承机制就是通过原型对象实现继承的,原型对象的作用就是定义所有实例对象共享的属性与方法
>
>###### 什么是原型链?
>
>>每个对象都可以有一个隐式原型 `_proto_`, 这个原型还可以有它自己的原型,以此类推形成一个原型链:
>
>>* 查找特定属性的时候,我们先去这个对象里面去找
>>* 如果没有的话就去它的原型对象里面去找
>>* 如果还没有就再去原型对象的原型对象里去找..........
>
>>这个操作被委托在整个原型链上,这个就是我们所说的原型链了
>
>###### 原型链结论
>
>>* `_proto_`是原型链查询中实际用到的,它总是指向显式原型 `prototype`
>>* prototype 是函数独有的,在定义构造函数时自动创建,它总是被创建的实例的 `_proto_` 所指
>>* 所有对象都有`_proto_`属性,**函数这个特殊对象** 除了具有`_proto_`属性,还有特有的原型属性`Prototype`(因为它本身也是一种对象)

------



### 2、Prototype 与 `_proto_` 区别与关系

>* 每一个函数 function 都有一个 `prototype` ,即显式原型
>
>* 每个实例对象都有一个 `_proto_` ,即隐式原型
>
>* 对象的 隐式原型(`_proto_`) 的值 为其 对应构造函数的 显示原型(`prototype`) 的值
>
>>可以这样理解 构造函数的prototype <-- 默认创建的Object(指向此地址值) --> 对象的`_proto_`
>
>* 隐式原型为对象独有的,而 显式原型(它是一个对象) 是函数独有的
>
>**总结**
>
>* 函数的 `prototype` 属性: 在定义函数时自动添加的,默认值时一个空Object对象
>* 对象的 `_proto_` 属性: 创建对象时自动添加的, 默认值为 `构造函数的 protopyte 属性值`
>* 程序员 可以直接操作 显式原型 而不能直接操作隐式原型(ES6之前)
>* prototype 属性可以给函数和对象添加可共享(继承)的方法、属性,而`_proto_`是查找某函数或对象的原型链的方法
>
>###### 图
>
>>![image-20211025145849223](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025145849223.png)

------



### 3、如何理解构造函数，原型对象和实例的关系

>* 每个构造函数都有一个原型对象(prototype)
>* 原型对象都包含一个指向构造函数的指针(prototype中有constructor)
>* 而实例都包含一个原型对象的指针(实例的`_proto_` 的值 指向 原型对象prototype 的值)
>
>![image-20211025150900591](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025150900591.png) 
>
>###### 构造函数
>
>>构造函数特点: 1. 函数体内使用this关键字,代表了所要生成的对象实例 2. 生成对象,必须使用 new关键字实例化
>
>###### instanceof 用法:可以忽略 new 用构造函数声明实例
>
>>```js
>>function Person(name) {
>>// 判断this是否指向了当前的实例
>>if (this instanceof Person) {
>>// this指向了当前的实例，外部使用了关键字new
>>this.name = name
>>}else {
>>// this指向window，外部没有使用关键字new
>>return  new Person(name)
>>}
>>}
>>var p1 = new Person("咚咚")
>>var p2 =  Person("锵锵")
>>console.log("p1",p1);
>>console.log("p2",p2);
>>```







# 五、JS命名空间（namespace）

>1. 命名空间namespace（某些语言中叫package），是一个在静态语言中常见的概念。它可以帮助我们更好地整理代码，并可避免命名冲突。
>
>2. 如果使用[`ES6的模块`](https://gitee.com/hongjilin/hongs-study-notes/tree/master/%E7%BC%96%E7%A8%8B_%E5%89%8D%E7%AB%AF%E5%BC%80%E5%8F%91%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0/ES6%E5%AD%A6%E4%B9%A0%E8%B5%84%E6%96%99%E6%91%98%E5%BD%95%E4%B8%8E%E7%AC%94%E8%AE%B0)相关知识，则大多数场景不需要名称空间。
>
>    1) 命名空间的目的是防止定义相同名称的不同文件之间发生冲突。 
>
>    2) 模块通过让callsite选择一个名称来为其提供所需的每个模块，从而完全消除了这个问题。 
>
>    3) 您只需导出一个包含所需内容的简单对象，其他文件可以将其导入到他们选择的任何名称。
>
>    4) 但是该知识在某些地方仍是有需求的,学会该知识点对于编程思维是有所提升的,不要成为`API战士啊,亲` 

## Ⅰ-常见应用场景

>1. 在多人合作写脚本的时候，会发生方法名冲突的情况
>
>2. 在现代的大规模JS开发中，不采用命名空间会造成非常糟糕的命名方式，比如用`前缀命名函数和变量`，导致代码丑陋不可读。当引入第三方库后，更可能会发生`命名覆盖`的情况 
>
>3. 为了方便大家理解,下面代码举例:
>
>  ```JS
>  <html lang="en">
>  <head>
>      <meta charset="UTF-8">
>      <title>命名空间的用法</title>
>      <script src="1.js"></script>
>      <script src="2.js"></script>
>      <script src="3.js"></script>
>  </head>
>  <body>
>
>  </body>
>  <script type="text/javascript">
>      //如此调用岂不比专门去加前缀命名更明显
>      hello();
>  	//DocHello() 如果你要解决此问题,然后不用命名空间时 是否会使用类似方法
>  	//HongHello() 
>      DOC.hello();
>      HONG.hello();
>      HONG.getName("HONG");
>  </script>
>  </html>
>
>  <---------------- 如果有三个开发者,分别写三个js文件且定义方法名相同,同时又被同一个页面引用时,我使用命名空间的方式 -------------------->
>     //1.js 
>   const hello=()=>{  console.log(1)}  
>     //2.js
>   const DOC= DOC || {};
>   OC.hello = () =>{console.log("hello DOC")}  
>     //3.js 
>   const HONG = HONG || {};
>   HONG.hello = ()=> { console.log("hello Hong")}
>   HONG.getName=name => { console.log(name)}
>
>   <----------------不使用命名空间的方式,而是使用加前缀方式 -------------------->
>    //1.js 
>   const hello=()=>{  console.log(1)}  
>     //2.js
>   const  DocHello = () =>{console.log("hello DOC")}  
>    //3.js 
>   const HongHello = ()=> { console.log("hello Hong")}
>   const HongGetName=name => { console.log(name)}
>  ```
>
>  当然,上面这种情况只是简单的场景,举一反三能力要有

## Ⅱ-使用简单对象字面量模拟命名空间

>1. 我们可以创建一个简单对象字面量来打包所有的相关函数和变量。这个简单对象字面量模拟了命名空间的作用。
>
>  ```js
>const MYNAMESPACE = {
>    person: function(name) {
>        this.name = name;
>        this.getName = () => this.name;
>    }
>};
>  ```
>
>2. person对象被完整包含到MYNAMESPACE这个命名空间中了，使用方法也很简单：
>
>  ```js
>const H = new MYNAMESPACE.person("hong");
>H.getName();    
>const JL=new MYNAMESPACE.person("jilin");
>JL.getName();   
>  ```
>
>  如此一来，通过命名空间我们就可以声明多个`person对象`了。

## Ⅲ-嵌套命名空间

>1. 我们用嵌套命名空间可以更详细的归类对象：
>
>  ```js
>const MYNAMESPACE = {
>    PEOPLE: {
>        person: function(name) {
>            this.name = name;
>            this.getName = () => this.name;
>        }
>    },
>    PET: {
>        dog: function(petName) {
>            this.petName = petName;
>            this.getPetName = () => this.petName;  
>        }
>    }
>};
>  ```
>
>2. 上面这个模拟的命名空间代码好像看起来不错的亚子. 但这里还是有一个问题:在添加这个“命名空间”的时候，我们有可能覆盖全局空间中的同名对象。因此我们需要在声明命名空间前进行检查,声明的方法也需要作改动，保证全局空间的安全：
>
>  ```js
>  const MYNAMESPACE = MYNAMESPACE || {};
>
>  MYNAMESPACE.person = name =>{  this.name = name};
>  MYNAMESPACE.person.prototype.getName = ()=> this.name;
>
>  // 使用方法
>  const p = new MYNAMESPACE.person("hong");
>  p.getName();        // hong
>  ```
>
>  若全局空间中已有同名对象，则不覆盖该对象；否则创建一个新的命名空间。
>
>3. `注意`在定义命名空间构造函数时，需要将其定义在`prototype`上，否则新建的实例无法访问对象的方法。

## Ⅳ-自执行函数 - 伪命名空间封装法

### 1、什么是自执行函数

>1. 自执行函数就是为了不污染全局变量命名空间的一中匿名函数，相当于自己创建了一个作用域，下面我来说一下它的原理：
>
>  ```js
>function foo() {...}   // 这是定义，Declaration；定义只是让解释器知道其存在，但是不会运行。
>foo();          // 这是语句，Statement；解释器遇到语句是会运行它的。
>  ```
>
>2. 上面的函数就是传统的函数，它写起来有点啰嗦，而且会污染全局命名空间，这样对我们来说并不友好，所以自执行函数就出现了，写法如下：
>
>  ```js
>(function foo("参数") {" 函数方法"})(" 给参数传的值或者不传");
>(function foo("参数") {" 函数方法"}(" 给参数传的值或者不传"));//推荐使用这种形式
>!function("参数"){" 函数方法"}(" 给参数传的值或者不传") //此处的`!`可以换做其他运算符或者void
>  ```
>
>3. `自执行函数是自私的`:它的内部可以访问全局变量。但是除了自执行函数自身内部，是无法访问它的
>
>  ```js
>const aaa=(a1,b1)=> sum1 = a1 + b1 //普通函数
>(const bbb=(a2,b2)=>{return sum2 = a2 + b2}() //自执行函数
>console.log(aaa)
>console.log(bbb) //报错,找不到该变量
>  ```
>
>4. 如何简单理解自执行函数?
>
>  自执行函数相当于一个瓶口朝下的杯子，当定义它的时候，它会倾斜，把杯口露出来，吸收外面的新鲜空气；当它执行完毕，杯口不再外露，紧闭起来，与外界再无关联。

### 2、使用自执行函数模拟命名空间

>1. 为何使用自执行函数这种方式进行封装?
>
>  当然就是保护了自执行函数内的方法、变量、属性等。这样代码更加安全了。
>
>2. 自执行函数模拟命名空间代码:
>
>  ```js
>  /********* 使用自执行函数模拟命名空间 ****************/
>  (function() {
>  //根据id获取对象
>  function $(id) { return document.getElementById(id); }
>  //内部函数，在外层是不可以调用的
>  function _setStyle(id, styleName, styleValue) {
>  $(id).style[styleName] = styleValue;
>  }
>
>  //创建伪命名空间
>  window.mySpace = {};
>  //将内部函数_setStyle封装在mySpace命名空间内
>  //调用时，使用window.mySpace.setStyle(id, styleName, styleValue)
>  window.mySpace.setStyle = _setStyle;
>  })();
>
>  //下面是测试代码
>  window.onload = function() {
>  //将id为test的对象的文字颜色设置为红色
>  window.mySpace.setStyle("test", "color", "#f00");
>  }
>
>  /*********与下方代码效果等同,外部能访问其所有属性,相对来说缺少安全性****************/
>  window.mySpace = {};
>  window.mySpace.$ = function(id) { return document.getElementById(id); }
>  window.mySpace.setStyle = function(id, styleName, styleValue) {
>  window.mySpace.$("test").style[styleName] = styleValue;
>  }
>  //下面是测试代码
>  window.onload = function() {
>  window.mySpace.setStyle("test", "backgroundColor", "#f00");
>  window.mySpace.setStyle("test", "color", "#fff");
>  }
>  ```
>
>3. 比较之后我们可以发现`，第二方法更加的直观`，易于理解。`但是少了封装过程，代码完全裸露在外`
>
>  `ps`:不一定使用`window`,也可以自己声明全局变量进行使用,此处是为了更明显展示



## Ⅴ-通过druid源码部分剖析js命名空间

>这是在看阿里员工写的开源数据库连接池的druid的源代码时，发现了其中在jquery的原代码中又定义了一个命名空间的函数:`$.namespace()`

### 1、源码截图与使用方式举例

>1. 代码截图
>
>  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210608112006677.png" alt="image-20210608112006677" style="zoom:67%;" />
>
>2. 使用代码举例:
>
>  ```js
>//注意,因为此处人家直接在`jquery-1.11.1.min.js`中加的方法,所以导入后可以直接使用
><script type="text/javascript" src="js/jquery-1.11.1.min.js"></script> 
><script type="text/javascript">
>$.namespace("druid.index");
>//注意:此处用子调用函数,否则你下面调用不能`druid.index.login();` 而是要 `druid.index().login();`的方式
>druid.index=(function(){
>    return {
>        login:function(){  方法的实现 },
>        submit:function(){  方法的实现 }
>    };
>}());
>//使用命名空间的函数
>druid.index.login();
>druid.index.submit();
>  ```
>
>   这样的话，就不会在全局变量区，引入很多的函数，将所有要使用的函数已经变量都放入了命名空间druid.index中，避免了不同js库中的函数名的冲突
>
>3. 控制台使用效果截图<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210608120149921.png" alt="image-20210608120149921" style="zoom:67%;" />
>
>4. 想看人家源码的同学点这里:[源码地址](https://github.com/alibaba/druid/blob/master/src/main/resources/support/http/resources/js/jquery.min.js)

### 2、如何理解源代码?

>1. 代码加自己注释
>
>  ```js
>$.namespace = function() { 
>    	//arguments->是默认的传入参数
>       var a=arguments, o=null, i, j, d; 
>       for (i=0; i<a.length; i=i+1) { 
>        //将传入参数分割成数组 标识是`.` -->druid.index  就会变成 ['druid','index']
>          d=a[i].split("."); 
>        //将全局的window浅拷贝到O对象上  -->此步作用应为用来判断window全局上是否有传入参数的属性-> 例如['druid','index']
>          o=window; 
>          for (j=0; j<d.length; j=j+1) { 
>        //判断全局中是否有该属性,有则不覆盖,没有则创建   -->注意:此时O并不是代表window,而只是浅拷贝了window上的数据   
>             o[d[j]]=o[d[j]] || {}; 
>        //将o[d[j]]保存下来,用作出循环后返回使用
>             o=o[d[j]]; 
>          } 
>       } 
>    return o; 
>};
>  ```
>
>2. 代码理解-->
>
>  1)` o[d[j]]=o[d[j]] || {}; `: 可以看上述代码中,我先将`o`指向了`window`,所以如o.index={}就等同于window.index={};就相当于在window上定义了一个名叫index的对象
>
>  2)在上一句后接` o=o[d[j]];`:上面的代码中：o = o.druid; 之后，因为 o 是指向 window，为什么console.log(o); 打印 Object {}；而 console.log(window); 打印输出Window呢？这里的原因是，没有理解引用的含义。o 和 window 都是stack上的一个变量，他们都指向heap上的全局window对象，我们修改 o 这个引用，让它指向另外的一个空对象，而这并不会同时修改stack上的window这个引用的指向。也就是就像两条绳子 a, b 都指向一条船，我让其中的一条绳子b指向第二条船，并不会影响绳子a还指向第一条船。
>
>  o = o.druid; 执行之后，o 不再执行window对象了，而是指向了window.druid对象，那么最后的console.log(o.druid);为什么打印输出 undefined 呢？很简单，因为 o 已经指向了 window.druid; 而window.druid是个空对象，其下并没有个druid的属性，所以自然就打印输出 undefined 了。也就是说最后的console.log(o.druid); 就相当于 console.log(window.druid.druid);
>
>    3) 我们看到了已经形成了我们需要的命名空间：window.druid.index ，其实命名空间是使用对象链条来实现的。因为 o = o.druid; 之后，o 已经指向了 window.druid ，那么 o.index = {}; 就相当于 window.druid.index = {};而 后面的 o = o.index; 又将 o 对象变成了一个空对象，不再指向 window.druid，打印一个空对象的 index 属性自然就输出 undefined.

### 3、核心知识点

>1）利用了 window 这个特殊引用的不可覆盖性，不可修改；
>
>2）命名空间其实是对象链条来模拟的；
>
>3）理解引用的含义：引用是个在stack上的变量，可以修改它指向不同的对象，要访问或者说修改他指向的对象，必须使用 “.” 点操作符，比如 o.index ={}; 而单纯的修改 o ，比如 o = {}; 并不会修改他指向的对象，因为 没有访问到他指向的对象，怎么能修改到他指向的对象呢？

### 4、设计封装理念

>1. 首先 $.namespace("druid.index"); 定义了一个命名空间：druid.index，它其实是 window.druid.index , 然后下面将一个**匿名函数的调用**的返回值赋值给window.druid.index
>2. 然后这个函数返回的是： return {} ，这是什么？显然**我们在js中可以这样定义一个对象： var obj = {}; 所以这里返回的是一个js对象**，那么这个js对象的内容是什么呢：{login:xxx, submit:xxx} 这是什么？？**显然这和我们的 json 格式是一模一样的，所以返回的对象是一个json对象**，当然也是一个js对象，只不过，**该json对象的属性的值，不是普通的字符串或者json对象，而是一个函数**，仅此而已。

------



## Ⅵ-应用实例举例1-自封装命名空间函数

>此处是本人利用命名空间进行对`localStorage`与`sessionStorage`存取方法的封装,此处就应用到上述几个知识点
>
>且不要论本人编码能力(毕竟本人还没毕业,编码能力肯定没多年大佬强),此处举例出来是为的让大伙知道有此写法

### 1、需求场景分析

> 举个栗子:当我们同一项目有两个客户端,登录后我们要分别将其登录数据存入本地,如:token userData等,但明明都属于登录时的数据,为了方便归类也为了防止本地变量混乱,就可以使用此方法,这样我们可以有效区分本地存储数据,并且使用方便

### 2、功能实现

>本地存储的增删改查,并且通过命名空间,闭包的相关知识,可以很轻松的将不同常量直接添加到一个对象变量中并存到本地
>
>![image-20210521202047347](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E6%9C%AC%E5%9C%B0%E5%AD%98%E5%82%A8(LocalStorage%E3%80%81Session)%E7%9B%B8%E5%85%B3%E5%B0%81%E8%A3%85%E4%B8%AD%E7%9A%84%E5%9B%BE%E7%89%87.png)

### 3、封装代码实现

>```tsx
>import {
>//检查 value 是否是普通对象.也就是说该对象由 Object 构造函数创建，或者 [[Prototype]] 为 null 。
>isPlainObject,
>//检查 value 是否是 Array 类对象。
>isArray,
>//创建一个 debounced（防抖动）函数
>debounce
>} from 'lodash/fp';
>
>interface Params {
>key: any;
>value?: any;
>}
>
>interface StorageOperate {
>add?: ({ key, value }: Params) => void;
>remove?: ({ key }: Params) => void;
>get?: ({ key }: Params) => any;
>clear?: () => void;
>}
>//LocalStorage 类型
>const LOCALSTORAGE = 'LOCALSTORAGE';
>//Session Storage类型
>const SESSIONSTORAGE = 'SESSIONSTORAGE';
>//对象类型
>const OBJECTSTORAGE = 'OBJECTSTORAGE';
>
>//LocalStorage存储类型的操作函数重写
>const _localStorage: StorageOperate = (() => {
>//将window的localStorage赋值到_db上
>const _db = window.localStorage;
>return {
>//实际上只是二次封装,统一调用方式
>add({ key, value }) {
>// 当调用其add方法函数时,实际上是去调用其`setItem方法`
>_db?.setItem(key, value);
>},
>remove({ key }) {
>_db?.removeItem(key);
>},
>get({ key }) {
>return _db?.getItem(key) || null;
>},
>clear() {
>_db?.clear();
>},
>};
>})();
>//SessionStorage存储类型的操作函数重写
>const _sessionStorage: StorageOperate = (() => {
>const _db = window.sessionStorage;
>return {
>add({ key, value }) {
>_db?.setItem(key, value);
>},
>remove({ key }) {
>_db?.removeItem(key);
>},
>get({ key }) {
>return _db?.getItem(key) || null;
>},
>clear() {
>_db?.clear();
>},
>};
>})();
>//对象存储类型操作函数
>const _objectStorage: StorageOperate = (() => {
>let _db = {};
>return {
>add({ key, value }) {
>_db[key] = value;
>},
>remove({ key }) {
>delete _db[key];
>},
>get({ key }) {
>return _db[key];
>},
>clear() {
>_db = {};
>},
>};
>})();
>
>//声明私有变量_DB对象  此处`db`在构造函数中已经经过判断,转换为特定类型的存储对象了
>const _DB = {
>_get({ db, domain, type }) {
>//根据传入的已经转换的`db`对象调用其获取方法获取本地存储数据
>let _val = db.get({ key: domain });
>let _obj;
>try {
>//如果取得的_val数据是空的,或者获取的类别是对象存储,则赋予`_val(如果_val为空则赋予空对象)`
>//如果不为空,将得到的`_val`数据格式转换为json对象
>_obj = !_val || type === OBJECTSTORAGE ? _val || {} : JSON.parse(_val);
>} catch ($$) {//此处$$只是一个占位,无作用
>//如果发生异常,则直接赋予空对象
>_obj = {};
>}
>return _obj;//最后将处理好的json对象数据返回
>},
>//set写入方法
>_set(obj: any, { db, domain, type }) {
>//如果传入为空,则返回错误
>if (!obj) return false;
>//如果传入的是一个对象或者 是一个数组且类型不为对象存储时,就进行类型转换
>if (isPlainObject(obj) || (isArray(obj) && type !== OBJECTSTORAGE)) obj = JSON.stringify(obj);
>//根据传入的已经转换的`db`对象调用其写入方法写入本地存储数据
>db.add({ key: domain, value: obj });
>return true;
>},
>//删除方法
>_remove({ db, domain }) {
>//根据传入的已经转换的`db`对象调用其删除方法删除本地存储数据
>db.remove({ key: domain });
>},
>};
>
>
>//定义DB类,这里是对于_DB的调用
>class DB {
>source: any = {};
>option = null;
>backup = null;
>
>setOrigin = debounce(10)(function () {
>_DB._set(this.source, this.option);
>});
>
>/**构造函数
>*调用示例 const loginDB = new DB('LOGIN', DB.LOCALSTORAGE);
>* @param param0 {用作存储的key名 , 存储类型 }
>*/
>constructor({ domain, storageType = OBJECTSTORAGE }) {
>this.option = {
>  //用作后续存储的key名,可以省略后续输入
>  domain,
>  //存储类型
>  type: storageType,
>  //通过存储类型判断决定db使用上述什么类型的存储操作函数
>  //以达到同一函数根据不同参数做出不同反应的效果
>  db:
>    storageType === LOCALSTORAGE
>      ? _localStorage //如果是LocalStorage类型
>      : storageType === SESSIONSTORAGE
>        ? _sessionStorage//如果SessionStorage类型
>        : _objectStorage,//如果是其他类型,则用对象存储
>};
>//此处是`flag`作用-->当传入的存储类型不是对象存储时为`true`
>this.backup = storageType !== OBJECTSTORAGE;
>//当类别不为对象存储时 this.source以该配置信息获取数据,此处得到的数据应是json格式对象或者空对象
>//此处将其提前存储,后续在构造函数get方法中可以直接调用,节省性能
>if (this.backup) this.source = _DB._get(this.option);
>}
>
>/** 重新初始化函数
> * 针对特殊场景防错方法:
>   1. 因为上面_update中调用的`setOrigin()`方法是防抖功能,延迟设置storage来达到防止频繁操作storage(异步操作)
>   2. 但也因为如此,在某些特定场景下导致初始化拿不到数据,举个栗子:
> 		1) 当你同一浏览器开两个本项目页面,当我将storage所有数据清空后或者第一次使用时,先登录一个页面账户,在登陆另一个页面账户
>		2) 登录账户的token是存在storage,那么我在登录第二个账户时,第一个账户的token就会被删除,导致不同账号却能挤下线
>	* 原因:
>	 1. 当你打开两个页面时,其实两个页面都初始化了,这时`this.source`都为undefined,但我在其中一个页面登录后写入,另外一个页面却不会监听到,
>	 2. 导致另一个页面按照storage为空处理,直接覆盖,导致上述情况发生
>	* 解决:
>	    调用时在重新初始化`this.source`即可	
>	* 该函数调用:如上述特殊情况时调用此方法(初始化使用),通常就是这种登录初始化渲染的极端情况
> */
>syncSource() {
>  if (this.backup)  this.source = _DB._get(this.option);
>}  
>
>/**
>* 外部调用的获取函数
>* @param key  获取数据的KEY
>* @param getOriginal 是否强制重新获取 -->因为有可能在构造时传入的是对象存储类型,导致`this.source`为空
>* @returns 
>*/
>get(key: string, getOriginal?: boolean ) {
>//如果`getOriginal`为true时根据构造函数时传入的option获取该类型的Storage 否则直接用调用构造函数时取得的数据
>//此处是必要的,因为删除后将其置空了,所以置空后再次get就需要此步,否则取不到值
>const source = getOriginal ? _DB._get(this.option) : this.source
>//这时候拿到的source其实是一个对象,里面存了多个json对象,这时候根据key获取其中具体的属性,详见运行示例截图
>return key !== undefined ? source[key] : this.source;//如果key传入空,则直接返回所有
>}
>
>/**
>* 私有--更新方法,即重新写入this.source
>* @param imd 是否进行防抖更新
>*/
>_update(imd?: boolean) {
>if (!imd)  this.setOrigin(); //如果为false,则防抖
>else  _DB._set(this.source, this.option);//为true则不防抖
>}
>/**
>* 外部调用的写入函数
>* 此处是给实例化后的该json对象写入特定key于value
>* @param key  写入的key
>* @param val  要写入的value
>* @param imd  是否防抖 默认false
>* @returns 
>*/
>set(key: any, val: any, imd = false) {
>//如果传入的key是空的,返回空字符串,并且不写入
>if (key === undefined) return '';
>this.source[key] = val; //将source对象中新创一个[key]属性并赋值val
>this._update(imd); //调用更新,即将this.source重新写入到本地中
>return true;
>}
>//复制,将传入的对象直接复制到 this.source上,随后直接写入
>assign(obj: any, imd?: boolean) {
>if (!isPlainObject(obj) && !isArray(obj)) {
>  console.log('value 必须是 object 或 array 类型');
>  return false;
>}
>this.source = obj;
>this._update(imd);
>return true;
>}
>//删除本地存储
>remove(key?: any, imd?: boolean) {
>//如果删除不传入key,则删除当前实例下的数据,然后通过调用` _DB._remove`进行删除
>if (key === undefined) {
>  this.source = {};         //将 this.source置空
>  _DB._remove(this.option); //删除本地存储
>  return;
>}
>//如果当前删除特定属性的不为空
>if (this.source[key] !== undefined) {
>  //如果为数组,且key为下标的话 使用`splice`删除
>  if (isArray(this.source) && /^([1-9]\d*)|0$/.test(key))  this.source?.splice(key, 1);
>  else  delete this.source[key];
>  //删除完后再写入本地
>  this._update(imd);
>}
>return true;
>}
>clear() {
>return this.remove(); //调用上面的remove,不传值即使置空
>}
>}
>
>//导出  且此处使用一个自运行函数形成闭包,即命名空间
>export default (function () {
>//此处是利用闭包的原理,每次调用该实例操作的都是此数,可以理解为此数是盛放所有new DB() 类型的容器
>let store = {};
>let index = 0;
>
>const Storage = function (domain?: string, storageType?: string): void {
>//如果不传入key 则默认随机生成key且不重复
>if (!domain) {
>  domain = +new Date() + '-' + index;
>  index++;
>}
>//如果不存在该属性,则进行子实例创建,并挂载到store对象上
>if (!store[domain])  store[domain] = new DB({ domain, storageType });
>return store[domain];
>};
>//清理函数
>Storage.clear = function (domain?: string) {
>//如果不传入参数,就将所有类型的全删除
>if (!domain) {
>  _localStorage.clear();
>  _sessionStorage.clear();
>  _objectStorage.clear();
>  store = {};
>} else {
>  if (store[domain]) {
>    store[domain].clear();
>    store[domain] = null;
>  }
>}
>};
>
>Storage.LOCALSTORAGE = LOCALSTORAGE;
>Storage.SESSIONSTORAGE = SESSIONSTORAGE;
>Storage.OBJECTSTORAGE = OBJECTSTORAGE;
>//此处是环境变量配置,不需要
>// const __DEV__ = process.env.NODE_ENV == 'development';
>// if (__DEV__) {
>//   window['abs'] = store;
>// }
>return Storage;
>})();
>
>```

### 4、调用与使用

>1. 声明创建实例
>
>```tsx
>import DB from '~/utils/DB';
>//此处可以直接调用到内部的常量是因为有做返回处理
>//此处可以 `new DB('PLATFORM', "常量名");`这样调用是因为命名空间的原因
>export const platformDB = new DB('PLATFORM',"常量名");
>```
>
>此处可以 `new DB('PLATFORM', DB.SESSIONSTORAGE);`这样调用是因为命名空间的原因
>
>2. 调用-->此间大写都是常量
>
>```tsx
>//取
>const tabPanes = platformDB.get("常量名");
>const activeKey = platformDB.get("常量名");
>//存
>platformDB.set("常量名", this.tabPanes);
>//删
>platformDB.remove("常量名");
>```
>
>3. 重新初始化函数调用  --`针对特殊场景检查`
>
> ```tsx
>/**此处有一个BUG :
>     1. 使用同一浏览器,同时打开两个页面,清空LicalStrage后 
>     2. 先后登录 用户端后台和 运维端后台,先登录的那个用户的LicalStrage会被覆盖
>     3. 但是随后继续重新登录后就都不会出问题
>*/
>       if (isEmpty(loginDB.get())) {
>       // 因为loginDB使用对象保存key/value延迟设置storage来达到防止频繁操作storage，
>      //因此在另一个页面清空storage，另一个页面对象在不刷新情况无法初始化感知，针对特殊场景检查。
>       loginDB.syncSource();
>     }
> ```

### 5、函数概要截图

>![image-20210521202903681](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E6%9C%AC%E5%9C%B0%E5%AD%98%E5%82%A8(LocalStorage%E3%80%81Session)%E7%9B%B8%E5%85%B3%E5%B0%81%E8%A3%85%E4%B8%AD%E7%9A%84%E6%A6%82%E8%A6%81.png)







# 六、变量声明

## Ⅰ -变量的声明分显式声明和隐式声明

>* **显示声明** 是程序中的一条说明语句，它列出一批变量名并指明这些变量的类型。
>
> >```js
> >// 显示声明 变量name，但不知其类型，也不知其占用空间大小
> >var name ;
> >```
>
>* **隐式声明** 指通过某种默认协定的方法将变量名与类型绑定。所有隐式声明的变量默认都是全局变量，无论函数内外
>
> >```js
> >// 赋值语句其实隐式的声明了变量name，类型为string
> >name = '努力学习的汪';//隐式声明(为全局变量的一个属性) --> 注意:是属性
> >```
> >
> >隐式声明带来了些许的方便，但却被认为有损于程序的可读性，因为它可能会带来隐藏的错误，Bug。

## Ⅱ - 结合实例说明

### 1、当我们使用访问一个没有声明的变量时，JS会报错

>```js
>console.log(1,userName);  //报错,因为没有声明
>```

### 2、当我们给一个没有声明的变量赋值时，JS不会报错

>* 相反它会认为我们是要隐式声明一个 **全局** 变量，这一点一定要注意。
>
>```js
>userName = 'hongjilin'
>console.log(1,userName);   //打印hongjilin
>console.log('window',window.userName) //打印window上的userName
>function  person(){
>    userName = '努力学习的汪';
>    console.log(2,userName); //打印 努力学习的汪
>}
>person();
>console.log(3,userName); //打印 努力学习的汪
>console.log('window',window.userName) //打印window上的userName
>```
>
>可以明显看到,实际上变量是挂载在全局对象window上,以属性的形式存在
>
>![image-20210918135428949](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210918135428949.png) 

### 3、当我们给声明过的变量赋值

>与上方代码基本一致,只有第一行代码改为声明变量
>
>```js
>let userName = 'hongjilin'  //##只有这一行声明改变
>console.log(1,userName);   //打印hongjilin
>console.log('window',window.userName) //打印window上的userName
>function  person(){
>userName = '努力学习的汪';
>console.log(2,userName); //打印 努力学习的汪
>}
>person();
>console.log(3,userName); //打印 努力学习的汪
>console.log('window',window.userName) //打印window上的userName
>```
>
>可以明显看到,实际上声明后的变量是局部存在的,在window上是找不到这个属性的![image-20210918135820760](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210918135820760.png) 

## Ⅲ - 总结

>在当前域中声明变量. 如果在方法中声明，则为局部变量（local variable）；如果是在全局域中声明，则为全局变量。
>
>1. 而事实上是对属性赋值操作。
>
>  * 首先，它会尝试在当前作用域链: 如在方法中声明, (先找方法当前的作用域）中解析 userName；
>  * 如果在任何当前作用域链中找到name，则会执行对name属性赋值； 
>  * 如果没有找到name，它才会层层往上找,最终在全局对象(即当前作用域链的最顶层对象，如window对象)中创造name属性并赋值。
>
>2. **注意**: 它并不是声明了一个全局变量，而是创建了一个全局对象的属性
>
>  - 即便如此，可能你还是很难明白“变量声明”跟“创建对象属性”在这里的区别,别急! 继续往下看
>  - 事实上，Javascript的变量声明、创建属性以及每个Javascript中的每个属性都有一定的标志说明它们的属性
>  - 如只读（ReadOnly）不可枚举（DontEnum）不可删除（DontDelete）等等。
>
>3.  由于变量声明自带不可删除属性，比较 **var userName = '努力学习的汪'** 跟 **userName = '努力学习的汪'**
>
>  - 前者是变量声明，带不可删除属性，因此无法被删除 -->  **delete userName；** 无效
>  - 后者为全局变量的一个属性，因此可以从全局变量中删除  -->  **delete userName；** 有效





# 七、jsonP解决跨域方案





## 一、jsonP概念

>1)JSONP 是什么?
>
>> JSONP(JSON with Padding)，是一个非官方的跨域解决方案，纯粹凭借程序员的聪明 才智开发出来，只支持 get 请求。
>
>> 首先抛出浏览器同源策略这个概念，为了保证用户访问的安全，现代浏览器使用了同源策略，即不允许访问非同源的页面，详细的概念大家可以自行百度。这里大家只要知道，在ajax中，不允许请求非同源的URL就可以了，比如[www.a.com](#)下的一个页面，其中的ajax请求是不允许访问[www.b.com/c.php]()这样一个页面的
>
>2)JSONP 怎么工作的？
>
>> 在网页有一些标签天生具有跨域能力，比如：img link iframe script。 JSONP 就是利用 script 标签的跨域能力来发送请求的。
>
>3)JSONP原理
>
>> ajax请求受同源策略影响，不允许进行跨域请求，而script标签src属性中的链接却可以访问跨域的js脚本，利用这个特性，服务端不再返回JSON格式的数据，而是返回一段调用某个函数的js代码，在src中进行了调用，这样实现了跨域。

### Ⅰ-jsonP的使用

```js
   // 1. 动态的创建一个 script 标签------------------------------------------------------------
    var script = document.createElement("script");
	//2. 设置 script 的 src， 设置回调函数
    script.src = "http://localhost:3000/testAJAX?callback=abc";
    function abc(data) {
      alert(data.name);
    };
   // 3. 将 script 添加到 body 中
    document.body.appendChild(script);

   // 4. 服务器中路由的处理------------------------------------------------------
    router.get("/testAJAX", function (req, res) {
      console.log("收到请求");
      var callback = req.query.callback;
      var obj = {
        ame: "孙悟空",
        age: 18
      }
      res.send(callback + "(" + JSON.stringify(obj) + ")");
    });
```

### Ⅱ-jQuery发送jsonP请求

```js
//前端代码-----------------------------------------------------------------------------------
$('button').eq(0).click(function () {
  $.getJSON('http://127.0.0.1:8000/jquery-jsonp-server?callback=?', function (data) {
    $('#result').html(`
                名称: ${data.name}<br>
                校区: ${data.city}
            `)
  });
});

//服务端代码-----------------------------------------------------------
app.all('/jquery-jsonp-server', (request, response) => {
  // response.send('console.log("hello jsonp")');
  const data = {
    name: '尚硅谷',
    city: ['北京', '上海', '深圳']
  };
  //将数据转化为字符串
  let str = JSON.stringify(data);
  //接收 callback 参数
  let cb = request.query.callback;

  //返回结果
  response.end(`${cb}(${str})`);
});
```

## 二、我自己开发封装的jsonP插件

>1、代价:需要前后端联动
>	2、精髓:自动的由插件生成方法名,并在当前的页面动态的生成函数,然后再生成的函数里头调用用户预留的回调函数
>	3、插件：自动化的去模拟基于script去实现跨域请求的过程（对用户来说是黑盒子）
>	4、参数拼接：url已经是带参的。和不带参的
>	5、id优化 额可以添加一个容器来管理id

## 代码示例

> > 1、前端调用测试封装好的jsonP代码
>
> ```js
> //测试调用函数
>     let test=function () {
>         jsonP.req({
>             url:"http://localhost:3000/jsonpx",
>             data:{
>                 a:"111"
>             },
>             callback:function (result) {
>                 alert("成功"+result)
>             }
>         })
>     }
> ```
>
> > 2、服务端测试代码
>
> ```js
> router.get('/jsonpx', async function (req, resp, next) {
>     let callback=req.query.callback;
>     let data=req.query.a;
>     if (!data){
>         resp.send(`${callback}('洪jl:我是服务端代码')`)
>     }
>     resp.send(`${callback}('洪jl:我是服务端代码`+data+`')`)
> })
> ```
>
> > 3、封装原生代码
>
> ```js
> <script>
>     /**author:@hongjilin
>      * 1.声明一个jsonP插件对象
>      * 作用：隔开作用域
>      */
>     let jsonP = {};
> 
>     /**
>      *2.在插件对象中创建两个名字备用符数组
>      */
>     jsonP.char = {
>         Number: '0123456789',
>         Letter: 'qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM'
>     }
>     /**
>      * 通过随机数抽取备用字符数组库拼凑函数id
>      * @param charLen
>      * @param numLen
>      */
>     jsonP.newFunId = function (charLen, numLen) {
>         let id = '';
>         for (let i = 0; i < charLen; i++) {
>             id += this.char.Letter.charAt(Math.random() * 52)
>         }
>         for (let j = 0; j < numLen; j++) {
>             id += Math.floor(Math.random() * 10);
>         }
>         return id;
>     }
>     /**
>      * 拼接路径
>      * @param url
>      * @param key
>      * @param value
>      */
>     jsonP.jointUrl = function (url, key, value) {
>         if (url && key && value) {
>             let sign = "&"
>             //如果是第一次
>             if (url.indexOf('?') == -1) {
>                 sign = '?'
>             }
> 
>             url += sign + key + "=" + value
>         }
>         return url;
>     }
>     /**
>      封装err属性方便
>      */
>     jsonP.err = function (msg) {
>         console.error(msg)
>     }
> 
>     /**
>      * 发送请求函数
>      * @param options
>      */
>     jsonP.req = function (options) {
>         let jsonId={};
>         //1.生成方法名
>         jsonId.funId = this.newFunId(4,8);
>         let Userurl = options.url;
>         let Userdata = options.data;
>         if (!options) {
>             this.err("输入不能空")
>             return;
>         } else if (!Userurl) {
>             this.err("url不能空")
>             return;
>         } else if (!Userdata) {
>             //如果没有data,初始化
>             Userdata = {};
>         }
>         //将函数名赋值给userdata的回调函数属性中
>         Userdata.callback = jsonId.funId;
>         for (let key in Userdata) {
>             Userurl = this.jointUrl(Userurl, key, Userdata[key])
>         }
>         let script = document.createElement('script');
>         script.setAttribute("id" , jsonId.funId);
>         script.setAttribute("src" , Userurl);
>         //动态生成函数
>         let callback=function (result) {
>             console.log("xxxxxxx")
>             //业务逻辑回调
>             if (options.callback){
>                 try {
>                     options.callback(result)
>                 }catch (e) {
>                     this.err(e.message)
>                 }
>             }
>             //善后
>             let tmp=document.getElementById(jsonId.funId)
>             tmp.parentNode.removeChild(tmp);
>             eval(jsonId.funId+'=null')
>         }
>         eval("window."+jsonId.funId+"=function(result){ callback(result) }")
>         document.head.appendChild(script)
> 
>     }
> </script>
> ```
>



# 八、 setInterval和setTimeout第一个参数加与不加引号的区别

## Ⅰ- 问题的提出

### 1、代码示例

>```js
>function func(){console.log("延时器演示")}
>setTimeout(func, 0);
>setTimeout("func()", 0);
>```
>
>定时器中，两个调用函数的方法都是正确的。这时可能就有同学要提出疑问了:为什么有时候要有引号有时候不用引号,分别在什么场景会用到呢?那为什么我之前都不会遇到这个问题呢?

### 2、为什么之前没遇到这个问题

>在此之前,我使用的都是箭头函数的写法,所以都没有在意过这个问题
>
>```js
>setTimeout(()=>{ console.log("箭头函数延时器") }, 0);
>```
>
>但并不是说少遇到就不去解决,这不,在我刷题的时候就遇到了.....

### 3、什么场景会用?

>当你想用定时器，调用函数的时候，给函数传参的话，必须要加引号，否则会没有延时效果
>
>```js
>const name='努力学习的汪'
>const name1='努力学习的汪不带双引号'
>function func(name){console.log(name,"延时器演示")}
>setTimeout("func(name)", 100);//努力学习的汪 延时器演示
>setTimeout(func, 100);//undefined "延时器演示"
>setTimeout(func(name1), 100); //没有延时效果
>```
>
>![image-20210909105738170](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210909105738170.png) 

## Ⅱ - 第一个参数为字符串时

### 1、实际情况会发生什么

>如果您将字符串作为函数的第一个参数传递，实际情况会发生什么
>
>```js
>setTimeout('string',number)
>```
>
>是在运行时(在经过number毫秒之后)评估的第一个参数的值。基本上它等于:
>
>```js
>setTimeout(eval('string'), number)
>```

### 2、作用域发生改变

>```js
>//它会优先寻找当前的作用域中是否有func函数,如果局部没有的话,则会依次按照顺序往上查找,直到全局作用域中。
>setTimeout(func, 0); 　　　　　　
>setTimeout("func()", 0);//而这个定时器他的寻找func函数只会从全局寻找这个方法，不会从局部寻找。
>```
>
>在全局环境中执行时，从全局环境中找，如果全局环境并没有定义**func**，且作用域链规定了外部作用域是不能访问内部作用域中的相关函数和变量的，所以会报错。

### 3、this指向发生变化

>```javascript
>//在不加引号的定时器方法中
>setTimeout(func, 0);//this的指向是指向当前函数的主人
>
>//而在加引号的定时器中
>setTimeout("func()", 0);//他的指向永远是 Window -->因为调用的是window.eval()方法进行了执行
>```

### 4、举个栗子

>1. 带引号，该方法在**全局环境**中寻找；      
>2. 不带引号，该方法在**局部环境**中寻找。     
>
>```js
>;(function () {
>  //局部声明函数
> function fn() { 
>   console.log('局部 声明的fn函数')
> }
> setTimeout('fn()', 1000); // 找到全局函数进行执行
> setTimeout(fn, 1000); // 找到局部函数进行执行
>})()
>//全局声明函数
>function fn(){
>console.log('全局 声明的fn函数')
>}
>```
>
>![image-20210909111212708](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210909111212708.png) 

## Ⅲ - 安全问题

>尽管可能，但不应将字符串传递给setTimeout或setInterval。传递字符串使setTimeout()或setInterval()使用类似于eval()的功能，将字符串作为脚本执行，从而使任意和可能有害的脚本执行成为可能。



# 九、addEventListener与事件冒泡及捕获



## 1、addEventListner基本用法

>在复杂的项目中,JS与html的解耦变得至关重要.W3C为我们提供了 `addEventListener()` 函数用来为指定的dom元素动态绑定事件,这个函数有三个参数:
>
>* 第一个参数是事件类型 (如'click')
>* 第二个参数是事件触发后调用的函数
>* 第三个参数是个布尔值: 默认是false(冒泡阶段执行)  true(捕获阶段产生) 
>
>一般来说,前面两个参数就足以满足我们为按钮绑定事件的需求了
>
>###### 实际代码
>
>```html
><!DOCTYPE html>
><html lang="en">
><head>
> <meta charset="UTF-8">
> <meta name="viewport" content="width=device-width, initial-scale=1.0">
> <title>Document</title>
></head>
><body>
> <div class="main" id="main">
>   <div id="grandpa" style="background-color: aqua; width: 200px;height: 200px;">最外层爷爷
>     <div id="father" style="background-color: aquamarine; width: 180px;height: 180px;">父亲
>       <div id="child" style="background-color: azure; width: 150px;height: 150px;">儿子
>         <div id="grandson" style="background-color: bisque; width: 100px;height: 100px;">孙子</div>
>       </div>
>     </div>
>   </div>
>
> </div>
></body>
><script>
> var grandpa = document.getElementById("grandpa");
> var father = document.getElementById("father");
> var child = document.getElementById("child");
> var grandson = document.getElementById("grandson");
>
> //绑定事件,true为捕获阶段产生
> grandpa.addEventListener("click", sleep, true);
> father.addEventListener("click", watchTV, true);
> child.addEventListener("click", playingCard, true);
> grandson.addEventListener("click", doingHomework, true);
>
>
>
> /*   定义方法       **/
> function sleep() {
>   // event.stopPropagation(); //阻止事件冒泡
>   console.log("爷爷:我是最外层");
> }
>
> function watchTV() {
>
>   console.log("父亲: 我在第二层");
> }
>
> function playingCard() {
>   console.log("儿子: 我在第三层");
> }
>
> function doingHomework() {
>   event.stopPropagation();
>   console.log("孙子: 我在最里面");
> }
></script>
>
></html>
>```
>
>**下方其他栗子都是基于此代码举例,所以下方代码将只给出代码块**



## 2、事件冒泡概念

>`IE`的事件流叫做事件冒泡. 
>
>* 即事件开始时由 **最具体的元素**(点击处文档中嵌套层次最深的那个节点) 接收到
>* 然后逐级向上传播到较为不具体的节点(文档)
>* 所有现代浏览器都支持事件冒泡,并且会一直冒泡到`Window`
>* **即内部元素的事件会先被触发，然后再触发外部元素**
>
>事件流如图:![image-20211025182218634](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025182218634.png) 
>
>###### 具体示例:
>
>![image-20211025182742516](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025182742516.png) 

## 3、事件捕获概念

>事件捕获的思想时不太具体的节点应该更早地接收到事件,而在最具体的节点应该最后接收到事件
>
>* 事件捕获的用途在于 **事件到达预定目标之前捕获他** 
>* `IE9+`以上支持他,但因为老版本浏览器不支持,所以很少有人使用事件捕获
>* 它从`window`开始捕获(尽管有些地方规定从document开始)
>
>事件流如图:![image-20211025183312862](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025183312862.png) 
>
>###### 具体实例:
>
>![image-20211025183549639](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025183549639.png) 

## 4、DOM事件流

>'DOM2级事件' 规定事件流包括三个阶段: 事件捕获阶段、处于目标阶段、事件冒泡阶段
>
>* 首先发生事件的捕获,为截获事件提供了机会
>* 然后是实际的目标接受了事件
>* 最后一个阶段是冒泡阶段,可以在这个阶段对事件做出响应
>
>![image-20211025183946955](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025183946955.png) 

## 5、事件冒泡与事件捕获如果同时进行会怎样?

>###### 跟我一样善于思考的同学们肯定也会思考这么一个问题: 
>
>>在上述代码中的 `addEventListener()` 第三个参数,如果一部分是true 一部分是false;就是一部分为冒泡一部分为捕获,这时候的运行结果是什么?
>
>>实际上我们的浏览器更倾向于使用 **事件捕获**:
>
>>* 他会先把 **第三个参数为true** 的元素绑定事件按照正常顺序绑定事件
>>* 然后才会为 **第三个参数为false** 的元素按照冒泡事件的顺序执行绑定的事件
>
>###### 直接上结果:
>
>![image-20211025185559445](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025185559445.png) 

## 6、阻止事件冒泡与捕获

>我们可以利用事件对象event的 `stopPropagation()` 方法阻止事件的进一步传播
>
>* 值得注意的是: event.stopPropagation
>
>```js
>//这里我们可以修改爷爷绑定的事件
> /*   定义方法       **/
> function sleep() {
>   event.stopPropagation(); //阻止事件冒泡
>   console.log("爷爷:我是最外层");
> }
>```
>
>![image-20211025190446711](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20211025190446711.png) 

## 7、preventDefault 及 stopPropagation函数以及`return false`的作用与区别?

>实际上因为本人在实际开发中基本就没用到这两个函数,所以在一次别人问我关于这个的问题时我是一脸?
>
>所以我专门来学习并梳理这一块的知识点笔记

### Ⅰ -  event.stopPropagation()

>###### 这个函数是阻止事件冒泡:实际上在上面的内容已经解释过了,这里当作复习再叙述一遍
>
>>事件可以再各层级的节点中传递,不管是冒泡还是捕获,有时我们希望事件在特定节点执行完后不再传递,就可以使用 `event.stopProgation()`来阻止事件冒泡
>
>当然,他只会阻止事件传播,并不会阻止事件本身的默认行为(如a标签的跳转)

### Ⅱ - event.preventDefault()

>###### **此函数是阻止默认行为触发**,什么是默认行为?
>
>>即标签属性本身具备的功能,就是类似于a标签所带的href与submit所带的提交等
>
>>对于默认行为,浏览器**优先执行事件函数后 再执行默认行为**
>
>当然,他不会阻止事件传播,所以可以两个搭配着用

### Ⅲ -  return false

>包含特有退出执行`return false ` 之后的所有触发事件和动作都不会被执行,有时候`return false` 可以替代`event.stopPropagation`和`event.preventDefult()`来阻止默认行为发生和冒泡
>
>```html
><body>
><br />
><div>
>    <a href="http://www.baidu.com">点击</a>
></div>
><script type="text/javascript">
>   document.querySelector('a').onclick=function(){
>       alert('警告');
>       return false;
>   }
></script>
></body>
>```
>
>结果只是出现了警告的弹窗,并没有跳转到百度页面
>
>如果将 `retuen false` 提前到 `alert('警告')` 的前面,结果就是什么都不显示,原因是 return false 会中止事件与默认行文

### Ⅳ - `return false ` 和 `event.stopPropagation`区别?

>* `return false` 不仅阻止了冒泡而且还阻止了事件本身
>* `event.stopPropagation()`只阻止了冒泡
>
>注意: 虽然`teturn false` 能够替代前面两个阻止默认行为和冒泡函数,但也有其他作用(比如中止循环);可能导致不可预料的结果,所以推荐还是使用前两者更好,提高代码的高效性 









# 十、 时间moment 



## 一、moment常用方法

> moment获取天的23时59分59秒可以用moment().endOf(String)，以及获取天的0时0分0秒可以用moment().startOf('day')

### 1、获取时间

#### Ⅰ-获取开始(Start of Time)时间

>- ##### 获取今天0时0分0秒
>
>```js
>moment().startOf('day')
>```
>
>- ##### 获取本周第一天(周日)0时0分0秒
>
>```js
>moment().startOf('week')
>```
>
>- ##### 获取本周周一0时0分0秒
>
>```js
>moment().startOf('isoWeek')
>```
>
>- ##### 获取当前月第一天0时0分0秒
>
>```js
>moment().startOf('month')
>```
>
>- 当前季度的开始时间：
>
>```js
>moment().startOf('quarter').format("YYYY-MM-DD")
>```
>
>- 指定年指定季度的开始时间：（某年某季度的开始时间）
>
>```js
>moment(moment().format("YYYY-02-01")).startOf('quarter').format("YYYY-MM-DD")
>```

 #### Ⅱ-获取结束(End of Time)时间

>格式`moment().endOf(String)`
>
> - ##### 获取今天23时59分59秒
>
>   ```js
>   moment().endOf('day')
>   ```
>
> - ##### 获取本周最后一天(周六)23时59分59秒
>
>   ```js
>   moment().endOf('week')
>   ```
>
> - ##### 获取本周周日23时59分59秒
>
>   ```js
>   moment().endOf('isoWeek')
>   ```
>
> - ##### 获取当前月最后一天23时59分59秒
>
>   ```js
>   moment().endOf('month')
>   ```
>
>
>- 当前季度的结束时间：
>
> ```js
>moment().endOf('quarter').format("YYYY-MM-DD")
> ```
>
>- 指定年指定季度的结束时间：（某年某季度的结束时间）
>
> ```js
>moment(moment().format("YYYY-02-01")).endOf('quarter').format("YYYY-MM-DD")
> ```

#### Ⅲ-获取当前月的总天数(Days in Month)

>- 获取当前月的总天数
>
> ```js
>moment().daysInMonth()
> ```

#### Ⅳ- 获取时间戳(以秒为单位)

>1. 获取时间戳(以秒为单位)
>
>  ```js
>   // 获取当前时间的时间戳 (秒)  大写的X 返回值为字符串类型
>  const miao = moment().format("X")  
>   // 获取当前时间的时间戳 (毫秒)  小写的x
>  const haomiao moment().format("x")  
>
>  moment().unix() // 返回值为数值型
>  ```
>
>2. moment时间戳与时间的转换
>
>  ```js
>  	// 获取当前时间
>      const currentTime = moment()
>      // 获取当前时间的时间戳 (秒)  大写的X
>      const miao = moment().format("X")  
>      // 获取当前时间的时间戳 (毫秒)  小写的x
>      const haomiao moment().format("x")  
>
>      //秒时间戳转换为北京时间
>      moment.unix(miao).format('YYYY-MM-DD HH:mm:ss') 	// format 用来设置你想展示的时间格式
>
>  	//毫秒时间戳转换为北京时间
>  	moment(haomiao).format('YYYY-MM-DD HH:mm:ss')
>  ```

#### Ⅴ- 获取具体时间(Get Time)

>1. 获取年份
>
>  ```js
>  moment().year()
>
>  moment().get('year')
>  ```
>
>2. 获取月份
>
>  ```js
>  moment().month() (0~11, 0: January, 11: December)
>
>  moment().get('month')
>  ```
>
>3. 获取一个月中的某一天
>
>  ```js
>  moment().date()
>
>  moment().get('date')
>  ```
>
>4. 获取一个星期中的某一天
>
>  ```js
>  moment().day() (0~6, 0: Sunday, 6: Saturday)
>
>  moment().weekday() (0~6, 0: Sunday, 6: Saturday) moment().isoWeekday() (1~7, 1: Monday, 7: Sunday) moment().get('day') mment().get('weekday') moment().get('isoWeekday')
>  ```
>
>5. 获取小时
>
>  ```js
>  moment().hours()
>
>  moment().get('hours')
>  ```
>
>6. 获取分钟
>
>  ```js
>  moment().minutes()
>
>  moment().get('minutes')
>  ```
>
>7. ##### 获取秒数
>
>  ```js
>  moment().seconds()
>
>  moment().get('seconds')
>  ```
>
>8. ##### 获取当前的年月日时分秒
>
>  ```js
>  moment().toArray() // [years, months, date, hours, minutes, seconds, milliseconds]
>
>  moment().toObject() // {years: xxxx, months: x, date: xx ...}
>  ```

#### Ⅵ- 获取当前时间往前的时间

>```js
>moment().format("YYYY-MM-DD HH:mm:ss"); //当前时间
>
>moment().subtract(1, "days").format("YYYY-MM-DD"); //当前时间的前1天时间
>
>moment().subtract(1, "years").format("YYYY-MM-DD"); //当前时间的前1年时间
>
>moment().subtract(1, "months").format("YYYY-MM-DD"); //当前时间的前1个月时间
>
>moment().subtract(1, "weeks").format("YYYY-MM-DD"); //当前时间的前一个星期时间
>
>//如果不设置格式的去掉后面的format()即可
>
>let  date = moment().subtract(1, "months");  //设置时间为当前时间的前一个月
>```

#### Ⅷ-(上/下)获取(年/季/月)

>上一年/下一年
>
>```js
>上一年：moment().add(-1, 'y').format("YYYY")
>下一年：moment().add(1, 'y').format("YYYY")
>上几年和下几年同理，做momment日期加减，月季度亦同理
>```
>
>上一季度/下一季度
>
>```js
>上一季度：moment().add(-1, 'Q').quarter()
>下一季度：moment().add(1, 'Q').quarter()
>```

#### Ⅸ- 获取当前日期是当年的第几周

>此函数是网上查阅资料,摘录整理进来
>
>```js
>/**
>     * 实现当前日期是当年的第几周,再向前和向后推几周
>     * js数组保存当前日期的前后两周(共五周的数据)
>     * */
>    let initSearchMajorChanges = function(vv){
>        //实现当前日期是当年的第几周,再向前和向后推几周,js数组保存当前日期的前后两周(共五周的数据)
>        let vNowDate=moment(new moment(vv).format("YYYY-MM-DD"));//.add('month',0).add('days',-1);
>        let vWeekOfDay=moment(vNowDate).format("E");//算出这周的周几
>        let vWeekOfDays=7-vWeekOfDay-1;
>        let vStartDate=moment(vNowDate).add('days',vWeekOfDays);
>        let vEndDate=moment(vNowDate).add('days',-vWeekOfDay);
>        let vStartDateNew=moment(vStartDate).add('days',7*$scope.gWeeks);
>        let vEndDateNew=moment(vEndDate).add('days',-(7*$scope.gWeeks));
>        searchMajorChanges(vStartDateNew,vEndDateNew);
>    }
>
>   initSearchMajorChanges('2021-06-06')
>
>```





### 2、设置时间

>`常被用做获取某一特定时间的moment`

#### Ⅰ- Set Time

>**`常用格式`**  --直接设置时间
>
>```js
>moment().year(Number), moment().month(Number)
>moment().set(String, Int)
>moment().set(Object)
>```
>
>- ##### 设置年份
>
> ```js
> moment().year(2019)
>
> moment().set('year', 2019)
>
> moment().set({year: 2019})
> ```
>
>- ##### 设置月份
>
> ```js
>moment().month(11) (0~11, 0: January, 11: December) moment().set('month', 11) 
> ```
>
>- ##### 设置某个月中的某一天
>
> ```js
> moment().date(15)
>
> moment().set('date', 15)
> ```
>
>- ##### 设置某个星期中的某一天
>
> ```js
> moment().weekday(0) // 设置日期为本周第一天（周日）
>
> moment().isoWeekday(1) // 设置日期为本周周一
>
> moment().set('weekday', 0) moment().set('isoWeekday', 1)
> ```
>
>- ##### 设置小时
>
> ```js
> moment().hours(12)
>
> moment().set('hours', 12)
> ```
>
>- ##### 设置分钟
>
> ```js
> moment().minutes(30)
>
> moment().set('minutes', 30)
> ```
>
>- ##### 设置秒数
>
> ```js
> moment().seconds(30)
>
> moment().set('seconds', 30)
> ```

#### Ⅱ- Add Time

>  **`常用格式`** --增加(符号时为减少) 时间
>
>  ```js
>  moment().add(Number, String)
>  moment().add(Object)
>  ```
>
>      - ##### 设置年份
>
>    ```js
>      moment().add(1, 'years')
>  
>      moment().add({years: 1})
>    ```
>
>  - ##### 设置月份
>
>    ```js
>      moment().add(1, 'months')
>    ```
>
>  - ##### 设置日期
>
>    ```js
>      moment().add(1, 'days')
>    ```
>
>  - ##### 设置星期
>
>    ```js
>      moment().add(1, 'weeks')
>    ```
>
>  - ##### 设置小时
>
>    ```js
>      moment().add(1, 'hours')
>    ```
>
>  - ##### 设置分钟
>
>    ```js
>      moment().add(1, 'minutes')
>    ```
>
>  - ##### 设置秒数
>
>    ```js
>      moment().add(1, 'seconds')
>    ```

#### Ⅲ- Subtract Time

>**`常用格式`** --往前多少的 时间
>
>```js
>moment().subtract(Number, String)
>
>moment().subtract(Object)
>```
>
>- ##### 设置年份
>
> ```js
> moment().subtract(1, 'years')
>
> moment().subtract({years: 1})
> ```
>
>- ##### 设置月份
>
> ```js
>moment().subtract(1, 'months')
> ```
>
>- ##### 设置日期
>
> ```js
>moment().subtract(1, 'days')
> ```
>
>- ##### 设置星期
>
> ```js
>moment().subtract(1, 'weeks')
> ```
>
>- ##### 设置小时
>
> ```js
>moment().subtract(1, 'hours')
> ```
>
>- ##### 设置分钟
>
> ```js
>moment().subtract(1, 'minutes')
> ```
>
>- ##### 设置秒数
>
> ```js
>moment().subtract(1, 'seconds')
> ```



### 3、格式化时间

>#### 格式:Format Time
>
>```js
>moment().format()
>moment().format(String)
>```
>
>- ##### 格式化年月日： 'xxxx年xx月xx日'
>
> ```js
>moment().format('YYYY年MM月DD日')
> ```
>
>- ##### 格式化年月日： 'xxxx-xx-xx'
>
> ```js
>moment().format('YYYY-MM-DD')
> ```
>
>- ##### 格式化时分秒(24小时制)： 'xx时xx分xx秒'
>
> ```js
>moment().format('HH时mm分ss秒')
> ```
>
>- ##### 格式化时分秒(12小时制)：'xx:xx:xx am/pm'
>
> ```js
>moment().format('hh:mm:ss a')
> ```
>
>- ##### 格式化时间戳(以秒为单位)
>
> ```js
>moment().format('X') // 返回值为字符串类型
> ```
>
>- ##### 格式化时间戳(以毫秒为单位)
>
> ```js
>moment().format('x') // 返回值为字符串类型
> ```

### 4、比较时间

>#### Difference
>
>```js
>moment().diff(Moment|String|Number|Date|Array)
>```
>
>- ##### 获取两个日期之间的时间差
>
> ```js
> let start_date = moment().subtract(1, 'weeks')
>
> let end_date = moment()
>
> end_date.diff(start_date) // 返回毫秒数 end_date.diff(start_date, 'months') // 0 end_date.diff(start_date, 'weeks') // 1 end_date.diff(start_date, 'days') // 7 start_date.diff(end_date, 'days') // -7
> ```



### 5、转化为JavaScript原生Date对象

>  ```js
>  moment().toDate()
>  new Date(moment())
>  ```
>
>  - 将Moment时间转换为JavaScript原生Date对象
>
>    ```js
>    let m = moment()
>      
>    let nativeDate1 = m.toDate()
>      
>    let nativeDate2 = new Date(m) String(nativeDate1) === String(nativeDate2) // true
>    ```

### 6、引入moment时使用中文

>在入口文件处引用即可显示中文
>
>```js
>import moment from 'moment';
>
>moment.locale('zh-cn');或者moment.lang('zh-cn');即可显示中文
>```



## 二、moment问题与解决

### Ⅰ-取出Moment格式中的具体时间报错(`TS报错`)

>1. 报错:`property '_d' does not exist on type 'moment'.`
>2. 出现错误原因分析:![image-20210422115014706](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E5%8F%96%E5%87%BAMoment%E6%A0%BC%E5%BC%8F%E4%B8%AD%E7%9A%84%E5%85%B7%E4%BD%93%E6%97%B6%E9%97%B4%E6%8A%A5%E9%94%99%E5%8E%9F%E5%9B%A0%E5%88%86%E6%9E%901.png)
>
>​	![image-20210422115208905](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/%E5%8F%96%E5%87%BAMoment%E6%A0%BC%E5%BC%8F%E4%B8%AD%E7%9A%84%E5%85%B7%E4%BD%93%E6%97%B6%E9%97%B4%E6%8A%A5%E9%94%99%E5%8E%9F%E5%9B%A0%E5%88%86%E6%9E%902.png)
>
>3. 解决
>
> 4. 其实不用`_d`去取出来,Moment格式有相应的取出方法
>
>    ![image-20210422115825841](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210422115825841.png)



### Ⅱ- TS定义时间格式

>1. 应用场景:当我使用Antd的时间选择框时需要给其绑定的时间限制Ts格式(不设置的时候会报红),这时候就可以用monent自带的格式
>
>   ![image-20210412191035956](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210412191035956.png) 
>
>2. 应用代码
>
>  ```tsx
>//1. 导入
>import { Moment } from 'moment';
>//2. 定义类型接口
>interface ISearchParams {
>  storeId: any;
>  agentId: any;
>  status: string;
>  regDate: [Moment, Moment];
>  creDate: [Moment, Moment];
>  format: string;
>  loading: boolean;
>  listLoading: boolean;
>}
>//3. 将定义好的ts格式赋进去
> searchParams: ISearchParams = {
>    storeId: '',
>    agentId: '',
>    status: null,
>    regDate: undefined,
>    creDate: undefined,
>    format: 'YYYY-MM-DD',
>    loading: false,
>    listLoading: false,
>  };
>  ```





# 十一、将Json数据导出Excel 文件







## Ⅰ-代码示例与注释

>```jsx
>//1、定义导出文件名称
>var filename = "write.xlsx";
>// 定义导出数据 此处需传入数组类型的数据
>var data = dataSource
>// 定义excel文档的名称
>var ws_name = "SheetJS";
>// 初始化一个excel文件
>var wb = XLSX.utils.book_new();
>// 初始化一个excel文档，此时需要传入数据
>var ws = XLSX.utils.aoa_to_sheet(data);
>// 将文档插入文件并定义名称
>XLSX.utils.book_append_sheet(wb, ws, ws_name);
>// 执行下载
>XLSX.writeFile(wb, filename);
>
>//自己模拟服务端数据
>const dataSource = [
>{
>agentTotalAmt: '999',
>agentId: 'hongjilin',
>name: '努力学习的汪',
>cooperationStatus: 2,
>month: '202106',
>totalCompany: 666,
>qty: 999,
>increaQty: 666,
>totalAmt: 9999,
>incomeType: '收款方式',
>algorithm: '帅的很',
>},
>{
>agentTotalAmt: '888',
>agentId: 'jilinhong',
>name: '特别努力学习的单身汪',
>cooperationStatus: 2,
>month: '202107',
>totalCompany: 666,
>qty: 1111,
>increaQty: 111,
>totalAmt: 1111,
>incomeType: '收款方式',
>algorithm: '可怜得很',
>},
>];
>```
>
>使用xlse导出文件时，json数据需要转换为数组，通常为二维数组，通常第一行为表头，如：***`['第一列','第二列','第三列']`\***，然后就是使用xlse的步骤了，通常分为如下几个步骤：
>
>1、调用XLSX.utils.book_new()初始化excel文件。
>
>2、调用XLSX.utils.aoa_to_sheet(data),初始化excel文档，此时需要传入数据，数据为二维数组，第一行通常为表头。
>
>3、调用XLSX.utils.book_append_sheet(wb, ws, ws_name)，将文档插入excel文件，并为文档命名。
>
>4、调用XLSX.writeFile(wb, filename)下载excel文件，并为excel文件命名。

## Ⅱ-本人在自己React中使用

>本人项目代码中会多处使用该导出功能,所以会进行封装
>
>1. 工具包封装(函数实现主体)
>
> ```tsx
>import XLSX from 'xlsx';
>class Tool {
>  /**
>   * 导出成XLSX文件
>   * @param dataSource  传入的对象数组
>   * @param fileName  生成的文件名
>   * @param title 设置列名,如果不传入则默认将对象数组的key当作表头
>   */
>  OnExport = (dataSource: Array<object>, fileName: string, title?: any) => {
>    //当传入的数组长度为0,直接退出  此处加[?]是因为防错,防止真有人乱传参数
>    //[!dataSource ]是防止传入undefined导致函数执行错误
>     if (!dataSource || dataSource?.length == 0) return;
>    let data = dataSource;
>    let head = Object.keys(data[0]);
>    //取出json格式数据中的[value]值
>    data = data.map((e) => Object.values(e));
>    //如果不传入[title],则用keys当表头  
>    data.unshift(title || head);
>    //文件名
>    let filename = `${fileName}.xlsx`;
>    // let ws_name = "xxx";
>    let wb = XLSX.utils.book_new();
>    let ws = XLSX.utils.aoa_to_sheet(data);
>    XLSX.utils.book_append_sheet(wb, ws);
>    XLSX.writeFile(wb, filename);
>  };
>}
>export const tool = new Tool();
>export default Tool;
> ```
>
>2. 调用
>
> ```jsx
> //导入工具包
> import { Tool } from '~/utils';
> const tools = new Tool();
>
> //[this.manage.date]是一个时间数据
> //[this.datas]是要导出的数据  -->通常是服务端给定的数据,经过我们处理后成为如[Ⅰ]中示例代码的那种格式
>
>  exportXlsx = () => {
>      //用于拼接月份
>    const month = this.manage.date.format('MM');
>    /*此处是列表头要渲染成中文,自定义列表头写法
>    let titles = Object.keys(this.datas[0]).map((key) => DATAS[key]);
>     console.log(titles, "titlestitlestitles")'
>     tools.OnExport(toJS(this.datas), `${month}月份的数据表`,titles);
>     */
>     //没有数据能导出时给出提示  -->此处调用的是封装好的[信息提示]组件,同学们可以忽略此行代码
>    if (this.datas?.length == 0)  SuperNotification.warning({  msg: '无数据可导出'});
>    //调用工具函数
>    tools.OnExport(toJS(this.datas), `${month}月份的数据表`);
>  };
>
> --------------- 将其绑定于点击事件上 ----------------------------------------
>  <Button type="primary"  onClick={() => { store.exportXlsx(); }} >
>    导出
>  </Button>
> ```
>
> [`this.manage.date`]是一个时间数据
> [`this.datas`]是要导出的数据  -->通常是服务端给定的数据,经过我们处理后成为如[`Ⅰ`]中示例代码的假数据那种格式

## Ⅲ-成功截图示例

>1. 点击导出下载成功
>
>  ![image-20210721154328134](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210721154328134.png)  
>
>  当然,有的浏览器是直接下载不会给出下载提示
>
>2. xlsx文件查看![image-20210721154626462](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210721155153046.png)
>
>3. OK了,其实不止在`React`中能使用,在`Vue`甚至原生js都可以调用这个函数







# 十二、OtherKnowledge

## localStorage  

只读的`localStorage` 属性允许你访问一个[`Document`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 源（origin）的对象 [`Storage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Storage)；其存储的数据能在跨浏览器会话保留。`localStorage` 类似 [`sessionStorage`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/sessionStorage)，但其区别在于：存储在 `localStorage` 的数据可以长期保留；而当页面会话结束——也就是说，当页面被关闭时，存储在 `sessionStorage` 的数据会被清除 。  



## eval() 

```
用来执行一段字符串形式的JS代码，并将执行结果返回，如果使用eval()执行的字符串中含有{},它会将{}当成是代码块，不希望将其当成代码块解析，则需要在字符串前后各加一个()

 eval()这个函数的功能很强大，可以直接执行一个字符串中的js代码， 但是在开发中尽量不要使用，首先它的执行性能比较差，然后它还具有安全隐患 
```



```js
var str = '{"name":"孙悟空","age":18,"gender":"男"}';  
var obj = eval("("+str+")");  
```

### 编码  

```html  
<!DOCTYPE html>  
<html>  
	<head>  
		<meta charset="UTF-8">  
		<title></title>  
		<script type="text/javascript">  
			  
			/*  
			 * 在字符串中使用转义字符输入Unicode编码  
			 * 	\u四位编码  
			 */  
			console.log("\u2620");	  
		</script>  
	</head>  
	<body>		  
		<!--在网页中使用Unicode编码  
			&#编码; 这里的编码需要的是10进制  
		-->  
		<h1 style="font-size: 200px;">&#9760;</h1>  
		<h1 style="font-size: 200px;">&#9856;</h1>		  
	</body>  
</html>  
  
```

`confirm()`用于弹出一个带有确认和取消按钮的提示框，需要一个字符串作为参数，该字符串将会作为提示文字显示出来 ，如果用户点击确认则会返回true，如果点击取消则返回false 

```js
var flag = confirm("确认删除"+name+"吗?");  
```



## 原生js  

## 原生js实现复制内容到剪切板  

```js  
copy() {  
    const input = document.createElement("input");  
    document.body.appendChild(input);  
    input.setAttribute("value",this.solution.code);  
    input.select();  
    if (document.execCommand("copy")) {  
        document.execCommand("copy");  
        // console.log("复制成功");  
    }  
    document.body.removeChild(input);  
}  
```



## JS运行机制

###  预解析

- js引擎会把 js 里面所有的`var` 和`function`  提升到当前作用域的最前面

- 变量提升：将所有变量声明提升到当前作用域的最前面，不进行赋值
- 函数提升：将所有函数声明提升到当前作用域的最前面，不进行调用



### 代码执行

- 按照书写的顺序从上往下执行 















