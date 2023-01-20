> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

[转载大佬笔记，添加个人笔记](https://github.com/JERRY-Z-J-R/I-love-you-3-thousand/tree/master/%E6%88%91%E7%88%B1%E4%BD%A0%EF%BC%8C%E4%B8%8D%E6%AD%A2%E4%B8%89%E5%8D%83%E9%81%8D/HTML%20CSS)



# 一、CSS简介

**CSS 的主要使用场景就是布局网页，美化页面的。**

## 1.1 HTML的局限性

HTML 只关注内容的语义，虽然 HTML 可以做简单的样式，但是带来的是无尽的臃肿、繁琐和难以维护

## 1.2 CSS网页的美容师

CSS 是 `层叠样式表` 的简称。

有时我们也会称之为 `CSS样式表` 或 `级联样式表`。

CSS 也是一种 `标记语言`。

CSS 主要用于设置 HTML 页面中的文本样式（字体、大小、颜色、对齐方式……）、图片样式（宽高、边框样式、边距……）以及版面的布局和外观显示样式。

CSS 让我们的网页更加丰富多彩，布局更加灵活自如，简单理解：CSS 可以美化 HTML，让 HTML 更漂亮，同时让页面布局更简单。

**总结：**

- HTML 搭建结构，填入元素内容
- CSS 美化 HTML，布局网页元素
- CSS 最大价值：由 HTML 专注去做结构呈现，样式交给 CSS，即：**结构 与 样式 分离**

## 1.3 CSS语法规范

使用 HTML 时，需要遵从一定的规范，CSS 也是如此，要想熟练地使用 CSS 对网页进行修饰，首先需要了解 CSS 样式规则。

CSS 规则由两个主要的部分构成：`选择器` 以及 `一条或多条声明`。

- `选择器` 是用于选出需要设置 CSS 样式的 HTML 标签，选择器后跟的**花括号**内是对该对象设置的具体样式
- `属性` 和 `属性值` 以 “键值对” 的形式出现 `属性: 属性值;`
- 属性是对指定的对象设置的样式属性，例如：字体大小、文本颜色等
- 属性和属性值之间用英文 `:` 分开
- 多个 “键值对” 之间用英文 `;` 进行区分（末尾的键值对可以不加 `;`）

所有的样式，都包含在 `<style>` 标签内，表示是样式表。

`<style>` 一般写到 `</head>` 里。

```html
<head>
    <style type="text/css">
        h4 {
            color: bule;
            font-size: 100px;
        }
    </style>
</head>
```

注意：`<style>` 标签可以写到其他标签内部并作用与该标签区域内，但是强烈不推荐这种写法！

> `type="text/css"` 可以省略。





实例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!-- css控制 -->
    <style>
        /* 找到对应的标签名称,后续通过设置选择器来改变对应的样式 */
        p{
            /* 字体颜色 */
            color: brown;
            /* 添加背景颜色 */
            background-color: blue;
            width: 500px;
            height: 50px;
        }

    </style>


</head>
<body>
    <p>css和html 之间的联系</p>
</body>
</html>
```



![image-20221023162933409](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221023162933409.png)

## 1.4 CSS代码风格

### 1.4.1 样式格式书写

- 紧凑格式（不推荐）

```css
h3 { color: deeppink; font-size: 20px; }
```

- 展开格式（**推荐**）

```css
h3 {
	color: deeppink;
	font-size: 20px;
}
```

强烈推荐第二种格式，因为更直观！不用担心占用空间，因为后期可以通过代码压缩工具来压缩代码。

### 1.4.2 样式大小书写

- 大写（不推荐）

```css
H3 {
	COLOR: PINK;
}
```

- 小写（**推荐**）

```css
h3 {
	color: pink;
}
```

强烈推荐样式选择器，属性名，属性值关键字**全部使用小写字母**，特殊情况除外。

> 凡是你不确定是否用大写的都一律用小写就对了！

### 1.4.3 空格规范

```css
h3 {
	color: pink;
}
```

- **属性值前面**，**冒号后面**，保留一个空格
- **选择器（标签）和前花括号中间**，保留一个空格

# 二、CSS基础选择器

## 2.1 CSS选择器的作用

选择器就是根据不同的需求把不同的标签选出来，这就是选择器的作用，简单来说，就是：选择标签用的。

```css
h1 {
	color: red;
	font-size: 25px;
}
```

以上 CSS 做了两件事：

- 找到所有的 h1 标签。（选对人）
- 设置这些标签的样式：颜色为红色、字体大小为 25 像素。（做对事）

## 2.2 选择器的分类

选择器分为 `基础选择器` 和 `复合选择器` 两个大类，本文首先介绍一下基础选择器。

- 基础选择器是由 `单个` 选择器组成的
- 基础选择器（以下四种）
  1. 标签选择器 （使用标签名 引用）
  2. 类选择器 （使用 `.`）
  3. id选择器 （使用 `#`）
  4. 通配符选择器 


## 2.3 标签选择器

`标签选择器`（元素选择器）是指用 HTML 标签名称作为选择器，按标签名称分类，为页面中某一类标签指定统一的 CSS 样式。

**语法：**

```css
标签名 {
	属性1: 属性值1;
	属性2: 属性值2;
	属性3: 属性值3;
	...
}
```

**作用：**

标签选择器可以把某一类标签全部选择出来，比如所有的 `<div>` 标签和所有的 `<span>` 标签。

**优点：**

能快速为页面中同类型的标签统一设置样式。

**缺点：**

不能设计差异化样式，只能选择全部的当前标签。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之标签选择器</title>
    <style type="text/css">
        /* 会对所有的该标签元素运用样式，优点：快速统一，缺点：无法差异化设置 */
        p {
            color: green;
        }

        div {
            color: pink;
        }
    </style>
</head>

<body>
    <p>男</p>
    <p>男</p>
    <p>男</p>
    <div>女生</div>
    <div>女生</div>
    <div>女生</div>
</body>

</html>
```

## 2.4 类选择器

如果想要差异化选择不同的标签，单独选一个或者某几个标签，可以使用 `类选择器` 。

**CSS 语法：**

```css
.类名 {
	属性1: 属性值1;
	...
}
```

例如：将所有拥有 red 类的 HTML 元素均设置为红色。

```css
.red {
	color: red;
}
```

**HTML 语法：**

```html
<div class="red">变红色</div>
```

类选择器在 HTML 中以 class 属性表示，在 CSS 中，类选择器以一个 `.` 号显示。

**注意：**

- 类选择器使用 `.`（英文点号）进行标识，后面紧跟类名（自定义，我们自己命名的）
- 可以理解为给这个标签起了一个别名来表示
- 长名称或词组可以使用**中横线** `-` 来为类命名
- 不能使用已有的关键字作为类名
- 不要使用纯数字、中文等命名，尽量使用英文字母来表示
- 命名要见名知意（**可读性第一，长度第二，推荐使用英语，如果是使用拼音请使用全拼**）
- 命名规范：见附件（CSS 命名规范.md）

记忆口诀：**样式点定义**，**结构类调用**，**一个或多个**，**开发最常用**。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之类选择器</title>
    <style type="text/css">
        /* 类选择器口诀：样式 . 定义，结构 class 调用，一个或多个，开发最常用 */
        .red {
            width: 100px;
            height: 100px;
            background-color: red;
        }

        .green {
            width: 100px;
            height: 100px;
            background-color: green;
        }
    </style>
</head>

<body>
    <div class="red"></div>
    <div class="green"></div>
    <div class="red"></div>
</body>

</html>
```

**类选择器——多类名**

我们可以给一个标签指定多个类名，从而达到更多的选择目的，这些类名都可以选出这个标签，简单理解就是一个标签有多个名字。

- 在标签 class 属性中写多个类名
- 多个类名中间必须用 `空格` 分开
- 这个标签就可以分别具有这些类名的样式

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之类选择器</title>
    <style type="text/css">
        /* 一个标签可以运用多个类选择器，之间用空格隔开 */
        .red {
            color: red;
        }

        .font35 {
            font-size: 35px;
        }
    </style>
</head>

<body>
    <div class="red font35">kcs</div>
</body>

</html>
```

**多类名开发中使用场景**

- 可以把一些标签元素相同的样式（共同的部分）放到一个类里面
- 这些标签都可以调用这个公共的类，然后再调用自己独有的类
- 从而节省 CSS 代码，统一修改也非常方便（**模块化、可重用化**）

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之类选择器</title>
    <style type="text/css">
        /* 类选择器最大的优势在于：复用 */
        .box {
            width: 100px;
            height: 100px;
        }

        .red {
            background-color: red;
        }

        .green {
            background-color: green;
        }
    </style>
</head>

<body>
    <div class="box red"></div>
    <div class="box green"></div>
    <div class="box red"></div>
</body>

</html>
```

多类名选择器在后期布局比较复杂的情况下，是使用得较多的。

## 2.5 id选择器

id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。

HTML 元素以 id 属性来设置 id 选择器，CSS 中 id 选择器以 `#` 来定义。

**语法：**

```css
#id名 {
	属性1: 属性值1;
	...
}
```

**例如：**将 id 为 nav 元素中的内容设置为红色。

```css
#nav {
	color: red;
}
```

**注意：**id 属性只能在每个 HTML 文档中出现一次。

**口诀：**样式 `#` 定义，结构 `id` 调用，只能调用一次，别人切勿使用。

**id 选择器和类选择器的区别：**

- 类选择器 (class) 好比人的名字，一个人可以有多个名字，同时一个名字也可以被多个人使用
- id 选择器好比人的身份证号码，全中国是唯一的，不可重复（同一个 id 选择器只能调用一次）
- id 选择器和类选择器最大的不同在于使用次数上
- 类选择器在修改样式中用的最多，id 选择器一般用于页面唯一性的元素上，经常和 JavaScript 搭配使用

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之id选择器</title>
    <style type="text/css">
        /* id 选择器口诀：样式 # 定义，结构 id 调用，只能调用一次，别人切勿使用 */
        #pink {
            color: pink;
        }
    </style>
</head>

<body>
    <div id="pink">kcs</div>
</body>

</html>
```

再次强调：**同一 id 只能定义一次，同一 id 选择器也只能调用一次！**（对于 CSS 修改样式来说，最好使用类选择器，id 选择器主要与后面的 JS 搭配使用）。

## 2.6 通配符选择器

在 CSS 中，通配符选择器使用 `*` 定义，它表示选取页面中**所有元素**（标签）。

**语法：**

```css
* {
	属性1: 属性值1;
	...
}
```

- 通配符选择器不需要调用，自动就给所有的元素使用样式
- 特殊情况才使用，后面讲解使用场景

```css
// 利用通配符选择器清除所有的元素标签的内外边距，后期讲
* {
	margin: 0;
	padding: 0;
}
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>基础选择器之通配符选择器</title>
    <style type="text/css">
        /* * 给 html 标签所有的元素都使用样式，并且这个过程是自动完成的，不需要手动调用 */
        * {
            color: red;
        }
    </style>
</head>

<body>
    <div>我的</div>
    <span>我的</span>
    <ul>
        <li>还是我的</li>
    </ul>
</body>

</html>
```

## 2.7 基础选择器总结

| 基础选择器   | 作用                            | 特点                                                  | 使用情况       | 用法                 |
| ------------ | ------------------------------- | ----------------------------------------------------- | -------------- | -------------------- |
| 标签选择器   | 可以选出所有相同的标签，比如：p | 不能差异化选择                                        | 较多           | `p {color: red;}`    |
| 类选择器     | 可以选出 1 个或者 多个 标签     | 可以根据需求选择                                      | 非常多         | `.nav {color: red;}` |
| id 选择器    | 一次只能选择 1 个标签           | ID 属性只能在每个 HTML 文档中出现一次，也只能调用一次 | 一般和 js 搭配 | `#nav {color: red;}` |
| 通配符选择器 | 选择所有的标签                  | 选择的太多，有部分不需要                              | 特殊情况使用   | `* {color: red;}`    |

- 每个基础选择器都有使用场景，都需要掌握
- 如果是修改样式，类选择器是使用最多的









# 三、CSS字体属性

CSS Fonts（字体）属性用于定义：`字体系列`、`大小`、`粗细`、和 `文字样式`（如：斜体）。

## 3.1 字体系列

CSS 使用 font-family 属性定义文本的字体系列。

```css
p {
	font-family: "Microsoft YaHei";
}

div {
	font-family: Arial, "Microsoft YaHei";
}
```

- 各种字体之间必须使用英文状态下的逗号隔开
- 一般情况下，如果有空格隔开的多个单词组成的字体，加引号
- 尽量使用系统默认自带字体，保证在任何用户的浏览器中都能正确显示
- 最常用的字体：`body {font-family: "Microsoft YaHei", tahoma, arial, sans-serif, "Hiragino Sans GB";}`

> B站官网字体：
>
> ```css
> body {
>     font-family: -apple-system,BlinkMacSystemFont,Helvetica Neue,Helvetica,Arial,PingFang SC,Hiragino Sans GB,Microsoft YaHei,sans-serif!important;
> }
> ```

> Apple 官网字体：
>
> ```css
> body {
> 	font-family: "SF Pro SC", "SF Pro Text", "SF Pro Icons", "PingFang SC", "Helvetica Neue", "Helvetica", "Arial", sans-serif
> }
> ```

> Instagram 官网字体：
>
> ```css
> body {
> 	font-family: -apple-system, BlinkMacSystemFont,"Segoe UI", Roboto, Helvetica, Arial, sans-serif
> }
> ```

>知乎官网字体：
>
>```css
>body {
>	font-family: -apple-system, BlinkMacSystemFont, Helvetica Neue, PingFang SC, Microsoft YaHei, Source Han Sans SC, Noto Sans CJK SC, WenQuanYi Micro Hei, sans-serif
>}
>```

> 爱奇艺官网字体：
>
> ```css
> body {
> font-family: PingFangSC-Regular, Helvetica, Arial, Microsoft Yahei, sans-serif
> }
> ```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之字体系列</title>
    <style type="text/css">
        /* 浏览器会从第一个字体开始进行适配，如果本机可以适配的话，那么就使用该字体，否则看下一个字体，
           如果都不可以，那么浏览器会使用自带的默认字体，所以实际开发中一般建议使用比较标准化的字体 */
        h2 {
            /* font-family: '微软雅黑'; 可以使用中文，但不建议 */
            font-family: "Microsoft YaHei", Arial, sans-serif;
        }

        p {
            font-family: "Times New Roman", Times, serif;
        }
    </style>
</head>

<body>
    <h2>个人介绍</h2>
    <p>姓名：十二</p>
    <p>生日：2001.12.01</p>
    <p>性别：男</p>
    <p>婚姻状况：恋爱</p>
</body>

</html>
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之字体系列</title>
    <style type="text/css">
        /* 一些情况下，如果要全局设置字体可以直接在 body 标签选择器中指明 */
        body {
            font-family: "Microsoft YaHei", Arial, sans-serif;
        }
    </style>
</head>

<body>
    <h2>个人介绍</h2>
    <p>姓名：十二</p>
    <p>生日：2001.12.01</p>
    <p>性别：男</p>
    <p>婚姻状况：恋爱</p>
</body>

</html>
```

注意：浏览器字体是依据用户操作系统来调用的，所以这里介绍一种 Windows 系统安装字体的方法。

> 当然实际开发中通常浏览器请求时，会把字体文件随 HTML CSS JS 等一同传送到客服端。



## 3.2 字体大小

CSS 使用 font-size 属性定义字体大小。

```css
p {
	font-size: 20px;
}
```

- px（像素）大小是我们网页的最常用的单位
- 谷歌浏览器默认的文字大小为：16px
- 不同浏览器可能默认显示的字号大小不一致，我们尽量给一个明确值大小，不要默认大小
- 可以给 body 指定整个页面文字的大小

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之字体大小</title>
    <style type="text/css">
        /* 全局设置时，一般在 body 标签选择器中指定文字大小，谷歌浏览器默认 16px，
           但是最好还是指定一个明确值，以保证在不同浏览器中的效果是一样的 */
        body {
            font-size: 24px;
        }

        /* 标题标签比较特殊，body 中的设置对其是不生效的，需要单独指定文字大小 */
        h2 {
            font-size: 54px;
        }
    </style>
</head>

<body>
    <h2>个人介绍</h2>
    <p>姓名：十二</p>
    <p>生日：2001.12.01</p>
    <p>性别：男</p>
    <p>婚姻状况：恋爱</p>
</body>

</html>
```

## 3.3 字体粗细

CSS 使用 font-weight 属性设置文本字体的粗细。

```css
p {
	font-weight: bold;
}
```

| 属性值    | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| `normal`  | 默认值（不加粗的）                                           |
| `bold`    | 定义粗体（加粗的）                                           |
| `100-900` | 400 等同于 normal，而 700 等同于 bold，其它值一般不使用，注意这个数字后面不跟单位 |

- 学会让加粗标签（比如 h 和 strong 等）变为不加粗，或者让其他标签加粗
- 实际开发时，我们更喜欢用数字表示粗细

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之字体粗细</title>
    <style type="text/css">
        .bold {
            /* font-weight: bold; */
            /* 实际开发中，我们更提倡使用数字来表示加粗的效果 */
            /* 这个 700 的后面不要跟单位 */
            font-weight: 700;
        }

        /* 使文字不加粗 */
        h2 {
            /* font-weight: normal; */
            font-weight: 400;
        }
    </style>
</head>

<body>
    <h2>个人介绍</h2>
    <p>姓名：十二</p>
    <p>生日：2001.12.01</p>
    <p>性别：男</p>
    <p class="bold">婚姻状况：恋爱</p>
</body>

</html>
```

## 3.4 文字样式

CSS 使用 font-style 属性设置文本的风格。

```css
p {
	font-style: normal;
}
```

| 属性值   | 作用                                                   |
| -------- | ------------------------------------------------------ |
| `normal` | 默认值，浏览器会显示标准的字体样式 font-style: normal; |
| `italic` | 浏览器会显示斜体的字体样式                             |

**注意：**平时我们很少给文字加斜体，反而要给斜体标签 (em、i) 改为不倾斜字体。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之字体样式（风格）</title>
    <style type="text/css">
        p {
            /* 让不倾斜的字体倾斜 */
            font-style: italic;
        }

        em {
            /* 让倾斜的字体不倾斜 */
            font-style: normal;
        }
    </style>
</head>

<body>
    <p>上课时候的你</p>
    <em>下课时候的你</em>
</body>

</html>
```

## 3.5 字体复合属性

字体属性可以把以上文字样式综合来写，这样可以更节约代码。

```css
body {
	font: font-style font-weight font-size/line-height font-family;
  /*字体是否倾斜 字体加粗 字体大小，字体种类*/
}

body {
	font: normal 400 font-size/line-height "Microsoft YaHei", Arial, sans-serif;
}
```

- 使用 font 属性时，必须按上面语法格式中的==顺序书写==，不能更换顺序，并且各个属性间以空格隔开

- 不需要设置的属性可以省略（取默认值），但必须保留 font-size 和 font-family 属性，否则 font 属性将不起作用

  ```css
  font: 20px 'Microsoft YaHei';
  ```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS字体属性之复合属性</title>
    <style type="text/css">
        /* 想要 div 文字变倾斜、加粗、字号设置为 16 像素，并且是微软雅黑 */
        div {
            /* font-style: italic;
               font-weight: 700;
               font-size: 16px;
               font-family: 'Microsoft YaHei'; */

            /* 复合属性：简写的方式，里面的顺序不能打乱 以空格隔开 */
            /* font: font-style font-weight font-size/line-height font-family; */
            font: italic 700 16px 'Microsoft YaHei';
        }
    </style>
</head>

<body>
    <div>三生三世十里桃花，一心一意百行代码</div>
</body>

</html>
```

## 3.6 字体属性总结

| 属性          | 表示     | 注意点                                                       |
| ------------- | -------- | ------------------------------------------------------------ |
| `font-size`   | 字号     | 我们通常用的单位是 px 像素，一定要跟上单位                   |
| `font-family` | 字体     | 实际工作中按照团队约定来写字体                               |
| `font-weight` | 字体属性 | 记住加粗是 700 或者 bold 不加粗 是 normal 或者 400 记住数字不要跟单位 |
| `font-style`  | 字体样式 | 记住倾斜是 italic 不倾斜是 normal 工作中我们最常用 normal    |
| `font`        | 字体连写 | 1、字体连写是有顺序的不能随意换位置，2、其中字号和字体必须同时出现 |



层叠性：后面的属性值覆盖前面的属性值





# 四、CSS文本属性

CSS Text（文本）属性可定义文本的 `外观`，比如：`文本颜色`、`文本对齐`、`文本装饰`、`文本缩进`、`行间距` 等。

## 4.1 文本颜色

`color` 属性用于定义文本的颜色。

```css
div {
	color: red;
}
```

| 表示方式       | 属性值                                              |
| -------------- | --------------------------------------------------- |
| 预定义的颜色值 | red，green，blue，black，white，gray                |
| 十六进制       | #FF0000，#FF6600，#29D794（每两位对应：#红R绿G蓝B） |
| RGB 代码       | rgb(255, 0, 0) 或 rgb(100%, 0%, 0%)                 |

**注意：**开发中最常用的是十六进制。

> 熟记开发常用色：
>
> 黑色：`black`、`#000000`、`rgb(0, 0, 0)`（三原色啥也没有混合就为黑）
>
> 白色：`white`、`#FFFFFF`、`rgb(255, 255, 255)`（三原色全满混合就为白）
>
> 灰色：`gray`、`#808080`、`rgb(128, 128, 128)`（三原色全半混合就为灰）
>
> 红色：`red`、`#FF0000`、`rgb(255, 0, 0)`
>
> 绿色：`green`、`#008000`、`rgb(0, 128, 0)`（绿色较为特殊，green 对应的是 #008000）
>
> 蓝色：`blue`、`#0000FF`、`rgb(0, 0, 255)`
>
> 黄色：`yellow`、`#FFFF00`、`rgb(255, 255, 0)`
>
> 青色：`#00FFFF`、`rgb(0, 255, 255)`
>
> 洋红：`#FF00FF`、`rgb(255, 0, 255)`
>
> 橙色：`orange`
>
> 粉色：`pink`
>
> 烈粉色：`hotpink`（浓度低）、`deeppink`（浓度高）
>
> 天蓝色：`skyblue`
>
> 深色系：`dark颜色` 如：`darkgreen`
>
> 浅色系：`light颜色` 如：`lightgreen`

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观属性之文本颜色</title>
    <style type="text/css">
        div {
            /* color: deeppink; */
            /* color: #FF1493; 最常用 */
            color: rgb(255, 20, 147);
        }
    </style>
</head>

<body>
    <div>pink</div>
</body>

</html>
```



## 4.2 文本对齐

`text-align` 属性用于设置元素内文本内容的水平对齐方式。

```css
div {
	text-align: center;
}
```

| 属性值 | 解释             |
| ------ | ---------------- |
| left   | 左对齐（默认值） |
| rigth  | 右对齐           |
| center | 居中对齐         |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观之文本对齐</title>
    <style type="text/css">
        h1 {
            /* 本质是让 h1 盒子里面的文字水平居中对齐 */
            /* text-align: center; */
            text-align: right;
        }
    </style>
</head>

<body>
    <h1>右对齐的标题</h1>
</body>

</html>
```

注意：

`text-align` 属性只能作用于 `块级元素`，并让该块级元素内的 `行内元素` 实现居中（不一定是文字,还可以是图片等其他内容设置对其方式）。

上述例子中：h1 为块级元素，所以给 h1 设置 text-align，便会作用于里面的文本（如果里面还有行内元素的话，也会一同作用）。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观之文本对齐</title>
    <style type="text/css">
        div {
            text-align: center;
        }
    </style>
</head>

<body>
   <div>
	   <p>kkkssccc</p>
   </div>
</body>

