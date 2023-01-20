> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

## 基础命令

ctrl + C  退出状态

**pwd  查看当前处于的文件位置**



### cd 切换文件夹

- cd /home 绝对路径 以根目录开头

- cd kcs 相对路径  不以根目录开头

- cd .. 返回到上级目录

- cd ~ 回到自己根目录  /home/kcs

- cd - 回看目录





### ls 查看当前文件夹的内容

- ls -a ：显示所有文件 包括隐藏文件 . xxx

- ls -l ：显示详细列表信息

- ls -lh ：把文件大小单位为   **k**

- ls - lah ：人性化大小显示结果

- ll  = ls -l 

- ls  目录  ：查看指定目录表下的内容

- ls  *xx :查看以xx结尾的文件    * 通配符

### ls 详细解读

- d rwx rwx r-x	d 代表文件夹	– 代表文件
- rwx rwx r-x    r 可读     w 可写     x 执行
- 第一组指文件的拥有者的权限，第二组代表文件拥有的组的权限，第三组代表其他用户的权限



### mkdir 创建文件夹

- mkdir 文件夹名    ：相对路径创建文件夹 当前目录下创建文件夹

- mkdir  /home/kcs/文件夹名     ：绝对路径创建文件夹  **文件名 之前的都文件必须存在**

- mkdir  -p  /home/kcs/文件夹名  ：若上级目录不存在就先创建父目录，在创建文件  **-p：表示创建多级目录**

- mkdir  上一级文件夹/{文件夹1，文件夹2}，则创建的文件的就会在上一级的文件夹下面，括号里面的文件夹处于同一级别

- mkdir . 文件夹名  ：创建文件夹名

- madir a b 当前目录下创建多个文件夹



### touch 创建空文件

- touch a.txt  ：创建一个txt文件 空文件

- touch a  b  c  ： 创建多个文件 

- touch  .abc  创建隐藏文件



- ### gedit 使用记事本打开文件

- **gedit a.txt**  ： **打开文件**

- gedit test.txt   ：创建并打开文件 



### rm删除文件

- rm 文件名 ：删除单个文件

- rm a b c ：删除多个文件

- rm a -r ： 删除a文件夹 -r ：递归删除所有文件夹里面的所有文件

- rm *  ： 删除当前文件夹下的文件  不包括隐藏文件

- rm * -r ： 删除所有文件夹和文件 但不包括隐藏文件
- rm -rf ：强制删除并且不提示信息







### clear 清屏





### 自动补全

> 输入首个字母 按tab 就会自动补全
>
> 上下滚轮，查看历史命令



### cp 拷贝

- cp  1.txt  b   ：  把 1.txt文件复制到 b目录下  

- **cp 源文件  目标文件  ：把源文件内容  复制到目标文件中 ，若目标文件不存在 ，则会创建目标文件**

- cp  1.txt  2.txt  - a ：把源文件所有的属性复制过来

- **cp  a  a_bak -r :  拷贝文件夹 需要加 -r** ：表示递归复制整个文件夹
- cp  1.txt  2.txt -i ： - i 是否覆盖2.txt文件
- \cp ：强制覆盖并且不提示



### mv：移动、重命名

- mv  a.txt  a1.txt  : 把a文件  移动并重命名成a1 
- mv  a.txt  ~/a1.txt  :移动到指定 (~) 目录 
- mv  a1  a2  ：把a1文件夹 重命名 为 a2  直接覆盖a2







### >：重定向 ，>> ：追加

把命令返回的结果输出到文件中

- ls > 1.txt  ： 就是把当前的ls内容存放在1.txt文件中  ； >  是直接覆盖； 

- ls >> 1.txt  ：>> 追加  不覆盖
- cal >>2.txt ：把当前的日期信息追加到2.txt里面



### cat 显示文件内容

- cat  1.txt  ：查看1.txt里面的内容

- cat  1.txt  2.txt  ：	显示1.txt  2.txt 文件内容  在屏幕上

- cat  1.txt  2.txt  >3.txt  :	1.txt  2.txt 文件内容 合并到 3.txt文件里面
- cat 文件名 -n ：-n 表示显示行号



### more  查看一般大文件

- 一个屏幕显示不完

- 按b ：返回翻页 ()

- 按空格 ：向下翻页

- 按enter：向下翻页一行

- 按q键 ：退出
- Ctrl + F：向下滚动一屏
- Ctrl + B：返回上一屏
- = ：输出当前行号
- :f ：输出文件名和当前行好

### less 分屏查看更大文件内容

~~~
less 要查看的文件
~~~



![image-20220715211537042](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220715211537042.png)





### echo 输出内容到控制台

~~~linux
echo [选项] [输出内容]
echo "hello"
~~~



### head 指令

> 用于显示文件的开头部分，默认显示前10行

~~~Linux
head 文件名

head -n 5 文件名 :显示文件前5行
~~~

### tail 显示文件末尾内容

~~~
tail 文件名

tail -n 5 文件名 :显示文件前5行
tail -f 文件名 ：追溯文件的所有更新
~~~











### ln 软连接

相当于windows中的快捷方式

- ln -s  1.txt  1_soft  :   1_soft -> 1.txt      源文件是1.txt     源文件必须存在  ，源文件名称一样 则能使用软连接

- 若是删除 1_soft 这不会影响源文件



### 硬链接

> ln 1.txt  1.hard _link



