

> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



Hexo框架：butterfly魔改（一）

# 前言

这一篇内容在上篇的基础上进行魔改，并对上篇的内容进行了补充

# butterfly魔改

* 看到这里相信大家已经搭建好了属于自己的博客，本来想这先出优化博客的教程，但是我觉得通过上篇的教程，网页还是有很多不足的地方，本篇教程继续带领大家，完成博客的美化，搭好框架，打造一个属于自己免费的炫酷博客。

  

* 还是那句话，魔改的尽头是默认，哈哈，我只挑我觉得不足的地方，争取教会大家方法，大家也可以根据自己的喜好，查询官方文档，设置自己的博客。

  官方文档链接：https://butterfly.js.org/posts/4aa8abbe/
  
  

* 如果你没有 pug 以及 stylus 的渲染器，请下载安装

  `npm install hexo-renderer-pug hexo-renderer-stylus --save`

  

### 主页的美化



* 我发现每次进来这个部分的背景颜色都不一样，有的时候随机匹配出来的很丑，于是乎我就开始看代码，查官方文档的帮助文档，将这部分内容做了修改，觉得没有影响的可以忽略这部分的内容。

![image-20220821141701041](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220821141701041.png)

* 我设置了主题配置文件以下内容：

  * 方式一：删除掉后面的值，我觉得更美观些

  ![image-20220804134357404](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804134357404.png)

  * 方式二：将背景改成透明



### 生成文章唯一链接

* Hexo的默认文章链接格式是年，月，日，标题这种格式来生成的。如果你的标题是中文的话，那你的URL链接就会包含中文，复制后的URL路径就是把中文变成了一大堆字符串编码，如果你在其他地方用这边文章的url链接，偶然你又修改了改文章的标题，那这个URL链接就会失效。为了给每一篇文章来上一个属于自己的链接，利用 hexo-abbrlink 插件 ,来解决这个问题。 
* 参考github官方： hexo-abbrlink 按照此教程配置完之后如下：
* 记得修改每篇文章 abbrlink 的值

1、安装插件，在博客根目录下打开终端，运行以下指令：

```
npm install hexo-abbrlink --save
```

2、插件安装成功后，在根目录  的配置文件 _config.yml 找到 permalink：

```
permalink: :year/:month/:day/:title/
#修改为
permalink: post/:abbrlink.html # post为自定义前缀
abbrlink:
        alg: crc32   #算法： crc16(default) and crc32
        rep: hex     #进制： dec(default) and hex
```



### 打字效果

修改主题配置文件 `_config.butterfly.yml` 的 activate_power_mode即可

```
activate_power_mode:
  enable: true
  colorful: true # open particle animation (冒光特效)
  shake: true #  open shake (抖動特效)
  mobile: false
```





### 网站副标题

可设置主页中展示的网站副标题或者自己喜欢的座右铭

修改主题配置文件 `_config.butterfly.yml`

```
# Site
title: Hexo
subtitle:
  enable: true
  # Typewriter Effect (打字效果)
  effect: true
  # loop (循環打字)
  loop: true
  # source 調用第三方服務
  # source: false 關閉調用
  # source: 1  調用一言網的一句話（簡體） https://hitokoto.cn/
  # source: 2  調用一句網（簡體） http://yijuzhan.com/
  # source: 3  調用今日詩詞（簡體） https://www.jinrishici.com/
  # subtitle 會先顯示 source , 再顯示 sub 的內容
  # source: 3
  # 如果關閉打字效果，subtitle 只會顯示 sub 的第一行文字
  sub:
    - 我双手合十的愿望里永远有你。
    - 穿越人海，只为与你相拥。
    - 手握日月摘 ♥ 陈。
```



### 文章置顶

方式一：

Hexo 本身并没有内置文章置顶功能，因此需要自行安装。

```
# 先卸载
npm uninstall --save hexo-generator-index

# 再安装
npm install --save hexo-generator-index-pin-top

```

就需要在文章的头部信息栏加入一个 header 属性：

```
title: 谢谢你来看我的博客
date: 2020-01-31 17:09:13
top: true
header: false
```



方式二：

​		




### 代码高亮主题

`Butterfly` 支持6种代码高亮样式：

- darker
- pale night
- light
- ocean
- mac
- mac light

修改主题配置文件 `_config.butterfly.yml`

```
highlight_theme: mac light
```

这个自行选择



### 运行时间

网页已运行时间

修改主题配置文件 `_config.butterfly.yml`

```
runtimeshow:
  enable: true
  publish_date: 6/7/2018 00:00:00  
  ##网页开通时间
  #格式: 月/日/年 时间
  #也可以写成 年/月/日 时间
```

![image-20220821141723516](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220821141723516.png)

### 代码复制

主题支持代码复製功能

修改 主题配置文件

```
highlight_copy: true
```



### 侧边栏时钟

1、安装插件，在博客根目录 `[Blog]` 下打开终端，运行以下指令：

```
npm install hexo-butterfly-clock --save
```

2、添加配置信息，以下为写法示例

在站点配置文件 `_config.yml` 或者主题配置文件 `_config.butterfly.yml` 中添加：

```
# electric_clock
# see https://akilar.top/posts/4e39cf4a/
electric_clock:
  enable: true # 开关
  priority: 5 #过滤器优先权
  enable_page: all # 应用页面
  exclude:
    # - /posts/
    # - /about/
  layout: # 挂载容器类型
    type: class
    name: sticky_layout
    index: 0
  loading: https://npm.elemecdn.com/hexo-butterfly-clock/lib/loading.gif #加载动画自定义
  clock_css: https://npm.elemecdn.com/hexo-butterfly-clock/lib/clock.min.css
  clock_js: https://npm.elemecdn.com/hexo-butterfly-clock/lib/clock.min.js
  ip_api: https://pv.sohu.com/cityjson?ie=utf-8
```

放在公告栏里面

~~~yaml
<p>公告内容</p ><div class="twopeople"><div class="container" style="height:200px;"><canvas class="illo" width="800" height="800" style="max-width:200px;max-height:200px;touch-action:none;width:640px;height:640px;"></canvas></div><script src="https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/js/twopeople1.js"></script><script src="https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/js/zdog.dist.js"></script><script id="rendered-js" src="https://cdn.jsdelivr.net/gh/Justlovesmile/CDN/js/twopeople.js"></script><style>.twopeople{margin:0;align-items:center;justify-content:center;text-align:center;}canvas{display:block;margin:0 auto;cursor:move;}</style></div>
~~~





### 字数统计

要为 Butterfly 配上字数统计特性, 你需要如下几个步骤:

1. 打开 hexo 工作目录
2. npm install hexo-wordcount —save or yarn add hexo-wordcount
3. 修改主题配置文件 `_config.butterfly.yml`

```
wordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```



### 公告2个小人

在 `node_modules\hexo-theme-butterfly\layout\includes\widget\card_announcement.pug` 下添加如下代码：

```
 .xpand(style='height:200px;')
  canvas.illo(width='800' height='800' style='max-width: 200px; max-height: 200px; touch-action: none; width: 640px; height: 640px;')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople1.js')
script(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/zdog.dist.js')
script#rendered-js(src='https://fastly.jsdelivr.net/gh/xiaopengand/blogCdn@latest/xzxr/twopeople.js')
style.
  .card-widget.card-announcement {
  margin: 0;
  align-items: center;
  justify-content: center;
  text-align: center;
  }
  canvas {
  display: block;
  margin: 0 auto;
  cursor: move;
  }
```



### 星空背景和流星特效

这部分建议不要加，加上的效果没出来的话，在网址上建议 ctrl+F5 刷新下本地