</html>
```

上述例子中：为 div 设置 text-align 之所以能够使其内部的块级元素 p 里的文字居中，原因是 p 会继承父元素 div 的 text-align 属性，所以相当于对 p 设置了 text-align。

## 4.3 文本装饰

`text-decoration` 属性规定添加到文本的修饰，可以给文本添加 `下划线`、`删除线`、`上划线` 等。

```css
div {
	text-decoration: underline;
}
```

| 属性值         | 描述                              |
| -------------- | --------------------------------- |
| `none`         | 默认，没有装饰线（**最常用**）    |
| `underline`    | 下划线，链接 a 自带下划线（常用） |
| `overline`     | 上划线（几乎不用）                |
| `line-through` | 删除线（不常用）                  |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观之文本装饰</title>
    <style type="text/css">
        /* 默认为 none 没有装饰 */
        div {
            /* 上划线 几乎不用 */
            /* text-decoration: overline; */
            /* 删除线 不常用 */
            /* text-decoration: line-through; */
            /* 下划线 常用，链接 a 自带下划线 */
            text-decoration: underline;
        }

        a {
            /* 取消 a 默认的下划线 */
            text-decoration: none;
            color: #333333;
        }
    </style>
</head>

<body>
    <div>记录笔记博客</div>
    <a href="https://shier-blog.vercel.app/">JERRY</a>
</body>

</html>
```

## 4.4 文本缩进

`text-indent` 属性用来指定文本的第一行的缩进，通常是将段落的首行缩进。

```css
div {
	text-indent: 10px;
}
```

通过设置该属性，所有元素的第一行都可以缩进一个给定的长度，甚至该长0可以是负值。

```css
p {
	text-indent: 2em;
}
```

em 是一个相对单位，就是当前元素 (font-size) 1 个文字的大小，如果当前元素没有设置大小，则会按照父元素的 1 个文字大小。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观之文本缩进</title>
    <style type="text/css">
        p {
            font-size: 24px;
            /* 文本的首行缩进多少距离，不仅可以为正值，还可以为负值 */
            /* text-indent: 20px; */
            /* em 为相对于当前元素的大小单位 */
            text-indent: 2em;
        }
    </style>
</head>

<body>
    <p>打开北京、上海与广州的地铁地图，你会看见三张纵横交错的线路网络，
        这代表了中国最成熟的三套城市轨道交通系统</p>

    <p>可即使是这样，在北上广生活的人依然少不了对地铁的抱怨，其中谈及最多的问题便是拥挤，
        对很多人而言，每次挤地铁的过程，都像是一场硬仗。更何况，还都是败仗居多。</p>

    <p>那么，当越来越多的二线甚至三线城市迎接来了自己的地铁，中国哪里的地铁是最拥挤的呢？</p>
</body>

</html>
```

## 4.5 行间距（行高）

`line-height` 属性用于设置行间的距离（行高），可以控制文字行与行之间的距离。

```css
p {
	line-height: 26px;
}
```

- `行间距 = 上间距 + 文本高度 + 下间距`

- `上下间距 = （行间距 - 文本高度）/ 2`

- `文本高度 = font-size`

  ![image-20221024101743196](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221024101743196.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS文本外观之行间距</title>
    <style type="text/css">
        /* 行间距 = 上间距 + 文本高度 + 下间距 */
        /* 行间距 = 行高 */
        /* 文本高度 = 字体像素大小 */
        /* 上下间距 = （行间距 - 文本高度）/ 2 */
        p {
            line-height: 25px;
        }
    </style>
</head>

<body>
    <p>打开北京、上海与广州的地铁地图，你会看见三张纵横交错的线路网络，
        这代表了中国最成熟的三套城市轨道交通系统</p>

    <p>可即使是这样，在北上广生活的人依然少不了对地铁的抱怨，其中谈及最多的问题便是拥挤，
        对很多人而言，每次挤地铁的过程，都像是一场硬仗。更何况，还都是败仗居多。</p>

    <p>那么，当越来越多的二线甚至三线城市迎接来了自己的地铁，中国哪里的地铁是最拥挤的呢？</p>
</body>

</html>
```

补充：行间距测量技巧：上一行文字的底部与本行文字的底部之间的距离就是行间距。

font 复合属性

```css
font: style weight size/line-height family;
		/* 倾斜  加粗 大小/行高 字体  */ 
```



## 4.6 文本属性总结

| 属性              | 表示     | 注意点                                                       |
| ----------------- | -------- | ------------------------------------------------------------ |
| `color`           | 文本颜色 | 我们通常用 十六进制 而且通常是简写形式 #fff（6 个一样可以简写） |
| `text-align`      | 文本对齐 | 可以设定文字水平的对齐方式                                   |
| `text-indent`     | 文本缩进 | 通常我们用于段落首行缩进2个字的距离 text-indent: 2em;        |
| `text-decoration` | 文本修饰 | 牢记 添加下划线 underline 取消下划线 none                    |
| `line-height`     | 行高     | 控制行与行之间的距离                                         |

# 五、CSS引入方式

## 5.1 CSS的三种引入方式

按照 CSS 样式书写的位置（或者引入的方式），CSS 样式表可以分为三大类：

- 行内样式表（行内式）
- 内部样式表（嵌入式）
- 外部样式表（外链式）

## 5.2 行内样式表

行内样式表（内联样式表）是在元素标签内部的 style 属性中设定 CSS 样式，适合于修改简单样式。

```html
<div style="color: red; font-size: 12px;">
    青春不常在，抓紧谈恋爱
</div>
```

- `style` 其实就是标签的属性
- 在双引号中间，写法要符合 CSS 规范
- 可以控制当前的标签设置样式
- 由于书写繁琐，并且没有体现出结构与样式相分离的思想，所以不推荐大量使用，只有对当前元素添加简单样式的时候，可以考虑使用
- 使用行内样式表设定 CSS，通常也被称为 `行内式引入`

## 5.3 内部样式表

内部样式表（嵌入样式表）时写到 HTML 页面内部，是将所有的 CSS 代码抽取出来，单独放到一个 `<style>` 标签中。

```html
<style type="text/css">
    div {
        color: red;
        font-size: 12px;
    }
</style>
```

- `<style>` 标签理论上可以放在 HTML 文档的任何地方，但一般会放到文档的 `<head>` 标签中
- 目前的浏览器已经支持**省略** `type` **属性**
- 通过此种方式，可以方便控制当前整个页面中的元素样式设置
- 代码结构清晰，但是并没有实现结构与样式完全分离
- 使用内部样式表设定 CSS，通常也被称为 `嵌入式引入`，这种方式是我们练习时常用的方式

## 5.4 外部样式表

实际开发都是外部样式表，适合于样式比较多的情况，核心是：样式单独写到 CSS 文件中，之后把 CSS 文件引入到 HTML 页面中使用。

引入外部样式表分为两步：

- 新建一个后缀名为：`.css` 的样式文件，把所有的 CSS 代码都放入此文件中
- 在 HTML 页面中，在`head` 标签内，使用 `<link>` 标签引入这个文件

```html
<link rel="stylesheet" type="text/css" href="css文件路径">
```

| 属性   | 作用                                                         |
| ------ | ------------------------------------------------------------ |
| `rel`  | 定义当前文档与被链接文档之间的关系，在这里**需要指定为 "stylesheet"**，表示被链接的文档是一个样式表文件 |
| `type` | 定被链接文档的 MIME 类型，该属性最常见的 MIME 类型是 "text/css"，该类型描述样式表，目前的浏览器**已经支持省略 "type" 属性** |
| `href` | 定义所链接外部样式表文件的 URL，可以是相对路径，也可以是绝对路径 |

**注意：**使用外部样式表设定 CSS，通常也被称为 `外链式` 或 `链接式引入`，这种方式是开发中常用的方式。

## 5.5 CSS引入方式总结

| 样式表               | 优点                     | 缺点         | 使用情况       | 控制范围     |
| -------------------- | ------------------------ | ------------ | -------------- | ------------ |
| 行内样式表（行内式） | 书写方便，权重高         | 结构样式混写 | 较少           | 控制一个标签 |
| 内部样式表（嵌入式） | 部分结构和样式分离       | 没有彻底分离 | 较多           | 控制一个页面 |
| 外部样式表（外链式） | 完全实现结构和样式相分离 | 需要引入     | 最多，吐血推荐 | 控制多个页面 |




# 六、CSS的复合选择器

## 6.1 什么是复合选择器

在 CSS 中，可以根据选择器的类型把选择器分为：`基础选择器` 和 `复合选择器`，复合选择器是建立在基础选择器之上，对基础选择器进行**组合形成**的。

- 复合选择器可以更准确、更高效的选择目标元素（标签）
- 复合选择器是由两个或多个基础选择器，通过不同的方式组合而成的
- 常用的复合选择器包括：**后代选择器**、**子选择器**、**并集选择器**、**伪类选择器**等

## 6.2 后代选择器

`后代选择器` 又称为 `包含选择器`，可以选择父元素里面子元素。其写法就是把外层标签写在前面，内层标签写在后面，中间用空格分隔。当标签发生嵌套时，内层标签就成为外层标签的后代。

**语法：**

```css
元素1 元素2 { 样式声明 }
标签1 标签2 { 样式声明 }
```

上述语法表示选择 元素 1 里面的**所有**元素 2 （后代元素）。 

**例如：**

```css
ul li { 样式声明 } 		/* 选择 ul 里面所有的 li 标签元素 */
div p { color: red; } 		/* 选择 div 里面所有的 p 标签元素 */
```

- 元素1 和 元素2 中间用 **空格** 隔开
- 元素1 是父级，元素2 是子级，最终选择的是 元素2，即：元素1 是不会生效样式的
- 元素2 可以是儿子，也可以是孙子等，只要是 元素1 的后代即可
- 元素1 和 元素2 **可以是任意基础选择器**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>复合选择器之后代选择器</title>
    <style>
        /* 把 ol 里面的小 li 选出来改为 pink */
        ol li {
            color: pink;
        }

        /* 把 ol 里面的小 a 选出来改为 red */
        ol a {
            color: red;
        }

        /* 把 ul 里面的小 li 选出来改为 green */
        ul li {
            color: green;
        }

        /* 把 nav 类中的 li 里面的 a 选出来改为 yellow */
        .nav li a {
            color: yellow;
        }
    </style>
</head>

<body>
    <ol>
        <li>我是 ol 的孩子</li>
        <li>我是 ol 的孩子</li>
        <li>我是 ol 的孩子</li>
        <li><a href="#">我是 ol 的孙子</a></li>
    </ol>
    <ul>
        <li>我是 ul 的孩子</li>
        <li>我是 ul 的孩子</li>
        <li>我是 ul 的孩子</li>
        <li><a href="#">我是 ul 的孙子，但是我不会变化</a></li>
    </ul>
    <ul class="nav">
        <li><a href="#">我偏要变色！并且只能我一个人色……</a></li>
    </ul>
</body>

</html>
```

## 6.3 子选择器

子元素选择器（子选择器）只能选择作为某元素的**最近一级子元素**，简单理解就是选亲儿子元素。

注意：是**最近一级而并非最近一个**！

**语法：**

```css
元素1>元素2 { 样式声明 }
```

上述语法表示选择元素1 里面的所有直接后代（子元素）元素2。

**例如：**

```css
div > p { 样式声明 } 	/* 选择 div 里面所有最近一级 p 标签元素 */
```

- 元素1 和 元素2 中间用 **大于号** 隔开
- 元素1 是父级，元素2 是子级，最终选择的是元素2，即元素1 是不会生效样式的
- 元素2 **必须是亲儿子，其孙子、重孙之类都不归他管**，你也可以叫：亲儿子选择器

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>复合选择器之子元素选择器</title>
    <style>
        .nav > a {
            color: red;
        }
    </style>
</head>

<body>
    <div class="nav">
        <a href="#">我是儿子1</a>
        <p>
            <a href="#">我是孙子1</a>
            <a href="#">我是孙子2</a>
        </p>
        <a href="#">我是儿子2</a>
    </div>
</body>

</html>
```

## 6.4 并集选择器

`并集选择器` 可以选择多组标签，同时为他们定义相同的样式，通常用于**集体声明**。
`并集选择器` 是各选择器通过**英文逗号** `,` 连接而成，任何形式的选择器都可以作为并集选择器的一部分。

**语法：**

```css
元素1, 元素2, 元素3 { 样式声明 }
```

推荐写法，编码风格：

```css
元素1,
元素2,
元素3 {
    样式声明
}
```

上述语法表示选择元素1、元素2 和 元素3。

**例如：**

```css
ul, div { 样式声明 }		 /* 选择 ul 和 div标签元素 */
```

- 元素1 和 元素2 中间用逗号隔开（最后一个不加逗号）
- 逗号可以理解为和的意思
- 并集选择器通常用于集体声明

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>复合选择器之并集选择器</title>
    <style>
        /* 要求1：请把熊大和熊二改为粉色 */
        /* div,
        p {
            color: pink;
        } */

        /* 要求2：请把熊大和熊二改为红色，还有小猪一家改为粉色 */
        div,
        p,
        .pig li {
            color: pink;
        }
        /* 语法规范：并集选择器通常竖着写 */
    </style>
</head>

<body>
    <div>熊大</div>
    <p>熊二</p>
    <span>光头强</span>
    <ul class="pig">
        <li>小猪佩奇</li>
        <li>猪爸爸</li>
        <li>猪妈妈</li>
    </ul>
</body>

</html>
```



选择器 - 交集

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>交集选择器</title>
    <style>
        /* id选择器 */
        #p1{
            color: red;
        }
        /* 类选择器 */
        .p2{
            color: green;
        }
        /* 交集选择器 */
        span.s2{
            color: blue;
        }
      	/* 交集选择器 */
        div.d2{
            font: italic bold 25px 宋体;
        }
    </style>
</head>

<body>
    <p>pppp</p>
    <p id="p1">pppp11111</p>
    <p class="p2">pppp22222</p>

    <span>spanspan</span>
    <span id="s1">spanspan11111</span>
    <span class="s2">spanspan2222</span>

    <div>divdiv</div>
    <div id="d1">divdiv11111</div>
    <div class="d2">divdiv22222</div>
</body>

</html>
```



## 6.5 伪类选择器

`伪类选择器` 用于**向某些选择器添加特殊的效果**，比如：给链接添加特殊效果（链接伪类），或选择第 n 个元素（结构伪类）。
`伪类选择器` 书写最大的特点是用**冒号** `:` 表示，比如：`:hover`、`:first-child`。 
因为伪类选择器很多，比如：`链接伪类`、`结构伪类` 等，所以这里先讲解常用的链接伪类选择器。

> 伪类的由来：因为在页面中并没有这个真实存在的类，所以称为 “伪类”。

## 6.6 链接伪类选择器

**链接伪类选择器注意事项：**

- 为了确保生效且不冲突，请按照 `LVHA` 的顺序声明 `:link` `:visited` `:hover` `:active`

- 记忆法：love hate 或者 lv 包包 hao 

- 因为 a 链接在浏览器中具有默认样式，所以我们实际工作中都需要给链接单独指定样式

**链接伪类选择器实际工作开发中的写法：**

```css
/* a 是标签选择器 所有的链接 */
a {
	color: gray;
}

/* :hover 是链接伪类选择器 鼠标经过 */
a:hover {
	color: red; 	/* 鼠标经过的时候，由原来的 灰色 变成了红色 */
}
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>复合选择器之链接伪类选择器</title>
    <style>
        /* 注意：要学会触类旁通，这里不只是可以改变颜色，当链接为图片时还可以改图片 */
        /* 1、a:link 把没有点击过的（访问过的）链接选出来 */
        a:link {
            color: #333;
            text-decoration: none;
        }

        /* 2、a:visited 选择点击过的（访问过的）链接选出来 */
        a:visited {
            color: orange;
        }

        /* 3、a:hover 选择鼠标经过（停留）的那个链接 */
        a:hover {
            color: skyblue;
        }

        /* 4、a:active 选择的是我们鼠标正在按下还没有弹起鼠标的那个链接 */
        a:active {
            color: green;
        }
    </style>
</head>

<body>
    <a href="#">小猪佩奇</a>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405203010954.gif)

> 注意：`:hover` `:active` 也适用于其他标签元素。

## 6.7 :focus伪类选择器

`:focus` 伪类选择器用于选取获得焦点的表单元素。

焦点就是光标，一般情况 `<input>` 类表单元素才能获取，因此这个选择器也主要针对于表单元素来说。

```css
input:focus {
	background-color: yellow;
}
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>复合选择器之focus伪类选择器</title>
    <style>
        /* 把获得光标的 input 表单元素选区出来 */
        input:focus {
            background-color: pink;
            color: red;
        }
    </style>
</head>

<body>
    <input type="text">
    <input type="text">
    <input type="text">
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405202554834.gif)

## 6.8 复合选择器总结

| 选择器          | 作用                   | 特征             | 使用情况 | 隔开符号及用法                             |
| --------------- | ---------------------- | ---------------- | -------- | ------------------------------------------ |
| 后代选择器      | 用来选择后代元素       | 可以是子孙后代   | 较多     | 符号是空格 `.nav a`                        |
| 子代选择器      | 选择最近一级元素       | 只选亲儿子       | 较少     | 符号是大于 `.nav>p`                        |
| 并集选择器      | 选择某些相同样式的元素 | 可以用于集体声明 | 较多     | 符号是逗号 `.nav`, `.header`               |
| 链接伪类选择器  | 选择不同状态的链接     | 跟链接相关       | 较多     | 重点记住 `a{}` 和 `a:hover` 实际开发的写法 |
| `:focus` 选择器 | 选择获得光标的表单     | 跟表单相关       | 较少     | `input:focus` 记住这个写法                 |

强调：复合选择器的层级写得越细越好（可读性，可维护性，安全性），同时将复合选择器的层级写得越细，可以提前避免大部分的选择器优先级混乱！

# 七、CSS 的元素显示模式

## 7.1 什么是元素显示模式

**作用：**网页的标签非常多，在不同地方会用到不同类型的标签，了解他们的特点可以更好的布局我们的网页。

`元素显示模式` 就是元素（标签）以什么方式进行显示，比如 `<div>` 自己占一行，比如一行可以放多个 `<span>`。

HTML 元素一般分为 `块元素` 和 `行内元素` 两种类型。

## 7.2 块元素

常见的块元素有 `<h1> ~ <h6>`、`<p>`、`<div>`、`<ul>`、`<ol>`、`<li>`、`<dl>`、`<dt>`、`<dd>`、`<table>`、`<tr>`、`<form>` 等，其中  `<div>` 标签是最典型的块元素。

**块级元素的特点：**

- 比较霸道，自己独占一行
- 高度，宽度、外边距以及内边距都可以控制
- 宽度默认是容器（父级宽度）的 100%
- 是一个容器及盒子，里面可以放行内或者块级元素

**注意：**

- 文字类的块级元素内不能放置块级元素，会发生语法错误
- `<p>` 标签主要用于存放文字，因此 `<p>` 里面不能放块级元素，特别是不能放 `<div>`
- 同理， `<h1> ~ <h6>` 等都是文字类块级标签，里面也不能放其他块级元素

## 7.3 行内元素

常见的行内元素有 `<a>`、`<span>`、`<em>`、`<strong>` 等，其中 `<span>` 标签是最典型的行内元素，有的地方也将行内元素称为内联元素。

**行内元素的特点：**

- 相邻行内元素在一行上，一行可以显示多个

- 高、宽直接设置是无效的

- 默认宽度就是它本身内容的宽度

- 行内元素只能容纳文本或其他行内元素（a 除外）

**注意：**

- 链接里面不能再放链接
- 特殊情况链接 `<a>` 里面可以放块级元素，但是给 `<a>` 转换一下块级模式最安全

## 7.4 行内块元素



在行内元素中有几个特殊的标签：`<img>`、`<input>`、`<th>`、`<td>`，它们同时具有 `块元素` 和 `行内元素` 的特点，有些资料称它们为 `行内块元素`。

**行内块元素的特点：**

- 和相邻行内元素（行内块）在一行上，但是他们之间会有空白缝隙。一行可以显示多个（行内元素特点）
- 默认宽度就是它本身内容的宽度（行内元素特点）
- ==高度，行高、外边距以及内边距都可以控制==（块级元素特点）

## 7.5 元素显示模式总结

| 元素模式   | 元素排列               | 设置样式                 | 默认宽度         | 包含                   |
| ---------- | ---------------------- | ------------------------ | ---------------- | ---------------------- |
| 块级元素   | 一行只能放一个块级元素 | 可以设置宽度和高度       | 容器的 100%      | 容量级可以包含任何标签 |
| 行内元素   | 一行可以放多个行内元素 | 不可以直接设置宽度和高度 | 它本身内容的宽度 | 容纳文本或其他行内元素 |
| 行内块元素 | 一行放多个行内块元素   | 可以设置宽度和高度       | 它本身内容的宽度 |                        |

学习元素显示模式的主要目的是分清它们各自的特点，当我们网页布局的时候，在合适的地方用合适的标签元素。

## 7.6 元素显示模式转换

特殊情况下，我们需要元素模式的转换，简单理解: 一个模式的元素需要另外一种模式的特性
比如：想要增加链接 `<a>` 的触发范围。

| 属性                   | 效果                                                         | 频率 |
| ---------------------- | ------------------------------------------------------------ | ---- |
| display: block;        | 转换为块元素（由于经常需要设置宽高，所以通常会将行内元素转换为块元素） | 较多 |
| display: inline;       | 转换为行内元素                                               | 较少 |
| display: inline-block; | 转换为行内块                                                 | 常用 |



```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>元素显示模式之显示模式的转换</title>
    <style>
        a {
            width: 150px;
            height: 50px;
            background-color: orange;
            /* 把行内元素 a 转换为 块级元素 */
            display: block;
        }

        div {
            width: 300px;
            height: 100px;
            background-color: black;
            color: white;
            /* 把 div 块级元素转化为行内元素 */
            display: inline;
        }

        span {
            width: 300px;
            height: 30px;
            background-color: skyblue;
            /* 行内元素转化为行内块元素 */
            display: inline-block;
        }
    </style>
</head>

<body>
    <a href="#">我是行内元素</a>
    <a href="#">我是行内元素</a>
    <div>我是块级元素</div>
    <div>我是块级元素</div>
    <span>行内元素转化为行内块元素</span>
    <span>行内元素转化为行内块元素</span>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405205009406.jpg)

## 7.7 简洁版小米侧边栏案例

```html
<!doctype html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>简洁版小米侧边栏案例</title>
    <style>
        /* 1、把 a 转换为块级元素 */
        a {
          /* 块模式 每个元素换行显示*/
            display: block;
            width: 230px;
            height: 40px;
            background-color: #55585a;
            font-size: 14px;
            color: #fff;
            text-decoration: none;
            text-indent: 2em;
            /* 一个小技巧：单行文字垂直居中的代码，让文字的行高等于盒子的高度 */
            line-height: 40px;
        }

        /* 2、鼠标经过链接变换背景颜色 */
        a:hover {
            background-color: #ff6700;
        }
    </style>
</head>

<body>
    <!--
    说明：在实际开发中，为了避免链接堆叠，从而降低浏览器排名
    开发中一般都将这些链接放在无序列表中，这里只是为了方便演示才这样使用
	-->
    <a href="#">手机 电话卡</a>
    <a href="#">电视 盒子</a>
    <a href="#">笔记本 平板</a>
    <a href="#">出行 穿戴</a>
    <a href="#">智能 路由器</a>
    <a href="#">健康 儿童</a>
    <a href="#">耳机 音响</a>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405205628339.gif)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        a {
            width: 100px;
            height: 50px;
            display: inline-block;
            text-decoration: none;
            text-align: center;
            line-height: 50px;
            background-color: yellow;
        }

        a:hover {
            background-color: orange;
        }
    </style>

</head>

<body>
    <a href="#">导航1</a>
    <a href="#">导航2</a>
    <a href="#">导航3</a>
    <a href="#">导航4</a>
    <a href="#">导航5</a>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/QQ%E5%BD%95%E5%B1%8F20221024193039.gif)

## 7.8 小技巧：单行文字垂直居中



CSS 没有给我们提供文字垂直居中的代码，这里我们可以使用一个小技巧来实现。

**解决方案：**让 `文字的行高` 等于 `盒子的高度` 就可以让文字在当前盒子内垂直居中。

**简单理解：**行高的上空隙和下空隙把文字挤到中间了，如果行高小于盒子高度，文字会偏上，如果行高大于盒子高度，则文字偏下。

## 7.9 一个注意点：块级元素不会自动换行

当块级元素的宽度超过其父元素宽度时，其不会发生换行。

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0"
          name="viewport">
    <meta content="ie=edge" http-equiv="X-UA-Compatible">
    <title>块级元素不会自动换行</title>
    <style>
        .clearfix:before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }

        div {
            background-color: #FFFF00;
            width: 600px;
            height: 300px;
            color: #FFFFFF;
            font-size: 24px;
        }

        .div {
            background-color: #000;
            width: 730px;
            height: 100px;
            margin: 20px 0;
        }

        span {
            background-color: #000;
            width: 700px;
            height: 100px;
            margin: 20px 0;
        }
    </style>