### history 查看历史命令

~~~l
history
~~~









### find 查找文件

- find  .  -n -name  文件名  ：  . 是指目录
- find  ~  -n -name  ‘ *文件名 ’  : 在 ~ 目录下 查找以  *文件名  结尾的文件



### tar 归档管理

- tar -cf  txt.tar  2.txt  ：   将2.txt文件打包成 txt.tar(以tar 为扩展名的会报红)

- tar tf  txt.tar   ：列出包的文件

- tar xvf  txt.tar  ： 解开  解包       v 代表查看过程

- tar xvf  txt.tar  -C tar  ：解包到指定的文件 tar  这个文件要提前创建好



## 时间日期指令

### 基础语法

- date  ：显示当前时间
- date +%Y：显示当前年份
- date +%m：显示当前月份
- date +%d：显示当前天
- date "+%Y-%m-%d  %H:%M:%S" ：显示年月日，时分秒

+：加号也要添加上

### 设置日期

~~~
date -s 字符串时间
~~~

- date -s "2022 - 12-12 12:22:45"

### cal 查看日历

~~~
cal  显示今天的日历
~~~

- cal 2023 ：显示2023年的日历



## 搜索查找

### find 指令

- 指定目录向下查找子目录

~~~Linux
find [搜索范围] [选项]
~~~

![image-20220716103236043](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716103236043.png)

- 按名字查找：find /home  -name  *.txt
- 按拥有者查找：find /opt -user nobody
- 按文件大小查找：find / -size +200M   
  - +：大于多少，- ：小于多少，= ：等于多少

### locate 定位文件路径

- 无需遍历整个文件系统，查找速度快

- 首次使用locate，必须先使用updatedb创建locate数据库

~~~
locate 检索的文件
~~~

### which 

- 可以查看指令在哪个目录下

~~~
which ls
~~~

### grep 过滤查找 和 |  管道 

~~~
grep [] 查找内容 源文件
~~~

- grep  指定内容   指定的文件 

- grep -n  指定内容   指定的文件   ：能查看搜索出**内容的所在行**

- grep -i  指定内容   指定的文件 ：不分大小写

- grep -v  指定内容   指定的文件  ：搜索内容之外的内容

- grep -n  指定内容  .  -r  ：当前目录下存在指定内容的文件  

![image-20220716110030432](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716110030432.png)



- 左边命令返回结果的 交给右边的命令处理
- ls  -al / | more  ： 查看根目录下返回的结果用于more处理 翻页，只能向下翻页 不能往前翻页   超出屏幕
- cat 文件名 -n | more  

~~~ 
法一：cat 1.txt | grep "yes" -n  ：查看1.txt文件中，yes所在的行号
法二：grep "yes" -n 1.txt
~~~



##  解压 和 解压

### gzip：压缩文件 ，gunzip：用于解压的

~~~
gzip 文件 
gunzip 文件.gz
~~~

- 压缩文件，只能将文件压缩为*.gz文件

### zip 压缩文件，unzip：解压文件

~~~
zip [选项] 文件
unzip [选项] 压缩包（*.gz）
~~~

- 选项：-r ：向下递归解压或压缩，压缩目录
- -d <目录> ：指定解压后文件的存放目录

~~~lin
zip -r myhom.gz /home/  压缩：整个home文件夹
unzip -d /opt/tmep /home/myhome.gz  解压到指定的文件目录下
~~~



### tar 打包文件

- 打包后的文件类型是 `.tar.gz`

~~~
tar [选项] *.tar.gz 打包的内容
~~~

选项：

![image-20220716112941616](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716112941616.png)

~~~
tar -zcvf pc.tar.gz /home/文件1 /home/文件2
~~~

解压到指定目录下

~~~
tar -zxvf /home/myhome.tar.gz -C /opt/temp2
~~~

- -C：表示解压到指定的目录

1. 压缩

   - 打包


   > tar cf a.tar *    			生产a.tar文件

   - 压缩

      > gzip -r  a.tar  			 生成  a.tar.gz文件

2. 解压

   - 解压


   > gzip -d  a.tar.gz  		生成a.tar文件

   - 解包


   > tar xf a.tar -C ~/atar   生成到家目录下的atar文件下



### 一步到位压缩和解压

**打包并且压缩**：

- tar  czf b.tar.gz  *txt    	 		将以txt结尾的文件进行打包和压缩  生成一个b.tar.gz 的wenjian

**解包并且解压**

- tar zxf  b.tar.gz -C btar      	  将b.tar.gz解压到btar文件中  btar要事先创建好





## 其他的基础指令



which 查看命令位置

su 切换用户需要密码

exit退出用户

who查看终端用户

pts ：就是打开终端的页面

tty：就是登录操作系统的用户



###  shutdown 关机 

- 需要root

- shutdown -h 10  系统十分钟后关机

- shutdown -h 20:00  系统在20:00关机

- shutdown -h now  系统立即关机

- 不需要root

- reboot  重启操作系统



### passwd 修改密码





## vim 

语法：

> vim 指定的文件  ：打开指定的文件

#### 插入模式：

- i ：输入
- I ：插入行首
- a：插入光标后一个
- A:插入行末
- o：向下新开一行
- O：向上新开一行

#### 命令模式

- ESC：进入插入模式或者命令模式

- 移动光标

- h：左移

- l：右移

- k：上

- j：下


wq保存并退出