在 `[Blog]\source\js\` 目录下新建  universe.js  文件，如果没有js就先新建js 文件夹，输入以下代码：

```
function dark() {window.requestAnimationFrame=window.requestAnimationFrame||window.mozRequestAnimationFrame||window.webkitRequestAnimationFrame||window.msRequestAnimationFrame;var n,e,i,h,t=.05,s=document.getElementById("universe"),o=!0,a="180,184,240",r="226,225,142",d="226,225,224",c=[];function f(){n=window.innerWidth,e=window.innerHeight,i=.216*n,s.setAttribute("width",n),s.setAttribute("height",e)}function u(){h.clearRect(0,0,n,e);for(var t=c.length,i=0;i<t;i++){var s=c[i];s.move(),s.fadeIn(),s.fadeOut(),s.draw()}}function y(){this.reset=function(){this.giant=m(3),this.comet=!this.giant&&!o&&m(10),this.x=l(0,n-10),this.y=l(0,e),this.r=l(1.1,2.6),this.dx=l(t,6*t)+(this.comet+1-1)*t*l(50,120)+2*t,this.dy=-l(t,6*t)-(this.comet+1-1)*t*l(50,120),this.fadingOut=null,this.fadingIn=!0,this.opacity=0,this.opacityTresh=l(.2,1-.4*(this.comet+1-1)),this.do=l(5e-4,.002)+.001*(this.comet+1-1)},this.fadeIn=function(){this.fadingIn&&(this.fadingIn=!(this.opacity>this.opacityTresh),this.opacity+=this.do)},this.fadeOut=function(){this.fadingOut&&(this.fadingOut=!(this.opacity<0),this.opacity-=this.do/2,(this.x>n||this.y<0)&&(this.fadingOut=!1,this.reset()))},this.draw=function(){if(h.beginPath(),this.giant)h.fillStyle="rgba("+a+","+this.opacity+")",h.arc(this.x,this.y,2,0,2*Math.PI,!1);else if(this.comet){h.fillStyle="rgba("+d+","+this.opacity+")",h.arc(this.x,this.y,1.5,0,2*Math.PI,!1);for(var t=0;t<30;t++)h.fillStyle="rgba("+d+","+(this.opacity-this.opacity/20*t)+")",h.rect(this.x-this.dx/4*t,this.y-this.dy/4*t-2,2,2),h.fill()}else h.fillStyle="rgba("+r+","+this.opacity+")",h.rect(this.x,this.y,this.r,this.r);h.closePath(),h.fill()},this.move=function(){this.x+=this.dx,this.y+=this.dy,!1===this.fadingOut&&this.reset(),(this.x>n-n/4||this.y<0)&&(this.fadingOut=!0)},setTimeout(function(){o=!1},50)}function m(t){return Math.floor(1e3*Math.random())+1<10*t}function l(t,i){return Math.random()*(i-t)+t}f(),window.addEventListener("resize",f,!1),function(){h=s.getContext("2d");for(var t=0;t<i;t++)c[t]=new y,c[t].reset();u()}(),function t(){document.getElementsByTagName('html')[0].getAttribute('data-theme')=='dark'&&u(),window.requestAnimationFrame(t)}()};
dark()
```

2、在 `[Blog]\source\css\` 目录下新建 universe.css输入：

```
/* 背景宇宙星光  */
#universe{
  display: block;
  position: fixed;
  margin: 0;
  padding: 0;
  border: 0;
  outline: 0;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: -1;
}
```

3、在 `[Blog]\_config.butterfly.yml` 的 `inject` 配置项中 `bottom` 下填入：

```
# 星空背景
      - <canvas id="universe"></canvas>
      - <script defer src="/js/universe.js"></script>
```

4、在 `[Blog]\_config.butterfly.yml` 的 `inject` 配置项中 `head` 下填入：

```
## 星空背景
     - <link rel="stylesheet" href="/css/universe.css">
```



### 樱花飘落效果

在主题配置文件_config.butterfly.yml的inject配置项中bottom下引入sakura.js即可。注意自己调下格式

```
inject:
  bottom:
    # 樱花飘落效果
    # - <script async src="https://npm.elemecdn.com/tzy-blog/lib/js/other/sakura.js"></script>
```



### 给文章标题添加表情

在source\css\style.css 添加以下代码

```
.post-body h2:before,
.post-body h3:before,
.post-body h4:before,
.post-body h5:before,
.post-body h6:before {
  margin-right: 5px;
  font-style: normal;
  font-variant: normal;
  line-height: 1;
  -webkit-transition: all 0.2s ease-out;
  -moz-transition: all 0.2s ease-out;
  -o-transition: all 0.2s ease-out;
  -ms-transition: all 0.2s ease-out;
  transition: all 0.2s ease-out;
  text-rendering: auto;
  -webkit-font-smoothing: antialiased;
  font-weight: 600;
}

.post-body h1:before {
  content: '🎉';
}
.post-body h2:before {
  content: '💡';
}
.post-body h3:before {
  content: '🩸';
}
.post-body h4:before {
  content: '📍';
}
.post-body h5:before {
  content: '🌶️';
}
.post-body h6:before {
  content: '🌏';
}
```



### 添加个性化板娘

以下整理了很多类别，选择自己喜好的怕动手就第一种，现在都很成熟，放心大胆的引用，我使用的就是第一种，但每种都试过了，才写出来不怕动手建议选择大神魔改版本，可以根据自己的喜好进行配置，修改！！！



第一种：最简单引用方式在`Butterfly/_config.yml`中`inject`添加，复制的时候注意一下格式

```
inject:
   head:
     - <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/font-awesome/css/font-awesome.min.css">
   bottom:
    - <script src="https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/autoload.js"></script>
```



第二种：Hexo插件版看板娘（不能换装）

* 在Hexo根目录[Blogroot]下打开终端，输入以下指令安装必要插件。

```
npm install --save hexo-helper-live2d
```

* 打开站点配置文件`[Blog]\config.yml`
  搜索live2d,按照如下注释内容指示进行操作。
  如果没有搜到live2d的配置项，就直接把以下内容复制到最底部

  ```
  # Live2D
  ## https://github.com/EYHN/hexo-helper-live2d
  live2d:
    enable: true #开关插件版看板娘
    scriptFrom: local # 默认
    pluginRootPath: live2dw/ # 插件在站点上的根目录(相对路径)
    pluginJsPath: lib/ # 脚本文件相对与插件根目录路径
    pluginModelPath: assets/ # 模型文件相对与插件根目录路径
    # scriptFrom: jsdelivr # jsdelivr CDN
    # scriptFrom: unpkg # unpkg CDN
    # scriptFrom: https://npm.elemecdn.com/live2d-widget@3.x/lib/L2Dwidget.min.js # 你的自定义 url
    tagMode: false # 标签模式, 是否仅替换 live2d tag标签而非插入到所有页面中
    debug: false # 调试, 是否在控制台输出日志
    model:
      use: live2d-widget-model-wanko # npm-module package name
      # use: wanko # 博客根目录/live2d_models/ 下的目录名
      # use: ./wives/wanko # 相对于博客根目录的路径
      # use: https://npm.elemecdn.com/live2d-widget-model-wanko@1.0.5/assets/wanko.model.json # 你的自定义 url
    display:
      position: right #控制看板娘位置
      width: 150 #控制看板娘大小
      height: 300 #控制看板娘大小
    mobile:
      show: true # 手机中是否展示
  ```

  

* 完成后保存修改，在Hexo根目录下运行指令

  ```
  hexo clean
  hexo g
  hexo s
  ```

* 之所以必须要使用hexo clean是因为我们需要清空缓存重新生成静态页面，不然看板娘没被加入生成的静态页面里，是不会出现的。

  

### 更换看板娘

1. 同样是在Hexo根目录`[Blog]`下，打开终端，选择想要的看板娘进行安装，例如我这里用到的是 `live2d-widget-model-koharu`，一个Q版小正太。其他的模型也可以在[模型预览](https://huaji8.top/post/live2d-plugin-2.0/)里查看以供选择。

2. 输入指令

   ```
   BASH
   npm install --save live2d-widget-model-koharu
   ```

3. 然后在站点配置文件

   ```
   [Blogroot]\_config.yml
   ```

   里找到

   ```
   model
   ```

   项修改为期望的模型。

   ```
   YML
   model:
     use: live2d-widget-model-koharu
     # 默认为live2d-widget-model-wanko
   ```

4. 之后按部就班的运行

   ```
   BASH
   hexo clean
   hexo g
   hexo s
   ```

   就能在

   ```
   localhost:4000
   ```

   上查看效果了。

   

### 卸载看板娘

这个是第二种方式安装看板娘的卸载方法，其它方式很简单就不说了 

卸载插件和卸载模型的指令都是通过npm进行操作的。在博客根目录`[Blog]`打开终端，输入：

```
npm uninstall hexo-helper-live2d #卸载看板娘插件
npm uninstall live2d-widget-model-modelname #卸载看板娘模型。记得替换modelname为看板娘名称
```

卸载后为了保证配置项不出错，记得把`[Blog]\_config.yml`里的配置项给注释或者删除掉。



### 大神魔改看板娘

会说话，能换装，来自张书樵大神 	链接：https://github.com/stevenjoezhang/live2d-widget.git



1. 在[Blog]\node_modules\hexo-theme-butterfly\source目录下打开终端,输入

   ```
   git clone https://github.com/stevenjoezhang/live2d-widget.git live2d-widget
   ```

   这行指令的意思就是`clone`这个项目到`source`路径下并重命名为`live2d-widget`。

   我下载失败了就去了网址下载了压缩包，如果是用下载项目压缩包，解压后放到这里的，也记得把文件夹`更名为live2d-widge`t。

   

2. 找到路径`[Blog]\node_modules\hexo-theme-butterfly\source\live2d-widget\autoload.js`，打开`autoload.js`，找到这行代码，修改为如下内容：

   ```
   const live2d_path = "/live2d-widget/";
   ```

   此处引用一下参考教程原话：`autoload.js`中的注释的绝对地址指的是，将资源打包放到`[Blogroot]/theme/next/source`中后，以`[Blogroot]/theme/next/source`为根目录（/）的绝对路径。【旧版教程，可能和新版本路径不一样，明白意思即可】

   

3. 在`Butterfly`的主题配置文件`[Blog]\_config.butterfly.yml`中,`butterfly`主题其实自带`fontawesome`依赖，无需引入

   ```
   inject
         bottom:
          - <script defer src="/live2d-widget/autoload.js"></script>
   ```

   引入的时候记得写注释，以后改起来也方便

   

4. 保存所有文件的修改，然后照例执行

   ```
   hexo clean
   hexo g
   hexo s
   ```

   就能在`localhost:4000`看到预览了。

   

5. 自定义修改
   有一定前端基础的小伙伴可以通过修改`[Blog]\\node_modules\hexo-theme-butterfly\source\live2d-widget`路径下的样式资源文件：

   - `waifu-tips.js`:包含了按钮和对话框的逻辑
   - `waifu-tips.json` :定义了触发条件（selector，CSS 选择器）和触发时显示的文字（text）；
   - `waifu.css`:看板娘的样式表。可以对看板娘的位置布局等做自定义修改。



#### 关于一些bug说明

* 在配置了`gulp`和`pwa`之后，看板娘消失。这个是`gulp-babel`压缩导致的。

  

#### 解决方法

1. 直接把看板娘提取出来作为单独的项目，然后借助jsdelivr引用相应的静态资源。`live2d-widget`文件夹不放在博客的`source`目录中，而是存在独立的`github`仓库里。这样`gulp`怎么也压缩不到。而且得益于`jsdelivr`，看板娘的加载速度也有所提高。

   

2. 配置方法是将live2d-widget 项目fork到自己的仓库（用原项目也可以，但是那样不方便更改样式啊），然后修改 autoload.js 里的路径为你自己的仓库名。【看清楚需要修改的地方】

   ```
    const live2d_path = "https://cdn.jsdelivr.net/gh/stevenjoezhang/live2d-widget/";
    const live2d_path = "https://cdn.jsdelivr.net/gh/YourGithubName/live2d-widget/";
   ```

3. 在主题配置项里也可以使用`https://cdn.jsdelivr.net/gh/YourGithubName/live2d-widget/autoload.js`来引入。