</head>
<body>
<div class="clearfix">
    <div class="div">块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素 块级元素</div>
    <span>行内元素 行内元素 行内元素 行内元素 行内元素 行内元素 行内元素 行内元素</span>
</div>
</body>
</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220125215313482.png)

# 八、CSS 的背景

通过 CSS 背景属性，可以给页面元素添加背景样式。
背景属性可以设置 `背景颜色`、`背景图片`、`背景平铺`、`背景图片位置`、`背景图像固定` 等。

## 8.1 背景颜色

`background-color` 属性定义了元素的背景颜色。

```css
background-color: 颜色值;
```

一般情况下元素背景颜色默认值是 `transparent`（透明），我们也可以手动指定背景颜色为透明色。

```css
background-color: transparent;
```

目前 CSS 还支持丰富的渐变色，但是某些浏览器不支持，这里了解即可，具体内容请查阅资料。

```html
<!doctype html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>渐变</title>
    <style>
        #grad1 {
            height: 200px;
            /* 浏览器不支持时显示 */
            background-color: red;
            /* 线性渐变 - 从上到下（默认情况下）*/
            background-image: linear-gradient(#e66465, #9198e5);
        }
    </style>
</head>

<body>
    <h3>线性渐变 - 从上到下</h3>
    <p>从顶部开始的线性渐变。起点是红色，慢慢过渡到蓝色：</p>

    <div id="grad1"></div>

    <p><strong>注意：</strong> Internet Explorer 9 及之前的版本不支持渐变。</p>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405211456978.jpg)

## 8.2 背景图片

`background-image` 属性描述了元素的背景图像，实际开发常用于 **logo** 或者一些**装饰性的小图片**或者是**超大的背景图片**, 优点是非常便于控制位置（精灵图也是一种运用场景）。

```css
background-image : none | url(图片路径)
```

| 参数值 | 作用                           |
| ------ | ------------------------------ |
| `none` | 无背景图（默认的）             |
| `url`  | 使用绝对或相对地址指定背景图像 |

注意：背景图片后面的地址，千万不要忘记加 URL， 同时里面的路径不要加引号。

```css
background-color: pink;
background-image: url(../images/logo.png);
/* 1、背景图片不平铺 */
/* background-repeat: no-repeat; */
/* 2、默认情况下，背景图片是平铺的 */
/* background-repeat: repeat; */ /* 页面元素既可以添加背景颜色也可以添加背景图片，只不过背景图片区域会覆盖背景颜色 */
```

- 重要的图片使用img属性
- 美化的背景颜色等使用css的背景属性

## 8.3 背景平铺

如果需要在 HTML 页面上对背景图像进行平铺，可以使用 `background-repeat` 属性。

注：平铺可以简单的理解为“重复”。

```css
background-repeat: repeat | no-repeat | repeat-x | repeat-y
```

| 参数值      | 作用                                 |
| ----------- | ------------------------------------ |
| `repeat`    | 背景图像在纵向和横向上平铺（默认的） |
| `no-repeat` | 背景图像不平铺                       |
| `repeat-x`  | 背景图像在横向上平铺                 |
| `repeat-y`  | 背景图像在纵向上平铺                 |

## 8.4 背景图片位置

利用 `background-position` 属性可以改变图片在背景中的位置。

```css
background-position: x y;
```

参数代表的意思是：x 坐标 和 y 坐标，可以使用 `方位名词` 或者 `精确单位`。

| 参数值     | 说明                                              |
| ---------- | ------------------------------------------------- |
| `length`   | 百分数 \| 由浮点数字和单位标识符组成的长度值      |
| `position` | top \| center \| bottom \| left \| rigth 方位名词 |

- 参数是方位名词
  - 如果指定的两个值都是方位名词，则两个值前后顺序无关，比如 left top 和 top left 效果一致
  - 如果只指定了一个方位名词，另一个值省略，则**第二个值默认居中对齐**


- 参数是精确单位
  - 如果参数值是精确坐标，那么第一个肯定是 x 坐标，第二个一定是 y 坐标
  - 如果只指定一个数值，那该数值一定是 x 坐标，**另一个默认垂直居中**


- 参数是混合单位
  - 如果指定的两个值是精确单位和方位名词混合使用，则第一个值是 x 坐标，第二个值是 y 坐标

## 8.5 背景图像固定（背景附着）

`background-attachment` 属性设置背景图像是否固定或者随着页面的其余部分滚动。

`background-attachment` 后期可以制作 `视差滚动` 的效果。

```css
background-attachment : scroll | fixed
```

| 参数     | 作用                                                       |
| -------- | ---------------------------------------------------------- |
| `scroll` | 背景图像是随对象内容滚动的（可见区域取决于背景图像的高度） |
| `fixed`  | 背景图像固定                                               |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>超大背景图片</title>
    <style>
        body {
            background-image: url(images/bg.jpg);
            background-repeat: no-repeat;
            background-position: center top;
            /* 把背景图片固定住 */
            background-attachment: fixed;
            color: #fff;
            font-size: 20px;
        }
    </style>
</head>

<body>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
    <p>天王盖地虎, pink老师一米五</p>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405212447451-16422629370077.gif" style="zoom: 33%;" />

## 3.6 背景复合写法

为了简化背景属性的代码，我们可以将这些属性合并简写在同一个属性 `background` 中，从而节约代码量。
当使用简写属性时，没有特定的书写顺序，一般习惯约定顺序为：
`background`: `背景颜色` `背景图片地址` `背景平铺` `背景图像滚动` `背景图片位置`

```css
background: transparent url(url地址) no-repeat fixed top;
```

这是实际开发中，我们更提倡的写法。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>背景复合</title>
    <style>
        div {
            width: 1800px;
            height: 1000px;
            /* 不分先后顺序：背景色、背景图、背景图平铺、背景图位置 */
            /* 背景图位置如果是英文单词可以颠倒顺序 如果背景图的位置单位为像素，则不能颠倒顺序，颠倒顺序结果和预期不一样*/
            background: red url(../../BlogImage/25.jpeg) no-repeat center top;
            
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```



## 8.7 背景色半透明

CSS3 为我们提供了背景颜色半透明的效果。

```css
background: rgba(0, 0, 0, 0.3);
```

- 最后一个参数是 `alpha` 透明度，取值范围在 `0~1` 之间
- 习惯把 0.3 的 0 省略掉，写为 `background: rgba(0, 0, 0, .3);`
- 注意：背景半透明是指盒子背景半透明，盒子里面的内容不受影响
- CSS3 新增属性，是 IE9+ 版本浏览器才支持的
- 但是现在实际开发，我们不太关注兼容性写法了，可以放心使用

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>背景色透明写法</title>
    <style>
        div {
            width: 300px;
            height: 300px;
            /* background-color: black; */
            background: rgba(0, 0, 0, .3);
        }
    </style>
</head>

<body>
    <!-- 只是让背景颜色半透明，盒子里的内容并不受影响 -->
    <div>zhoujirui</div>
</body>

</html>
```

## 8.8 背景总结

| 属性                   | 作用           | 值                                               |
| ---------------------- | -------------- | ------------------------------------------------ |
| `backgroud-color`      | 背景颜色       | 预定义的颜色值 / 十六进制 / RGB代码              |
| `backgroud-image`      | 背景图片       | url（图片路径）                                  |
| `backgroud-repeat`     | 是否平铺       | repeat / no-repeat / repeat-x / repeat-y         |
| `backgroud-position`   | 背景位置       | length / position 分别是 x 和 y 坐标             |
| `backgroud-attachment` | 背景附着       | scroll（背景滚动）/ fixed（背景固定）            |
| `背景简写`             | 书写更简单     | 背景颜色 背景图片地址 背景平铺 背景滚动 背景位置 |
| `背景色半透明`         | 背景颜色半透明 | background: rgba(0, 0, 0, 0.3); 后面必须是4个值  |

背景图片：实际开发常见于 logo 或者一些装饰性的小图片或者是超大的背景图片，优点是非常便于控制位置（精灵图也是一种运用场景）。

## 8.9 王者荣耀案例

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>背景位置案例一之王者荣耀点击选项</title>
    <style>
        /* 对于 logo 图片来说，最常用的方法便是利用背景来设置，而并非直接插入图片 */
        h3 {
            width: 118px;
            height: 40px;
            font-size: 14px;
            font-weight: 400;
            line-height: 40px;
            background-image: url(../image/icon.png);
            background-repeat: no-repeat;
            background-position: left center;
            text-indent: 2em;
        }

        h3 a {
            color: #000;
            text-decoration: none;
        }
    </style>
</head>

<body>
    <h3><a href="#">成长守护平台</a></h3>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210405213212859.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>背景位置案例二之王者荣耀背景图片</title>
    <style>
        body {
            background-image: url(../image/b.jpg);
            background-repeat: no-repeat;
            background-position: center top;
        }
    </style>
</head>

<body>
    <!-- 对于网页中的大面积图片而言，一般不采用直接插入图片的方式来做，
    因为图片的分辨率及尺寸是固定的但是显示器或网页窗口的大小分辨率则是会改变的，
    直接插入图片的话不方便控制图片大小及位置 -->
    <!-- <img src="../image/b.jpg" alt=""> -->
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/202104052132139.jpg)



# 九、CSS三大特性



CSS 有三个非常重要的特性：`层叠性`、`继承性`、`优先级`。

## 9.1 层叠性

给同一个选择器设置相同的样式，此时一个样式就会**覆盖**（层叠）另一个冲突的样式，**层叠性主要解决样式冲突的问题**。

层叠性原则：

- 样式冲突，遵循的原则是 `就近原则`，哪个样式距离结构近，就执行哪个样式
- 样式不冲突，不会层叠

注：就近的标准是：**后 > 前**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之层叠性</title>
    <style>
        div {
            color: red;
        }

        div {
            color: pink;
        }
    </style>
</head>

<body>
    <!-- pink 色 -->
    <div>周吉瑞</div>
</body>

</html>
```

## 9.2 继承性

现实中的继承：我们继承了父亲的姓。

CSS 中的继承：**子标签会继承父标签的某些样式**，如：文本颜色和字号，简单的理解就是：子承父业。

- 恰当地使用继承可以简化代码，降低 CSS 样式的复杂性
- 子元素可以继承父元素的样式（ `text-`、`font-`、`line-`、`color` ） 文本、字体、段落、颜色

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之继承性</title>
    <style>
        div {
            color: pink;
            font-size: 14px;
        }
    </style>
</head>

<body>
    <div>
        <p>周吉瑞</p>
    </div>
</body>

</html>
```

**行高的继承**

```css
body {
    font: 12px/1.5 'Microsoft YaHei';
}
```

- 行高可以跟单位也可以不跟单位
- 如果子元素没有设置行高，则会继承父元素的行高为 1.5
- 此时子元素的行高是：**当前元素**的**文字大小** * 1.5
- body 行高 1.5 这样写法最大的优势就是**里面的子元素可以根据自己文字的大小自动调整行高**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之继承性——行高的继承</title>
    <style>
        body {
            color: pink;
            /* font: 12px/18px; */
            font: 12px/1.5;		/* 12 + 12 * 0.5 = 18 */
        }

        div {
            /* 子元素继承了父元素 body 的行高 1.5 */
            /* 这个 1.5 就是当前元素文字大小 font-size 的 1.5 倍 */
            /* 所以当前 div 的行高就是：14 + 14 * 0.5 = 21px */
            font-size: 14px;
        }

        p {
            /* 1.5 * 16 = 24 当前行高 */
            font-size: 16px;
        }

        /* li 没有手动指定文字大小，则会继承父亲（此处的父亲可以层层向上推）的文字大小  */
        /* 即：body 12px 所有 li 的文字大小为 12px */
        /* 当前 li 的行高就是 12 * 1.5 = 18  */
    </style>
</head>

<body>
    <div>周吉瑞</div>
    <p>JERRY</p>
    <ul>
        <li>没有指定文字大小</li>
    </ul>
</body>

</html>
```

## 9.3 优先级

- 选择器相同，则执行层叠性
- 选择器不同，则根据选择器权重执行

**选择器权重如下表所示：**

| 选择器               | 选择器权重 |
| -------------------- | ---------- |
| 继承 或  `*`         | `0,0,0,0`  |
| 元素选择器           | `0,0,0,1`  |
| 类选择器、伪类选择器 | `0,0,1,0`  |
| ID 选择器            | `0,1,0,0`  |
| 行内样式 style=""    | `1,0,0,0`  |
| !important 重要的    | `∞` 无穷大 |

**规则：**比较位级别，位级别相同时比较位大小。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之优先级</title>
    <style>
        div {
            color: pink;
        }

        .test {
            color: red;
        }

        #demo {
            color: green;
        }
    </style>
</head>

<body>
    <div class="test">你笑起来真好看</div> <!-- red -->
    <div class="test" id="demo">你笑起来真好看</div> <!-- green -->
    <div class="test" id="demo" style="color: blue;">你笑起来真好看</div> <!-- blue -->
<!-- 
    假如在 css 选择器 某一个属性值后面跟上 !important，那么这个属性一定会执行！
    例如：div {
             color: pink !important;  
          }
          ...
    <div class="test" id="demo" style="color: blue;">你笑起来真好看</div> -- pink --
-->

</body>

</html>
```

**优先级注意问题：**

- 优先级顺序
  - 继承 < 通配符选择器  < 标签选择器  < 类选择器  < id选择器 < 行内样式 < !important
  - 所包含的范围越小，优先级就越高
  - 行内选择器：只包含在一个标签内
  - id选择器：可以多个标签内具有相同的 id
  - 类选择器也如id选择器
  - 标签选择器范围比类标签大
  - 调配符选择器的范围是全部标签，也比标签选择器大
  - 继承比通配符选择器范围大

- 权重是由 4 组数字组成的，但是不会有进位！
- 可以理解为：`类选择器` 永远大于 `元素(标签)选择器`，`ID 选择器` 永远大于 `类选择器`，以此类推！
- 等级判断 `从左到右`，如果某一位数值相同，则判断下一位数值
- 可以简单的记忆：`通配符` 和 `继承` 权重为 0，`标签选择器` 为 1，`类`（`伪类`）选择器为 10，`ID` 选择器为 100，`行内样式表` 为 1000，`!important` 无穷大
- 继承的权重是 0，不管父元素权重多高，子元素得到的权重都是 0 ！
- `a` 链接浏览器默认指定了一个样式，所以它不参与继承，所以设置样式需要选中单独设置

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之优先级——注意问题</title>
    <style>
        /* 父亲的权重是 100 */
        #father {
            color: red !important;
        }

        /* p 继承的权重为 0 */
        /* 所以以后我们看标签到底执行哪一个样式，就先看这个标签有没有直接被选出来
           如果直接被选择出来了，那么就与父亲无关了！*/
        p {
            color: pink;
        }
    </style>
</head>

<body>
    <!-- 继承的权重是 0，不管父元素权重多高，子元素得到的权重都是 0 -->
    <div id="father">
        <p>你还是很好看</p> <!-- pink -->
    </div>
    <!-- a 链接浏览器默认指定了一个样式，所以它不参与继承，所以给 a 改样式必须直接把 a 选出来 -->
    <a href="#">我是单独的样式</a>
</body>

</html>
```

**权重的叠加：**

如果是复合选择器，则会有权重叠加，需要计算权重。

> （`行内选择器个数` ` id(#)选择器个数` ` 类(.)选择器个数` `标签选择器个数`  ）

注意：再次强调！权重虽然会叠加，但一定不会进位！（1万个元素选择器也比不过一个类选择器）。

从左到右逐位比较，只有左一位同样大，才比较右边一位！

**例如：**

- `div ul li` ——> `0,0,0,3`
- `.nav ul li` ——> `0,0,1,2`
- `a:hover` ——> `0,0,1,1`
- `.nav a` ——> `0,0,1,1`

如果要对某一元素设置样式，那么就必须给它足够高的权重（注意：是给他，而不是他的父亲！）。

> 提高选择器权重的技巧之一：
>
> - 多写几层类选择器

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS三大特性之优先级——权重叠加</title>
    <style>
        /* 复合选择器会有权重叠加的问题 */
        /* 权重虽然会叠加，但是永远不会有进位 例如：十个 0,0,0,1 相加为 0,0,0,10 而不是 0,0,1,0 */
        /* ul li 权重 0,0,0,1 + 0,0,0,1 = 0,0,0,2 */
        ul li {
            color: green;
        }

        /* li 的权重是 0,0,0,1 */
        li {
            color: red;
        }

        /* .nav li 权重 0,0,1,0 + 0,0,0,1 = 0,0,1,1 */
        .nav li {
            color: pink;
        }
    </style>
</head>

<body>
    <ul class="nav">
        <li>大猪蹄子</li>	<!-- pink -->
        <li>大肘子</li>	<!-- pink -->
        <li>猪尾巴</li>	<!-- pink -->
    </ul>
</body>

</html>
```

# 十、Emmet

`Emmet` 语法的前身是 `Zen coding`，它使用缩写，来提高 `html/css` 的编写速度,，`VSCode` 内部已经集成该语法。

- 快速生成 HTML 结构语法
- 快速生成 CSS 样式语法

## 10.1 快速生成HTML结构语法

- 生成标签直接输入标签名按 <kbd>tab</kbd> 键即可，比如 `div` 然后 <kbd>tab</kbd> 键， 就可以生成 `<div></div>`
- 如果想要生成多个相同标签加上 `*` 就可以了，比如 `div*3` 就可以快速生成 3 个 `div`
- 如果有父子级关系的标签，可以用 `>` 比如 `ul>li` 就可以了
- 如果有兄弟关系的标签，用 `+` 就可以了 比如 `div+p`
- 如果生成带有 `类名` 或者 `id` 名字的标签， 直接写 `标签.demo` 或者 `标签#demo` 再按下 tab 键就可以了
- 如果生成的事物有顺序，可以用自增符号 `$`
- 如果想要在生成的标签内部写内容可以用 `{}` 表示

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emmet语法之快速生成HTML结构语法</title>
</head>

<body>
    <!-- div -->
    <div></div>
    <!-- table -->
    <table></table>
    <!-- div*6 -->
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <!-- p*4 -->
    <p></p>
    <p></p>
    <p></p>
    <p></p>
    <!-- ul>li -->
    <ul>
        <li></li>
    </ul>
    <!-- div>span -->
    <div><span></span></div>
    <!-- div+p -->
    <div></div>
    <p></p>
    <!-- .nav -->
    <div class="nav"></div>
    <!-- #banner -->
    <div id="banner"></div>
    <!-- p.one -->
    <p class="one"></p>
    <!-- span.gray -->
    <span class="gray"></span>
    <!-- ul>li#two -->
    <ul>
        <li id="two"></li>
    </ul>
    <!-- .demo*5 -->
    <div class="demo"></div>
    <div class="demo"></div>
    <div class="demo"></div>
    <div class="demo"></div>
    <div class="demo"></div>
    <!-- .demo$*5 -->
    <div class="demo1"></div>
    <div class="demo2"></div>
    <div class="demo3"></div>
    <div class="demo4"></div>
    <div class="demo5"></div>
    <!-- div{pink老师不是gay} -->
    <div>pink老师不是gay</div>
    <!-- div{他不喜欢男人}*6 -->
    <div>他不喜欢男人</div>
    <div>他不喜欢男人</div>
    <div>他不喜欢男人</div>
    <div>他不喜欢男人</div>
    <div>他不喜欢男人</div>
    <div>他不喜欢男人</div>
    <!-- div{$}*6 -->
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
    <div>6</div>
</body>

</html>
```

## 10.2 快速生成CSS样式语法

CSS 基本采取简写形式即可。

- 比如 `w200` 按 <kbd>tab</kbd> 可以 生成 `width: 200px;`
- 比如 `lh26px` 按 <kbd>tab</kbd> 可以生成 `line-height: 26px;`

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emmet语法之快速生成CSS样式语法</title>
    <style>
        .one {
            /* tac */
            text-align: center;
            /* ti2e */
            text-indent: 2em;
            /* w */
            /* width: ; */
            /* h */
            /* height: ; */
            /* w24 */
            width: 24px;
            /* h24 */
            height: 24px;
            /* tdn */
            text-decoration: none;
        }
    </style>
</head>

<body>

</body>

</html>
```

## 10.3 快速格式化代码

`VSCode` 快速格式化代码：<kbd>Shift</kbd> + <kbd>Alt</kbd> + <kbd>F</kbd>。

`WebStorm` 快速格式化代码：<kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>L</kbd>。





PxCook 测量工具 ：https://www.fancynode.com.cn/



# 十一、CSS盒子模型



页面布局要学习**三大核心**：**盒子模型**、**浮动**和**定位**。

学习好盒子模型能非常好的帮助我们布局页面。

## 11.1 看透网页布局的本质

网页布局过程：

- 先准备好相关的网页元素，网页元素基本都是盒子

- 利用 CSS 设置好盒子样式，然后摆放到相应位置

- 往盒子里面装内容

网页**布局的核心**本质： 就是**利用 CSS 摆盒子！**

## 11.2 盒子模型（Box Model）组成

所谓盒子模型：就是把 HTML 页面中的布局元素看作是一个矩形的盒子，也就是一个盛**装内容的容器**。
CSS 盒子模型本质上是一个盒子，封装周围的 HTML 元素，它包括：`边框`、`外边距`、`内边距`、和 `内容`。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406122442654.png" style="zoom: 80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/v2-6cbd8a1b054611f584f56ce791739a3f_1440w.jpg"  />

## 11.3 边框（border）

`border` 可以设置元素的边框。

边框有三部分组成：`边框宽度（粗细）`、`边框样式`、`边框颜色`。

**语法：**

```css
border: border-width || border-style || border-color
```

| 属性           | 作用                      |
| -------------- | ------------------------- |
| `border-width` | 定义边框粗细，单位是 `px` |
| `border-style` | 边框的样式                |
| `border-color` | 边框颜色                  |


边框样式 border-style 可以设置如下值：

- `none`：没有边框，即忽略所有边框的宽度（默认值）
- `solid`：边框为单实线（最为常用的）
- `dashed`：边框为虚线
- `dotted`：边框为点线

**边框简写：**

```css
border: 1px solid red; 	/* 没有顺序 */
```

**边框分开写法：**

```css
border-top: 1px solid red; 		/* 只设定上边框，其余同理 */
```

**案例：**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子模型之边框的复合写法</title>
    <style>
        div {
            width: 300px;
            height: 200px;
            /* 
            -- border-width 边框的粗细，一般情况下使用 px --
            border-width: 5px;
            -- border-width 边框的样式 solid 实线边框 dashed 虚线边框 dotted 点线边框 --
            border-style: solid;
            background-color: pink;
            */
            /* 边框的复合写法 简写： */
            border: 10px dotted skyblue;
            /* 利用 CSS 层叠性将上边框单独覆盖 */
            border-top: 10px dotted pink;
            background-color: black;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406123444188.jpg)

### 11.3.1 表格的细线边框

表格中两个单元格相邻的边框会重叠在一起，呈现出加粗的效果。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>表格边框——今日小说排行榜</title>
    <style>
        table {
            width: 500px;
            height: 249px;
        }

        th {
            height: 35px;
        }

        table,
        td,
        th {
            border: 1px solid black;
            /* 合并相邻的边框 */
            /* border-collapse: collapse; */
            font-size: 14px;
            text-align: center;
        }
    </style>
</head>

<body>
    <table align="center" cellspacing="0">
        <thead>
            <tr>
                <th>排名</th>
                <th>关键词</th>
                <th>趋势</th>
                <th>进入搜索</th>
                <th>最近七日</th>
                <th>相关链接</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>鬼吹灯</td>
                <td><img src="down.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>

            <tr>
                <td>1</td>
                <td>鬼吹灯</td>
                <td><img src="down.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>
            <tr>
                <td>3</td>
                <td>西游记</td>
                <td><img src="up.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>
            <tr>
                <td>1</td>
                <td>鬼吹灯</td>
                <td><img src="down.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>
            <tr>
                <td>1</td>
                <td>鬼吹灯</td>
                <td><img src="down.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>
            <tr>
                <td>1</td>
                <td>鬼吹灯</td>
                <td><img src="down.jpg"></td>
                <td>456</td>
                <td>123</td>
                <td> <a href="#">贴吧</a> <a href="#">图片</a> <a href="#">百科</a> </td>
            </tr>
        </tbody>
    </table>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220116025240291.png)

