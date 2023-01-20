

> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



hexo官网：https://hexo.io/zh-cn/

butterfly 主题设置：https://butterfly.js.org/

GitHub地址：https://github.com/jerryc127/hexo-theme-butterfly

其他博主的教程：

- [唐志远博主](https://tzy1997.com/)
- [糖果屋](https://akilar.top/)

# 基础命令

- 初始化博客命令：hexo init "文件名"
- 开启本地服务（本地运行）的命令：hexo s 
- 生成页面（生成博客）： hexo g
- 创建文章（md形式）：hexo n "文章名字"
- 清理缓存：hexo clean
- 依赖安装：npm install
- 新建文章：hexo n "文章名"



发布顺序

1. 先清理缓存：hexo clean
2. 再重新生成博客页面：hexo g
3. 预览：hexo serve
4. 上传到GitHub创库：hexo d 





# Hexo+Github搭建个人博客

## 前言

* 完全免费的搭建个人博客，没有任何收费，零基础小白也能上手，不需要编程基础，跟着操作来即可。

  

* 首先要了解一下我们搭建博客要用到的框架。Hexo是高效的静态站点生成框架，它基于Node.js。通过Hexo，你可以直接使用Markdown语法来撰写博客。相信很多小伙伴写工程都写过README.md文件吧，对，就是这个格式的！写完后只需两三条命令即可将生成的网页上传到你的github上，然后别人就可以看到你的网页啦。是不是很简单？你无需关心网页源代码的具体细节，你只需要用心写好你的博客内容就行。

  

## Hexo环境准备

*  【2021版本】保姆级Hexo+Github搭建个人博客步骤      

​			单纯搭建发布视频讲解地址：https://www.bilibili.com/video/BV1mU4y1j72n?t=2.5&vd_source=71e92a1364cbcaf80125baa05f89bc60	 
​			详细视频讲解：https://www.bilibili.com/video/BV1oU4y1n7hn/?spm_id_from=pageDriver&vd_source=91c74d407fc476374430aea2a76f7aca				

### Node.js安装

 			https://www.cnblogs.com/liuqiyun/p/8133904.html



### Git安装

* 安装步骤参考以下步骤

  ​	https://www.cnblogs.com/xueweisuoyong/p/11914045.html


### Vscode安装

* 后面涉及到代码的修改，建议大家使用 Vscode 软件 

  * 安装链接：  「VSCodeUserSetup-x64-1.65.0.exe」 https://pan.quark.cn/s/f64b7413660c       提取码：7eMQ

    

  * 本文软件需要用到的操作说明：

    * 打开终端，本文用到的命令都是在终端里面输入命令+回车的
    * ctrl + f   查找内容的快捷键，因为配置文件的代码太多了，需要用到这个快捷键，然后在搜索框输入要搜索的内容，就能实现快速查找

### Typroa 

- 用于写文章
- [Markdown介绍](https://blog.csdn.net/u014061630/article/details/81359144?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166105644016782395369722%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=166105644016782395369722&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-2-81359144-null-null.142^v42^pc_rank_34,185^v2^control&utm_term=markdown%E8%AF%AD%E6%B3%95&spm=1018.2226.3001.4187) 





### Github

* github访问加速

​    「fastgithub_win版-x64.zip」		链接：https://pan.quark.cn/s/4c170f5763d2 						提取码：sFNj

​		其余版本建议访问：	https://github.com/dotnetcore/FastGithub	

* 注册Github账号

​       接下来就去注册一个github账号，用来存放我们的网站，注册、使用教程 CSDN自己搜，这里就不提供了

* 搭建仓库

​       打开https://github.com/，新建一个项目，如下所示：

​	![image-20220816161920867](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220816161920867.png)



* 然后如下图所示，输入自己的项目名字，后面一定要加`.github.io`后缀，README初始化可选可不选。**名称一定要和你的github名字完全一样，比如你github名字叫`abc`，那么仓库名字一定要是`abc.github.io`。**	最后选择Create 创建，项目就建成功了

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801225841175.png" alt="image-20220801225841175" style="zoom:67%;" />



## Hexo搭建

一定要保证前面的步骤成功后，在执行该章节后面的步骤



### 安装Hexo

* 在你的电脑上任意位置，新建一个文件夹，用来存放自己的博客文件，比如我的博客存放位置`D:\boke\blog`目录下。

* 在该根目录下，鼠标右击，选择`Git Bash Here`，打开git的控制台窗口，输入`npm i hexo-cli -g`安装Hexo。会有几个报错，无视它就行。

* 安装完成后，验证是否安装成功，该窗口输入`hexo -v`验证是否安装成功。

  

### 生成ssh keys

* 在任意文件夹位置，鼠标右击，选择`Git Bash Here`，输入 ssh 检查有没有安装ssh

*  生成ssh命令：  

   ~~~
   ssh-keygen -t rsa -C "2927527234@qq.com"  
   ~~~

*  总共需要敲四次回车。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/88fe196d4b93872edf40766575f35af3.png" alt="img" style="zoom:67%;" />

* 找到  id_rsa.pub 文件，并打开复制里面所有的代码，大致路径： c盘----->用户------>管理员名称-------->.ssh文件夹下

​	或者

* git bash中输入`cat ~/.ssh/id_rsa.pub`下命令，将输出的内容复制到框中，点击确定保存。



* 打开github，在头像下面点击`settings`，在新出的导航栏，找到 ssh，点击后，在新的页面点击 ssh keys 的新建钥匙，新建钥匙的  title（名称）随意起名，如：blog，将 id_rsa.pub 文件复制的公钥，粘贴到 key 里面，保存。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802152610379.png" alt="image-20220802152610379" style="zoom:67%;" />





* 测试ssh是否绑定成功命令： 	ssh -T git@github.com

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801231554912.png" alt="image-20220801231554912" style="zoom: 80%;" />



### 本地博客生成

* 初始化博客命令：hexo init

![image-20220801212856707](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801212856707.png)



* 开启本地服务的命令：hexo s 

![image-20220801212953228](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801212953228.png)

* 然后浏览器打开http://localhost:4000/，就可以看到我们的博客啦，按`ctrl+c`关闭本地服务器。
* 具体效果如下：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801234836437.png" alt="image-20220801234836437" style="zoom:67%;" />



## 发布博客到互联网

**建议先将网站美化了，然后在用此步骤发布到互联网上**

* 修改-config.yml文件

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/76aa4fb226389c10209b17cd97f1b7d8.png" alt="img" style="zoom:67%;" />

* 将改配置文件最后的 deploy  部分完善，type和 branch 是固定不变的，repository修改为你的 github 地址 ，  ==注意：注意网址前面，冒号后面有一个空格==    

```
deploy:
  type: 'git'
  repository: '刚刚新建的GitHub仓库地址，完整地址复制到这里'
  branch: main
```

* 你的github地址：在github找到你之前新建的仓库，然后找到仓库地址，复制仓库地址，将我的地址替换为你的即可。

​		<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802145731910.png" alt="image-20220802145731910" style="zoom:67%;" />

* 修改好配置文件后，在你的博客文件夹下git bash，将本地文件上传到github里面，根据以下命令，一步一步的走即可：


​			安装 `hexo-deployer-git` 自动部署发布工具： `npm install hexo-deployer-git --save`

​			![img](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/a94aa787c8627d7bc2d95fc3aabe211d.png)



* 生成页面： `hexo g` 

​			<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802145929980.png" alt="image-20220802145929980" style="zoom:80%;" />

* 然后输入下面命令，用户名和邮箱根据你注册github的信息自行修改。			

```bash
git config --global user.name "kongshier"
git config --global user.email "2927527234@qq.com"
```

* 本地文件上传到Github上面：`hexo d`
  * 如果出现这个界面关掉即可

​			<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802183045420.png" alt="image-20220802183045420" style="zoom: 67%;" />

* 然后会出现一个登录界面，输入 GitHub 账号，千万别输错了，要不然有得重来

​		<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802183241566.png" alt="image-20220802183241566" style="zoom: 67%;" />

* 到下面输入密码这一步，先暂缓一下，先创建一个令牌，然后将创建的令牌复制粘贴进去就行【记住不要输入密码，需要将你的令牌输入进去，而不是密码】

​		<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802183347638.png" alt="image-20220802183347638" style="zoom:67%;" />

* 设置令牌步骤：

​			setting--------->developer settings（开发者设置）---------> 后续步骤按照下方图片操作

![image-20220802114624730](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802114624730.png)

* 然后新建令牌，有效期30天，为令牌赋权限，建议把所有选项都选上，然后生成令牌

![image-20220802114843927](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802114843927.png)

* 将生成的令牌输入到密码那个对话框，一定要将这个令牌，拍照等方式保存好，后面在去找这个令牌它就不显示了 

![image-20220802115012539](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802115012539.png)

* 上传到github后，就可以用仓库名称访问你的网址

  



## hexo 博客版本控制（git版本控制）

在有的时候代码可能会丢失，代码有些错误，这种时候我们可以通过版本控制，来回退我们的版本，从而保证我们的代码不会丢失。	

如果没有git基础的有些地方不理解的，可以先去看下git 几十分钟搞定，当然按照我的步骤一步一步来，没有任何问题！！！

* 打开github 新建一个仓库，新建完成后不要关掉这个界面

​		![image-20220803100423813](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803100423813.png)

* 新建文件 .gitignore，这个文件的作用就是帮我们过滤掉不需上传到仓库的文件,注意文件位置：根目录下

* 代码内容如下：

  ```
  .DS_Store
  Thumbs.db
  db.json
  *.log
  node_modules/
  public/
  .deploy*/
  .vscode/
  /.idea/
  .deploy_git*/
  .idea
  themes/butterfly/.git
  ```

* 终端输入，生成仓库命令  ： git init

  

* 建好仓库后，将仓库推送到远程上面去

  在建立github仓库时，有怎么推送到仓库的说明，只需要将代码按照说明步骤一步一步复制，终端输入即可

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803101940561.png" alt="image-20220803101940561" style="zoom:67%;" />

* 重要代码说明，其余没有强调的按照文档说明复制就行

## 上传 GitHub

### 把本地的上传到 GitHub 仓库

```git
git init
git add .
git commit -m "注解"
git branch -M main
git remote rm origin  # 首次不用执行这个
git remote add origin https://github.com/kongshier/Myblog.git
git push -u origin main
```

```
git add .													 将代码提交到暂存区
git commit -m "feat：初始化仓库"			提交到本地
```

如果你clone下来一个别人的仓库，在此基础上完成你的代码，推送到自己的仓库可能遇到如下问题：
error: remote origin already exists.表示远程仓库已存在。
因此你要进行以下操作：
1、先输入git remote rm origin 删除关联的origin的远程库
2、关联自己的仓库 git remote add origin https://github.com/kongshier/blog.git
3、最后git push origin master，这样就推送到自己的仓库了。



* 当你仓库有内容时完成将代码推送到远程分支上面，后面就算你更换设备，都可以将代码从远程克隆下来

* 克隆步骤

  ```
  git clone 仓库地址
  切换到你下载好的文件目录
  npm install												这是安装依赖
  ```


### 拉取远程仓库

```git
git clone <repositories>  # 拉取默认分支

git clone -b <branch> <repositories> 拉取远程仓库中指定的分支
```

以HTTPS方式拉取  一般都是这个克隆

![image-20220820123326690](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220820123326690.png)

~~~
git clone https://github.com/kongshier/blog.git
~~~

以SSH方式拉取仓库

~~~
git clone 《git@gitee.com:holyking/test-2.git 这个是需要拉取仓库的SSH》
~~~

#### 下载到本地后执行以下

- 安装依赖：npm install

- 再重新生成博客页面：hexo g
- 预览：hexo serve
- 上传到GitHub创库：hexo d 



## 博客文件夹的介绍

![image-20220802180850120](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802180850120.png)

- `_config.yml`：俗称站点配置文件，很多与博客网站的格式、内容相关的设置都需要在里面改。

- `node_modules`:存储Hexo插件的文件，可以实现各种扩展功能。一般不需要管。

- `package.json`：别问我，我也不知道干嘛的。

- `scaffolds`：模板文件夹，里面的`post.md`文件可以设置每一篇博客的模板。具体用起来就知道能干嘛了。

- `source`：非常重要。所有的个人文件都在里面！

- `themes`：主题文件夹，可以从[Hexo主题官网](https://hexo.io/themes/)或者网上大神的Github主页下载各种各样美观的主题，让自己的网站变得逼格高端的关键！

  

接下来重点介绍`source`文件夹。新建的博客中，`source`文件夹下默认只有一个子文件夹——`_posts`。我们写的博客都放在这个子文件夹里面。我们还可以在`source`里面新建各种子文件夹满足自己的个性化需求，对初学者而言，我们先把精力放在主线任务上，然后再来搞这些细节。



* _config.yml 文件详解

  * 严格注意缩进，缩进不对也会报错，所以这里不推荐使用记事本，使用 Vscode 编辑器

    

  * title部分：

    ​					![image-20220802204126485](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802204126485.png)

    

  * url ：只用配置第一行，其余的都不用动，更换为你的远程地址就可以了

    <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802204305728.png" alt="image-20220802204305728" style="zoom: 67%;" />

  

  * 文件夹的设置，这些东西都不用管，默认即可

    ![image-20220802204452588](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802204452588.png)

  * 首页的设置，用默认的就好了

    ![image-20220802204604046](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802204604046.png)

  * 预设的分类，uncategorized 意思是未分类，先不用管用默认的就好

    ![image-20220802204643225](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802204643225.png)

  * 日期的显示格式：用默认的就好了

    ![image-20220802204804934](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802204804934.png)

  * 分页的设置：默认是一页10行数据，数据修改随意

​						![image-20220802204853131](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802204853131.png)





## 网址的美化

* 下面的这个个性化设置主要针对的是`matery`主题

​		主题的原地址在这里：[hexo-theme-matery](https://github.com/blinkfox/hexo-theme-matery)，它的文档写得也非常的详细，还有中英文两个版本，按照文档教程安装一遍主题，然后是可以正常打开的，如果你是一般使用的话，基本没啥问题了。



* butterfly官方主题配置教程

  https://butterfly.js.org/posts/21cfbf15/

  Ps：根据帮助文档，一步一步来即可，两个主题选择一个配置安装即可，原理相同
  
  ​		我这里选择的是	butterfly，butterfly官方文档地址： https://butterfly.js.org/posts/21cfbf15



## butterfly主题安装详细步骤

PS：

* 使用vscode软件进行文件的修改，直接将整个文件拖进该软件即可
* 这后面的章节其实就是带大家看帮助文档，然后一些 bug 的处理，建议大家看不懂文档的结合我这篇文章理解



### butterfly的安装

* 使用npm 的方式，在vscode终端安装

* ~~~
  npm update hexo-theme-butterfly  # 更新主题
  ~~~

![image-20220816174000370](Hexo+Github搭建个人博客教程.assets/image-20220816174000370.png)

* 修改配置文件

  ![image-20220802195512536](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802195512536.png)



* 在终端 清理缓存 hexo clean，然后我这里报错了 

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802200625850.png" alt="image-20220802200625850" style="zoom:67%;" />

​		解决办法：

​			在自己对应的”nodejs“文件夹下的“node_global" 下找到对应的“指令名.ps1"删除掉，然后再运行对应的指令即可



* hexo s 运行，将网址在浏览器粘贴，最终效果如下

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802201740296.png" alt="image-20220802201740296" style="zoom:67%;" />

​												<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220802201848536.png" alt="image-20220802201848536" style="zoom: 50%;" />

​											

2. 其余的主题的安装方式和这一样，不管安装什么都要先看帮助文档。然后记得用 `hexo clean` 清理缓存后在运行


### 更多主题

1、fluid ：https://github.com/fluid-dev/hexo-theme-fluid

2、Volantis：https://github.com/volantis-x/hexo-theme-volantis

3、next ：https://github.com/iissnan/hexo-theme-next/

4、nexmoe：https://github.com/theme-nexmoe/hexo-theme-nexmoe

5、butterfly：https://github.com/jerryc127/hexo-theme-butterfly

6、bamboo：https://github.com/yuang01/hexo-theme-bamboo



### 主题页面

说明：

* 这一部分和上一部分没什么区别，就是看帮助文档，然后输入对应的命令，如果没有强调的话，就按照帮助文档的命令敲就行，重要的地方会阐明以下！！！

  

* **后面的内容就是看帮助文档，一定要按照帮助文档划分的步骤来，就比如说主页配置，等这一项弄完了然后在弄下一项，后面章节我会挑重要的部分说一下**

  

* 鉴于每个人的根目录名称都不一样，本帖**博客根目录**一律以 `[Blog]` 指代。

  

* 请读者优先掌握 [Butterfly 主题官方文档](https://butterfly.js.org/) 的内容后再来进行魔改。以避免不必要的兼容性问题。



#### 主页基本信息修改

1. 先将主页的基本信息进行完善，就是 包含 title 的部分，前面已经详细说过，这里就不详细讲述了

   ![image-20220803074857161](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803074857161.png)

​	

### 博客关键页面生成

博客有一些关键页面需要手动生成。

##### 标签页

进入 Hexo 博客的根目录，执行：

```
hexo new page tags
```

打开 `source/tags/index.md` 文件，修改如下：

```
---
title: 标签
date: 2022-08-03 12:53:45
type: "tags"
---
```

##### 分类页

进入 Hexo 博客的根目录，执行：

```
hexo new page categories
```

打开 `source/categories/index.md 文件`，修改如下：

```
---
title: 分类
date: 2022-03-11 12:56:06
type: "categories"
---
```

##### 友情链接

##### 创建友情链接页面

进入 Hexo 博客的根目录，执行：

```
hexo new page link
```



打开 `source/link/index.md` 文件，修改如下：

```
---
title: 友情链接
date: 2022-03-11 12:57:48
type: "link"
---
```

##### 友情链接添加

在Hexo博客目录中的 `source/friends/创建一个文件 `lndex.md`

![image-20220804182129527](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804182129527.png)

```
---
title: friends
date: 2022-08-03 08:18:23
type: "friends"
layout: "friends"
---

# 友链交换
想要交换友链的小伙伴，欢迎在留言板留言，留言格式：
* **名称：**你的博客名称
* **地址：**你的博客地址
* **简介：**一句话简介
* **头像：**你的头像地址

例如我的博客友链，大家可以加到自己博客里哦：
* **名称：**十二
* **地址：**https://kongshier.github.io/
* **简介：**无处不在
* **头像：**头像地址
```

* 预览效果如下，就表示成功了，然后直接跳到帮助文档的404页面

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803090849053.png" alt="image-20220803090849053" style="zoom:50%;" />



##### 关于我

进入 Hexo 博客的根目录，执行：

```
hexo new page about
```


打开 `source/about-me/index.md` 文件，修改如下：

```
---
title: 关于作者
date: 2022-03-11 13:01:21
type: "about"
---
```

* 说明：

​				重点：**所有的文件都在source，这个文件夹下**，按照官方文档提示，修改文件即可！

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803075725093.png" alt="image-20220803075725093" style="zoom:50%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803080209008.png" alt="image-20220803080209008" style="zoom:50%;" />

* 修改完成后，通过路由本地预览一下好了没，要养成习惯，完成一步，预览一步！！！！

​						路由格式：http://localhost:4000/ tags                             

​						tags 其实就是对应的你要实现功能的名称，需要预览什么 功能，就修改成对应的功能名称

* 预览效果如下，就表示成功了，然后直接跳到帮助文档的404页面

  





#### 404 页面添加

* 找到：node_modules------------>hexo-theme-butterfly------------>_config.yml

* 将文件里面的内容全部复制，执行图下面的操作，然后将所有代码粘贴到新建的文件里，这个文件就是我们主题配置的文件![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803094322872.png)

* 找到error 404 ，将帮助内容置换即可

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803094913962.png" style="zoom:67%;" />



#### 主页背景更改

方式一：

更改其图标、主页背景等部分内容，在主题的配置文件下

* 更改背景的话建议使用占位图（就是将本地图片上传到图床）

  ![image-20220804164957434](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804164957434.png)

  

* 更改主页 主题背景的时候，如果要使用本地图片记得创建文件夹 img ，将图片放进此文文件，复制其路径，粘贴到对应位置，然后在注意一下本地图片的格式即可， .表示当前路径

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804144408584.png" alt="image-20220804144408584" style="zoom:67%;" />



* 留意: 如果你的网站根目录不是`/`,使用本地图片时，需加上你的根目录。
  例如：网站是`https://yoursite.com/blog`,引用一张`img/xx.png`图片，则设置`background`为 `url(/blog/img/xx.png)`

  
  
  方式二（通过数据文件的方式）：
  
  ​	在 source/_data/style.styl 文件中添加：（如果没有这个路径的话添加即可）
  
  ```
  // 背景
  body {
    background-image:url(../images/bg.webp);
    height:100%;
    width:100%;
    background-repeat:repeat-x;
    background-attachment:fixed;
    background-size:cover;
  }
  
  //设置透明度
  //侧边框的透明度设置
  .sidebar-inner {
    background: rgba(255,255,255,0.8);
  }
  
  //菜单栏的透明度设置
  .header-inner {
    background: rgba(255,255,255,0.8);
  }
  
  //搜索框（local-search）的透明度设置
  .popup {
    opacity: 0.8;
  }
  
  ```
  
  background-image 就是你的背景图啦。
  
  

### 主题配置（一）	

前面章节带大家看了一下文档，当然官方文档还有很多，这里就不罗列了，希望大家掌握方法，仔细阅读文档，重要的我会在这强调



这里只强调几点：

* 官方文档，可能格式没有设置，需要自己调整一下缩进

  

* 每新增一个功能最好本地预览下，成功了在执行后面的

  

* 为了以后大家配置方便，最好配置一下package.json

  ```
  "server": "hexo clean && hexo generate && hexo server"
  修改第九行，这行代码可以省去每次都要清理，然后生成静态页面，这个步骤，
  然后每次运行的时候也可以不用去输入命令行，可以找到这行代码然后点击 server 运行即可
  ```



* 都开始主题配置了，大多数修改的文件都是_ config.butterfly.yml 这个文件

  

#### 导航栏的说明：

* 注意：

  * 圆圈是你要在 source 文件夹下建立的文件夹，名称相同，然后在新建的文件夹下，新建index.md 文件

    

  * 方框的内容是自己随意更改的

    

  * 注意一下文档的缩进

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804151047939.png" alt="image-20220804151047939" style="zoom:67%;" />

* 详解：

  * 分类                             是指标签栏的名称
  * /  内容  /                       是指路径，source文件夹下----->categories文件夹下----->i ndex.md 文件【自动去匹配】
  * fas fa-home                是图标

  ​			![](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220804151824283.png)

  

* 导航栏的修改（注意二级的格式）

  ```
  menu:
    主页: / || fas fa-home
    时间线: /archives/ || fas fa-archive
    标签: /tags/ || fas fa-tags
    分类: /categories/ || fas fa-folder-open
    链接||fas fa-list:
      友链: /link/ || fas fa-link
      关于: /about/ || fas fa-heart
  ```



#### 顶部图



#### 字数统计

```
BASH
cnpm install hexo-wordcount --save
```

修改主题配置文件：

```
YMLwordcount:
  enable: true
  post_wordcount: true
  min2read: true
  total_wordcount: true
```

如需调整右侧卡片网站信息内项目的数据，在文件`/butterfly/layout/includes/widgets/card_webinfo.pug`中操作。

#### 目录折叠

由于我个人的目录比较大，完全展开三级目录的话，右边栏就完全被目录铺满了。`butterfly`主题提供了目录可折叠的选项，只需要在主题配置文件`/butterfly/config.yml`设置：

```yml
card_categories: 
  enable: true
  limit: 0 # if set 0 will show all
  expand: true # none/true/false
  sort_order: # Don't modify the setting unless you know how it works
```



### 主题配置（二）

重点看下我提的内容，其余想加的可以自己看下文档，然后添加上即可



* 评论系统 （我目前使用来必力，但是我觉得没必要，为了给你们演示下，后期应该会关掉，毕竟也没多少人看我的文章）

  

* 搜索系统

  * 直接点 本地搜素 ------> hexo-algoliasearch  然后看帮助文档，按照文档步骤一步一步操作即可

    * 打开终端 使用命令：`npm install hexo-algoliasearch --save`，安装需要的插件

    * 项目的根目录 _config.yml 配置文件下，将如下我修改过的代码复制到文件末尾（官方给的那个有 坑 ）。

      ```
      search:
        path: search.xml
        field: post
        format: html
        limit: 10000
      ```

    * 看下 _config.butterfly.yml 文件的 local_search 有没有打开，打开了就预览一下效果,有搜索框了就欧克了！！

​										<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803160405455.png" alt="image-20220803160405455" style="zoom:67%;" />

​								

* 页面美化

  * 根据官方文档和我修改的beautifly，在结合你的喜好，修改一下就好了

    ```
    beautify:
      enable: true
      field: post # site/post
      title-prefix-icon: # '\f0c1'
      title-prefix-icon-color: # '#F47466'
    ```

* 网站的副标题，根据自己的喜好调试即可，附上我的样式

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803164034567.png" alt="image-20220803164034567" style="zoom:67%;" />

  

*  设置主页面高度，根据自己的喜好设置即可

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803165153927.png" alt="image-20220803165153927" style="zoom:67%;" />



* 字数统计

  ​	根据文档自己设置一下

  

* prefetch (預加載)、pangu、pjax，将这些服务开启。（false改为true即可）



### 进阶文档

PS:

* 这部分根据自己喜好，看官方文档配置即可
* 魔改官方主题的尽头其实就是默认就好哈哈



* gulp压缩 【 **这一部分 官方文档移除了  不用作用也不大** 】

  随着网站的发展，你的文件会越来越多，安装这个插件，可以压缩代码，从而实现代码部分的优化,根据我的步骤一步一步操作即可

  配置了淘宝的镜像源所以使用 cnpm 
  
  ~~~bash
  npm install -g cnpm --registry=https://registry.npm.taobao.org
  ~~~
  
  
  
  
  
  ```
  安装gulp的cli：
  cnpm install --global gulp-cli
  	
  安装gulp本身工具：
  cnpm install gulp -g
  
  cnpm install gulp-htmlclean --save-dev
  
  cnpm install --save gulp-html-minifier-terser
  
  cnpm install gulp-clean-css --save-dev
  
  cnpm install --save-dev gulp-uglify
  
  cnpm install --save-dev gulp-babel @babel/core @babel/preset-env
  
  cnpm install --save-dev gulp-imagemin
  ```
  
  在根目录下，创建文件 gulpfile.js 文件（ 后面等我学习下在更，没有这块内容也没影响）
  
  

### 	添加来必力评论系统

​	我选择这个系统，是因为这个系统能过滤一些不友好的评论，当然也可以选择其它的，自己根据帮助文档配置下

​	喜欢折腾，美观的就不建议这个评论系统了，建议 Twikoo



* 在主题配置文件找到 comments

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803173343335.png" alt="image-20220803173343335" style="zoom:67%;" />

* 注册来必力，然后登录，然后右上角管理页面，输入必要的信息，最后出现以下的界面，将对应的uid 输入配置文件即可

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803174708485.png" alt="image-20220803174708485" style="zoom:67%;" />

​			

​			<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803174840722.png" alt="image-20220803174840722" style="zoom:67%;" />

​		粘贴的时候注意格式，只粘贴引号里面的内容，还有冒号后面有一个空格



* 在来必力系统进行一些必要的设置，比如：评论邮件提醒，选择登录方式等等

  

* 最后本地运行，随便找一篇文章，看效果即可

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803175530564.png" alt="image-20220803175530564" style="zoom:67%;" />



### 插入代码自定义样式

* 自定义代码的拆入方法

  * 先找到 主题配置文件的  inject 

    一般样式文件会放到 head 里面 ，js文件放在 bottom 里面

  * 新建文件夹，按照箭头位置创建即可，名称随意

    <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803180720134.png" alt="image-20220803180720134" style="zoom:67%;" />

  * 将新建的文件夹，引入到 inject 里面即可，然后运行项目即可

    <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803181203355.png" alt="image-20220803181203355" style="zoom:67%;" />

  

* 底部的样式修改（掌握方法后，直接去网上找一些别人改好的样式，复制粘贴即可）

  方法：直接F12然后找到你要修改的标签id，然后返回刚才那个建好的css文件，在里面添加css代码，修改对应的样式即可

  比如修改底部样式为透明

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803181853683.png" alt="image-20220803181853683" style="zoom:67%;" />



![image-20220803182602841](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803182602841.png)



* 底部添加多个内容信息，并且点击跳转的说明：（有需要的自行了解一下）

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803184455538.png" alt="image-20220803184455538" style="zoom:67%;" />

​	效果：

​		<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220803184107209.png" alt="image-20220803184107209" style="zoom:67%;" />



## 博客添加文章

* 首先在博客根目录下右键打开git bash，安装一个扩展`npm i hexo-deployer-git`。

  

* 然后输入 hexo new post "article title" ，新建一篇文章。

  

* 然后打开`D:blog\source\_posts`的目录，可以发现下面多了一个文件夹和一个`.md`文件，一个用来存放你的图片等数据，另一个就是你的文章文件啦。

  

* 编写完markdown文件后，根目录下输入`hexo g`生成静态网页，然后输入`hexo s`可以本地预览效果，最后输入`hexo d`上传到github上。这时打开你的github.io主页就能看到发布的文章啦。

  ```
  hexo clean
  hexo g
  hexo s
  hexo d
  ```

  ​		

## 问题汇总

​	这是我在操作过程中遇见的一些bug ，在这里汇总一下



1. 安装Hexo时遇见的报错

   ![image-20220801193727750](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/1024/image-20220801193727750.png)

​	解决办法：

​			重新配置了下npm安装的全局模块所在的路径，以及缓存cache的路径，又检查了一下环境变量是否正确

设置全局模块命令：

```
npm config set prefix "D:\node\node_global"
```

设置cache模块命令

```
npm config set cache "D:\node\node_cache"
```



2. 上传到GitHub碰到 “ Deployer not found ”  问题

​		解决办法：重新 deploy 即可。

```
npm install hexo-deployer-git --save
```

然后  hexo d  就能提交成功



#### 总结

按照步骤本教程一个基本的网页就搭建出来了，后面就是对网页的美化和优化，如果想简洁一点的话直接看 hexo框架-文章篇 即可