说明：不知道怎么弄的可以去 csdn 搜一下 本地仓库上传到github 教程





#### 本地化API配置

1. 懒人配置方案:修改张书樵大神的项目内的`~\live2d-widget\autoload.js`,将模型资源由`cdnPath`改为`apiPath`。

   ```
     // 加载 waifu.css live2d.min.js waifu-tips.js
     if (screen.width >= 768) {
     	Promise.all([
     		loadExternalResource(live2d_path + "waifu.css", "css"),
     		loadExternalResource(live2d_path + "live2d.min.js", "js"),
     		loadExternalResource(live2d_path + "waifu-tips.js", "js")
     	]).then(() => {
     		initWidget({
     			waifuPath: live2d_path + "waifu-tips.json",
   - 			//apiPath: "https://live2d.fghrsh.net/api/",
   -  			cdnPath: "https://cdn.jsdelivr.net/gh/fghrsh/live2d_api/"
   + 			apiPath: "https://live2d.fghrsh.net/api/",
   +  			//cdnPath: "https://cdn.jsdelivr.net/gh/fghrsh/live2d_api/"
     		});
     	});
     }
   ```

2. 上面已经说到过，张书樵大神的魔改方案其实已经实现了`本地化API`，只是因为模型配置路径不同才导致无法换装的。所以其实只要注意配置模型时，保证每个可以展示的模型都有相应的`index.json`并且在`model_list.json`里有相应的模型路径就可以了。这里读者可以直接使用我配置好的本地化项目的路径：修改张书樵大神的项目内的`~\live2d-widget\autoload.js`,修改`cdnPath`

   ```
     // 加载 waifu.css live2d.min.js waifu-tips.js
     if (screen.width >= 768) {
     	Promise.all([
     		loadExternalResource(live2d_path + "waifu.css", "css"),
     		loadExternalResource(live2d_path + "live2d.min.js", "js"),
     		loadExternalResource(live2d_path + "waifu-tips.js", "js")
     	]).then(() => {
     		initWidget({
     			waifuPath: live2d_path + "waifu-tips.json",
     			//apiPath: "https://live2d.fghrsh.net/api/",
   -  			cdnPath: "https://cdn.jsdelivr.net/gh/fghrsh/live2d_api/"
   +  			cdnPath: "https://npm.elemecdn.com/akilar-live2dapi@latest/"
   //因为jsdelivr不支持50MB以上的包的加速，可能报403错误，所以用的vercel的CDN服务。
   //可以考虑clone我配置好的live2d_api仓库自己部署到其他更快的cdn服务上。
     		});
     	});
     }
   ```

   除了让原有模型换装可用化以为，还顺便添加了`亚丝娜`、`和泉纱雾`，`血小板`、`土间埋（干物妹小埋）`和`香风智乃`的模型哦。

3. 

#### 页脚跳动的♥

编辑博客根目录`node_modules\hexo-theme-butterfly\layout\includes\footer.pug`文件，修改以下内容

* 改第一部分内容

```
.copyright!= `&copy;${theme.footer.owner.since} - ${nowYear} By ${config.author}`
```

将上面代码改为下面的

```
.copyright!= `&copy;${theme.footer.owner.since} - ${nowYear} <i id="heartbeat" class="fa fas fa-heartbeat"></i>  ${config.author}`
```



* 改第二部分内容

  ```
  .copyright!= `&copy;${nowYear} By ${config.author}`
  ```

  将上面代码改为下面的

  ```
  .copyright!= `&copy;${nowYear} <i id="heartbeat" class="fa fas fa-heartbeat"></i> ${config.author}`
  ```

  

* 编辑`butterfly.yml`文件

  在`inject->head`下面添加如下内容：

  ```
  - <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/HCLonely/images@master/others/heartbeat.min.css">
  ```



### Butterfly加载动画修改

添加配置文件，在目录`node_modules\hexo-theme-butterfly\layout\includes\loading\loaded.ejs`下添加 loaded.ejs 文件，代码如下

```
<% if (theme.preloader.enable) { %>
<div id='loader'>
    <% if(theme.preloader.layout == 'gear' ) {%>
    <div class="outer_box">
    <div class='loader_overlay'></div>
    <div class='loader_cogs'>
        <div class='loader_cogs__top'>
            <div class='top_part'></div>
            <div class='top_part'></div>
            <div class='top_part'></div>
            <div class='top_hole'></div>
        </div>
        <div class='loader_cogs__left'>
            <div class='left_part'></div>
            <div class='left_part'></div>
            <div class='left_part'></div>
            <div class='left_hole'></div>
        </div>
        <div class='loader_cogs__bottom'>
            <div class='bottom_part'></div>
            <div class='bottom_part'></div>
            <div class='bottom_part'></div>
            <div class='bottom_hole'></div>
        </div>
        <p style="text-align:center">&nbsp;&nbsp;&nbsp;loading...</p>
    </div>
    </div>
  <% } else if(theme.preloader.layout == 'spinner-box') { %>
    <div class="loading-left-bg"></div>
    <div class="loading-right-bg"></div>
    <div class="spinner-box">
        <div class="configure-border-1">
            <div class="configure-core"></div>
        </div>
        <div class="configure-border-2">
            <div class="configure-core"></div>
        </div>
        <div class="loading-word">加载中...</div>
    </div>
  <% } %>
</div>

<script>
  var endLoading = function () {
    document.body.style.overflow = 'auto';
    document.getElementById('loader').classList.add("loading");
  }
  window.addEventListener('load',endLoading);
</script>
<% } %>
```

### 引入样式文件

* 引入spinner-boxbutterfly，在主题配置文件 inject 处 heard处引入以下代码

```
- <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/zyoushuo/Blog@latest/hexo/css/loading_style_1.css" >
```

gear风格样式文件引入

```
- <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/zyoushuo/Blog@latest/hexo/css/loading_style_2.css" >
```



* 引入到页面

​	找到 node_modules\hexo-theme-butterfly\layout\includes\layout.pug ,将如下代码替换

```
if theme.preloader
      !=partial('includes/loading/loading', {}, {cache:theme.fragment_cache})
```

替换为如下代码：

```
if theme.preloader
      !=partial('includes/loading/loaded.ejs', {}, {cache:theme.fragment_cache})
```



* 开启加载

  主题配置文件下的

  ```
  preloader: true
  ```

  改为如下：

  ```
  preloader:
    enable: true
    layout: gear # gear, spinner-box 两种样式
  ```

  

* 不需要的话关掉即可

  

### 浏览器标题恶搞

在`node_modules\hexo-theme-butterfly\source\js\crash_cheat.js`文件夹下添加`crash_cheat.js`文件 填入以下内容：（记得修改你喜好的标题）

```
var OriginTitle = document.title;
 var titleTime;
 document.addEventListener('visibilitychange', function () {
     if (document.hidden) {
         $('[rel="icon"]').attr('href', "/joke.ico");
         document.title = '💙不要走，再看看💙';
         clearTimeout(titleTime);
     }
     else {
         $('[rel="icon"]').attr('href', "/favicon.ico");
         document.title = '发现宝藏~';
         titleTime = setTimeout(function () {
             document.title = OriginTitle;
         }, 2000);
     }
 });
```

在 node_modules\hexo-theme-butterfly\layout\includes\layout.pug  中添加以下代码来引入

```
script(type='text/javascript', src='/js/crash_cheat.js')
```

在`inject:` -> `bottom:` 引入以下文件

```javascript
- <script src="https://cdn.jsdelivr.net/gh/weilain/cdn-photo/js/jquery.min.js"></script>
```



自定义文章封面

* 首先：找到主题配置文件  cover ，文章主题的修改在 cover 下，如果不想麻烦可以选择统一的封面，把上面那个url修改成自己喜欢的图片地址即可

  ![image-20220804204629098](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804204629098.png)