`border-collapse` 属性控制浏览器绘制表格边框的方式。

它控制相邻单元格的边框。

**语法：**

```css
border-collapse: collapse;
```

- `collapse` 单词是合并的意思
- `border-collapse: collapse;` 表示相邻边框合并在一起

```css
	table,
	td,
	th {
	    border: 1px solid black;
	    /* 合并相邻的边框 */
	    border-collapse: collapse;
	    font-size: 14px;
	    text-align: center;
	}
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220116025315666.png)

### 11.3.2 边框会影响盒子实际大小

边框会额外增加盒子的实际区域大小。因此我们有两种方案解决：

- 测量盒子大小的时候，不量边框
- 如果测量的时候包含了边框，则需要 width、height 减去边框宽度（注意减单边还是双边）

> 注意：盒子实际区域大小 = 内容区大小 + 内边距大小 + 边框大小 + 外边距大小

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>边框会影响盒子的实际大小</title>
    <style>
        /* 我们需要一个 200*200 的盒子, 但是这个盒子有 10 像素的红色边框 */
        div {
            width: 180px;
            height: 180px;
            background-color: pink;
            border: 10px solid black;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406125405658.gif)

## 11.4 内边距（padding）

padding 属性用于设置**内边距**，即**边框与内容之间的距离**。

| 属性             | 作用     |
| ---------------- | -------- |
| `padding-left`   | 左内边距 |
| `padding-rigth`  | 右内边距 |
| `padding-top`    | 上内边距 |
| `padding-bottom` | 下内边距 |

padding 属性（简写属性）可以有一到四个值。

| 值的个数                       | 表达意思                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| `padding: 5px;`                | 1 个值，代表上下左右都有 5 像素内边距                        |
| `padding: 5px 10px;`           | 2 个值，代表上下内边距是 5 像素，左右内边距是 10 像素        |
| `padding: 5px 10px 20px;`      | 3 个值，代码上内边距 5 像素，左右内边距 10 像素，下内边距 20 像素 |
| `padding: 5px 10px 20px 30px;` | 4 个值，上是 5 像素，右 10 像素，下 20 像素，左是 30 像素（顺时针） |

以上 4 种情况，我们实际开发都会遇到。

当我们给盒子指定 `padding` 值之后，发生了 2 件事情：

- 内容和边框有了距离，添加了内边距
- `padding` 影响了盒子实际区域大小

也就是说，如果盒子已经有了宽度和高度，此时再指定内边距，会撑大盒子区域！

解决方案：

- 如果保证盒子跟效果图大小保持一致，则让 width、height 减去多出来的内边距大小即可
- 如果盒子本身没有指定 width、height 属性，则此时 padding 不会撑开盒子区域大小

【padding 撑大盒子】

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>padding 撑大盒子</title>
    <style>
        div {
            background-color: #000;
            width: 100px;
            height: 100px;
            /* padding: 30px; */
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/00914ec7f1e04382af64f589013d6d59.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>padding 撑大盒子</title>
    <style>
        div {
            background-color: #000;
            width: 100px;
            height: 100px;
            padding: 30px;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/6d3ff73d65154f358ba03b447f9daec8.png)

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子模型之内边距</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            /*
            padding-top: 5px;
            padding-rigth: 10px;
            padding-bottom: 20px;
            padding-rigth: 30px;
             */
            /* 内边距复合写法（简写） 上、右、下、左 */
            padding: 5px 10px 20px 30px;
            /* 由于在对盒子指定高宽后，padding 会撑大盒子 */
            /* 所以，此时盒子大小为：240*225 */
            /* 注意：这里的“盒子大小”指的是盒子所占据的大小，盒子真实的 width 和 height 依旧是 200px */
        }
    </style>
</head>

<body>
    <div>
        盒子内容是 content，盒子内容是 content，盒子内容是 content
    </div>
</body>

</html>
```

padding 的使用技巧：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406131156754.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>新浪导航案例-padding影响盒子的好处</title>
    <style>
        .nav {
            height: 41px;
            border-top: 3px solid #ff8500;
            border-bottom: 1px solid #edeef0;
            background-color: #fcfcfc;
            line-height: 41px;
        }

        .nav a {
            /* a 属于行内元素，要指定高度，必须要转换为行内块元素 */
            display: inline-block;
            height: 41px;
            /* 没有指定宽度，此时设置 padding 会使盒子内容之间的距离相同 */
            padding: 0 20px;
            font-size: 12px;
            color: #4c4c4c;
            text-decoration: none;
        }

        .nav a:hover {
            background-color: #eee;
            color: #ff8500;
        }
    </style>
</head>

<body>
    <div class="nav">
        <a href="#">设为首页</a>
        <a href="#">手机新浪网</a>
        <a href="#">移动客户端</a>
        <a href="#">登录</a>
        <a href="#">微博</a>
        <a href="#">博客</a>
        <a href="#">邮箱</a>
        <a href="#">网站导航</a>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406131403183.gif)

```html
<!doctype html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>简洁版小米侧边栏案例-padding影响盒子大小计算</title>
    <style>
        a {
            /* 1、把 a 转换为块级元素 */
            display: block;
            /* 230 - 30（padding-left）= 200 */
            width: 200px;
            height: 40px;
            background-color: #55585a;
            font-size: 14px;
            color: #fff;
            text-decoration: none;
            padding-left: 30px;
            /* 一个小技巧：单行文字垂直居中的代码，让文字的行高等于盒子的高度 */
            line-height: 40px;
        }

        /* 2、鼠标经过链接变换背景颜色 */
        a:hover {
            background-color: #ff6700;
        }
    </style>
</head>

<body>
    <a href="#">手机 电话卡</a>
    <a href="#">电视 盒子</a>
    <a href="#">笔记本 平板</a>
    <a href="#">出行 穿戴</a>
    <a href="#">智能 路由器</a>
    <a href="#">健康 儿童</a>
    <a href="#">耳机 音响</a>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406132137553.gif)

## 11.5 外边距（margin）

`margin` 属性用于设置**外边距**，即控制**盒子和盒子之间的距离**。

| 属性            | 作用     |
| --------------- | -------- |
| `margin-left`   | 左外边距 |
| `margin-right`  | 右外边距 |
| `margin-top`    | 上外边距 |
| `margin-bottom` | 下外边距 |

`margin` 简写方式代表的意义跟 `padding` 完全一致。

外边距典型应用：

外边距可以让**块级盒子水平居中**，但是必须满足两个条件：

- 盒子必须指定了宽度 `width`
- 盒子左右的外边距都设置为 `auto`

```css
.header { width: 960px; margin: 0 auto;}
```

常见的写法，以下三种都可以：

- `margin-left: auto; margin-right: auto;`
- `margin: auto;`
- `margin: 0 auto;`

注意：以上方法是让块级元素水平居中，行内元素或者行内块元素水平居中给其父元素添加 `text-align: center` 即可。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子模型之外边距margin</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        /* 
        .one {
            margin-bottom: 20px;
        } 
        */

        .two {
            margin-top: 20px;
        }
    </style>
</head>

<body>
    <div class="one">1</div>
    <div class="two">2</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406133231459.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>块级盒子水平居中对齐</title>
    <style>
        .header {
            width: 900px;
            height: 200px;
            background-color: pink;
            /* 上下 100 左右 auto */
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="header"></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406133231524.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>行内元素、行内块元素水平居中对齐</title>
    <style>
        .header {
            width: 900px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            /* 行内元素或者行内块元素水平居中给其父元素添加 text-align: center 即可 */
            text-align: center;
        }

        /* 这样是不起作用的 */
        /* 
        span {
            margin: 0 auto;
        } 
        */
    </style>
</head>

<body>
    <div class="header">
        <span>里面的文字</span>
    </div>
    <div class="header">
        <img src="../image/icon.png" alt="">
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406133231531.jpg)



案例：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>热搜新闻</title>
    <style>
        * {
            /* 去除内外边距 */
            padding: 0;
            margin: 0;
            /* 自减模式 */
            box-sizing: border-box;
        }

        .fireNews {
            width: 400px;
            height: 500px;
            border: 1px solid #ccc;
            margin: 50px auto;
            padding: 42px 30px 0;
        }

        .fireNews h2 {
            border-bottom: 1px solid #ccc;
            font-size: 30px;
            /* 设置行高，字号大小 */
            line-height: 1;
            padding-bottom: 10px;
            text-align: center;
        }

        /* 去掉列表符号 */
        ul {
            list-style: none;
        }

        .fireNews li {
            line-height: 50px;
            border-bottom: 1px dashed #ccc;
            padding-left: 30px;
        }

        .fireNews a {
            text-decoration: none;
            font-size: 18px;
            color: #ccc;
        }
        /* 光标放置文字显示颜色 */
        .fireNews a:hover {
            color: rgb(0, 0, 0);
        }
    </style>

</head>

<body>
    <div class="fireNews">
        <h2>最近热搜话题</h2>
        <ul>
            <li><a href="#">Java面试</a></li>
            <li><a href="#">毕业即失业?</a></li>
            <li><a href="#">前端面试</a></li>
            <li><a href="#">全栈工程师</a></li>
            <li><a href="#">后端工程师</a></li>
        </ul>
    </div>
</body>

</html>
```

![image-20221029163950458](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221029163950458.png)

### 11.5.1 外边距合并

使用 `margin` 定义块元素的垂直外边距时，可能会出现外边距的合并。

注意：**内边距没有合并一说！浮动的盒子不会发生外边距合并！**

主要有两种情况:

- **相邻块元素垂直外边距的合并**
- **嵌套块元素垂直外边距的塌陷**

#### 11.5.1.1 相邻块元素垂直外边距的合并

当上下相邻的两个块元素（兄弟关系）相遇时，如果上面的元素有下外边距 `margin-bottom`，下面的元素有上外边距 `margin-top` ，则他们之间的垂直间距不是 `margin-bottom` 与 `margin-top` 之和。而是取两个值中的**较大者**，这种现象被称为相邻块元素垂直外边距的合并（准确的描述应该是：**大的外边距覆盖小的**）。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406134634404.jpg)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210412112840415.jpg)

**解决方案：**

尽量只给一个盒子添加 `margin` 值。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>相邻块元素垂直外边距的合并</title>
    <style>
        .one {
            width: 200px;
            height: 200px;
            background-color: hotpink;
            margin-bottom: 100px;
        }

        .two {
            width: 200px;
            height: 200px;
            background-color: skyblue;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="one">one</div>
    <div class="two">two</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410205508662.gif)

#### 11.5.1.2 嵌套块元素垂直外边距的塌陷

对于两个嵌套关系（父子关系）的块元素，当子元素有上外边距，此时父元素会塌陷较大的外边距值（**外边距效果显示在父元素之上**）。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220116024700165.png)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210412112840510.jpg)

**解决方案：**

- 可以为父元素定义上边框（比如：可以给一个透明 transparent 边框）
- 可以为父元素定义上内边距
- 可以为父元素添加 `overflow: hidden`

还有其他方法，比如浮动、固定，绝对定位的盒子不会有塌陷问题，后面咱们再总结。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>外边距合并-嵌套块级元素垂直外边距塌陷</title>
    <style>
        .father {
            width: 400px;
            height: 400px;
            background-color: black;
            margin-top: 50px;
        }

        .son {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410205223833.gif)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>外边距合并-嵌套块级元素垂直外边距塌陷</title>
    <style>
        .father {
            width: 400px;
            height: 400px;
            background-color: black;
            margin-top: 50px;
            /* border: 1px solid transparent; */
            overflow: hidden;
        }

        .son {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin-top: 100px;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406134634343-164227252890423.jpg" style="zoom:50%;" />

**注意：外边距的合并在利用盒子布局页面的时候是经常发生的！**

## 11.6 清除内外边距

网页元素很多都带有默认的内外边距，而且不同浏览器默认的也不一致。因此我们在布局前，首先要清除下网页元素的内外边距。

```css
* {
	padding:0; 	/* 清除内边距 */
	margin:0; 	/* 清除外边距 */
}
```



注意：行内元素为了照顾兼容性，尽量只设置左右内外边距，不要设置上下内外边距（某些时候，行内元素对上下内外边距不生效）。但是转换为块级和行内块元素就可以了。



### 11.6.1 CSS3模型自动内减

给盒子模型 设置属性 `box-sizing;` `border-box;`  

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS3内减模式</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            border: 10px solid #000;
            padding: 10px;

            /* 不内减之前宽为140、高为140 自动内减，内减之后就直接是宽高的取值 */
            box-sizing: border-box;
        }
    </style>
</head>

<body>
    <div>

    </div>
</body>

</html>
```





## 11.7 案例

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406135403826.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>综合案例-MI产品模块</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        body {
            background-color: #f5f5f5;
        }

        a {
            color: #333;
            text-decoration: none;
        }

        .box {
            width: 298px;
            height: 415px;
            background-color: #fff;
            /* 让块级的盒子水平居中对齐 */
            margin: 100px auto;
        }

        .box img {
            /* 图片的宽度和父亲一样宽 */
            width: 100%;
        }

        .review {
            height: 70px;
            font-size: 14px;
            /* 因为这个段落没有 width 属性，所以 padding 不会撑开盒子的宽度 */
            padding: 0 28px;
            /* 因为这个段落有 height 属性，所以 padding-top 会撑大盒子，所以我们用 margin-top */
            /* 其实用 padding-top 也可以，但是需要手动减去 top 值，麻烦且不规范 */
            margin-top: 30px;
        }

        .appraise {
            font-size: 12px;
            color: #b0b0b0;
            padding: 0 28px;
            margin-top: 20px;
        }

        .info {
            font-size: 14px;
            padding: 0 28px;
            margin-top: 15px;
        }

        .info h4 {
            display: inline-block;
            font-weight: 400;

        }

        .info span {
            color: #ff6700;
        }

        .info em {
            /* 不倾斜 */
            font-style: normal;
            color: #ebe4e0;
            margin: 0 6px 0 15px;
        }
    </style>
</head>

<body>
    <div class="box">
        <img src="images/img.jpg" alt="">
        <p class="review">快递牛，整体不错蓝牙可以说秒连。红米给力</p>
        <div class="appraise">来自于 117384232 的评价</div>
        <div class="info">
            <h4> <a href="#">Redmi AirDots真无线蓝...</a></h4>
            <!-- 特殊元素可以用 em 包裹 -->
            <em>|</em>
            <span> 99.9元</span>
        </div>
    </div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406135403703.jpg" style="zoom:50%;" />

```html
<!doctype html>
<html lang="zh-CN">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>综合案例-快报模板</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            /* 去除列表前的圆点 */
            /* 之所以把这条语句单独写，是因为整个页面都需要把 li 的圆点去除 */
            list-style: none;
        }

        .box {
            width: 248px;
            height: 163px;
            border: 1px solid #ccc;
            margin: 100px auto;
        }

        .box h3 {
            height: 32px;
            border-bottom: 1px dotted #ccc;
            font-size: 14px;
            font-weight: 400;
            line-height: 32px;
            /* 由于该盒子带有一个下边框，所以缩进不能使用 margin，否则下边框也会一同缩进，
            此处就用 padding。并且此处没有设置 width，所以 padding-left 也不会撑大盒子 */
            padding-left: 15px;
        }

        .box ul li a {
            font-size: 12px;
            color: #666;
            text-decoration: none;
        }

        .box ul li a:hover {
            text-decoration: underline;
        }

        .box ul li {
            height: 23px;
            line-height: 23px;
            padding-left: 20px;
        }

        .box ul {
            margin-top: 7px;
        }
    </style>
</head>

<body>
    <div class="box">
        <h3>品优购快报</h3>
        <ul>
            <li><a href="#">【特惠】爆款耳机5折秒！</a></li>
            <li><a href="#">【特惠】母亲节，健康好礼低至5折！</a></li>
            <li><a href="#">【特惠】语音折叠台灯99元！</a></li>
            <li><a href="#">【特惠】9.9元3D打印！</a></li>
            <li><a href="#">【特惠】格力智能空调立省1000元！</a></li>
        </ul>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210406135403715.gif)

## 11.8 总结

### a、布局为啥用不同盒子，我只想用 div？

标签都是有语义的，合理的地方用合理的标签。比如产品标题就用 `h`，大量文字段落就用 `p`。

### b、为啥用辣么多类名？

类名就是给每个盒子起了一个名字，可以更好的找到这个盒子，选取盒子更容易，后期维护也更方便。

### c、到底用 margin 还是 padding？

大部分情况两个可以混用，两者各有优缺点，但是根据实际情况，总是有更简单的方法实现。

一般来说，盒子与盒子之间统一用 margin，内容与边框之间用 padding。

### d、自己做没有思路？

布局有很多种实现方式，可以开始先模仿大牛的写法，然后再做出自己的风格。

最后一定多运用辅助工具，比如屏幕画笔，PS 等等。





# 十二、边框阴影样式

## 1. 圆角边框

CSS 3 新增了圆角边框样式。

border-radius 属性用于设置元素的外边框圆角。

语法：

```css
border-radius: length;
```

原理：

border-radius 顾名思义：边框半径。

（椭）圆与边框的交集形成圆角效果。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210407171139155.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>圆角边框</title>
    <style>
        div {
            width: 300px;
            height: 150px;
            background-color: pink;
            border-radius: 24px;
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210407171251321.jpg)

注意：

- 参数值可以为数值或百分比的形式
- 如果是正方形，想要设置为圆形，那么只需要把数值修改为高度或者宽度的一半即可，或者直接写为 50%
- 如果是个矩形，设置为高度的一半就可以做 “胶囊” 效果了
- 该属性是一个简写属性，可以跟多个值
  - 四个值：左上角、右上角、右下角、左下角（从左上开始顺时针）
  - 三个值：左上、右上+左下、右下（对角为一组）
  - 两个值：左上+右下、右上+左下（对角为一组）
- 同时可以对特定角单独设置
  - 左上角：`border-top-left-radius`
  - 右上角：`border-top-right-radius`
  - 右下角：`border-bottom-right-radius`
  - 左下角：`border-bottom-left-radius`

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>圆角边框常用写法</title>
    <style>
        .yuanxing {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* border-radius: 100px; */
            /* 50% 就是宽度和高度的一半  等价于 100px */
            border-radius: 50%;
        }

        .juxing {
            width: 300px;
            height: 100px;
            background-color: pink;
            /* 圆角矩形设置为高度的一半 */
            border-radius: 50px;
        }

        .radius {
            width: 200px;
            height: 200px;
            /* border-radius: 10px 20px 30px 40px; */
            /* border-radius: 10px 40px; */
            border-top-left-radius: 20px;
            background-color: pink;
        }
    </style>
</head>

<body>
    1. 圆形的做法:
    <div class="yuanxing"></div>
    2. 圆角矩形的做法:
    <div class="juxing"></div>
    3. 可以设置不同的圆角:
    <div class="radius"></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210407172402316.jpg)

## 2. 盒子阴影

CSS 3 新增了盒子阴影。

box-shadow 属性用于为盒子添加阴影。

语法：

```css
box-shadow: h-shadow v-shadow blur spread color inset;
```

| 值         | 描述                                                         |
| ---------- | ------------------------------------------------------------ |
| `h-shadow` | 必须。水平阴影的位置，允许负值。                             |
| `v-shadow` | 必须。垂直阴影的位置，允许负值。                             |
| `blur`     | 可选。模糊距离（虚实程度）。                                 |
| `spread`   | 可选。阴影的尺寸（大小）。                                   |
| `color`    | 可选。阴影的颜色，请参阅 CSS 颜色值（阴影多为半透明颜色）。  |
| `inset`    | 可选。将外部阴影（outset）改为内部阴影（outset 不能指定，默认为空即可）。 |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>盒子阴影</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: salmon;
            margin: 100px auto;
            /* box-shadow: 10px 10px; */
        }

        /* 伪类不仅仅可以用于 a 链接，还能用于其他标签 */
        /* 原先盒子没有影子,当我们鼠标经过盒子就添加阴影效果 */
        div:hover {
            box-shadow: 10px 10px 10px -4px rgba(0, 0, 0, .3);
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210407181220613.gif)

**三边阴影、双边阴影、单边阴影的设置方法：**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>盒子阴影 三边阴影、双边阴影、单边阴影</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: #000;
            margin: 25px auto;
            color: white;
        }

        .a {
            box-shadow: 0 0 25px 5px red;
        }

        /* 三边阴影就是直接把整个阴影部分往下边移 */
        .b {
            box-shadow: 0 6px 10px 0 red;
        }

        /* 两边阴影要用盒子嵌套来解决 */
        .c1 {
            box-shadow: 0 10px 10px -5px red;
        }

        .c2 {
            width: 100%;
            box-shadow: 0 -10px 10px -5px red;
        }

        /* 单边阴影就是直接把整个阴影部分往下边移，并且减小阴影大小 */
        .d {
            box-shadow: 0 10px 10px -5px red;
        }
    </style>
</head>

<body>
    <div class="a">四边阴影</div>
    <div class="b">三边阴影</div>
    <div class="c1">
        <div class="c2">两边阴影</div>
    </div>
    <div class="d">一边阴影</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410202736632.jpg)

## 3. 文字阴影

CSS 3 新增了文字阴影。

text-shadow 属性用于为文本添加阴影。

语法：

```css
text-shadow: h-shadow v-shadow blur color;
```

| 值         | 描述                                |
| ---------- | ----------------------------------- |
| `h-shadow` | 必须。水平阴影的位置。允许负值。    |
| `v-shadow` | 必须。垂直阴影的位置。允许负值。    |
| `blur`     | 可选。模糊的距离（虚实程度）。      |
| `color`    | 可选。阴影的颜色。参阅 CSS 颜色值。 |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>文字阴影</title>
    <style>
        div {
            font-size: 50px;
            color: salmon;
            font-weight: 700;
            text-shadow: 5px 5px 6px rgba(0, 0, 0, .3);
        }
    </style>
</head>

<body>
    <div>
        你是阴影,我是火影
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210407182002202.jpg)





# 十三、浮动（float）



### 结构伪类选择器

- 作用：根据元素在HTMl中的结构关系查找元素
- 优势：减少对于HTML中类的依赖，有利于保持代码整洁
- 场景：查找某父级选择器中的子元素





| 选择器                  | 说明                                   |
| ----------------------- | -------------------------------------- |
| `E:first-child{}`       | 匹配父元素中第一个子元素，并且是E元素  |
| `E:last-child{}`        | 匹配父元素中最后一个元素，并且是E元素  |
| `E:nth-child(n){}`      | 匹配父元素中第n个元素，并且是E元素     |
| `E:nth-last-child(n){}` | 匹配父元素中倒数第n个元素，并且是E元素 |



n具有的公式：

1. 偶数：2n、even
2. 奇数：2n-1、odd
3. 找到前5个：-n+5
4. 找到第五哥往后：n+5



### 伪元素

- 能够使用伪元素在网页中创建内容

- 由CSS模拟出但标签效果

- 种类

  | 伪元素      | 作用                             |
  | ----------- | -------------------------------- |
  | `::before ` | 在父元素内容的最前添加一个伪元素 |
  | `::afther`  | 在父元素内容的最后添加一个伪元素 |

- 需要设置 context 属性

- 伪元素默认为行内元素

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>伪元素</title>
    <style>
        .father {
            width: 300px;
            height: 300px;
            background-color: pink;
        }

        .father::before {
            /* 添加伪元素 */
            content: "你";
            width: 20px;
            height: 20px;
            text-align: center;
            /* 设置行内 不换行 */
            display: inline-block;
        }

        .father::after {
            content: "绿了";
            color: green;
        }
    </style>
</head>

<body>
    <!--伪元素 通过css创建标签 -->
    <div class="father">被</div>

</body>

</html>
```



![image-20221029173828038](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221029173828038.png)



## 13.1 传统网页布局的三种方式

网页布局的本质：用 CSS 来摆放盒子，把盒子摆放到相应位置。

CSS 提供了三种传统布局方式（简单说就是盒子如何进行排列）。

- 普通流（标准流）
- 浮动
- 定位

> 这里指的只是传统布局，其实还有一些特殊高级的布局方式。

## 13.2 标准流（普通流/文档流）

所谓的标准流：==标签按照规定好的默认方式进行排列。==

1. **块级元素会独占一行，从上向下顺序排列。**
2. **行内元素会按照顺序，从左到右顺序排列，碰到父元素边缘则自动换行。**

以上都是标准流布局，我们前面学习的就是标准流，标准流是最基本的布局方式。

这三种布局方式都是用来摆放盒子的，盒子摆放到合适位置，布局自然就完成了。

**注意：**实际开发中，一个页面基本都包含了这三种布局方式（后面移动端学习新的布局方式） 。

## 13.3 为什么需要浮动？

提问：我们用标准流能很方便的实现如下效果吗？

1. **如何让多个块级盒子（div）水平排列成一行？**

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021040923145350.jpg)

比较难，虽然转换为行内块元素可以实现一行显示，但是他们之间会有大的**空白缝隙**，很难控制。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>行内块中间有缝隙</title>
    <style>
        div {
            width: 150px;
            height: 200px;
            background-color: #d87093;
            display: inline-block;
        }
    </style>
</head>

<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210409231914135.jpg)

2. **如何实现两个盒子的左右对齐？**

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210409232236196.jpg)

总结： 有很多的布局效果，标准流没有办法完成，此时就可以利用浮动完成布局。 因为浮动可以改变元素标签默认的排列方式。

**浮动最典型的应用：可以让多个块级元素一行内排列显示。**

**网页布局第一准则：多个块级元素纵向排列找标准流，多个块级元素横向排列找浮动！**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>多个块级元素横向排列找浮动</title>
    <style>
        div {
            float: left;
            width: 150px;
            height: 200px;
            background-color: #d87093;
        }
    </style>
</head>

<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210409232755502.jpg)

**拓展：**浮动的盒子不会发生外边距合并！

## 13.4 什么是浮动？

`float` 属性用于创建浮动框，将其移动到一边，直到左边缘或右边缘触及包含块或另一个浮动框的边缘。

语法：

```css
选择器 { float: 属性值;}
```

| 属性  | 描述                 |
| ----- | -------------------- |
| none  | 元素不浮动（默认值） |
| left  | 元素向左浮动         |
| right | 元素向右浮动         |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>什么是浮动</title>
    <style>
        .left,
        .right {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="left">左青龙</div>
    <div class="right">右白虎</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410105021368.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>什么是浮动</title>
    <style>
        .left,
        .right {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        /* 层叠性 */
        .right {
            float: right;
        }
    </style>
</head>

<body>
    <div class="left">左青龙</div>
    <div class="right">右白虎</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410104859778.jpg)

## 13.5 浮动特性（重难点）

加了浮动之后的元素，会具有很多特性，需要我们掌握。

1. 浮动元素会脱离标准流（脱标）
2. 浮动的元素会一行内显示并且元素顶部对齐
3. 浮动的元素会具有行内块元素的特性

下面分别解释：

**（1）浮动元素会脱离标准流（脱标）**

- 脱离标准普通流的控制（浮） 移动到指定位置（动），（俗称脱标）
- 浮动的盒子不再保留原先的位置

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410110624702.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动特性1</title>
    <style>
        /* 设置了浮动（float）的元素会：
        1.脱离标准普通流的控制（浮）移动到指定位置（动）。
        2.浮动的盒子不再保留原先的位置 */
        .box1 {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .box2 {
            width: 300px;
            height: 300px;
            background-color: gray;
        }
    </style>
</head>

<body>
    <div class="box1">浮动的盒子</div>
    <div class="box2">标准流的盒子</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410110837237.jpg)

**（2）浮动的元素会一行内显示并且元素顶部对齐**

- 如果多个盒子都设置了浮动，则它们会按照属性值一行内显示并且顶端对齐排列。
- 浮动的元素是互相贴靠在一起的（不会有缝隙），如果父级宽度装不下这些浮动的盒子，多出的盒子会另起一行对齐。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动元素特性-浮动元素一行显示</title>
    <style>
        div {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .two {
            background-color: skyblue;
            height: 249px;
        }

        .four {
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div>1</div>
    <div class="two">2</div>
    <div>3</div>
    <div class="four">4</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410111331406.jpg)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410111551264.gif)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/readme.gif)

**（3）浮动的元素会具有行内块元素的特性**

任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。

- 块级盒子：没有设置宽度时默认宽度和父级一样宽，但是添加浮动后，它的大小根据内容来决定
- 行内盒子：宽度默认和内容一样宽，直接设置高宽无效，但是添加浮动后，它的大小可以直接设置
- 浮动的盒子中间是没有缝隙的，是紧挨着一起的 
- **即：默认宽度由内容决定，同时支持指定高宽，盒子之间无空隙**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动的元素具有行内块元素特点</title>
    <style>
        /* 任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。 */
        span,
        div {
            float: left;
            width: 200px;
            height: 100px;
            background-color: pink;
        }

        /* 如果行内元素有了浮动，则不需要转换块级\行内块元素就可以直接给高度和宽度 */
        p {
            float: right;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <span>span1</span>
    <span>span2</span>

    <div>div</div>
    <p>pppppppppppppp</p>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410120453590.jpg)

注意：之所以顶部没有对齐，原因是 p 标签自带的外边距 > span div 自带的外边距。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动的元素具有行内块元素特点</title>
    <style>
        * {
            margin: 0px;
        }

        /* 任何元素都可以浮动。不管原先是什么模式的元素，添加浮动之后具有行内块元素相似的特性。 */
        span,
        div {
            float: left;
            width: 200px;
            height: 100px;
            background-color: pink;
        }

        /* 如果行内元素有了浮动,则不需要转换块级\行内块元素就可以直接给高度和宽度 */
        p {
            float: right;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <span>span1</span>
    <span>span2</span>

    <div>div</div>
    <p>pppppppppppppp</p>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410120744356.jpg)

## 13.6 浮动元素经常和标准流父级搭配使用

为了约束浮动元素位置，我们网页布局一般采取的策略是：

**先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置。符合网页布局第一准侧。**

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410121200199.jpg)

应用举例：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410121702801.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动元素搭配标准流父盒子1</title>
    <style>
        .box {
            width: 1200px;
            height: 460px;
            background-color: black;
            margin: 0 auto;
        }

        .left {
            float: left;
            width: 230px;
            height: 460px;
            background-color: pink;
        }

        .right {
            float: left;
            width: 970px;
            height: 460px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="left">左侧</div>
        <div class="right">右侧</div>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410121929718.jpg)

---

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410123510406.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动元素搭配标准流父盒子2</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        /* 取消 li 前的圆点 */
        li {
            list-style: none;
        }

        .box {
            width: 1226px;
            height: 285px;
            background-color: pink;
            /* 让大盒子水平居中 */
            margin: 0 auto;
        }

        .box li {
            width: 296px;
            height: 285px;
            background-color: gray;
            float: left;
            /* 每个小盒子用右边距隔开 */
            margin-right: 14px;
        }

        /* 取消最后一个小盒子的右外边距 */
        /* 这里必须写 .box .last 要注意权重的问题  20 */
        .box .last {
            margin-right: 0;
        }
    </style>
</head>

<body>
    <ul class="box">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li class="last">4</li>
    </ul>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410122632628.jpg)

---

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410123520625.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动布局练习3</title>
    <style>
        .box {
            width: 1226px;
            height: 615px;
            background-color: pink;
            margin: 0 auto;
        }

        .left {
            float: left;
            width: 234px;
            height: 615px;
            background-color: gray;
        }

        .right {
            float: left;
            width: 992px;
            height: 615px;
            background-color: skyblue;
        }

        .right>div {
            float: left;
            width: 234px;
            height: 300px;
            background-color: pink;
            margin-left: 14px;
            margin-bottom: 14px;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="left">左青龙</div>
        <div class="right">
            <div>1</div>
            <div>2</div>
            <div>3</div>
            <div>4</div>
            <div>5</div>
            <div>6</div>
            <div>7</div>
            <div>8</div>
        </div>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410122643298.jpg)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220116104204568.png)

## 13.7 常见网页布局

### 13.7.1 初识常见网页布局

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410125437174.jpg)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410125449278.jpg)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>常见网页布局</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style: none;
        }

        .top {
            height: 50px;
            background-color: gray;
        }

        .banner {
            width: 980px;
            height: 150px;
            background-color: gray;
            margin: 10px auto;
        }

        .box {
            width: 980px;
            margin: 0 auto;
            height: 300px;
            background-color: pink;
        }

        .box li {
            float: left;
            width: 237px;
            height: 300px;
            background-color: gray;
            margin-right: 10px;
        }

        .box .last {
            margin-right: 0;
        }

        /* 只要是通栏的盒子（和浏览器一样宽）不需要指定宽度 */
        .footer {
            height: 200px;
            background-color: gray;
            margin-top: 10px;
        }
    </style>
</head>

<body>
    <div class="top">top</div>
    <div class="banner">banner</div>
    <div class="box">
        <ul>
            <li>1</li>
            <li>2</li>
            <li>3</li>
            <li class="last">4</li>
        </ul>
    </div>
    <div class="footer">footer</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410125651546.jpg)

### 13.7.2 浮动布局注意点

**（1）浮动和标准流的父盒子搭配**

先用标准流的父元素排列上下位置，之后内部子元素采取浮动排列左右位置。

**（2）一个元素浮动了，理论上其余的兄弟元素也要浮动**

一个盒子里面有多个子盒子，如果其中一个盒子浮动了，那么其他兄弟也应该浮动，以防止引起问题。

浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动注意点</title>
    <style>
        /* 如果一个子元素浮动了，尽量其他盒子也浮动，这样保证这些子元素一行显示 */
        .box {
            width: 900px;
            height: 300px;
            background-color: black;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: palevioletred;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 150px;
            background-color: palegreen;
        }

        .sanmao {
            float: left;
            width: 300px;
            height: 240px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="damao">大毛</div>		<!-- float: left; -->
        <div class="ermao">二毛</div>		<!-- float: left; -->
        <div class="sanmao">三毛</div>	<!-- float: left; -->
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410130344660.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动注意点</title>
    <style>
        /* 浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流。 */
        /* 大毛为标准流，所以大毛会占据其所在的一行，后面的二毛就算浮动也不会跑到大毛上方！*/
        .box {
            width: 900px;
            height: 300px;
            background-color: black;
            margin: 0 auto;
        }

        .damao {
            /* float: left; */
            width: 200px;
            height: 200px;
            background-color: palevioletred;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 150px;
            background-color: palegreen;
        }

        .sanmao {
            float: left;
            width: 300px;
            height: 240px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="damao">大毛</div>		<!-- 标准流 -->
        <div class="ermao">二毛</div>		<!-- float: left; -->
        <div class="sanmao">三毛</div>	<!-- float: left; -->
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410130529987.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动注意点</title>
    <style>
        /* 浮动的盒子只会影响浮动盒子后面的标准流，不会影响前面的标准流。 */
        .box {
            width: 900px;
            height: 300px;
            background-color: black;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: palevioletred;
        }

        .ermao {
            /* float: left; */
            width: 200px;
            height: 150px;
            background-color: palegreen;
        }

        .sanmao {
            float: left;
            width: 300px;
            height: 240px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="damao">大毛</div>		<!-- float: left; -->
        <div class="ermao">二毛</div>		<!-- 标准流 -->
        <div class="sanmao">三毛</div>	<!-- float: left; -->
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410130858443.jpg)

由于大毛是浮动的，所以原来大毛的位置会空出来，此时二毛就会向上补齐空位，由于二毛高度小于大毛，所以二毛被大毛挡住了，又因为二毛是标准流，所以二毛会占据所在的一行，所以后面浮动的三毛就只能在二毛的底部之下，又由于大毛也是浮动的，所以三毛就会紧贴在大毛右侧。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410131113979.jpg)

## 13.8 清除浮动

### 13.8.1 思考题

我们前面浮动元素有一个标准流的父元素，他们有一个共同的特点，都是有高度的。

但是，所有的父盒子都必须有高度吗？

答案：不一定！比如，一个产品列表，随着时期的不同，产品数量也不同，所需的盒子大小也会随之改变，那么直接固定盒子高度的形式显然就是不行的。再比如，文章之类的盒子，不同的文章字数是不相同的，那么显然盒子也不能直接固定高度。

理想中的状态，让子盒子撑开父亲。有多少孩子，我父盒子就有多高。

但是不给父盒子高度会有问题吗？

答案：会！但有方法解决（清除浮动）。

### 13.8.2 为什么需要清除浮动？

由于父级盒子很多情况下不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为 0 时，就会影响下面的标准流盒子。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410133601570.png)

- 由于浮动元素不再占用原文档流的位置，所以它会对后面的元素排版产生影响

- 此时一但父盒子下面有其他盒子，那么布局就会发生严重混乱！

### 13.8.3 清除浮动本质

- 清除浮动的本质是清除浮动元素造成的影响
- 如果父盒子本身有高度，则不需要清除浮动
- 清除浮动之后，父级就会根据浮动的子盒子自动检测高度。父级有了高度，就不会影响下面的标准流了

### 13.8.4 清除浮动

语法：

```css
选择器 { clear: 属性值; }
```

| 属性值 | 描述                                       |
| ------ | ------------------------------------------ |
| left   | 不允许左侧有浮动元素（清除左侧浮动的影响） |
| right  | 不允许右侧有浮动元素（清除右侧浮动的影响） |
| both   | 同时清除左右两侧浮动的影响                 |

我们实际工作中，几乎只用 `clear: both;`

清除浮动的策略是：闭合浮动。

### 13.8.5 清除浮动方法

1. 额外标签法也称为隔墙法，是 W3C 推荐的做法。(实际开发不推荐)
2. 父级添加 overflow 属性
3. 父级添加 after 伪元素
4. 父级添加 双伪元素

### 13.8.6 清除浮动 —— 额外标签法

额外标签法也称为隔墙法，是 W3C 推荐的做法。

额外标签法会在浮动元素末尾添加一个空的标签。例如 `<div style="clear: both"></div>`，或者其他标签（如 `<br>` 等）。

- 优点： 通俗易懂，书写方便
- 缺点： 添加许多无意义的标签，结构化较差

注意： 要求这个新的空标签必须是**块级元素**。

总结：

- 清除浮动本质是？

清除浮动的本质是清除浮动元素脱离标准流造成的影响。

- 清除浮动策略是？

闭合浮动。只让浮动在父盒子内部影响，不影响父盒子外面的其他盒子。

- 额外标签法？

**隔墙法，就是在最后一个浮动的子元素后面添加一个额外空标签（块级标签），添加清除浮动样式。**

实际工作可能会遇到，但是不常用。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>清除浮动之额外标签法</title>
    <style>
        .box {
            width: 800px;
            border: 3px solid black;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 300px;
            height: 200px;
            background-color: salmon;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }

        .footer {
            height: 200px;
            background-color: gray;
        }

        .clear {
            clear: both;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="damao">大毛</div>
        <div class="ermao">二毛</div>
        <div class="ermao">二毛</div>
        <div class="ermao">二毛</div>
        <div class="ermao">二毛</div>
        <div class="clear"></div>
        <!-- 这个新增的盒子要求必须是块级元素不能是行内元素 -->
        <!-- <span class="clear"></span> -->
    </div>
    <div class="footer"></div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410140435474.jpg)

### 13.8.7 清除浮动 —— 父级添加 overflow

可以给父级添加 `overflow` 属性，将其属性值设置为 `hidden`、 `auto` 或 `scroll`。

子不教，父之过，注意是给父元素添加代码。

- 优点：代码简洁
- 缺点：无法显示溢出的部分

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>overflow清除浮动</title>
    <style>
        .box {
            /* 清除浮动 */
            overflow: hidden;
            width: 800px;
            border: 1px solid blue;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 300px;
            height: 200px;
            background-color: purple;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .footer {
            height: 200px;
            background-color: black;
        }
    </style>
</head>

<body>
    <div class="box">
        <div class="damao">大毛</div>
        <div class="ermao">二毛</div>
    </div>
    <div class="footer"></div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410141717785.jpg)

### 13.8.8 清除浮动 —— :after 伪元素法

`:after` 方式是额外标签法的升级版，也是给父元素添加代码。

原理：自动在父盒子里的末尾添加一个 行内盒子，我们将它转换为 块级盒子，就间接实现了额外标签法。

```css
.clearfix:after {
	content: "";
	display: block;
	height: 0;
	clear: both;
	visibility: hidden;
}

.clearfix { 
    /* IE6、7 专有 */
	*zoom: 1;
}
```

注意：类名不一定非要是 clearfix，但是还是推荐这么写以提高可读性。

- 优点：没有增加标签，结构更简单
- 缺点：需要单独照顾低版本浏览器
- 代表网站： 百度、淘宝网、网易等

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>伪元素清除浮动</title>
    <style>
        .clearfix:after {
            content: "";
            display: block;
            height: 0;
            clear: both;
            visibility: hidden;
        }

        .clearfix {
            /* IE6、7 专有 */
            *zoom: 1;
        }

        .box {
            width: 800px;
            border: 1px solid blue;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 300px;
            height: 200px;
            background-color: purple;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .footer {
            height: 200px;
            background-color: black;
        }
    </style>
</head>

<body>
    <div class="box clearfix">
        <div class="damao">大毛</div>
        <div class="ermao">二毛</div>
    </div>
    <div class="footer"></div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410141717785-164230099450328.jpg)

### 13.8.9 清除浮动 —— 双伪元素清除浮动

额外标签法的升级版，也是给给父元素添加代码。

原理：自动在父盒子里的两端添加两个行内盒子，并把它们转换为 表格，间接实现了额外标签法。

```css
.clearfix:before,
.clearfix:after {
	content: "";
	display: table;
}

.clearfix:after {
	clear: both;
}

.clearfix {
    /* IE6、7 专有 */
	*zoom:1;
}
```

注意：类名不一定非要是 clearfix，但是还是推荐这么写以提高可读性。

- 优点：代码更简洁
- 缺点：需要单独照顾低版本浏览器

- 代表网站：小米、腾讯等

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>双伪元素清除浮动</title>
    <style>
        .clearfix:before,
        .clearfix:after {
            content: "";
            display: table;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            *zoom: 1;
        }

        .box {
            width: 800px;
            border: 1px solid blue;
            margin: 0 auto;
        }

        .damao {
            float: left;
            width: 300px;
            height: 200px;
            background-color: purple;
        }

        .ermao {
            float: left;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .footer {
            height: 200px;
            background-color: black;
        }
    </style>
</head>

<body>
    <div class="box clearfix">
        <div class="damao">大毛</div>
        <div class="ermao">二毛</div>
    </div>
    <div class="footer"></div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410141717785-164230099808930.jpg)

### 13.8.10 清除浮动总结

为什么需要清除浮动？

- 父级没高度
- 子盒子浮动了
- 影响下面布局了，我们就应该清除浮动了

| 清除浮动的方式         | 优点               | 缺点                                 |
| ---------------------- | ------------------ | ------------------------------------ |
| 额外标签法（隔墙法）   | 通俗易懂，书写方便 | 添加许多无意义的标签，结构化较差     |
| 父级 overflow: hidden; | 书写简单           | 溢出隐藏                             |
| 父级 after 伪元素      | 结构语义化正确     | 由于 IE6~7 不支持 :after，兼容性问题 |
| 父级双伪元素           | 结构语义化正确     | 由于 IE6~7 不支持 :after，兼容性问题 |

> after 伪元素、双伪元素 清除浮动的原理将在后面的 CSS3 中解释。









# 十四、定位

## 14.1 为什么需要定位？

提问： 以下情况使用标准流或者浮动能实现吗？

1. 某个元素可以**自由**的在一个盒子内移动位置，并且压住其他盒子。

2. 当我们滚动窗口的时候，盒子是**固定**屏幕某个位置的。

以上效果，标准流或浮动都无法快速实现，此时需要定位来实现。

所以：

1. 浮动可以让多个块级盒子一行没有缝隙排列显示， 经常用于横向排列盒子。
2. 定位则是可以让盒子自由的在某个盒子内移动位置或者固定屏幕中某个位置，并且可以压住其他盒子。

## 14.2 定位组成

定位：将盒子定在某一个位置，所以定位也是在摆放盒子， 按照定位的方式移动盒子。

`定位 = 定位模式 + 边偏移`

- 定位模式用于指定一个元素在文档中的定位方式
- 边偏移则决定了该元素的最终位置

**（1）定位模式**

定位模式决定元素的定位方式，它通过 CSS 的 `position` 属性来设置，其值可以分为四个。

| 值         | 语义     |
| ---------- | -------- |
| `static`   | 静态定位 |
| `relative` | 相对定位 |
| `absolute` | 绝对定位 |
| `fixed`    | 固定定位 |

**（2）边偏移**

边偏移就是定位的盒子移动的最终位置。有 `top`、`bottom`、`left` 和 `right` 4 个属性。

注意：可以为负值。

| 边偏移属性 | 实例           | 描述                                           |
| ---------- | -------------- | ---------------------------------------------- |
| `top`      | `top: 80px`    | 顶端偏移量，定义元素相对于其父元素上边线的距离 |
| `bottom`   | `bottom: 80px` | 底部偏移量，定义元素相对于其父元素下边线的距离 |
| `left`     | `left: 80px`   | 左侧偏移量，定义元素相对于其父元素左边线的距离 |
| `rigth`    | `right: 80px`  | 右侧偏移量，定义元素相对于其父元素右边线的距离 |

## 14.3 静态定位 static（了解）

静态定位是元素的默认定位方式，无定位的意思。

语法：

```css
选择器 { position: static; }
```

1. 静态定位按照标准流特性摆放位置，它没有边偏移

2. 静态定位在布局时很少用到

## 14.4 相对定位 relative（重要）

相对定位是元素在移动位置的时候**相对于它原来的位置**来说的定位（自恋型）。

语法：

```css
选择器 { position: relative; }
```

相对定位的特点：（务必记住）

1. 它是相对于自己原来的位置来移动的（移动位置的时候参照点是自己原来的位置点）
2. 原来在**标准流的位置继续占有**，后面的盒子仍然以标准流的方式对待它

因此，**相对定位并没有脱标**。它最典型的应用是给绝对定位当爹的。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>相对定位</title>
    <style>
        .box1 {
            position: relative;
            top: 100px;
            left: 100px;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .box2 {
            width: 200px;
            height: 200px;
            background-color: deeppink;
        }
    </style>
</head>

<body>
    <div class="box1">

    </div>
    <div class="box2">

    </div>

</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021041022482559.gif" style="zoom:50%;" />

## 14.5 绝对定位 absolute（重要）

绝对定位是元素在移动位置的时候**相对于它祖先元素**来说的定位（拼爹型）。

语法：

```css
选择器 { position: absolute; }
```

绝对定位的特点：（务必记住）

1. 如果没有祖先元素或者祖先元素没有定位，则以浏览器为准定位（Document 文档）
2. 如果祖先元素有定位（相对、绝对、固定定位），则以**最近一级的有定位祖先元素为参考点**移动位置
3. 绝对定位**不再占有原先的位置**（脱标），并且**脱标的程度大于浮动**（会压住浮动）

所以绝对定位是**脱离标准流**的。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>绝对定位-无父亲或者父亲无定位</title>
    <style>
        .father {
            width: 500px;
            height: 500px;
            background-color: skyblue;
        }

        .son {
            position: absolute;
            /* top: 10px;
            left: 10px; */
            /* top: 100px;
            right: 200px; */
            left: 0;
            bottom: 0;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410225323359.gif" style="zoom:50%;" />

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>绝对定位-父级有定位-一级父亲</title>
    <style>
        .father {
            position: relative;
            width: 500px;
            height: 500px;
            background-color: skyblue;
        }
        
        .son {
            position: absolute;
            /* top: 10px;
            left: 10px; */
            /* top: 100px;
            right: 200px; */
            left: 0;
            bottom: 0;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
    </div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410225829682.gif" style="zoom:50%;" />

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>绝对定位-父级有定位-多级父亲</title>
    <style>
        /* 以最近一级的有定位祖先元素为参考点移动位置 */
        /* 即：谁带有定位并且离我最近，我就以谁为准！ */
        .yeye {
            position: relative;
            width: 800px;
            height: 800px;
            background-color: hotpink;
            padding: 50px;
        }

        .father {
            width: 500px;
            height: 500px;
            background-color: skyblue;
        }

        .son {
            position: absolute;
            left: 30px;
            bottom: 10px;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="yeye">
        <div class="father">
            <div class="son"></div>
        </div>
    </div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410230310223.gif" style="zoom:50%;" />

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>绝对定位-脱标</title>
    <style>
        .father {
            position: relative;
            width: 500px;
            height: 500px;
            background-color: skyblue;
        }

        .son {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 200px;
            height: 200px;
            background-color: pink;
        }

        .son2 {
            width: 200px;
            height: 200px;
            background-color: gray;
        }
    </style>
</head>

<body>
    <div class="father">
        <div class="son"></div>
        <div class="son2"></div>
    </div>

</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410231150803.gif" style="zoom:50%;" />

**问题：**

1. 绝对定位和相对定位到底有什么使用场景呢？
2. 为什么说相对定位给绝对定位当爹的呢？

## 14.6 子绝父相的由来

弄清楚这个口诀，就明白了绝对定位和相对定位的使用场景。

这个 “子绝父相” 太重要了，是我们学习定位的口诀，是定位中最常用的一种方式这句话的意思是：子级是绝对定位的话，父级要用相对定位。

1. **子级绝对定位，不会占有位置，可以放到父盒子里面的任何一个地方，不会影响其他的兄弟盒子**
2. **父盒子需要加定位限制子盒子在父盒子内显示**
3. **父盒子布局时，需要占有位置，因此父亲只能是相对定位**

这就是子绝父相的由来，所以相对定位经常用来作为绝对定位的父级。

总结： 因为父级需要占有位置，因此是相对定位， 子盒子不需要占有位置，则是绝对定位。

当然，子绝父相不是永远不变的，如果父元素不需要占有位置，“子绝父绝” 也会遇到。

**思考：为什么非要用定位？浮动不可以吗？**

答案：用浮动做某些布局远远没有定位简单和方便！例如，轮播图。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210410231958333-164233328088033.jpg" style="zoom:50%;" />

- 左右两边的图片切换按钮，利用浮动也可以做。但是，假如放置图片的盒子是在切换按钮之前添加的，那么根据浮动元素只能影响后面盒子的特性，切换按钮就只可能在图片底部之下，不可能浮于图片之上！
- 就算切换按钮用浮动实现了，但是左下角的轮播序号点图如果也用浮动实现，结果就是轮播序号点图会与切换按钮在一行并排浮动！

可见，浮动单纯用于左右排列盒子是非常适合的，但是用于空间层次上排列盒子就不适合了！应该用定位实现。

**重点：竖向上布局找标准流，横向上布局找浮动，空间上布局找定位！**

【案例：学成在线 hot new 模块】

```html
<div class="box-bd">
	<ul class="clearfix">	
    	<li>
            <!-- 
			<em> 不是单纯的倾斜文本，该标签本质上是告诉浏览器把其中的文本表示为强调的内容，
			所以，<em> 可以用来包含强调的元素。
			-->
        	<em>
            	<img src="images/hot.png" alt="">
          	</em>
         	<img src="images/pic.png" alt="">
          	<h4>
            Think PHP 5.0 博客系统实战项目演练
          	</h4>
          	<div class="info">
            	<span>高级</span> • 1125人在学习
          	</div>
    	</li>
        ...
    </ul>