* 自定义文章封面

  **写文章的时候在cover后面输入你想要的封面图片的url，在top_img后面加上你想要的顶部图片的url**



背景渐变

在css---->style.css 引入以下文件即可

```
#web_bg {
  background: -webkit-linear-gradient(
    0deg,
    rgba(247, 149, 51, 0.1) 0,
    rgba(243, 112, 85, 0.1) 15%,
    rgba(239, 78, 123, 0.1) 30%,
    rgba(161, 102, 171, 0.1) 44%,
    rgba(80, 115, 184, 0.1) 58%,
    rgba(16, 152, 173, 0.1) 72%,
    rgba(7, 179, 155, 0.1) 86%,
    rgba(109, 186, 130, 0.1) 100%
  );
  background: -moz-linear-gradient(
    0deg,
    rgba(247, 149, 51, 0.1) 0,
    rgba(243, 112, 85, 0.1) 15%,
    rgba(239, 78, 123, 0.1) 30%,
    rgba(161, 102, 171, 0.1) 44%,
    rgba(80, 115, 184, 0.1) 58%,
    rgba(16, 152, 173, 0.1) 72%,
    rgba(7, 179, 155, 0.1) 86%,
    rgba(109, 186, 130, 0.1) 100%
  );
  background: -o-linear-gradient(
    0deg,
    rgba(247, 149, 51, 0.1) 0,
    rgba(243, 112, 85, 0.1) 15%,
    rgba(239, 78, 123, 0.1) 30%,
    rgba(161, 102, 171, 0.1) 44%,
    rgba(80, 115, 184, 0.1) 58%,
    rgba(16, 152, 173, 0.1) 72%,
    rgba(7, 179, 155, 0.1) 86%,
    rgba(109, 186, 130, 0.1) 100%
  );
  background: -ms-linear-gradient(
    0deg,
    rgba(247, 149, 51, 0.1) 0,
    rgba(243, 112, 85, 0.1) 15%,
    rgba(239, 78, 123, 0.1) 30%,
    rgba(161, 102, 171, 0.1) 44%,
    rgba(80, 115, 184, 0.1) 58%,
    rgba(16, 152, 173, 0.1) 72%,
    rgba(7, 179, 155, 0.1) 86%,
    rgba(109, 186, 130, 0.1) 100%
  );
  background: linear-gradient(
    90deg,
    rgba(247, 149, 51, 0.1) 0,
    rgba(243, 112, 85, 0.1) 15%,
    rgba(239, 78, 123, 0.1) 30%,
    rgba(161, 102, 171, 0.1) 44%,
    rgba(80, 115, 184, 0.1) 58%,
    rgba(16, 152, 173, 0.1) 72%,
    rgba(7, 179, 155, 0.1) 86%,
    rgba(109, 186, 130, 0.1) 100%
  );
}
```

## 引入阿里矢量图标库

阿里图标库全名阿里巴巴矢量图标库。提供了丰富的免费图标资源。并且支持多种引入方式。

### 新建图标项目