</div>
```

```css
.box-bd ul {
    width: 1225px;
}
.box-bd ul li {
    /* 子绝父相 */
    position: relative;
    float: left;
    width: 228px;
    height: 270px;
    background-color: #fff;
    margin-right: 15px;
    margin-bottom: 15px;
   
}
.box-bd ul li > img {
    width: 100%;
}
.box-bd ul li h4 {
    margin: 20px 20px 20px 25px;
    font-size: 14px;
    color: #050505;
    font-weight: 400;
}
.box-bd ul li em {
    /* 子绝父相 */
    position: absolute;
    top: 4px;
    right: -4px;
}
.box-bd .info {
    margin: 0 20px 0 25px;
    font-size: 12px;
    color: #999;
}
.box-bd .info span {
    color: #ff7c2d;
}
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411001207402.jpg)

## 14.7 固定定位 fixed （重要）

固定定位是元素固定于浏览器可视区的位置。

主要使用场景： 可以在浏览器页面滚动时元素的位置不会改变。

语法：

```css
选择器 { position: fixed; }
```

固定定位的特点（务必记住）：

1. 以**浏览器的可视窗口为参照点**移动元素
   - 跟父元素没有任何关系
   - 不随滚动条滚动
2. 固定定位不再占有原先的位置
   - 固定定位也是**脱标**的，其实固定定位也可以看做是一种**特殊的绝对定位**。

应用举例：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411000419348.gif" style="zoom:50%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>固定定位</title>
    <style>
        .dj {
            position: fixed;
            top: 100px;
            left: 200px;
        }
    </style>
</head>

<body>
    <div class="dj">
        <img src="images/pvp.png" alt="">
    </div>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>
    <p>请尽情吩咐妲己，主人</p>

</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411002138603.gif" style="zoom:50%;" />

## 14.8 固定定位小技巧：固定在版心右侧位置

**小算法：**

1. 让固定定位的盒子 `left: 50%`，走到浏览器可视区（也可以看做版心） 一半的位置
2. 让固定定位的盒子 `margin-left: 版心宽度的一半距离`，多走版心宽度的一半位置

就可以让固定定位的盒子贴着版心右侧对齐了。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>固定定位小技巧-固定到版心右侧</title>
    <style>
        .w {
            width: 800px;
            height: 1400px;
            background-color: pink;
            margin: 0 auto;
        }

        .fixed {
            position: fixed;
            /* 1. 走浏览器宽度的一半 */
            left: 50%;
            /* 2. 利用 margin 走版心盒子宽度的一半距离（为了美观多加了 5px）*/
            margin-left: 405px;
            width: 50px;
            height: 150px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="fixed"></div>
    <div class="w">版心盒子 800像素</div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411002750577.gif)

## 14.9 粘性定位 sticky（了解）

粘性定位可以被认为是相对定位和固定定位的混合。

Sticky 粘性的。

语法：

```css
选择器 { position: sticky; top: 10px; }
```

粘性定位的特点：

1. 以浏览器的**可视窗口为参照点**移动元素（固定定位特点）
2. 粘性定位**占有原先的位置**（相对定位特点）
3. 必须添加 top 、left、right、bottom 其中一个才有效

跟页面滚动搭配使用。 兼容性较差，IE 不支持。

未来开发的趋势，但目前并不常用（目前用 javascript 来实现粘性定位效果）。

应用举例：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411000442416.gif" style="zoom:50%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>粘性定位</title>
    <style>
        body {
            height: 3000px;
        }

        .nav {
            /* 粘性定位 */
            position: sticky;
            top: 0;
            width: 800px;
            height: 50px;
            background-color: pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="nav">我是导航栏</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411003401335.gif)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/a6b709f41c9f42558b8d6870202bc171.gif)

## 14.10 定位的总结

| 定位模式          | 是否脱标         | 移动位置           | 是否常用   |
| ----------------- | ---------------- | ------------------ | ---------- |
| static 静态定位   | 否               | 不能使用边偏移     | 很少       |
| relative 相对定位 | 否（占有位置）   | 相对于自身位置移动 | 常用       |
| absolute 绝对定位 | 是（不占有位置） | 带有定位的父级     | 常用       |
| fixed 固定定位    | 是（不占有位置） | 浏览器可视区       | 常用       |
| sticky 粘性定位   | 否（占有位置）   | 浏览器可视区       | 当前阶段少 |

1. 一定记住，相对定位、固定定位、绝对定位 两个大的特点： 1. 是否占有位置（脱标否） 2. 以谁为基准点移动位置。
2. 学习定位重点学会子绝父相。

## 14.11 定位叠放次序 z-index

在使用定位布局时，可能会出现盒子重叠的情况。此时，可以使用 z-index 来控制盒子的前后次序（z轴）。

语法：

```css
选择器 { z-index: 1; }
```

- 数值可以是正整数、负整数或 0，默认是 auto，数值越大，盒子越靠上
- 如果属性值相同，则按照书写顺序，后来居上
- 数字后面不能加单位
- 只有定位的盒子才有 z-index 属性

## 14.12 定位的拓展

**（1）绝对定位的盒子居中**

加了绝对定位的盒子不能通过 `margin: 0 auto` 水平居中，但是可以通过以下计算方法实现水平和垂直居中。

1. `left: 50%;`：让盒子的左侧移动到父级元素的水平中心位置。
2. `margin-left: -0.5widthpx;`：让盒子向左移动自身宽度的一半。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>绝对定位水平垂直居中</title>
    <style>
        .box {
            position: absolute;
            /* 1. left 走 50%  父容器宽度的一半 */
            left: 50%;
            /* 2. margin 负值 往左边走 自己盒子宽度的一半 */
            margin-left: -100px;
            /* 垂直居中同理 */
            top: 50%;
            margin-top: -100px;
            width: 200px;
            height: 200px;
            background-color: pink;
            /* margin: auto; */
        }
    </style>
</head>

<body>
    <div class="box"></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411004813982.jpg)

**（2）定位特殊特性**

**绝对定位和固定定位也和浮动类似。**

1. 行内元素添加绝对或者固定定位，可以直接设置高度和宽度。
2. 块级元素添加绝对或者固定定位，如果不给宽度或者高度，默认大小是内容的大小。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>定位的特殊特性</title>
    <style>
        span {
            position: absolute;
            top: 100px;
            width: 200px;
            height: 150px;
            background-color: pink;
        }

        div {
            position: absolute;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <span>123</span>

    <div>abcd</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411005338704.jpg)

**（3）脱标的盒子不会触发外边距塌陷**

浮动元素、绝对定位（固定定位）元素的都不会触发外边距合并的问题。

**（4）绝对定位（固定定位）会完全压住盒子**

浮动元素不同，只会压住它下面标准流的盒子，但是不会压住下面标准流盒子里面的文字（图片）。

但是绝对定位（固定定位） 会压住下面标准流所有的内容。

浮动之所以不会压住文字，因为浮动产生的目的最初是为了做文字环绕效果的。 文字会围绕浮动元素。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>浮动产生原来的目的是做文字环绕效果</title>
    <style>
        img {
            float: left;
        }
    </style>
</head>

<body>
    1993年，在古装片《战神传说》中扮演一个武功超群的渔民；同年，主演动作喜剧片《至尊三十六计之偷天换日》，在片中饰演赌术高明的千门高手钱文迪；此外，他还主演了爱情片《天长地久》，在片中塑造了一个风流不羁的江湖浪子形象。
    1994年，刘德华投资并主演了剧情片《天与地》，在片中饰演面对恶势力却毫不退缩的禁毒专员张一鹏。1995年，主演赛车励志片《烈火战车》，在片中饰演叛逆、倔强的阿祖，并凭借该片获得第15届香港电影金像奖最佳男主角提名；同年在动作片《大冒险家》中演绎了立仁从小时候父母双亡到长大后进入泰国空军的故事。
    1996年，主演黑帮题材的电影《新上海滩》，在片中饰演对冯程程痴情一片的丁力。1997年，担任剧情片《香港制造》的制作人；同年，主演爱情片《天若有情之烽火佳人》，在片中饰演家世显赫的空军少尉刘天伟；12月，与梁家辉联袂主演警匪动作片《黑金》，在片中饰演精明干练、嫉恶如仇的调查局机动组组长方国辉。1998年，主演动作片《龙在江湖》
    <img src="images/img.jpg" alt="">
    ，饰演重义气的黑帮成员韦吉祥；同年，出演喜剧片《赌侠1999》；此外，他还担任剧情片《去年烟花特别多》的制作人。
    1993年，在古装片《战神传说》中扮演一个武功超群的渔民；同年，主演动作喜剧片《至尊三十六计之偷天换日》，在片中饰演赌术高明的千门高手钱文迪；此外，他还主演了爱情片《天长地久》，在片中塑造了一个风流不羁的江湖浪子形象。
    1994年，刘德华投资并主演了剧情片《天与地》，在片中饰演面对恶势力却毫不退缩的禁毒专员张一鹏。1995年，主演赛车励志片《烈火战车》，在片中饰演叛逆、倔强的阿祖，并凭借该片获得第15届香港电影金像奖最佳男主角提名；同年在动作片《大冒险家》中演绎了立仁从小时候父母双亡到长大后进入泰国空军的故事。
    1996年，主演黑帮题材的电影《新上海滩》，在片中饰演对冯程程痴情一片的丁力。1997年，担任剧情片《香港制造》的制作人；同年，主演爱情片《天若有情之烽火佳人》，在片中饰演家世显赫的空军少尉刘天伟；12月，与梁家辉联袂主演警匪动作片《黑金》，在片中饰演精明干练、嫉恶如仇的调查局机动组组长方国辉。1998年，主演动作片《龙在江湖》，饰演重义气的黑帮成员韦吉祥；同年，出演喜剧片《赌侠1999》；此外，他还担任剧情片《去年烟花特别多》的制作人。
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411005813237.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>定位会完全压住标准流盒子内容</title>
    <style>
        .box {
            /* 1.浮动的元素不会压住下面标准流的文字 */
            /* float: left; */
            /* 2. 绝对定位（固定定位） 会压住下面标准流所有的内容。 */
            position: absolute;
            width: 150px;
            height: 150px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="box"></div>
    <p>阁下何不同风起，扶摇直上九万里</p>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411005914370.jpg)

## 综合案例

**【案例：淘宝焦点图布局】**

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411010357458.jpg)

布局分析：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411010357453.jpg)

制作：

1. 大盒子我们类名为： tb-promo 淘宝广告
2. 里面先放一张图片
3. 左右两个按钮用链接就好了，左箭头 prev 右箭头 next
4. 底侧小圆点 ul 继续做，类名为 promo-nav

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>淘宝轮播图做法</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        li {
            list-style: none;
        }

        .tb-promo {
            position: relative;
            width: 520px;
            height: 280px;
            background-color: pink;
            margin: 100px auto;
        }

        .tb-promo img {
            width: 520px;
            height: 280px;
        }

        /* 并集选择器可以集体声明相同的样式 */
        .prev,
        .next {
            position: absolute;
            /* 绝对定位的盒子垂直居中 */
            top: 50%;
            margin-top: -15px;
            /* 加了绝对定位的盒子可以直接设置高度和宽度 */
            width: 20px;
            height: 30px;
            background: rgba(0, 0, 0, .3);
            text-align: center;
            line-height: 30px;
            color: #fff;
            text-decoration: none;
        }

        .prev {
            left: 0;
            /* border-radius: 15px; */
            border-top-right-radius: 15px;
            border-bottom-right-radius: 15px;
        }

        .next {
            /* 如果一个盒子既有 left 属性也有 right 属性，则默认会执行 left 属性 
            同理 top bottom 会执行 top */
            right: 0;
            /* border-radius: 15px; */
            border-top-left-radius: 15px;
            border-bottom-left-radius: 15px;
        }

        .promo-nav {
            position: absolute;
            bottom: 15px;
            left: 50%;
            margin-left: -35px;
            width: 70px;
            height: 13px;
            /* background-color: pink; */
            background: rgba(255, 255, 255, .3);
            border-radius: 7px;
        }

        .promo-nav li {
            float: left;
            width: 8px;
            height: 8px;
            background-color: #fff;
            border-radius: 50%;
            margin: 3px;
        }

        /* 不要忘记选择器权重的问题 */
        .promo-nav .selected {
            background-color: #ff5000;
        }
    </style>
</head>

<body>
    <div class="tb-promo">
        <img src="images/tb.jpg" alt="">
        <!-- 左侧按钮箭头 -->
        <a href="#" class="prev"> &lt; </a>
        <!-- 右侧按钮箭头 -->
        <a href="#" class="next"> &gt; </a>
        <!-- 小圆点 -->
        <ul class="promo-nav">
            <li class="selected"></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411010727218.jpg)

## 14.13 网页布局总结

通过盒子模型，清楚知道大部分 html 标签是一个盒子。

通过 CSS 浮动、定位可以让每个盒子排列成为网页。

一个完整的网页，是标准流、浮动、定位一起完成布局的，每个都有自己的专门用法。

1. 标准流

可以让盒子上下排列或者左右排列，垂直的块级盒子显示就用标准流布局。

2. 浮动

可以让多个块级元素一行显示或者左右对齐盒子，多个块级盒子水平显示就用浮动布局。

3. 定位

定位最大的特点是有层叠的概念，就是可以让多个盒子前后叠压来显示。如果元素自由在某个盒子内移动就用定位布局。

**重点：竖向上布局找标准流，横向上布局找浮动，空间上布局找定位！**

## 14.14 元素的显示与隐藏

类似网站广告，当我们点击关闭就不见了，但是我们重新刷新页面，会重新出现！

本质：让一个元素在页面中隐藏或者显示出来。

注意：是隐藏，不是删除！

1. display 显示隐藏（脱标）
2. visibility 显示隐藏（不脱标）
3. overflow 溢出显示隐藏

### 14.14.1 display 属性

display 属性用于设置一个元素应如何显示。

- `display: none`：隐藏对象
- `display：block`：除了转换为块级元素之外，同时还有显示元素的意思

display 隐藏元素后，不再占有原来的位置（**脱标**）。

后面应用及其广泛，搭配 JS 可以做很多的网页特效。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之display</title>
    <style>
        .peppa {
            display: none;
            /* display: block; */
            width: 200px;
            height: 200px;
            background-color: pink;

        }

        .george {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="peppa">佩奇</div>		<!-- 佩奇被隐藏 -->
    <div class="george">乔治</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021041101335757.gif)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之display</title>
    <style>
        .peppa {
            /* display: none; */
            display: block;
            width: 200px;
            height: 200px;
            background-color: pink;

        }

        .george {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="peppa">佩奇</div>		<!-- 佩奇被显示 -->
    <div class="george">乔治</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411013334551.gif)

### 14.14.2 visibility 可见性

visibility 属性用于指定一个元素应可见还是隐藏。

- `visibility：visible`：元素可视
- `visibility：hidden`：元素隐藏

visibility **隐藏元素后，继续占有原来的位置**。

如果隐藏元素想要原来位置， 就用 visibility：hidden。

如果隐藏元素不想要原来位置， 就用 display：none（用处更多，重点）。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之display</title>
    <style>
        .baba {
            visibility: hidden;
            width: 200px;
            height: 200px;
            background-color: pink;

        }

        .mama {
            width: 200px;
            height: 200px;
            background-color: skyblue;
        }
    </style>
</head>

<body>
    <div class="baba">猪爸爸</div>
    <div class="mama">猪妈妈</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411013759206.gif)

### 14.14.3 overflow 溢出

overflow 属性指定了如果内容溢出一个元素的框（**超过其指定高度及宽度**）时，会发生什么。

| 属性值    | 描述                                                   |
| --------- | ------------------------------------------------------ |
| `visible` | 不剪切内容也不添加滚动条（默认方式）                   |
| `hidden`  | 不显示超过对象尺寸的内容，超出的部分隐藏掉（并非删除） |
| `scroll`  | 不管超出的内容否，总是显示滚动条                       |
| `auto`    | 超出自动显示滚动条，不超出不显示滚动条                 |

一般情况下，我们都不想让溢出的内容显示出来，因为溢出的部分会影响布局。

但是如果有定位的盒子， 请慎用 overflow: hidden 因为它会隐藏多余的部分（例如：学成在线 hot new 模块，右上角有故意超出的部分，此时就不能使用 overflow: hidden）。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            /* overflow: scroll; */
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            /* overflow: auto; */
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》，是由英国人阿斯特利（Astley）、贝克（Baker）、戴维斯（Davis）创作、
        导演和制作的一部英国学前电视动画片，也是历年来最具潜力的学前儿童品牌。
        故事围绕小猪佩奇与家人的愉快经历，幽默而有趣，
        藉此宣扬传统家庭观念与友情，鼓励小朋友们体验生活。
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015310864.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            overflow: visible;
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            /* overflow: scroll; */
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            /* overflow: auto; */
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》，是由英国人阿斯特利（Astley）、贝克（Baker）、戴维斯（Davis）创作、
        导演和制作的一部英国学前电视动画片，也是历年来最具潜力的学前儿童品牌。
        故事围绕小猪佩奇与家人的愉快经历，幽默而有趣，
        藉此宣扬传统家庭观念与友情，鼓励小朋友们体验生活。
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015310864-164232733571925.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            overflow: hidden;
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            /* overflow: scroll; */
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            /* overflow: auto; */
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》，是由英国人阿斯特利（Astley）、贝克（Baker）、戴维斯（Davis）创作、
        导演和制作的一部英国学前电视动画片，也是历年来最具潜力的学前儿童品牌。
        故事围绕小猪佩奇与家人的愉快经历，幽默而有趣，
        藉此宣扬传统家庭观念与友情，鼓励小朋友们体验生活。
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015442418.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            overflow: scroll;
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            /* overflow: auto; */
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》，是由英国人阿斯特利（Astley）、贝克（Baker）、戴维斯（Davis）创作、
        导演和制作的一部英国学前电视动画片，也是历年来最具潜力的学前儿童品牌。
        故事围绕小猪佩奇与家人的愉快经历，幽默而有趣，
        藉此宣扬传统家庭观念与友情，鼓励小朋友们体验生活。
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015532804.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            overflow: scroll;
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            /* overflow: auto; */
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015657674.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            /* overflow: scroll; */
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            overflow: auto;
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》，是由英国人阿斯特利（Astley）、贝克（Baker）、戴维斯（Davis）创作、
        导演和制作的一部英国学前电视动画片，也是历年来最具潜力的学前儿童品牌。
        故事围绕小猪佩奇与家人的愉快经历，幽默而有趣，
        藉此宣扬传统家庭观念与友情，鼓励小朋友们体验生活。
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021041101581715.jpg)

---

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>显示隐藏元素之overflow</title>
    <style>
        .peppa {
            /* overflow: visible; */
            /* overflow: hidden; */
            /* scroll 溢出的部分显示滚动条  不溢出也显示滚动条 */
            /* overflow: scroll; */
            /* auto 溢出的时候才显示滚动条 不溢出不显示滚动条 */
            overflow: auto;
            width: 200px;
            height: 200px;
            border: 3px solid pink;
            margin: 100px auto;
        }
    </style>
</head>

<body>
    <div class="peppa">
        小猪佩奇》，又译作《粉红猪小妹》（台湾译为粉红猪），原名为《Peppa
        Pig》
    </div>

</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411015908937.jpg)

### 14.14.5 总结

1. display 显示隐藏元素 但是不保留位置
2. visibility 显示隐藏元素 但是保留原来的位置
3. overflow 溢出显示隐藏 但是只是对于溢出的部分处理

## 综合案例

**【案例：土豆网鼠标经过显示遮罩】**

1. 练习元素的显示与隐藏
2. 练习元素的定位

核心原理：原先半透明的黑色遮罩看不见， 鼠标经过大盒子，就显示出来。

遮罩的盒子不占有位置，就需要用绝对定位 和 display 配合使用。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>仿土豆网显示隐藏遮罩案例</title>
    <style>
        .tudou {
            position: relative;
            width: 444px;
            height: 320px;
            background-color: pink;
            margin: 30px auto;
        }

        .tudou img {
            width: 100%;
            height: 100%;
        }

        .mask {
            /* 隐藏遮罩层 */
            display: none;
            /* 添加定位使其能够浮与其他盒子上方 */
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, .4) url(images/arr.png) no-repeat center;
        }

        /* 当我们鼠标经过了 土豆这个盒子，就让里面遮罩层显示出来 */
        .tudou:hover .mask {
            /* 而是显示元素 */
            display: block;
        }
    </style>
</head>

<body>
    <div class="tudou">
        <div class="mask"></div>
        <img src="images/tudou.jpg" alt="">
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210411020723514.gif)









# 十五、动画转换



## 15.1 CSS3 2D转换

转换（transform）是 CSS3 中具有颠覆性的特征之一。可以实现元素的位移、旋转、缩放等效果。

转换（transform）你可以简单理解为变形。

- 移动：translate
- 旋转：rotate
- 缩放：scale

### 15.1.1 二维坐标系

2D 转换是改变标签在二维平面上的位置和形状的一种技术，先来学习二维坐标系。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210424224831926.png" style="zoom: 50%;" />

### 15.1.2 2D 转换之移动 translate

2D 移动是 2D 转换里面的一种功能，可以改变元素在页面中的位置，类似定位。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210424225359665.png)

语法：

```css
transform: translate(x, y); 
/* 或者分开写 */
transform: translateX(n);
transform: translateY(n);
```

重点：