1、访问 [阿里巴巴矢量图标库](https://www.iconfont.cn/) , 注册登录。

2、搜索自己心仪的图标，然后选择添加入库，加到购物车。

3、选择完毕后点击右上角的购物车图标，打开侧栏，选择添加到项目，如果没有项目就新建一个。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/81982c3a.png" alt="img" style="zoom: 50%;" />



### 引入图标

1、找到之前新建的图标项目，选择Symbol->查看在线链接，获取 `Symbol.js` 的在线链接，如果没有在线链接记得生成一下，并引入。在 `[Blog]\_config.butterfly.yml` 的 `inject` 配置项中填入：

```
 bottom:
     - <script async src="你生成的链接"></script>
```

2、打开 node_modules\hexo-theme-butterfly\source\css\custom.css（新建文件），输入以下内容：

```
svg.icon {
   width: 1em; height: 1em;
   /* width和height定义图标的默认宽度和高度*/
   vertical-align: -0.15em;
   fill: currentColor;
   overflow: hidden;
}
```

3、添加外挂标签，在 node_modules\hexo-theme-butterfly\scripts\tag目录下新建 `iconfont.js`，打开该文件输入：

```
'use strict';

function iconFont(args) {
  args = args.join(' ').split(',')
  let p0 = args[0]
  let p1 = args[1]?args[1]:1
  return `<svg class="icon" style="width:${p1}em; height:${p1}em" aria-hidden="true"><use xlink:href="#${p0}"></use></svg>`;
}

hexo.extend.tag.register('icon',iconFont);
```



`hexo cl && hexo g` 以后即可使用外挂标签的形式来写入图标了。



### Hexo-使用阿里iconfont图标

https://cloud.tencent.com/developer/article/1813883



### 添加标签云

使用命令进行安装插件

```
npm install hexo-tag-cloud --save
```

打开node_modules\hexo-theme-butterfly\layout\includes\widget\card_tags.pug 文件，用下面内容将其替换掉，最好把之前的文件备份一下,防止后悔

```
if site.tags.length
  .card-widget.card-tags
    .card-content
      .item-headline
        i.fa.fa-tags(aria-hidden="true")
        span= _p('aside.card_tags')
        script(type="text/javascript" charset="utf-8" src="/js/tagcloud.js")
        script(type="text/javascript" charset="utf-8" src="/js/tagcanvas.js")
        #myCanvasContainer.widget.tagcloud(align='center')
          canvas#resCanvas(width='200', height='200', style='width=100%')
            != tagcloud()
          != tagcloud({min_font: 16, max_font: 24, amount: 50, color: true, start_color: '#999', end_color: '#99a9bf'})
```



普通标签备份

```
if theme.aside.card_tags.enable
  if site.tags.length
    .card-widget.card-tags
      .item-headline
        i.fas.fa-tags
        span= _p('aside.card_tags')

      - let tagLimit = theme.aside.card_tags.limit === 0 ? 0 : theme.aside.card_tags.limit || 40
      if theme.aside.card_tags.color
        .card-tag-cloud!= cloudTags({source: site.tags, minfontsize: 1.15, maxfontsize: 1.45, limit: tagLimit, unit: 'em'})
      else
        .card-tag-cloud!= tagcloud({min_font: 1.1, max_font: 1.5, amount: tagLimit , color: true, start_color: '#999', end_color: '#99a9bf', unit: 'em'})

```





## 添加天气

https://cloud.tencent.com/developer/article/1935732

```html
<div id="he-plugin-simple"></div>
<script>
WIDGET = {
  "CONFIG": {
    "modules": "01234",
    "background": "5",
    "tmpColor": "FFFFFF",
    "tmpSize": "16",
    "cityColor": "FFFFFF",
    "citySize": "16",
    "aqiColor": "FFFFFF",
    "aqiSize": "16",
    "weatherIconSize": "24",
    "alertIconSize": "18",
    "padding": "10px 10px 10px 10px",
    "shadow": "0",
    "language": "auto",
    "fixed": "false",
    "vertical": "top",
    "horizontal": "left",
    "key": "e7e3ea403de040d8961ec5e85b1f7723"
  }
}
</script>
<script src="https://widget.qweather.net/simple/static/js/he-simple-common.js?v=2.0"></script>
```

## 白天夜间切换

https://akilar.top/posts/d9550c81/#:~:text=%E5%8E%9F%E7%94%9F%E7%9A%84-,%E5%A4%9C,-%E9%97%B4%E5%88%87%E6%8D%A2



# 自定义右键菜单

## 步骤

1. 在`BlogRoot/node_modules/hexo-theme-butterfly/layout/includes`文件夹下新建一个`right-menu`的文件夹，在此文件夹下新建一个`index.pug`文件

![image-20220818140803228](C:/Users/DELL/OneDrive/Study%2520Document/blog/butterfly%25E7%25BE%258E%25E5%258C%2596%25EF%25BC%2588%25E4%25BA%258C%25EF%25BC%2589.assets/image-20220818140803228.png)

将以下代码复制到文件中

~~~
#rightMenu
    .rightMenu-group.rightMenu-small
        .rightMenu-item#menu-backward
            i.fa-solid.fa-arrow-left
        .rightMenu-item#menu-forward
            i.fa-solid.fa-arrow-right
        .rightMenu-item#menu-refresh
            i.fa-solid.fa-arrow-rotate-right
        .rightMenu-item#menu-home
            i.fa-solid.fa-house
    .rightMenu-group.rightMenu-line.rightMenuOther
        a.rightMenu-item.menu-link(href='/archives/')
            i.fa-solid.fa-archive
            span='文章归档'
        a.rightMenu-item.menu-link(href='/categories/')
            i.fa-solid.fa-folder-open
            span='文章分类'
        a.rightMenu-item.menu-link(href='/tags/')
            i.fa-solid.fa-tags
            span='文章标签'
    .rightMenu-group.rightMenu-line.rightMenuNormal
        a.rightMenu-item.menu-link#menu-radompage(href='/random/index.html')
            i.fa-solid.fa-shoe-prints
            span='随便逛逛'
        .rightMenu-item#menu-translate
            i.fa-solid.fa-earth-asia
            span='繁简切换'
        .rightMenu-item#menu-darkmode
            i.fa-solid.fa-moon
            span='切换模式'
#rightmenu-mask
~~~

2. 在`BlogRoot/node_modules/hexo-theme-butterfly/layout/includes/layout.pug`中引入上一步中创建的`index.pug`文件。
   具体位置如下图：==路径要正确==

   ~~~
   !=partial('includes/right-menu/index', {}, {cache: true})
   ~~~

   

   ![image-20220818141151807](C:/Users/DELL/OneDrive/Study%2520Document/blog/butterfly%25E7%25BE%258E%25E5%258C%2596%25EF%25BC%2588%25E4%25BA%258C%25EF%25BC%2589.assets/image-20220818141151807.png)

3. 在`BlogRoot/node_modules/hexo-theme-butterfly/source/js`文件夹下新建一个`rightMenu.js`，将以下代码复制到文件中。

   ~~~bash
   let rm = {};
   rm.showRightMenu = function (isTrue, x = 0, y = 0) {
       let $rightMenu = $('#rightMenu');
       $rightMenu.css('top', x + 'px').css('left', y + 'px');
   
       if (isTrue) {
           stopMaskScroll()
           $rightMenu.show();
       } else {
           $rightMenu.hide();
       }
   };
   let rmWidth = $('#rightMenu').width();
   let rmHeight = $('#rightMenu').height();
   rm.reloadrmSize = function () {
       rmWidth = $("#rightMenu").width();
       rmHeight = $("#rightMenu").height()
   };
   window.oncontextmenu = function (event) {
       if (document.body.clientWidth > 768) {
           let pageX = event.clientX + 10;	
           let pageY = event.clientY;
           let $rightMenuNormal = $(".rightMenuNormal");
           let $rightMenuOther = $(".rightMenuOther");
           let $rightMenuReadmode = $("#menu-readmode");
           $rightMenuNormal.show();
           $rightMenuOther.show();
           rm.reloadrmSize();
           if (pageX + rmWidth > window.innerWidth) {
               pageX -= rmWidth;
           }
           if (pageY + rmHeight > window.innerHeight) {
               pageY -= rmHeight;
           }
           rm.showRightMenu(true, pageY, pageX);
           $('#rightmenu-mask').attr('style', 'display: flex');
           return false;
       }
   };
   function removeRightMenu() {
       rm.showRightMenu(false);
       $('#rightmenu-mask').attr('style', 'display: none');
   }
   function stopMaskScroll() {
       if (document.getElementById("rightmenu-mask")) {
           let xscroll = document.getElementById("rightmenu-mask");
           xscroll.addEventListener("mousewheel", function (e) {
               removeRightMenu();
           }, false);
       };
       if (document.getElementById("rightMenu")) {
           let xscroll = document.getElementById("rightMenu");
           xscroll.addEventListener("mousewheel", function (e) {
               removeRightMenu();
           }, false);
       }
   }
   /**
    * @name:  切換模式
    */
   function switchDarkMode() {
       removeRightMenu();
       const nowMode = document.documentElement.getAttribute('data-theme') === 'dark' ? 'dark' : 'light'
       if (nowMode === 'light') {
           activateDarkMode();
           saveToLocal.set('theme', 'dark', 2);
           GLOBAL_CONFIG.Snackbar !== undefined && btf.snackbarShow(GLOBAL_CONFIG.Snackbar.day_to_night);
       } else {
           activateLightMode();
           saveToLocal.set('theme', 'light', 2);
           GLOBAL_CONFIG.Snackbar !== undefined && btf.snackbarShow(GLOBAL_CONFIG.Snackbar.night_to_day);
       }
       typeof utterancesTheme === 'function' && utterancesTheme();
       typeof FB === 'object' && window.loadFBComment();
       window.DISQUS && document.getElementById('disqus_thread').children.length && setTimeout(() => window.disqusReset(), 200);
   };
   /* eslint-disable no-undef */
   document.addEventListener('DOMContentLoaded', function () {
       translateInitialization();
       document.addEventListener('pjax:complete', translateInitialization);
   });
   const translate = GLOBAL_CONFIG.translate;
   const snackbarData = GLOBAL_CONFIG.Snackbar;
   const defaultEncoding = translate.defaultEncoding; /* 網站默認語言，1: 繁體中文, 2: 簡體中文 */
   const translateDelay = translate.translateDelay; /* 延遲時間,若不在前, 要設定延遲翻譯時間, 如100表示100ms,默認為0 */
   const msgToTraditionalChinese = translate.msgToTraditionalChinese; /* 此處可以更改為你想要顯示的文字 */
   const msgToSimplifiedChinese = translate.msgToSimplifiedChinese; /* 同上，但兩處均不建議更改 */
   let currentEncoding = defaultEncoding;
   const targetEncodingCookie = 'translate-chn-cht';
   let targetEncoding =
       saveToLocal.get(targetEncodingCookie) === undefined
           ? defaultEncoding
           : Number(saveToLocal.get('translate-chn-cht'));
   let translateButtonObject
   const isSnackbar = GLOBAL_CONFIG.Snackbar !== undefined;
   function translateText(txt) {
       if (txt === '' || txt == null) return '';
       if (currentEncoding === 1 && targetEncoding === 2) return Simplized(txt);
       else if (currentEncoding === 2 && targetEncoding === 1) { return Traditionalized(txt) } else return txt;
   }
   function translateBody(fobj) {
       let objs;
       if (typeof fobj === 'object') objs = fobj.childNodes;
       else objs = document.body.childNodes;
       for (let i = 0; i < objs.length; i++) {
           const obj = objs.item(i);
           if (
               '||BR|HR|'.indexOf('|' + obj.tagName + '|') > 0 ||
               obj === translateButtonObject
           ) { continue }
           if (obj.title !== '' && obj.title != null) { obj.title = translateText(obj.title) };
           if (obj.alt !== '' && obj.alt != null) obj.alt = translateText(obj.alt);
           if (obj.placeholder !== '' && obj.placeholder != null) obj.placeholder = translateText(obj.placeholder);
           if (
               obj.tagName === 'INPUT' &&
               obj.value !== '' &&
               obj.type !== 'text' &&
               obj.type !== 'hidden'
           ) { obj.value = translateText(obj.value) }
           if (obj.nodeType === 3) obj.data = translateText(obj.data);
           else translateBody(obj);
       }
   }
   function translatePage() {
       if (targetEncoding === 1) {
           currentEncoding = 1;
           targetEncoding = 2;
           saveToLocal.set(targetEncodingCookie, targetEncoding, 2);
           translateBody();
           if (isSnackbar) btf.snackbarShow(snackbarData.cht_to_chs);
       } else if (targetEncoding === 2) {
           currentEncoding = 2;
           targetEncoding = 1;
           saveToLocal.set(targetEncodingCookie, targetEncoding, 2);
           translateBody();
           if (isSnackbar) btf.snackbarShow(snackbarData.chs_to_cht);
       }
   }
   function JTPYStr() {
       return '万与丑专业丛东丝丢两严丧个丬丰临为丽举么义乌乐乔习乡书买乱争于亏云亘亚产亩亲亵亸亿仅从仑仓仪们价众优伙会伛伞伟传伤伥伦伧伪伫体余佣佥侠侣侥侦侧侨侩侪侬俣俦俨俩俪俭债倾偬偻偾偿傥傧储傩儿兑兖党兰关兴兹养兽冁内冈册写军农冢冯冲决况冻净凄凉凌减凑凛几凤凫凭凯击凼凿刍划刘则刚创删别刬刭刽刿剀剂剐剑剥剧劝办务劢动励劲劳势勋勐勚匀匦匮区医华协单卖卢卤卧卫却卺厂厅历厉压厌厍厕厢厣厦厨厩厮县参叆叇双发变叙叠叶号叹叽吁后吓吕吗吣吨听启吴呒呓呕呖呗员呙呛呜咏咔咙咛咝咤咴咸哌响哑哒哓哔哕哗哙哜哝哟唛唝唠唡唢唣唤唿啧啬啭啮啰啴啸喷喽喾嗫呵嗳嘘嘤嘱噜噼嚣嚯团园囱围囵国图圆圣圹场坂坏块坚坛坜坝坞坟坠垄垅垆垒垦垧垩垫垭垯垱垲垴埘埙埚埝埯堑堕塆墙壮声壳壶壸处备复够头夸夹夺奁奂奋奖奥妆妇妈妩妪妫姗姜娄娅娆娇娈娱娲娴婳婴婵婶媪嫒嫔嫱嬷孙学孪宁宝实宠审宪宫宽宾寝对寻导寿将尔尘尧尴尸尽层屃屉届属屡屦屿岁岂岖岗岘岙岚岛岭岳岽岿峃峄峡峣峤峥峦崂崃崄崭嵘嵚嵛嵝嵴巅巩巯币帅师帏帐帘帜带帧帮帱帻帼幂幞干并广庄庆庐庑库应庙庞废庼廪开异弃张弥弪弯弹强归当录彟彦彻径徕御忆忏忧忾怀态怂怃怄怅怆怜总怼怿恋恳恶恸恹恺恻恼恽悦悫悬悭悯惊惧惨惩惫惬惭惮惯愍愠愤愦愿慑慭憷懑懒懔戆戋戏戗战戬户扎扑扦执扩扪扫扬扰抚抛抟抠抡抢护报担拟拢拣拥拦拧拨择挂挚挛挜挝挞挟挠挡挢挣挤挥挦捞损捡换捣据捻掳掴掷掸掺掼揸揽揿搀搁搂搅携摄摅摆摇摈摊撄撑撵撷撸撺擞攒敌敛数斋斓斗斩断无旧时旷旸昙昼昽显晋晒晓晔晕晖暂暧札术朴机杀杂权条来杨杩杰极构枞枢枣枥枧枨枪枫枭柜柠柽栀栅标栈栉栊栋栌栎栏树栖样栾桊桠桡桢档桤桥桦桧桨桩梦梼梾检棂椁椟椠椤椭楼榄榇榈榉槚槛槟槠横樯樱橥橱橹橼檐檩欢欤欧歼殁殇残殒殓殚殡殴毁毂毕毙毡毵氇气氢氩氲汇汉污汤汹沓沟没沣沤沥沦沧沨沩沪沵泞泪泶泷泸泺泻泼泽泾洁洒洼浃浅浆浇浈浉浊测浍济浏浐浑浒浓浔浕涂涌涛涝涞涟涠涡涢涣涤润涧涨涩淀渊渌渍渎渐渑渔渖渗温游湾湿溃溅溆溇滗滚滞滟滠满滢滤滥滦滨滩滪漤潆潇潋潍潜潴澜濑濒灏灭灯灵灾灿炀炉炖炜炝点炼炽烁烂烃烛烟烦烧烨烩烫烬热焕焖焘煅煳熘爱爷牍牦牵牺犊犟状犷犸犹狈狍狝狞独狭狮狯狰狱狲猃猎猕猡猪猫猬献獭玑玙玚玛玮环现玱玺珉珏珐珑珰珲琎琏琐琼瑶瑷璇璎瓒瓮瓯电画畅畲畴疖疗疟疠疡疬疮疯疱疴痈痉痒痖痨痪痫痴瘅瘆瘗瘘瘪瘫瘾瘿癞癣癫癯皑皱皲盏盐监盖盗盘眍眦眬着睁睐睑瞒瞩矫矶矾矿砀码砖砗砚砜砺砻砾础硁硅硕硖硗硙硚确硷碍碛碜碱碹磙礼祎祢祯祷祸禀禄禅离秃秆种积称秽秾稆税稣稳穑穷窃窍窑窜窝窥窦窭竖竞笃笋笔笕笺笼笾筑筚筛筜筝筹签简箓箦箧箨箩箪箫篑篓篮篱簖籁籴类籼粜粝粤粪粮糁糇紧絷纟纠纡红纣纤纥约级纨纩纪纫纬纭纮纯纰纱纲纳纴纵纶纷纸纹纺纻纼纽纾线绀绁绂练组绅细织终绉绊绋绌绍绎经绐绑绒结绔绕绖绗绘给绚绛络绝绞统绠绡绢绣绤绥绦继绨绩绪绫绬续绮绯绰绱绲绳维绵绶绷绸绹绺绻综绽绾绿缀缁缂缃缄缅缆缇缈缉缊缋缌缍缎缏缐缑缒缓缔缕编缗缘缙缚缛缜缝缞缟缠缡缢缣缤缥缦缧缨缩缪缫缬缭缮缯缰缱缲缳缴缵罂网罗罚罢罴羁羟羡翘翙翚耢耧耸耻聂聋职聍联聩聪肃肠肤肷肾肿胀胁胆胜胧胨胪胫胶脉脍脏脐脑脓脔脚脱脶脸腊腌腘腭腻腼腽腾膑臜舆舣舰舱舻艰艳艹艺节芈芗芜芦苁苇苈苋苌苍苎苏苘苹茎茏茑茔茕茧荆荐荙荚荛荜荞荟荠荡荣荤荥荦荧荨荩荪荫荬荭荮药莅莜莱莲莳莴莶获莸莹莺莼萚萝萤营萦萧萨葱蒇蒉蒋蒌蓝蓟蓠蓣蓥蓦蔷蔹蔺蔼蕲蕴薮藁藓虏虑虚虫虬虮虽虾虿蚀蚁蚂蚕蚝蚬蛊蛎蛏蛮蛰蛱蛲蛳蛴蜕蜗蜡蝇蝈蝉蝎蝼蝾螀螨蟏衅衔补衬衮袄袅袆袜袭袯装裆裈裢裣裤裥褛褴襁襕见观觃规觅视觇览觉觊觋觌觍觎觏觐觑觞触觯詟誉誊讠计订讣认讥讦讧讨让讪讫训议讯记讱讲讳讴讵讶讷许讹论讻讼讽设访诀证诂诃评诅识诇诈诉诊诋诌词诎诏诐译诒诓诔试诖诗诘诙诚诛诜话诞诟诠诡询诣诤该详诧诨诩诪诫诬语诮误诰诱诲诳说诵诶请诸诹诺读诼诽课诿谀谁谂调谄谅谆谇谈谊谋谌谍谎谏谐谑谒谓谔谕谖谗谘谙谚谛谜谝谞谟谠谡谢谣谤谥谦谧谨谩谪谫谬谭谮谯谰谱谲谳谴谵谶谷豮贝贞负贠贡财责贤败账货质贩贪贫贬购贮贯贰贱贲贳贴贵贶贷贸费贺贻贼贽贾贿赀赁赂赃资赅赆赇赈赉赊赋赌赍赎赏赐赑赒赓赔赕赖赗赘赙赚赛赜赝赞赟赠赡赢赣赪赵赶趋趱趸跃跄跖跞践跶跷跸跹跻踊踌踪踬踯蹑蹒蹰蹿躏躜躯车轧轨轩轪轫转轭轮软轰轱轲轳轴轵轶轷轸轹轺轻轼载轾轿辀辁辂较辄辅辆辇辈辉辊辋辌辍辎辏辐辑辒输辔辕辖辗辘辙辚辞辩辫边辽达迁过迈运还这进远违连迟迩迳迹适选逊递逦逻遗遥邓邝邬邮邹邺邻郁郄郏郐郑郓郦郧郸酝酦酱酽酾酿释里鉅鉴銮錾钆钇针钉钊钋钌钍钎钏钐钑钒钓钔钕钖钗钘钙钚钛钝钞钟钠钡钢钣钤钥钦钧钨钩钪钫钬钭钮钯钰钱钲钳钴钵钶钷钸钹钺钻钼钽钾钿铀铁铂铃铄铅铆铈铉铊铋铍铎铏铐铑铒铕铗铘铙铚铛铜铝铞铟铠铡铢铣铤铥铦铧铨铪铫铬铭铮铯铰铱铲铳铴铵银铷铸铹铺铻铼铽链铿销锁锂锃锄锅锆锇锈锉锊锋锌锍锎锏锐锑锒锓锔锕锖锗错锚锜锞锟锠锡锢锣锤锥锦锨锩锫锬锭键锯锰锱锲锳锴锵锶锷锸锹锺锻锼锽锾锿镀镁镂镃镆镇镈镉镊镌镍镎镏镐镑镒镕镖镗镙镚镛镜镝镞镟镠镡镢镣镤镥镦镧镨镩镪镫镬镭镮镯镰镱镲镳镴镶长门闩闪闫闬闭问闯闰闱闲闳间闵闶闷闸闹闺闻闼闽闾闿阀阁阂阃阄阅阆阇阈阉阊阋阌阍阎阏阐阑阒阓阔阕阖阗阘阙阚阛队阳阴阵阶际陆陇陈陉陕陧陨险随隐隶隽难雏雠雳雾霁霉霭靓静靥鞑鞒鞯鞴韦韧韨韩韪韫韬韵页顶顷顸项顺须顼顽顾顿颀颁颂颃预颅领颇颈颉颊颋颌颍颎颏颐频颒颓颔颕颖颗题颙颚颛颜额颞颟颠颡颢颣颤颥颦颧风飏飐飑飒飓飔飕飖飗飘飙飚飞飨餍饤饥饦饧饨饩饪饫饬饭饮饯饰饱饲饳饴饵饶饷饸饹饺饻饼饽饾饿馀馁馂馃馄馅馆馇馈馉馊馋馌馍馎馏馐馑馒馓馔馕马驭驮驯驰驱驲驳驴驵驶驷驸驹驺驻驼驽驾驿骀骁骂骃骄骅骆骇骈骉骊骋验骍骎骏骐骑骒骓骔骕骖骗骘骙骚骛骜骝骞骟骠骡骢骣骤骥骦骧髅髋髌鬓魇魉鱼鱽鱾鱿鲀鲁鲂鲄鲅鲆鲇鲈鲉鲊鲋鲌鲍鲎鲏鲐鲑鲒鲓鲔鲕鲖鲗鲘鲙鲚鲛鲜鲝鲞鲟鲠鲡鲢鲣鲤鲥鲦鲧鲨鲩鲪鲫鲬鲭鲮鲯鲰鲱鲲鲳鲴鲵鲶鲷鲸鲹鲺鲻鲼鲽鲾鲿鳀鳁鳂鳃鳄鳅鳆鳇鳈鳉鳊鳋鳌鳍鳎鳏鳐鳑鳒鳓鳔鳕鳖鳗鳘鳙鳛鳜鳝鳞鳟鳠鳡鳢鳣鸟鸠鸡鸢鸣鸤鸥鸦鸧鸨鸩鸪鸫鸬鸭鸮鸯鸰鸱鸲鸳鸴鸵鸶鸷鸸鸹鸺鸻鸼鸽鸾鸿鹀鹁鹂鹃鹄鹅鹆鹇鹈鹉鹊鹋鹌鹍鹎鹏鹐鹑鹒鹓鹔鹕鹖鹗鹘鹚鹛鹜鹝鹞鹟鹠鹡鹢鹣鹤鹥鹦鹧鹨鹩鹪鹫鹬鹭鹯鹰鹱鹲鹳鹴鹾麦麸黄黉黡黩黪黾'
   }
   function FTPYStr() {
       return '萬與醜專業叢東絲丟兩嚴喪個爿豐臨為麗舉麼義烏樂喬習鄉書買亂爭於虧雲亙亞產畝親褻嚲億僅從侖倉儀們價眾優夥會傴傘偉傳傷倀倫傖偽佇體餘傭僉俠侶僥偵側僑儈儕儂俁儔儼倆儷儉債傾傯僂僨償儻儐儲儺兒兌兗黨蘭關興茲養獸囅內岡冊寫軍農塚馮衝決況凍淨淒涼淩減湊凜幾鳳鳧憑凱擊氹鑿芻劃劉則剛創刪別剗剄劊劌剴劑剮劍剝劇勸辦務勱動勵勁勞勢勳猛勩勻匭匱區醫華協單賣盧鹵臥衛卻巹廠廳曆厲壓厭厙廁廂厴廈廚廄廝縣參靉靆雙發變敘疊葉號歎嘰籲後嚇呂嗎唚噸聽啟吳嘸囈嘔嚦唄員咼嗆嗚詠哢嚨嚀噝吒噅鹹呱響啞噠嘵嗶噦嘩噲嚌噥喲嘜嗊嘮啢嗩唕喚呼嘖嗇囀齧囉嘽嘯噴嘍嚳囁嗬噯噓嚶囑嚕劈囂謔團園囪圍圇國圖圓聖壙場阪壞塊堅壇壢壩塢墳墜壟壟壚壘墾坰堊墊埡墶壋塏堖塒塤堝墊垵塹墮壪牆壯聲殼壺壼處備複夠頭誇夾奪奩奐奮獎奧妝婦媽嫵嫗媯姍薑婁婭嬈嬌孌娛媧嫻嫿嬰嬋嬸媼嬡嬪嬙嬤孫學孿寧寶實寵審憲宮寬賓寢對尋導壽將爾塵堯尷屍盡層屭屜屆屬屢屨嶼歲豈嶇崗峴嶴嵐島嶺嶽崠巋嶨嶧峽嶢嶠崢巒嶗崍嶮嶄嶸嶔崳嶁脊巔鞏巰幣帥師幃帳簾幟帶幀幫幬幘幗冪襆幹並廣莊慶廬廡庫應廟龐廢廎廩開異棄張彌弳彎彈強歸當錄彠彥徹徑徠禦憶懺憂愾懷態慫憮慪悵愴憐總懟懌戀懇惡慟懨愷惻惱惲悅愨懸慳憫驚懼慘懲憊愜慚憚慣湣慍憤憒願懾憖怵懣懶懍戇戔戲戧戰戩戶紮撲扡執擴捫掃揚擾撫拋摶摳掄搶護報擔擬攏揀擁攔擰撥擇掛摯攣掗撾撻挾撓擋撟掙擠揮撏撈損撿換搗據撚擄摑擲撣摻摜摣攬撳攙擱摟攪攜攝攄擺搖擯攤攖撐攆擷擼攛擻攢敵斂數齋斕鬥斬斷無舊時曠暘曇晝曨顯晉曬曉曄暈暉暫曖劄術樸機殺雜權條來楊榪傑極構樅樞棗櫪梘棖槍楓梟櫃檸檉梔柵標棧櫛櫳棟櫨櫟欄樹棲樣欒棬椏橈楨檔榿橋樺檜槳樁夢檮棶檢欞槨櫝槧欏橢樓欖櫬櫚櫸檟檻檳櫧橫檣櫻櫫櫥櫓櫞簷檁歡歟歐殲歿殤殘殞殮殫殯毆毀轂畢斃氈毿氌氣氫氬氳彙漢汙湯洶遝溝沒灃漚瀝淪滄渢溈滬濔濘淚澩瀧瀘濼瀉潑澤涇潔灑窪浹淺漿澆湞溮濁測澮濟瀏滻渾滸濃潯濜塗湧濤澇淶漣潿渦溳渙滌潤澗漲澀澱淵淥漬瀆漸澠漁瀋滲溫遊灣濕潰濺漵漊潷滾滯灩灄滿瀅濾濫灤濱灘澦濫瀠瀟瀲濰潛瀦瀾瀨瀕灝滅燈靈災燦煬爐燉煒熗點煉熾爍爛烴燭煙煩燒燁燴燙燼熱煥燜燾煆糊溜愛爺牘犛牽犧犢強狀獷獁猶狽麅獮獰獨狹獅獪猙獄猻獫獵獼玀豬貓蝟獻獺璣璵瑒瑪瑋環現瑲璽瑉玨琺瓏璫琿璡璉瑣瓊瑤璦璿瓔瓚甕甌電畫暢佘疇癤療瘧癘瘍鬁瘡瘋皰屙癰痙癢瘂癆瘓癇癡癉瘮瘞瘺癟癱癮癭癩癬癲臒皚皺皸盞鹽監蓋盜盤瞘眥矓著睜睞瞼瞞矚矯磯礬礦碭碼磚硨硯碸礪礱礫礎硜矽碩硤磽磑礄確鹼礙磧磣堿镟滾禮禕禰禎禱禍稟祿禪離禿稈種積稱穢穠穭稅穌穩穡窮竊竅窯竄窩窺竇窶豎競篤筍筆筧箋籠籩築篳篩簹箏籌簽簡籙簀篋籜籮簞簫簣簍籃籬籪籟糴類秈糶糲粵糞糧糝餱緊縶糸糾紆紅紂纖紇約級紈纊紀紉緯紜紘純紕紗綱納紝縱綸紛紙紋紡紵紖紐紓線紺絏紱練組紳細織終縐絆紼絀紹繹經紿綁絨結絝繞絰絎繪給絢絳絡絕絞統綆綃絹繡綌綏絛繼綈績緒綾緓續綺緋綽緔緄繩維綿綬繃綢綯綹綣綜綻綰綠綴緇緙緗緘緬纜緹緲緝縕繢緦綞緞緶線緱縋緩締縷編緡緣縉縛縟縝縫縗縞纏縭縊縑繽縹縵縲纓縮繆繅纈繚繕繒韁繾繰繯繳纘罌網羅罰罷羆羈羥羨翹翽翬耮耬聳恥聶聾職聹聯聵聰肅腸膚膁腎腫脹脅膽勝朧腖臚脛膠脈膾髒臍腦膿臠腳脫腡臉臘醃膕齶膩靦膃騰臏臢輿艤艦艙艫艱豔艸藝節羋薌蕪蘆蓯葦藶莧萇蒼苧蘇檾蘋莖蘢蔦塋煢繭荊薦薘莢蕘蓽蕎薈薺蕩榮葷滎犖熒蕁藎蓀蔭蕒葒葤藥蒞蓧萊蓮蒔萵薟獲蕕瑩鶯蓴蘀蘿螢營縈蕭薩蔥蕆蕢蔣蔞藍薊蘺蕷鎣驀薔蘞藺藹蘄蘊藪槁蘚虜慮虛蟲虯蟣雖蝦蠆蝕蟻螞蠶蠔蜆蠱蠣蟶蠻蟄蛺蟯螄蠐蛻蝸蠟蠅蟈蟬蠍螻蠑螿蟎蠨釁銜補襯袞襖嫋褘襪襲襏裝襠褌褳襝褲襇褸襤繈襴見觀覎規覓視覘覽覺覬覡覿覥覦覯覲覷觴觸觶讋譽謄訁計訂訃認譏訐訌討讓訕訖訓議訊記訒講諱謳詎訝訥許訛論訩訟諷設訪訣證詁訶評詛識詗詐訴診詆謅詞詘詔詖譯詒誆誄試詿詩詰詼誠誅詵話誕詬詮詭詢詣諍該詳詫諢詡譸誡誣語誚誤誥誘誨誑說誦誒請諸諏諾讀諑誹課諉諛誰諗調諂諒諄誶談誼謀諶諜謊諫諧謔謁謂諤諭諼讒諮諳諺諦謎諞諝謨讜謖謝謠謗諡謙謐謹謾謫譾謬譚譖譙讕譜譎讞譴譫讖穀豶貝貞負貟貢財責賢敗賬貨質販貪貧貶購貯貫貳賤賁貰貼貴貺貸貿費賀貽賊贄賈賄貲賃賂贓資賅贐賕賑賚賒賦賭齎贖賞賜贔賙賡賠賧賴賵贅賻賺賽賾贗讚贇贈贍贏贛赬趙趕趨趲躉躍蹌蹠躒踐躂蹺蹕躚躋踴躊蹤躓躑躡蹣躕躥躪躦軀車軋軌軒軑軔轉軛輪軟轟軲軻轤軸軹軼軤軫轢軺輕軾載輊轎輈輇輅較輒輔輛輦輩輝輥輞輬輟輜輳輻輯轀輸轡轅轄輾轆轍轔辭辯辮邊遼達遷過邁運還這進遠違連遲邇逕跡適選遜遞邐邏遺遙鄧鄺鄔郵鄒鄴鄰鬱郤郟鄶鄭鄆酈鄖鄲醞醱醬釅釃釀釋裏钜鑒鑾鏨釓釔針釘釗釙釕釷釺釧釤鈒釩釣鍆釹鍚釵鈃鈣鈈鈦鈍鈔鍾鈉鋇鋼鈑鈐鑰欽鈞鎢鉤鈧鈁鈥鈄鈕鈀鈺錢鉦鉗鈷缽鈳鉕鈽鈸鉞鑽鉬鉭鉀鈿鈾鐵鉑鈴鑠鉛鉚鈰鉉鉈鉍鈹鐸鉶銬銠鉺銪鋏鋣鐃銍鐺銅鋁銱銦鎧鍘銖銑鋌銩銛鏵銓鉿銚鉻銘錚銫鉸銥鏟銃鐋銨銀銣鑄鐒鋪鋙錸鋱鏈鏗銷鎖鋰鋥鋤鍋鋯鋨鏽銼鋝鋒鋅鋶鐦鐧銳銻鋃鋟鋦錒錆鍺錯錨錡錁錕錩錫錮鑼錘錐錦鍁錈錇錟錠鍵鋸錳錙鍥鍈鍇鏘鍶鍔鍤鍬鍾鍛鎪鍠鍰鎄鍍鎂鏤鎡鏌鎮鎛鎘鑷鐫鎳鎿鎦鎬鎊鎰鎔鏢鏜鏍鏰鏞鏡鏑鏃鏇鏐鐔钁鐐鏷鑥鐓鑭鐠鑹鏹鐙鑊鐳鐶鐲鐮鐿鑔鑣鑞鑲長門閂閃閆閈閉問闖閏闈閑閎間閔閌悶閘鬧閨聞闥閩閭闓閥閣閡閫鬮閱閬闍閾閹閶鬩閿閽閻閼闡闌闃闠闊闋闔闐闒闕闞闤隊陽陰陣階際陸隴陳陘陝隉隕險隨隱隸雋難雛讎靂霧霽黴靄靚靜靨韃鞽韉韝韋韌韍韓韙韞韜韻頁頂頃頇項順須頊頑顧頓頎頒頌頏預顱領頗頸頡頰頲頜潁熲頦頤頻頮頹頷頴穎顆題顒顎顓顏額顳顢顛顙顥纇顫顬顰顴風颺颭颮颯颶颸颼颻飀飄飆飆飛饗饜飣饑飥餳飩餼飪飫飭飯飲餞飾飽飼飿飴餌饒餉餄餎餃餏餅餑餖餓餘餒餕餜餛餡館餷饋餶餿饞饁饃餺餾饈饉饅饊饌饢馬馭馱馴馳驅馹駁驢駔駛駟駙駒騶駐駝駑駕驛駘驍罵駰驕驊駱駭駢驫驪騁驗騂駸駿騏騎騍騅騌驌驂騙騭騤騷騖驁騮騫騸驃騾驄驏驟驥驦驤髏髖髕鬢魘魎魚魛魢魷魨魯魴魺鮁鮃鯰鱸鮋鮓鮒鮊鮑鱟鮍鮐鮭鮚鮳鮪鮞鮦鰂鮜鱠鱭鮫鮮鮺鯗鱘鯁鱺鰱鰹鯉鰣鰷鯀鯊鯇鮶鯽鯒鯖鯪鯕鯫鯡鯤鯧鯝鯢鯰鯛鯨鯵鯴鯔鱝鰈鰏鱨鯷鰮鰃鰓鱷鰍鰒鰉鰁鱂鯿鰠鼇鰭鰨鰥鰩鰟鰜鰳鰾鱈鱉鰻鰵鱅鰼鱖鱔鱗鱒鱯鱤鱧鱣鳥鳩雞鳶鳴鳲鷗鴉鶬鴇鴆鴣鶇鸕鴨鴞鴦鴒鴟鴝鴛鴬鴕鷥鷙鴯鴰鵂鴴鵃鴿鸞鴻鵐鵓鸝鵑鵠鵝鵒鷳鵜鵡鵲鶓鵪鶤鵯鵬鵮鶉鶊鵷鷫鶘鶡鶚鶻鶿鶥鶩鷊鷂鶲鶹鶺鷁鶼鶴鷖鸚鷓鷚鷯鷦鷲鷸鷺鸇鷹鸌鸏鸛鸘鹺麥麩黃黌黶黷黲黽'
   }
   function Traditionalized(cc) {
       let str = '';
       const ss = JTPYStr();
       const tt = FTPYStr();
       for (let i = 0; i < cc.length; i++) {
           if (cc.charCodeAt(i) > 10000 && ss.indexOf(cc.charAt(i)) !== -1) { str += tt.charAt(ss.indexOf(cc.charAt(i))) } else str += cc.charAt(i)
       };
       return str;
   }
   function Simplized(cc) {
       let str = '';
       const ss = JTPYStr();
       const tt = FTPYStr();
       for (let i = 0; i < cc.length; i++) {
           if (cc.charCodeAt(i) > 10000 && tt.indexOf(cc.charAt(i)) !== -1) { str += ss.charAt(tt.indexOf(cc.charAt(i))) } else str += cc.charAt(i)
       }
       return str;
   }
   function translateInitialization() {
       translateButtonObject = document.getElementById('menu-translate');
       if (translateButtonObject) {
           if (currentEncoding !== targetEncoding) {
               setTimeout(translateBody, translateDelay);
           }
           translateButtonObject.addEventListener('click', translatePage, false);
       }
   }
   $('#menu-backward').on('click', function () { window.history.back(); });
   $('#menu-forward').on('click', function () { window.history.forward(); });
   $('#menu-refresh').on('click', function () { window.location.reload(); });
   $('#menu-darkmode').on('click', function () { switchDarkMode() });
   $('#menu-home').on('click', function () { window.location.href = window.location.origin; });
   /* 简体繁体切换 */
   $('#menu-translate').on('click', function () {
       removeRightMenu();
       translateInitialization();
   });
   $(".menu-link").on("click", function () {
       removeRightMenu()
   });
   $("#rightmenu-mask").on("click", function () { removeRightMenu() });
   $("#rightmenu-mask").contextmenu(function () {
       removeRightMenu();
       return false;
   });
   
   ~~~

4. 在`BlogRoot/node_modules/hexo-theme-butterfly/source/css`文件夹下新建一个`rightMenu.css`，将以下代码复制到文件中

   ~~~bash
   #rightMenu {
       display: none;
       position: fixed;
       padding: 0 .25rem;
       width: 9rem;
       height: fit-content;
       top: 10%;
       left: 10%;
       background-color: rgba(238, 255, 255, .85);
       -webkit-backdrop-filter: blur(20px);
       backdrop-filter: blur(20px);
       color: #363636;
       border-radius: 12px;
       z-index: 99994;
       border: #e3e8f7;
       user-select: none;
       box-shadow: rgba(0, 0, 0, .05);
   }
   
   #rightMenu a {
       color: #363636;
   }
   
   #rightMenu .rightMenu-group {
       padding: .35rem .3rem;
       transition: .3s
   }
   
   #rightMenu .rightMenu-line {
       border-top: 1px dashed #4259ef23
   }
   
   #rightMenu .rightMenu-group.rightMenu-small {
       display: flex;
       justify-content: space-between
   }
   
   #rightMenu .rightMenu-group .rightMenu-item {
       border-radius: 8px;
       transition: .3s;
       cursor: pointer
   }
   
   #rightMenu .rightMenu-line .rightMenu-item {
       margin: .25rem 0;
       padding: .25rem 0
   }
   
   #rightMenu .rightMenu-group.rightMenu-line .rightMenu-item {
       display: flex
   }
   
   #rightMenu .rightMenu-group .rightMenu-item:hover {
       background-color: #6f42c1;
       color: #fff;
   }
   
   #rightMenu .rightMenu-group .rightMenu-item:active {
       transform: scale(.97)
   }
   
   #rightMenu .rightMenu-group .rightMenu-item i {
       display: inline-block;
       text-align: center;
       line-height: 1.5rem;
       width: 1.5rem;
       padding: 0 .25rem
   }
   
   #rightMenu .rightMenu-line .rightMenu-item i {
       margin: 0 .25rem
   }
   
   #rightMenu .rightMenu-group .rightMenu-item span {
       line-height: 1.5rem
   }
   
   .rightMenu-small .rightMenu-item {
       width: 30px;
       height: 30px;
       line-height: 30px
   }
   
   #rightmenu-mask {
       position: fixed;
       width: 100vw;
       height: 100vh;
       background: 0 0;
       top: 0;
       left: 0;
       display: none;
       z-index: 101;
       margin: 0 !important;
       z-index: 99993
   }
   ~~~

5. 在主题配置文件`_config.butterfly.yml`中引入`rightMenu.js`和`rightMenu.css`。