- 定义 2D 转换中的移动，沿着 X 和 Y 轴移动元素
- translate 最大的优点：**不会影响到任何其他元素的位置**（优于定位的地方）
- translate 中的百分比单位是**相对于自身**元素的 translate: (50%, 50%);
- **对行内元素没有效果**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>2D转换之移动translate</title>
    <style>
        /* 移动盒子的位置：定位、盒子的外边距、2D转换移动 */

        div {
            width: 200px;
            height: 200px;
            background-color: hotpink;
            /* x就是x轴上移动位置，y就是y轴上移动位置，中间用逗号分隔 */
            /* transform: translate(x, y); */
            /* transform: translate(100px, 100px); */
            /* 1. 只移动x坐标 */
            /* transform: translate(100px, 0); */
            /* transform: translateX(100px); */
            /* 2. 只移动y坐标 */
            /* transform: translate(0, 100px); */
            /* transform: translateY(100px); */
        }

        div:first-child {
            transform: translate(30px, 30px);
        }

        div:last-child {
            background-color: black;
        }
    </style>
</head>

<body>
    <div></div>
    <div></div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210424230655649.png" style="zoom: 80%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>让一个盒子水平居中</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        div {
            position: relative;
            width: 500px;
            height: 500px;
            background-color: hotpink;
            /* 1. 我们 tranlate 里面的参数是可以用 % */
            /* 2. 如果里面的参数是 % 那么移动的距离是以盒子自身的宽度或者高度来对比的 */
            /* 这里的 50% 就是 250px 因为盒子的宽度是 500px */
            /* transform: translateX(50%); */
        }

        p {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 200px;
            height: 200px;
            background-color: black;
            /*
            在前面的定位中使用直接减去自身宽度与高度的一半，此种方式的缺点在于不能随盒子大小的变化而变化
            margin-top: -100px;
            margin-left: -100px;
            */
            transform: translate(-50%, -50%);
        }

        span {
            /* translate 对于行内元素是无效的 */
            transform: translate(300px, 300px);
        }
    </style>
</head>

<body>
<div>
    <p></p>
</div>
<span>123</span>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425000618488.png" style="zoom:50%;" />

### 15.1.3 2D 转换之旋转 rotate

2D 旋转指的是让元素在 2 维平面内顺时针旋转或者逆时针旋转。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021042500110849.png" style="zoom:50%;" />

语法：

```css
transform: rotate(度数)
```

重点：

- rotate 里面跟度数，单位是 deg，比如 rotate(45deg)
- 角度为正时，顺时针；负时，逆时针
- 默认旋转的中心点是元素的中心点

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>2D转换之旋转rotate</title>
    <style>
        img {
            width: 150px;
            /* 顺时针旋转45度 */
            /* transform: rotate(45deg); */
            border-radius: 50%;
            border: 5px solid pink;
            /* 过渡写到本身上，谁做动画给谁加 */
            transition: all 0.5s;
        }

        img:hover {
            transform: rotate(360deg);
        }
    </style>
</head>

<body>
<img src="media/pic.jpg" alt="">
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021042500182360.gif)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>旋转三角</title>
    <style>
        div {
            position: relative;
            width: 249px;
            height: 35px;
            border: 1px solid #000;
        }

        /* 三角可以通过盒子来制作，不一定非得字体图标 */
        /* 让一个旋转45度的正方形（菱形）的两个边框显示出来 */
        div::after {
            content: "";
            position: absolute;
            top: 8px;
            right: 15px;
            width: 10px;
            height: 10px;
            border-right: 1px solid #000;
            border-bottom: 1px solid #000;
            transform: rotate(45deg);
            transition: all 0.2s;
        }

        /* 鼠标经过 div 里面的三角旋转 */
        div:hover::after {
            transform: rotate(225deg);
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425075729489.gif)

### 15.1.4 转换中心点 transform-origin

我们可以设置元素转换的中心点。

语法：

```css
transform-origin: x y;
```

重点：

- 注意后面的参数 x 和 y 用空格隔开
- x y 默认转换的中心点是元素的中心点（50% 50%）
- 还可以给 x y 设置 像素 或者 方位名词（top  bottom  left  right  center）

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>transform-origin</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            margin: 100px auto;
            transition: all 1s;
            /* 1.可以跟方位名词 */
            /* transform-origin: left bottom; */
            /* 2. 默认的是 50% 50% 等价于 center center */
            /* 3. 可以是 px 像素 */
            transform-origin: 25px 25px;
        }

        div:hover {
            transform: rotate(360deg);
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425081548859.gif" style="zoom: 33%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>旋转中心点</title>
    <style>
        div {
            /* 溢出隐藏 */
            overflow: hidden;
            width: 200px;
            height: 200px;
            border: 1px solid pink;
            margin: 10px;
            float: left;
        }

        div::before {
            content: "黑马";
            display: block;
            width: 100%;
            height: 100%;
            background-color: hotpink;
            transform: rotate(180deg);
            transform-origin: left bottom;
            transition: all 0.4s;
        }

        /* 鼠标经过 div 里面的 before 复原 */
        div:hover::before {
            transform: rotate(0deg);
        }
    </style>
</head>

<body>
<div></div>
<div></div>
<div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425082315183.gif)

### 15.1.5 2D 转换之缩放 scale

缩放，顾名思义，可以放大和缩小。只要给元素添加上了这个属性就能控制它放大还是缩小。

语法：

```css
transform: scale(x, y);
```

注意：

- 注意其中的 x 和 y 用逗号分隔
- transform: scale(1, 1) ：宽和高都放大一倍，相当于没有放大
- transform: scale(2, 2) ：宽和高都放大了 2 倍
- transform: scale(2) ：只写一个参数，第二个参数默认等于第一个参数，相当于 scale(2, 2)
- transform: scale(0.5, 0.5) ：缩小
- scale 缩放最大的优势：可以设置缩放的基准点（默认以中心点缩放）；并且缩放不会影响其他盒子的位置（以上两个特点都是直接设置 width 和 height 都无法做到的）

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>2D转换之缩放</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            /* 可以设置缩放的中心点 */
            /* transform-origin: left bottom; */
        }
        
        div:hover {
            /* 1. 里面写的数字不跟单位 就是倍数的意思， 1 就是 1 倍；2 就是 2 倍 */
            /* transform: scale(x, y); */
            /* transform: scale(2, 2); */
            /* 2. 修改了宽度为原来的 2 倍，高度不变 */
            /* transform: scale(2, 1); */
            /* 3. 等比例缩放 同时修改宽度和高度，我们有简单的写法以下是宽度修改了 2 倍，高度默认和第一个参数一样 */
            /* transform: scale(2); */
            /* 4. 我们可以进行缩小，小于 1就是缩小 */
            /* transform: scale(0.5, 0.5); */
            /* transform: scale(0.5); */
            /* 5. scale 的优势之处：不会影响其他的盒子，而且可以设置缩放的中心点 */
            /*
            直接设置宽高时无法做到以上优点的！
            width: 300px;
            height: 300px;
            */
            transform: scale(2);
        }
    </style>
</head>

<body>
    <div></div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425085529554.gif" style="zoom:50%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>图片放大案例</title>
    <style>
        div {
            width: 225px;
            height: 137px;
            overflow: hidden;
            float: left;
            margin: 10px;
        }

        div img {
            transition: all .4s;
        }

        div img:hover {
            transform: scale(1.1);
        }
    </style>
</head>

<body>
<div>
    <a href="#"><img src="media/scale.jpg" alt=""></a>
</div>
<div>
    <a href="#"><img src="media/scale.jpg" alt=""></a>
</div>
<div>
    <a href="#"><img src="media/scale.jpg" alt=""></a>
</div>
</body>
 
</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425085900832.gif)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        li {
            float: left;
            width: 30px;
            height: 30px;
            border: 1px solid hotpink;
            margin: 10px;
            text-align: center;
            line-height: 30px;
            list-style: none;
            border-radius: 50%;
            cursor: pointer;
            transition: all .4s;
        }

        li:hover {
            transform: scale(1.2);
        }
    </style>
</head>

<body>
<ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
    <li>6</li>
    <li>7</li>
</ul>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425090230504.gif)

### 15.1.6 2D 转换综合写法

注意：

1. 同时使用多个转换，其格式为：`transform: translate() rotate() scale()` ...等
2. 其顺序会影转换的效果。（先旋转会改变坐标轴方向）
3. 当我们同时有位移和其他属性的时候，记得要将**位移放到最前**

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            transition: all 1s;
        }

        div:hover {
            /* transform: rotate(180deg) translate(150px, 50px); */
            /* 我们同时有位移和其他属性，我们需要把位移放到最前面 */
            transform: translate(150px, 50px) rotate(180deg) scale(1.2);
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/readme-164241763228313.gif" style="zoom:50%;" />

### 15.1.7 2D 转换总结

- 转换 transform 我们简单理解就是变形，有 2D 和 3D 之分
- 我们暂且学了三个，分别是：位移、旋转 和 缩放
- 2D 移动 translate(x, y) 最大的优势是不影响其他盒子，里面参数用 %，是相对于自身宽度和高度来计算的
- 可以分开写比如 translateX(x)  和 translateY(y)
- 2D 旋转 rotate(度数) 可以实现旋转元素，度数的单位是 deg
- 2D 缩放 sacle(x, y) 里面参数是数字，不跟单位，可以是小数。最大的优势在于不影响其他盒子
- 设置转换中心点 transform-origin : x y; 参数可以百分比、像素或者是方位名词
- 当我们进行综合写法，同时有位移和其他属性的时候，记得要将位移放到最前

## 15.2 CSS3 动画

动画（animation）是 CSS3 中具有颠覆性的特征之一，可通过**设置多个节点来精确控制一个或一组动画**，常用来实现复杂的动画效果。

**相比较过渡，动画可以实现更多变化，更多控制，连续自动播放等效果。**

### 15.2.1 动画的基本使用

制作动画分为两步：

1. 先定义动画
2. 再使用（调用）动画

#### 15.2.1.1 用 keyframes 定义动画（类似定义类选择器）

```css
@keyframes 动画名称 {
   0% {
        width: 100px;
   }  
   100% {
        width: 200px;
   }
}
```

**动画序列**

- 0% 是动画的开始，100% 是动画的完成。这样的规则就是动画序列
- 在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果
- 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变任意多的样式任意多的次数
- 请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%

### 15.2.1.2 元素使用动画

```css
div {
	width: 200px;
	height: 200px;
	background-color: aqua;
	margin: 100px auto;
	/* 调用动画 */
	animation-name: 动画名称;
	/* 持续时间 */
	animation-duration: 持续时间;
}
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS3动画的基本使用</title>
    <style>
        /* 我们想页面一打开，一个盒子就从左边走到右边 */
        /* 1. 定义动画 */
        @keyframes move {
            /* 开始状态 */
            0% {
                transform: translateX(0px);
            }
            /* 结束状态 */
            100% {
                transform: translateX(1000px);
            }
        }

        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* 2. 调用动画 */
            /* 动画名称 */
            animation-name: move;
            /* 持续时间 */
            animation-duration: 2s;
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425104436533.gif)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>动画序列</title>
    <style>
        /* from to 等价于 0% 和 100% */
        /*
        @keyframes move {
            from {
                transform: translate(0, 0);
            }
            to {
                transform: translate(1000px, 0);
            }
        }
        */

        /* 动画序列 */
        /* 1. 可以做多个状态的变化 keyframe 关键帧 */
        /* 2. 里面的百分比要是整数 */
        /* 3. 里面的百分比就是 总的时间（我们这个案例 10s）的划分 25% * 10 = 2.5s */

        @keyframes move {
            0% {
                transform: translate(0, 0);
            }
            25% {
                transform: translate(1000px, 0)
            }
            50% {
                transform: translate(1000px, 500px);
            }
            75% {
                transform: translate(0, 500px);
            }
            100% {
                transform: translate(0, 0);
            }
        }

        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            animation-name: move;
            animation-duration: 10s;
        }
    </style>
</head>

<body>
<div>

</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425103016385.gif)

## 15.3 动画常用属性


| **属性**                  | **描述**                                                     |
| ------------------------- | ------------------------------------------------------------ |
| @keyframes                | 规定动画                                                     |
| animation                 | 所有动画属性的简写属性，除了animation-play-state 属性        |
| animation-name            | 规定 @keyframes 动画的名称（必须的）                         |
| animation-duration        | 规定动画完成一个周期所花费的秒或毫秒，默认是 0（必须的）     |
| animation-timing-function | 规定动画的速度曲线，默认是 “ease”                            |
| animation-delay           | 规定动画何时开始，默认是 0                                   |
| animation-iteration-count | 规定动画被播放的次数，默认是 1，还有 infinite                |
| animation-direction       | 规定动画是否在下一周期逆向播放，默认是 "normal", alternate 逆播放 |
| animation-play-state      | 规定动画是否正在运行或暂停。默认是 "running", 还有 "paused"  |
| animation-fill-mode       | 规定动画结束后状态，保持 forwards 回到起始 backwards         |

## 15.4 动画简写属性

animation：动画名称 持续时间 运动曲线 何时开始 播放次数 是否反方向 动画起始或者结束的状态。

```css
animation: myfirst 5s linear 2s infinite alternate;
```

- 简写属性里面不包含 animation-play-state
- 暂停动画：animation-play-state: puased; 经常和鼠标经过等其他配合使用
- 想要动画走回来，而不是直接跳回来：animation-direction: alternate
- 盒子动画结束后，停在结束位置：animation-fill-mode: forwards 

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>动画属性</title>
    <style>
        @keyframes move {
            0% {
                transform: translate(0, 0);
            }
            100% {
                transform: translate(1000px, 0);
            }
        }

        div {
            width: 100px;
            height: 100px;
            background-color: pink;
            /* 动画名称 */
            animation-name: move;
            /* 持续时间 */
            /* animation-duration: 2s; */
            /* 运动曲线 */
            /* animation-timing-function: ease; */
            /* 何时开始 */
            animation-delay: 1s;
            /* 重复次数 iteration 重复的 conut 次数 infinite 无限 */
            /* animation-iteration-count: infinite; */
            /* 是否反方向播放 默认的是 normal 如果想要反方向 就写 alternate */
            /* animation-direction: alternate; */
            /* 动画结束后的状态 默认的是 backwards 回到起始状态 我们可以让他停留在结束状态 forwards */
            /* animation-fill-mode: forwards; */
            /* animation: name duration timing-function delay iteration-count direction fill-mode; */
            /* animation: move 2s linear 0s 1 alternate forwards; */
            /* 前面 2 个属性 name duration 一定要写 */
            /* animation: move 2s linear alternate forwards; */
        }

        div:hover {
            /* 鼠标经过 div 让这个 div 停止动画，鼠标离开就继续动画 */
            animation-play-state: paused;
        }
    </style>
</head>

<body>
<div>

</div>
</body>

</html>
```

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>大数据热点图</title>
    <style>
        body {
            background-color: #333;
        }

        .map {
            position: relative;
            width: 747px;
            height: 616px;
            background: url(media/map.png) no-repeat;
            margin: 0 auto;
        }

        .city {
            position: absolute;
            top: 227px;
            right: 193px;
            color: #fff;
        }

        .tb {
            /* 此处只能使用 top right 因为这样才能层叠 city，
            否则如果使用 bottom 的话，还会基础 city 的 top，bottom 与 top 优先执行 top */
            top: 500px;
            right: 80px;
        }

        .dotted {
            width: 8px;
            height: 8px;
            background-color: #09f;
            border-radius: 50%;
        }

        .city div[class^="pulse"] {
            /* 保证我们小波纹在父盒子里面水平垂直居中 放大之后就会中心向四周发散 */
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 8px;
            height: 8px;
            box-shadow: 0 0 12px #009dfd;
            border-radius: 50%;
            animation: pulse 1.2s linear infinite;
        }

        .city div.pulse2 {
            animation-delay: 0.4s;
        }

        .city div.pulse3 {
            animation-delay: 0.8s;
        }

        @keyframes pulse {
            0% {
            }
            70% {
                /* transform: scale(5);  我们不要用scale 因为他会让 阴影变大*/
                width: 40px;
                height: 40px;
                opacity: 1;
            }
            100% {
                width: 70px;
                height: 70px;
                opacity: 0;
            }
        }
    </style>
</head>

<body>
<div class="map">
    <div class="city">
        <div class="dotted"></div>
        <div class="pulse1"></div>
        <div class="pulse2"></div>
        <div class="pulse3"></div>
    </div>
    <div class="city tb">
        <div class="dotted"></div>
        <div class="pulse1"></div>
        <div class="pulse2"></div>
        <div class="pulse3"></div>
    </div>
</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425105240855.gif)

## 15.5 速度曲线细节

animation-timing-function：规定动画的速度曲线，默认是 "ease"。

| **值**      | **描述**                                     |
| ----------- | -------------------------------------------- |
| linear      | 动画从头到尾的速度是相同的（匀速）           |
| ease        | 默认。动画以低速开始，然后加快，在结束前变慢 |
| ease-in     | 动画以低速开始                               |
| ease-out    | 动画以低速结束                               |
| ease-in-out | 动画以低速开始和结束                         |
| steps()     | 指定了时间函数中的间隔数量（步长）           |

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>速度曲线步长</title>
    <style>
        div {
            overflow: hidden;
            font-size: 20px;
            width: 0;
            height: 30px;
            background-color: pink;
            /* 让我们的文字强制一行内显示 */
            white-space: nowrap;
            /* steps 就是分几步来完成我们的动画 有了 steps 就不要在写 ease 或者 linear 了 */
            animation: w 4s steps(10) forwards;
        }

        @keyframes w {
            0% {
                width: 0;
            }
            100% {
                width: 200px;
            }
        }
    </style>
</head>

<body>
<div>世纪佳缘我在这里等你</div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425105455354.gif)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>奔跑的熊大案例</title>
    <style>
        body {
            background-color: #ccc;
        }

        div {
            position: absolute;
            width: 200px;
            height: 100px;
            background: url(media/bear.png) no-repeat;
            /* 我们元素可以添加多个动画，用逗号分隔 */
            animation: bear .4s steps(8) infinite, move 3s forwards;
        }

        @keyframes bear {
            0% {
                background-position: 0 0;
            }
            100% {
                background-position: -1600px 0;
            }
        }

        @keyframes move {
            0% {
                left: 0;
            }
            100% {
                left: 50%;
                /* margin-left: -100px; */
                transform: translateX(-50%);
            }
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425105628305.png)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425105802965.gif)

# 十六、CSS3 3D转换

我们生活的环境是 3D 的，照片就是 3D 物体在 2D 平面呈现的例子。

**有什么特点**

- 近大远小
- 物体后面遮挡不可见

当我们在网页上构建 3D 效果的时候参考这些特点就能产出 3D 效果。

## 16.1 三维坐标系

三维坐标系其实就是指立体空间，立体空间是由3个轴共同组成的。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425110200341.png" style="zoom: 33%;" />

- x 轴：水平向右（注意：x 右边是正值，左边是负值）
- y 轴：垂直向下（注意：y 下面是正值，上面是负值）
- z 轴：垂直屏幕（注意：往外面是正值，往里面是负值）

**3D 转换我们主要学习工作中最常用的 3D 位移 和 3D 旋转。**

**主要知识点**

- 3D 位移：translate3d(x, y, z)
- 3D 旋转：rotate3d(x, y, z)
- 透视：perspective
- 3D 呈现：transfrom-style

## 16.2 3D移动 translate3d

3D 移动在 2D 移动的基础上多加了一个可以移动的方向，就是 z 轴方向。

- transform:translateX(100px)：仅仅是在 X 轴上移动
- transform:translateY(100px)：仅仅是在 Y 轴上移动
- transform:translateZ(100px)：仅仅是在 Z 轴上移动（注意：translateZ 一般用 px 单位）
- transform:translate3d(x, y, z)：其中 x、y、z 分别指要移动的轴的方向的距离

因为 z 轴是垂直屏幕，由里指向外面，所以默认是看不到元素在 z 轴的方向上移动（要借助透视）。

## 16.3 透视 perspective

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425110852340.png" style="zoom: 25%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425111023799.png" style="zoom:25%;" />

在 2D 平面产生近大远小视觉立体，但是效果只是二维的。

- 如果想要在网页产生 3D 效果需要透视（理解成 3D 物体投影在 2D 平面内）
- 模拟人类的视觉位置，可认为安排一只眼睛去看
- 透视我们也称为视距：视距就是人的眼睛到屏幕的距离
- 距离视觉点越近的，在电脑平面成像越大，越远成像越小
- 透视的单位是像素

**透视写在被观察元素的父盒子上面。**

d：就是视距，视距就是一个距离人的眼睛到屏幕的距离。

z：就是 z 轴，物体距离屏幕的距离，z 轴越大（正值）我们看到的物体就越大。



```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>3D移动translate3d</title>
    <style>
        body {
            /* 透视写到被观察元素的父盒子上面 */
            perspective: 200px;
        }

        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* transform: translateX(100px) translateY(100px) translateZ(100px); */
            /* 1. translateZ 沿着 Z 轴移动 */
            /* 2. translateZ 后面的单位我们一般跟 px */
            /* 3. translateZ(100px) 向外移动 100px（向我们的眼睛来移动的） */
            /* 4. 3D 移动有简写的方法 */
            /* transform: translate3d(x, y, z); */
            /* transform: translate3d(100px, 100px, 100px); */
            /* 5. xyz 是不能省略的，如果没有就写 0 */
            transform: translate3d(400px, 100px, 100px);
        }
    </style>
</head>

<body>
<div></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425113455393.png)

## 16.4 translateZ

translform:translateZ(100px)：仅仅是在 Z 轴上移动。有了透视，就能看到 translateZ 引起的变化了。

- translateZ：近大远小
- translateZ：往外是正值
- translateZ：往里是负值

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>translateZ</title>
    <style>
        body {
            perspective: 500px;
        }

        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            transform: translateZ(0);
        }
    </style>
</head>

<body>
<div></div>
<div></div>
<div></div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425114658704.png" style="zoom:50%;" />

## 16.5 3D旋转 rotate3d

3D旋转指可以让元素在三维平面内沿着 x轴，y轴，z轴或者自定义轴进行旋转。

**语法**

- transform: rotateX(45deg)：沿着 x 轴正方向旋转 45 度
- transform: rotateY(45deg)：沿着 y 轴正方向旋转 45deg
- transform: rotateZ(45deg)：沿着 z 轴正方向旋转 45deg
- transform: rotate3d(x, y, z, deg)：沿着自定义轴旋转 deg 为角度（了解即可）

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425115234419.gif)

对于元素旋转的方向的判断，我们需要先学习一个左手准则。

**左手准则**

- 左手的手拇指指向 x 轴的正方向
- 其余手指的弯曲方向就是该元素沿着 x 轴旋转的方向

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425115458965.png" style="zoom:50%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>rotateX</title>
    <style>
        body {
            /* 利用透视产生近大远小效果 */
            perspective: 300px;
        }

        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }

        img:hover {
            transform: rotateX(45deg);
        }
    </style>
</head>

<body>
<img src="media/pig.jpg" alt="">
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425120806628.gif" style="zoom:50%;" />

---

- 左手的手拇指指向 y 轴的正方向
- 其余手指的弯曲方向就是该元素沿着 y 轴旋转的方向（正值）

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425115711121.png" style="zoom:33%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>rotateY</title>
    <style>
        body {
            perspective: 500px;
        }

        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }

        img:hover {
            transform: rotateY(45deg);
        }
    </style>
</head>

<body>
<img src="media/pig.jpg" alt="">
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425121401130.gif" style="zoom:50%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>rotateZ</title>
    <style>
        body {
            perspective: 500px;
        }

        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }

        img:hover {
            transform: rotateZ(180deg);
        }
    </style>
</head>

<body>
<img src="media/pig.jpg" alt="">
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425121713541.gif" style="zoom:50%;" />

transform: rotate3d(x, y, z, deg)：沿着自定义轴旋转 deg 为角度（了解即可）。

xyz 是表示旋转轴的矢量，表示你是否希望沿着该轴旋转，最后一个表示旋转的角度。

- transform: rotate3d(1, 0, 0, 45deg)：就是沿着 x 轴旋转 45deg
- transform: rotate3d(0, 1, 0, 45deg)：就是沿着 y 轴旋转 45deg
- transform: rotate3d(0, 0, 1, 45deg)：就是沿着 z 轴旋转 45deg
- transform: rotate3d(1, 1, 0, 45deg)：就是沿着对角线（矢量计算）旋转 45deg

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425122158983.png" style="zoom: 33%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>rotate3d</title>
    <style>
        body {
            perspective: 500px;
        }

        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }

        img:hover {
            /* transform: rotate3d(x,y,z,deg); */
            /* transform: rotate3d(1, 0, 0, 45deg); */
            /* transform: rotate3d(0, 1, 0, 45deg); */
            transform: rotate3d(1, 1, 0, 45deg);
        }
    </style>
</head>

<body>
<img src="media/pig.jpg" alt="">
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425121831607.gif" style="zoom:50%;" />

## 16.6 3D呈现 transfrom-style

- 控制子元素是否开启三维立体环境
- transform-style: flat 子元素不开启 3d 立体空间（默认的）
- transform-style: preserve-3d; 子元素开启立体空间
- 代码写给父级，但是影响的是子盒子
- 这个属性很重要，后面必用

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425123348956.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>transform-style</title>
    <style>
        body {
            perspective: 500px;
        }

        .box {
            position: relative;
            width: 200px;
            height: 200px;
            margin: 100px auto;
            transition: all 2s;
            /* 让子元素保持3d立体空间环境 */
            transform-style: preserve-3d;
        }

        .box:hover {
            transform: rotateY(60deg);
        }

        .box div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: pink;
        }

        .box div:last-child {
            background-color: purple;
            transform: rotateX(60deg);
        }
    </style>
</head>

<body>
<div class="box">
    <div></div>
    <div></div>
</div>
</body>

</html>
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425124112130.gif" style="zoom:50%;" />

【案例：两面翻转的盒子】

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425124741907.gif" style="zoom:50%;" />

实现步骤：

1. 搭建 HTML 结构

```html
<div class="box">
	<div class="front">黑马程序员</div>
    <div class="back">pink老师等你</div>
</div>
```

- box 父盒子里面包含前后两个子盒子
- box 是翻转的盒子 front 是前面盒子 back 是后面盒子

2. CSS 样式

- box 指定大小，切记要添加 3d 呈现
- back 盒子要沿着 Y 轴翻转 180 度
- 最后鼠标经过 box 沿着 Y 旋转 180deg

代码：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>两面翻转的盒子</title>
    <style>
        body {
            perspective: 400px;
        }

        .box {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 100px auto;
            transition: all .4s;
            /* 让背面的紫色盒子保留立体空间 给父级添加的 */
            transform-style: preserve-3d;
        }

        .box:hover {
            transform: rotateY(180deg);
        }

        .front,
        .back {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            font-size: 30px;
            color: #fff;
            text-align: center;
            line-height: 300px;
        }

        .front {
            background-color: pink;
            z-index: 1;
        }

        .back {
            background-color: purple;
            /* 像手机一样 背靠背 旋转 */
            transform: rotateY(180deg);
        }
    </style>
</head>

<body>
<div class="box">
    <div class="front">黑马程序员</div>
    <div class="back">pink老师这里等你</div>
</div>
</body>

</html>
```

---

【案例：3D 导航栏】

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425125609662.gif)

实现步骤：

1. 搭建 HTML 结构

```html
<ul>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
         </div>
    </li>
</ul>
```

- li 做导航栏
- .box 是翻转的盒子 front 是前面盒子 bottom 是底下盒子

2. CSS 样式

- li 设置大小，加透视和 3d 呈现
- front 需要前移 17.5 像素
- bottom 需要下移 17.5 像素并且要沿着 x 轴翻转 负 90 度
- 鼠标放到 box 让盒子旋转 90 度

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>3D导航栏案例</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }

        ul {
            margin: 100px;
        }

        ul li {
            float: left;
            margin: 0 5px;
            width: 120px;
            height: 35px;
            list-style: none;
            /* 一会我们需要给 box 旋转 也需要透视 干脆给 li 加 里面的子盒子都有透视效果 */
            perspective: 500px;
        }

        .box {
            position: relative;
            width: 100%;
            height: 100%;
            transform-style: preserve-3d;
            transition: all .4s;
        }

        .box:hover {
            transform: rotateX(90deg);
        }

        .front,
        .bottom {
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
        }

        .front {
            background-color: pink;
            z-index: 1;
            transform: translateZ(17.5px);
        }

        .bottom {
            background-color: purple;
            /* 这个x轴一定是负值 */
            /* 我们如果有移动 或者其他样式，必须先写我们的移动 */
            transform: translateY(17.5px) rotateX(-90deg);
        }
    </style>
</head>

<body>
<ul>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
    <li>
        <div class="box">
            <div class="front">黑马程序员</div>
            <div class="bottom">pink老师等你</div>
        </div>
    </li>
</ul>
</body>

</html>
```

---

【综合案例：旋转木马】

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210425130327326.gif)

1. 搭建 HTML 结构

```html
<section>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</section>
```

- 里面的 6 个 div 分别是 6 个狗狗图片
- 注意最终旋转是 section 标签旋转

2. CSS 样式

- 给 body 添加 透视效果 perspective: 1000px;
- 给 section 添加大小，一定不要忘记添加 3d 呈现效果控制里面的 6 个 div
  -  别忘记子绝父相，section 要加相对定位
- 里面 6 个 div 全部绝对定位叠到一起，然后移动不同角度旋转和距离
  - 注意：旋转角度用 rotateY 距离肯定用 translateZ 来控制
- 给 section 添加动画 animation，让它可以自动旋转即可

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>综合案例：旋转木马</title>
    <style>
        body {
            perspective: 1000px;
        }

        section {
            position: relative;
            width: 300px;
            height: 200px;
            margin: 150px auto;
            transform-style: preserve-3d;
            /* 添加动画效果 */
            animation: rotate 10s linear infinite;
            background: url(media/pig.jpg) no-repeat;
        }

        section:hover {
            /* 鼠标放入 section 停止动画 */
            animation-play-state: paused;
        }

        @keyframes rotate {
            0% {
                transform: rotateY(0);
            }
            100% {
                transform: rotateY(360deg);
            }
        }

        section div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url(media/dog.jpg) no-repeat;
        }

        section div:nth-child(1) {
            transform: rotateY(0) translateZ(300px);
        }

        section div:nth-child(2) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(60deg) translateZ(300px);
        }

        section div:nth-child(3) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(120deg) translateZ(300px);
        }

        section div:nth-child(4) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(180deg) translateZ(300px);
        }

        section div:nth-child(5) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(240deg) translateZ(300px);
        }

        section div:nth-child(6) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(300deg) translateZ(300px);
        }
    </style>
</head>

<body>
<section>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</section>
</body>

</html>
```

## 16.7浏览器私有前缀

浏览器私有前缀是为了**兼容老版本**的写法，**比较新版本的浏览器无须添加**。

### 16.7.1 私有前缀

- -moz-：代表 firefox 浏览器私有属性
- -ms-：代表 ie 浏览器私有属性
- -webkit-：代表 safari、chrome 私有属性
- -o-：代表 Opera 私有属性

### 16.7.2 提倡的写法

```css
-moz-border-radius: 10px; 
-webkit-border-radius: 10px; 
-o-border-radius: 10px; 
border-radius: 10px;
```





# 十七、美化技巧

## 17.1 精灵图

### 17.1.1 为什么需要精灵图？

一个网页中往往会应用很多小的背景图像作为修饰，当网页中的图像过多时，服务器就会频繁地接收和发送
请求图片，造成服务器请求压力过大，这将大大降低页面的加载速度。

因此，为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度，出现了 CSS 精灵技术（也称
CSS Sprites、CSS 雪碧）。

核心原理：将网页中的一些小背景图像整合到一张大图中 ，这样服务器只需要一次请求就可以了。

精灵技术目的：为了有效地减少服务器接收和发送请求的次数，提高页面的加载速度。

### 17.1.2 精灵图（sprites）的使用

使用精灵图核心：

1. 精灵技术主要针对于背景图片使用。就是把多个小背景图片整合到一张大图片中
2. 这个大图片也称为 sprites 精灵图 或者 雪碧图
3. 移动背景图片位置以控制显示区域， 此时可以使用 `background-position`
4. 移动的距离就是这个目标图片的 `x` 和 `y` 坐标。注意网页中的坐标有所不同
5. 因为一般情况下都是将精灵图往上往左移动，所以两个坐标数值基本是负值
6. 使用精灵图的时候需要精确测量，每个小背景图片的大小和位置

使用精灵图核心总结：

1. 精灵图主要针对于小的背景图片使用
2. 主要借助于背景位置来实现 `background-position`
3. 一般情况下精灵图都是负值（千万注意网页中的坐标： x轴右边走是正值，左边走是负值， y轴同理） 

【王者荣耀案例】

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420081150387.png)

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>精灵图使用</title>
    <style>
        .box1 {
            width: 60px;
            height: 60px;
            margin: 100px auto;
            background: url(images/sprites.png) no-repeat -182px 0;

        }

        .box2 {
            width: 27px;
            height: 25px;
            /* background-color: pink; */
            margin: 200px;
            background: url(images/sprites.png) no-repeat -155px -106px;

        }
    </style>
</head>

<body>
    <div class="box1"></div>
    <div class="box2"></div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/202104200817544.png)

### 17.1.3 案例：拼单词

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420081150457.jpg" style="zoom:67%;" />

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>利用精灵图拼出自己名字</title>
    <style>
        span {
            display: inline-block;
            background: url(images/abcd.jpg) no-repeat;
        }

        .p {
            width: 100px;
            height: 112px;
            /* background-color: pink; */
            background-position: -493px -276px;
        }

        .i {
            width: 60px;
            height: 108px;
            /* background-color: pink; */
            background-position: -327px -142px;
        }

        .n {
            width: 115px;
            height: 112px;
            /* background-color: pink; */
            background-position: -255px -275px;
        }

        .k {
            width: 105px;
            height: 114px;
            /* background-color: pink; */
            background-position: -495px -142px;
        }
    </style>
</head>

<body>
    <span class="p">p</span>
    <span class="i">i</span>
    <span class="n">n</span>
    <span class="k">k</span>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420083302981.png)

【PS 切片工具的使用】

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210424224831926.png" style="zoom: 50%;" />

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/8141d1fc65ba4b31acfc903b948a09a8.png)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/b9b0bf21c37a40a6a37a09f759218c16.png)

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/d8fea6eba89048dfb6cf0421f620d04e.png)

## 17.2字体图标

### 17.2.1 字体图标的产生

字体图标使用场景：主要用于显示网页中通用、常用的一些小图标。

精灵图是有诸多优点的，但是缺点很明显。

1. 图片文件还是比较大的
2. 图片本身放大和缩小会失真
3. 一旦图片制作完毕想要更换非常复杂

此时，有一种技术的出现很好的解决了以上问题，就是字体图标 iconfont。

字体图标可以为前端工程师提供一种方便高效的图标使用方式，展示的是图标，但本质却属于字体。

### 17.2.2 字体图标的优点

- 轻量级：一个图标字体要比一系列的图像要小。一旦字体加载了，图标就会马上渲染出来，减少了服务器请求
- 灵活性：本质其实是文字，可以很随意的改变颜色、产生阴影、透明效果、旋转等
- 兼容性：几乎支持所有的浏览器，请放心使用

注意： 字体图标不能替代精灵技术，只是对工作中图标部分技术的提升和优化。

总结：

1. 如果遇到一些结构和样式比较简单的小图标，就用字体图标
2. 如果遇到一些结构和样式复杂一点的小图片，就用精灵图

字体图标是一些网页常见的小图标，我们直接网上下载即可。 因此使用可以分为：

1. 字体图标的下载
2. 字体图标的引入（引入到我们 html 页面中）
3. 字体图标的追加（在原有的基础上添加新的小图标）

### 17.2.3 字体图标的下载

推荐下载网站：

- icomoon 字库 [https://icomoon.io/](https://icomoon.io/)

IcoMoon 成立于 2011 年，推出了第一个自定义图标字体生成器，它允许用户选择所需要的图标，使它们成一字型。该字库内容种类繁多，非常全面，唯一的遗憾是国外服务器，打开网速较慢。

- 阿里 iconfont 字库 [https://www.iconfont.cn/](https://www.iconfont.cn/)

这个是阿里妈妈 M2UX 的一个 iconfont 字体图标字库，包含了淘宝图标库和阿里妈妈图标库。可以使用 AI 制作图标上传生成。 重点是，免费！

> 以下内容以 icomoon 字库 为例。

### 17.2.4 字体图标的引入

下载完毕之后，注意原先的文件不要删，后面会用！

1. **把下载包里面的 fonts 文件夹放入页面根目录下**

不同浏览器所支持的字体格式是不一样的，字体图标之所以兼容，就是因为包含了主流浏览器支持的字体文件。

- TureType (.ttf) 格式 .ttf 字体是 Windows 和 Mac 的最常见的字体，支持这种字体的浏览器有 IE9+、Firefox3.5+、Chrome4+、Safari3+、Opera10+、iOS Mobile、Safari4.2+；
- Web Open Font Format (.woff) 格式 woff 字体，支持这种字体的浏览器有 IE9+、Firefox3.5+、Chrome6+、Safari3.6+、Opera11.1+；
- Embedded Open Type (.eot) 格式 .eot 字体是 IE 专用字体，支持这种字体的浏览器有 IE4+；
- SVG (.svg) 格式 .svg 字体是基于 SVG 字体渲染的一种格式，支持这种字体的浏览器有 Chrome4+、Safari3.1+、Opera10.0+、iOS Mobile Safari3.2+；

2. **在 CSS 样式中全局声明字体：简单理解把这些字体文件通过 css 引入到我们页面中**

一定注意字体文件路径的问题。

```css
@font-face {
	font-family: 'icomoon';
	src: url('fonts/icomoon.eot?7kkyc2');
	src: url('fonts/icomoon.eot?7kkyc2#iefix') format('embedded-opentype'),
	url('fonts/icomoon.ttf?7kkyc2') format('truetype'),
	url('fonts/icomoon.woff?7kkyc2') format('woff'),
	url('fonts/icomoon.svg?7kkyc2#icomoon') format('svg');
	font-weight: normal;
	font-style: normal;
}
```

3. **html 标签内添加小图标**

复制小图标对应的字符（一个小方框）到 html 中，一般建议放在 `<span></span>` 标签里。 

4. **给标签定义字体**

```css
span {
	font-family: "icomoon";
}
```

注意：务必保证这个字体和上面 @font-face 里面的字体保持一致（默认为：icomoon）。

### 17.2.5 字体图标的追加

如果工作中，原来的字体图标不够用了，我们便需要添加新的字体图标到原来的字体文件中。

选择 Import Icons 按钮，把原压缩包里面的 selection.json 重新上传，然后选中自己想要新的图标，从新下载压缩包，并替换原来的文件即可。

### 17.2.6 字体图标加载的原理

服务器只需接受一次浏览器请求便可以将 fonts 文件一次性返回，如此而来网页中所有用到 fonts 字体图标的部分便一次性加载好了，大大减轻了服务器压力。

```html
<!doctype html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>字体图标的使用</title>
  <style>
    /* 字体声明 */
    @font-face {
    	font-family: 'icomoon';
      	src: url('fonts/icomoon.eot?p4ssmb');
      	src: url('fonts/icomoon.eot?p4ssmb#iefix') format('embedded-opentype'),
        url('fonts/icomoon.ttf?p4ssmb') format('truetype'),
        url('fonts/icomoon.woff?p4ssmb') format('woff'),
        url('fonts/icomoon.svg?p4ssmb#icomoon') format('svg');
      	font-weight: normal;
      	font-style: normal;
      	font-display: block;
    }

    span {
      font-family: 'icomoon';
      font-size: 100px;
      color: salmon;
    }
  </style>
</head>

<body>
  <span></span>
  <span></span>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420093539188.png)

## 17.3 CSS三角

网页中常见一些三角形，使用 CSS 直接画出来就可以，不必做成图片或者字体图标。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420102851826.png)

CSS 三角是怎么来的？原理如下：

对一个没有大小的盒子设置边框，那么只要边框足够粗，就可以呈现三角效果。

如果只需要一个三角，那么对其他三个边框设置透明色即可。

通常 CSS 三角要配合定位来布局。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>CSS 三角制作</title>
    <style>
        .box1 {
            width: 0;
            height: 0;
            /* border: 10px solid pink; */
            border-top: 30px solid hotpink;
            border-right: 30px solid black;
            border-bottom: 30px solid skyblue;
            border-left: 30px solid gray;
        }

        .box2 {
            width: 0;
            height: 0;
            border: 50px solid transparent;
            border-left-color: black;
            margin: 50px;
        }

        .jd {
            /* 子绝父相 */
            position: relative;
            width: 120px;
            height: 249px;
            background-color: black;
        }

        .jd span {
            /* 子绝父相 */
            position: absolute;
            right: 15px;
            top: -20px;
            width: 0;
            height: 0;
            /* 下面两行为了照顾兼容性 */
            line-height: 0;
            font-size: 0;
            border: 10px solid transparent;
            border-bottom-color: black;
        }
    </style>
</head>

<body>
    <div class="box1"></div>
    <div class="box2"></div>
    <div class="jd">
        <span></span>
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420104336278.png)

## 17.4 CSS用户界面样式

### 17.4.1 什么是界面样式

所谓的界面样式，就是更改一些用户操作样式，以提高更好的用户体验。

- 更改用户的鼠标样式
- 表单轮廓
- 防止表单域拖拽

### 17.4.2 鼠标样式 cursor

```css
li { cursor: pointer; }
```

设置或检索在对象上移动的鼠标指针采用何种系统预定义的光标形状。

| 属性值        | 描述     |
| ------------- | -------- |
| `default`     | 默认箭头 |
| `pointer`     | 小手     |
| `move`        | 十字移动 |
| `text`        | 文本竖杠 |
| `not-allowed` | 禁止     |

注意：除了以上类型，还有其他很多类型。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>用户界面样式-鼠标样式</title>
</head>

<body>
    <ul>
        <li style="cursor: default;">我是默认的小白鼠标样式</li>
        <li style="cursor: pointer;">我是鼠标小手样式</li>
        <li style="cursor: move;">我是鼠标移动样式</li>
        <li style="cursor: text;">我是鼠标文本样式</li>
        <li style="cursor: not-allowed;">我是鼠标禁止样式</li>
    </ul>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021042011003289.gif)

### 17.4.3 轮廓线 outline

给表单添加 `outline: 0;` 或者 `outline: none;` 样式之后，就可以去掉默认的边框。

```css
input { outline: none; }
```

默认样式：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420111135354.gif)

修改后样式：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>轮廓线 outline</title>
    <style>
        input {
            /* 取消表单轮廓 */
            outline: none;
        }
    </style>
</head>

<body>
    <!-- 取消表单轮廓 -->
    <input type="text">
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420111315285.gif)

### 17.4.4 防止拖拽文本域 resize

实际开发中，我们文本域右下角是不允许拖拽的。（会破坏布局！）

```css
textarea { resize: none; }
```

默认样式：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/2021042011203862.gif)

修改后样式：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>防止拖拽文本域 resize</title>
    <style>
        textarea {
            /* 取消表单轮廓 */
            outline: none;
            /* 防止拖拽文本域 */
            resize: none;
        }
    </style>
</head>

<body>
    <!-- 防止拖拽文本域 -->
    <!-- <textarea></textarea>起始标签建议放在一行，因为这样不会导致文本域里文字前有空白，
    后期可以专门通过 padding 来设置文本周围的留白 -->
    <textarea name="" id="" cols="30" rows="10"></textarea>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/202104201120370.gif)

## 17.5 vertical-align 属性应用

CSS 的 vertical-align 属性使用场景：经常用于设置图片或者表单（行内块元素）与文字垂直对齐。

官方解释：用于设置一个元素的垂直对齐方式，但是它只针对于行内元素或者行内块元素有效。

语法：

```css
vertical-align: baseline | top | middle | bottom
```

| 值         | 描述                                   |
| ---------- | -------------------------------------- |
| `baseline` | 默认。元素放置在父元素的基线上         |
| `top`      | 把元素的顶端与行中最高元素的顶端对齐   |
| `middle`   | 把此元素放置在父元素的中部             |
| `bottom`   | 把元素的顶端与行中最低的元素的顶端对齐 |

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420124542850.png)

### 17.5.1 图片、表单和文字对齐

图片、表单都属于行内块元素，默认的 vertical-align 是基线对齐。

此时可以给图片、表单这些行内块元素的 vertical-align 属性设置为 middle 就可以让文字和图片垂直居中对齐了。

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>利用vertical-align实现图片文字垂直居中对齐</title>
    <style>
        img {
            /* vertical-align: bottom; */
            /* 让图片和文字垂直居中 */
            vertical-align: middle;
            /* vertical-align: top; */
        }

        textarea {
            vertical-align: middle;
        }
    </style>
</head>

<body>
    <img src="images/ldh.jpg" alt=""> pink老师是刘德华

    <br>
    <textarea name="" id="" cols="30" rows="10"></textarea> 请您留言
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420124932560.png)

> 运用重点：
>
> 我们知道，当对盒子设置 `line-height: 盒子高度;` 时，盒子内的 `文字` 会垂直居中，其实不只是文字可以垂直居中，盒子内的图片同样也能垂直居中，只不过图片默认是基于基线对齐的，所以要真正实现 `垂直居中` 需要在图片加上：`vertical-align: middle;`

### 17.5.2  解决图片底部默认空白缝隙问题

图片底侧会有一个空白缝隙，原因是行内块元素会和文字的基线对齐。

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420125635475.png)

主要解决方法有两种：

1. 给图片添加 `vertical-align: middle | top | bottom` 等（推荐）
2. 把图片转换为块级元素 `display: block;`

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>图片底侧空白缝隙解决方案</title>
    <style>
        div {
            border: 2px solid black;
        }

        img {
            vertical-align: middle;
            /* display: block; */
        }
    </style>
</head>

<body>
    <div>
        <img src="images/ldh.jpg" alt="">
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420125750954.png)

## 17.6 溢出的文字省略号显示

### 17.6.1 单行文本溢出省略号显示

三个必要条件：

```css
/* 1. 先强制一行内显示文本 */ 
white-space: nowrap; 	/*（ 默认 normal 自动换行）*/ 
/* 2. 超出的部分隐藏 */ 
overflow: hidden; 
/* 3. 文字用省略号替代超出的部分 */ 
text-overflow: ellipsis;
```

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单行文本溢出显示省略号</title>
    <style>
        div {
            width: 150px;
            height: 80px;
            background-color: pink;
            margin: 100px auto;
            /* 这个单词的意思是如果文字显示不开自动换行 */
            /* white-space: normal; */
            /* 1.这个单词的意思是如果文字显示不开也必须强制一行内显示 */
            white-space: nowrap;
            /* 2.溢出的部分隐藏起来 */
            overflow: hidden;
            /* 3.文字溢出的时候用省略号来显示 */
            text-overflow: ellipsis;
        }
    </style>
</head>

<body>
    <div>
        啥也不说，此处省略一万字
    </div>
</body>

</html>
```

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420132753998.png)

### 17.6.2 多行文本溢出省略号显示

多行文本溢出显示省略号，有较大兼容性问题， 适合于 webkit 浏览器或移动端（移动端大部分是 webkit 内核）。

```css
overflow: hidden;
text-overflow: ellipsis;
/* 弹性伸缩盒子模型显示 */
display: -webkit-box;
/* 限制在一个块元素显示的文本的行数 */
-webkit-line-clamp: 2;
/* 设置或检索伸缩盒对象的子元素的排列方式 */
-webkit-box-orient: vertical;
```

更推荐让后台人员来做这个效果，因为后台人员可以设置显示多少个字，操作更简单。

案例：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>单行文本溢出显示省略号</title>
    <style>
        div {
            width: 150px;
            height: 65px;
            background-color: pink;
            margin: 100px auto;
            overflow: hidden;
            text-overflow: ellipsis;
            /* 弹性伸缩盒子模型显示 */
            display: -webkit-box;
            /* 限制在一个块元素显示的文本的行数 */
            -webkit-line-clamp: 3;
            /* 设置或检索伸缩盒对象的子元素的排列方式 */
            -webkit-box-orient: vertical;
        }
    </style>
</head>

<body>
    <div>
        啥也不说，此处省略一万字,啥也不说，此处省略一万字此处省略一万字
    </div>
</body>

</html>
```

Chrome 浏览器效果：

![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/20210420132822674.png)
