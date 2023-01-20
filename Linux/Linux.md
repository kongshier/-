> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 一 、基础篇

## 1.1 Linux 入门

Linux和Unix的联系：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220713172104310.png" alt="image-20220713172104310" style="zoom:80%;" />







## 1.2 vm和Linux安装

安装VMware 破解版：

在VMware上安装Linux

分区： 

- /：根分区
- swap分区
- /boot：boot分区

![image-20220713182209068](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220713182209068.png)

![image-20220713182232596](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220713182232596.png)

![image-20220713182301764](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220713182301764.png)

### 网络链接的三种模式

![image-20220713204751659](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220713204751659.png)





## 1.3 虚拟机的操作

#### 虚拟机克隆：

- （先关闭虚拟机）复制粘贴虚拟机文件夹

#### 虚拟机快照

- 避免操作失误造成系统异常，还原到正常状态。

#### 虚拟机迁移和删除

- 直接copy
- 直接移除，没有删除文件内容 

#### 安装VMtools

- 更好管理vm虚拟机
- windows和centos共享文件夹

![image-20220714104144369](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714104144369.png)





## 1.4 Linux目录结构

- 根目录：/
- Linux的树状目录
- **一切皆文件** 

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714163026910.png" alt="image-20220714163026910" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714164742555.png" alt="image-20220714164742555" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714165154352.png" alt="image-20220714165154352" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714165407526.png" alt="image-20220714165407526" style="zoom:80%;" />

# 二、实际操作篇



## 2.1 远程登陆（XShell、 XFtp）

### Linux应用场景

- Linux服务器是共享的

- 通过Linux进行项目的管理或开发

  

### 登录客户：

- XShell：安全终端模拟软件，通过XShell控制Linux里面文件，使用命令进行操作文件
- XFtp：上传下载，在Linux和Windows之间进行传输文件

#### 查看IP地址：

- 指令：ifconfig

## 2.2 vi 和vim 编译器

### vim 编译器

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

- 移动光标
- h：左移
- l：右移
- k：上
- j：下
- wq：先按ESC，再输入wq，保存并退出
- q!：强制退出不保存
- q：退出

#### 模式切换

- 按ESC：把当前的模式改成另外的一个模式.

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714211504027.png" alt="image-20220714211504027" style="zoom:80%;" />

#### 快捷键

- 拷贝(复制)：yy，5yy：拷贝当前行向下的5行，并粘贴（输入p）
- 删除：dd，5dd：删除当前行向下的5行
- 查找：先按Esc切换到命令模式下，再输入’ / ‘， 命令行下 / 关键字，回车进行查找，输入n（next）查找下一个，要查找其他的内容，再次输入 ‘/’，清空当前的内容
- 设置文件行数 ：(命令模式输入)：set nu ，（取消行号）：:set nonu
- 光标跳至最后一行：(一般模式）G
- 光标跳至首行：(一般模式）gg
- 撤销动作：（一般模式）u
- 光标移动到20行：（一般模式下）20 shift + g

![image-20220714215336837](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220714215336837.png)

## 2.3 开机、重启和用户登录注销

### 关机、重启命令

- shutdown -h now ：立即关机
- shutdown -h 1 ：1分钟后关机
- shutdown -r now ：立即重启计算机
- halt：关机
- reboot：重启计算机
- sync：把内存的数据同步到磁盘

==关机 / 重启之前运行sync==

### 用户登录、注销



### 用户管理

- Linux是多用户多任务的OS

#### 添加用户

**基本语法** 

~~~linux
useradd 用户名
~~~

默认该用户目录在/home/用户名

指定新用户的位置：

~~~linu
useradd -d 指定位置 用户名
~~~

#### 指定 / 修改密码

~~~
passwd 用户名
~~~

#### 删除用户

~~~
userdel 用户名
userdel - r 用户名   : 删除用户以及该用户目录下的所有文件
~~~

#### 查看用户信息

~~~~
id root :查看root的信息

id 用户名
~~~~

#### 切换用户

切换管理员身份：su -用户名

~~~~Linux
su root  切换到管理员

logout：从管理员退回到客户用户（权限低一级的用户）

su 用户名 :切换到其他的普通用户下
~~~~

- 高级用户到低级用户，不要输入密码
- 低级 ==》 高级，需输入密码

#### 查看当前用户

~~~
who am I
whoami
~~~

- 显示第一登录的用户

### 用户组

> 对有共性 / 权限的多个用户进行统一的管理

#### 新增组

~~~Linux
groupadd 组名
~~~

#### 删除组

~~~Linux
groupdel 组名
~~~

#### 增加用户时直接加上组

~~~Linux
useradd -g 用户组 用户名
~~~

添加zwj，到wudang组中

~~~Linux
useradd  -g wudang zwj
~~~

![image-20220715134144236](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220715134144236.png)

#### 修改用户的组

~~~linux
usermod -g 用户组 用户名
~~~

- 把用户修改到其他的用户组下

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220715135047074.png" alt="image-20220715135047074" style="zoom:80%;" />

## 2.4 实际指令

### 2.4.1 运行级别

- 0：关机
- 1：单用户（可以找回密码）
- 2：多用户没有网络服务
- **3：多用户有网络服务**  {工作用得最多的}
- 4：系统未使用保留给用户
- **5：图像界面**
- 6：系统重启

~~~
init[0,1,2,3,4,5,6]
~~~



查看当前的运行级别：

~~~
systemctl  get-default
~~~

查看指定目标的运行级别

~~~
systemctl  set-default TARGET.target
systemctl  set-default mutl.target  :3
systemctl  set-default graph.target :5
~~~



### 2.4.2 找回root密码

[跟着文档来操作](E:\Linux\take notes\linux找回root密码.pdf)

### 2.4.3 帮组指令

1. man：获得帮助信息

   ~~~Linux
   man[命令或配置文件] 
   ~~~

2. help：获得shell内置命令的帮助信息

   ~~~
   help 
   ~~~

### 2.4.4 文件目录指令

==查看另一个文档==

- pwd：显示当前所在的目录

## 2.5  用户管理、组管理和权限管理



### 2.5.1 文件 / 目录的所有者

**创建文件的用户，就是该文件的所有者**

查看文件的所有者

~~~Linux
ls -ahl
~~~

修改文件的所有者

~~~
chown 用户名  文件名
~~~

- 修改的用户一定要存在

### 所在组

查看文件 / 目录所在组

~~~
 ls -ahl
~~~



- 每一个用户属于一个组

~~~~
groupadd 组名
~~~~

案例：

1. 创建一个组master
2. 创建一个用户for 放入到master组中

~~~
groupadd master

useradd -g maser for
~~~

#### 修改文件所在组

~~~
chgrp 组名 文件名
~~~



### 其他组

> 除文件的所有者和所在组的用户外，系统的其他用户都是文件的其他组

#### 改变用户的组

~~~
usermod -g 新组名  用户名

usermod -d 目录名 用户名 改变该用户登录的初始目录。具有进入到新目录的权限
~~~



### 2.5.2 rwx权限

- d rwx rwx r-x	：d 代表文件夹	– 代表文件
- rwx rwx r-x    ：r 可读     w 可写     x 可执行
- 第一组指文件的==所有者（1 ~ 3 位）的权限==，第二组代表文==所有组的权限（4 ~ 6）==，第三组代表==其他用户权限（7 ~ 9）==

![image-20220716170426945](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716170426945.png)

#### rwx ：目录

![image-20220716171510588](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716171510588.png)



#### rwx：文件

![image-20220716171521128](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220716171521128.png)

数字表示权限：r =4 , w = 2 , x = 1



### 修改权限- chmod

#### 1. 字母法  + 、-、= 三种赋予权限

> u ：所有者   g：所有组  o：其他人，a：所有人(u、g、a的总和)

~~~
chmod  u+r/w/x 指定的文件  	添加权限

chmod  u-r/w/x 指定的文件  	去除权限

chmod  u=r/w/x 指定的文件  	复制权限

chmod  u+r，g-r ,o+w  指定文件    三部分人的权限 

chmod u=rwx,g=rx,o=rx 文件
~~~



#### 2. 数字加法法

- 0 ：- ；
- 1：x (可执行) ；
- 2：w (可写); 
- 4：r  (可读)；
- chmod 000 指定的文件   权限没有 
- chmod  666 指定的文件   所有的都是  rw  4+2=6

~~~
chmod u=rwx,g=rx,o=rx 文件

chmod 755 文件
~~~

### 修改文件所有者 - chown

~~~
chown newowner 文件/目录 改变所有者

chown nerowner:newgroup 文件/目录 改变所有者和所在组

-R 向下递归子文件

chown -R tom /home/test
~~~

### 修改文件/目录所在组 - chgrp

~~~
chgrp newowner 文件/目录

chgrp tom 文件/目录
chgrp -R tom 文件/目录  :递归向下修改
~~~



### 实践案例

用户：

- police , bandit ：分组
- jack、jerry：警察
- xh, xq：土匪

1. 创建组

   ~~~
   groupadd police 
   
   groupadd brandit
   ~~~

2. 创建用户

   ~~~
   useradd -g police jack
   
   useradd -g police jerry
   
   useradd -g bandit xh
   
   useradd -g bandit xq
   ~~~

   

3. jack 创建一个文件，自己可以读r写w，本组人可以读r，其它组没人任何权限

   ~~~
   jack登录
   
   touch jack.txt
   
   chmod 640 jack.txt
   ~~~

4. jack 修改该文件，让其它组人可以读,本组人可以读写

   ~~~
   chmod o=r,g=r jack.txt
   ~~~

5. xh投靠警察，看看是否可以读写

   ~~~
   usermod -g police xh
   ~~~

## 2.6 定时任务调度 

### 2.6.1 crontab 定时任务的设置

- 任务调度：系统在某个时间执行的特定的命令或程序
- 完成重复的调度

~~~
crontab [选项]
~~~

选项：

![image-20220717102808092](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717102808092.png)

- crontab -l ：列出当前所有的任务
- contab -r：终止任务
- service crond restart ：重启任务调度

**每一分钟执行一次**

~~~
*/1 * * * * ls -l /etc/ > /tmp/to.txt
~~~

**五个占位符的说明**：

![image-20220717103159282](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717103159282.png)

**特殊符号意思：**

![image-20220717103751946](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717103751946.png)

**特定时间执行任务**

![image-20220717104117927](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717104117927.png)

**案例**：

- 每隔一分钟，将当前的日期信息，追加到/tmp/mydate 文件中

  ~~~
  */1 * * * * date >> /tmp/mydate
  ~~~

- 每隔一分钟，将当前的日期和日历追加到/home/mycal 文件中 (使用脚本来执行)

  ~~~
  (1) 编写脚本文件
  vim /home/my.sh  代码：date >> /home/mycal 、cal >> /home/mycal
  (2) 给my.sh增加执行权限，
  chmod u+x my.sh
  (3) 设置定时
  crontab -e  添加内容：*/1 * * * * /home/my.sh
  ~~~

- 每天凌晨 2：00 将mysql 数据库testdb ，备份到文件中。

  ~~~
  (1)设置定时
  crontab -e
  添加代码内容
  0 2 * * * mysqldump -u root -proot testdb > /home/db.bak
  ~~~



![image-20220717111828677](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717111828677.png)

### 2.6.2 at 定时任务

- 一次性定时计划任务，执行完就不再执行

- 使用at命令的时候，一定要保证atd进程的启动

  查看进程atd是否正在运行

  ~~~
  ps -ef | grep atd
  ~~~

- ![image-20220717112822357](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717112822357.png)

at **命令格式** 

~~~
at [选项] [时间]

Ctrl + D 结束at命令的输入
~~~

选项

![image-20220717113006772](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717113006772.png)



#### at 指定时间定义

![image-20220717113224341](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717113224341.png)

案例：

- 2天后的下午5点执行/bin/ls/home 

  ![image-20220717113544151](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717113544151.png)

- atq命令来查看系统中没有执行的工作任务

  ![image-20220717115026668](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717115026668.png)

- 明天17点钟，输出时间到指定文件内 比如/root/date100.log

  ![image-20220717115109159](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717115109159.png)

  

- 2分钟后，输出时间到指定文件内 比如/root/date200.log

  ![image-20220717115236502](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717115236502.png)



## 2.7 磁盘分区、挂载

### 2.7.1 Linux分区

- 只有一个根目录，独立且唯一的文件结构



Linux 的硬盘主要有

1. IDE硬盘

   标识符：hdx~

   - hd：分区所在设备类型
   - x：盘号

2. SCSI硬盘

   标识符：sdx~

   - sd：分区所在的设备类型

查看设备挂载情况

~~~
lsblk
lsblk -f
~~~



#### Linux 添加硬盘

1. 虚拟机添加硬盘

2. 分区

   ~~~
   fdisk /dev/sdb
   ~~~

   开始对/sdb分区：依次输入以下

   m：显示命令列表
   p：显示磁盘分区 同 fdisk -l

   n：新增分区
   d：删除分区

   w：写入并退出

   说明:开始分区后输入n，新增分区，然后选择p，分区类型为主分区。两次回车默认剩余全部空间。最后输入w写入分区并退出，若不保存退出输入q。

3. 格式化

   ~~~
   mkfs -t ext4 /dev/sdb1
   ~~~

4. 挂载

   ~~~
   mount 设备名称 挂载目录
   mount /dev/sdb  /newdisk
   
   umount 设备名称/挂载目录
   umount /dev/sdb1 
   umount /nwedisk
   ~~~

   umount ：卸载挂载

5. 设置自动挂载

- 永久挂载:通过修改/etc/fstab实现挂载 

  vim /etc/fstab

- 添加完成后执行mount -a即刻生效

### 磁盘查询情况

~~~
df -h
~~~

#### 查询指定目录的占用情况

- 不指定目录，默认为当前目录

~~~
du -h
~~~

- -s 指定目录占用大小汇总
- -h 带计量单位
- -a 含文件
- --max-depth = 1 子目录深度
- -c 列出明细的同时，增加汇总值

查看opt目录深度为1

~~~
du -hac --max-depth=1 /opt
~~~

#### 实用指令

![image-20220717142826357](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717142826357.png)

## 2.8 进程管理

- 执行的程序称为一个进程，每一个都分配有一个ID号（pid,进程号）
- 进程的两种存在形式：前台（后台运行，表面看不到）与后台（占用屏幕）

### 2.8.1 ps指令

- ps 用来查看系统中执行的程序

  ~~~
  ps
  ps -aux
  ~~~

  ![image-20220718093430189](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718093430189.png)

- 查看指定的进行。（grep 过滤）

  ~~~
  ps -aux | grep sshd
  ~~~

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718094212458.png" alt="image-20220718094212458" style="zoom:67%;" />

### 2.8.2 子、父进程

全格式显示当前所有的进程，查看进程的父进程



~~~
ps -ef :全格式显示当前所有的进程
~~~

-  -e：所有等进行。-f ：全格式

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718094448340.png" alt="image-20220718094448340" style="zoom:80%;" />

### 2.8.3 终止进程 kill 、killall

基本语法

~~~~
kill [选项] 进程号  ：通过进程号杀死进程
killall 进程名称 填过进程名称杀死进程，也支持通配符
~~~~

选项：

-9：强制杀死进程

杀死sshd之后，再次重启sshd服务

~~~
/bin/systemctl start sshd.service
~~~

终止多个gedit

~~~
killall gedit
~~~



### 2.8.4 查看进程树

~~~
pstree [选项] 
~~~

- -p：显示进程 的PID
- -u：显示进程的所属用户



### 2.8.5 服务管理

- 服务  == 进程，运行在后台，监听端口，等待其他程序的请求（守护进程）

#### service管理指令

~~~
service 服务名 [start | stop |restrat |reload |status]
~~~

~~~
关闭端口监听;service network stop
打开端口监听：service network start
~~~

查看服务名

~~~
setup
~~~

#### 服务运行级别

7中运行级别

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718102344827.png" alt="image-20220718102344827" style="zoom:67%;" />



开机流程

~~~mermaid
graph LR
1(开机)-->2(BIOS)-->4(/boot)-->5(systemd进程1)-->6(运行级别)-->7(运行级别对应的服务)
~~~

### 2.8.6 chkcomfig 指令

给服务的运行级别设置自 启动/关闭

查看服务

~~~
chkconfig --list [|grep xxx]

chkconfig 服务名 --list

chkconfig --level 0/1/2/3/4/5 服务名 on/off  :将服务在指定的级别关闭或启动
~~~

- 需要重启，才会生效

### 2.8.7 systemctl 管理

服务在 ==/usr/lib/systemd/system==查看

~~~
systemctl 服务名 [start | stop |restrat |reload |status]
~~~

systemctl设置服务的自启动状态

1. systemctl list-unit-files  [ l grep 务名 ] (管看服务开机后动状态, grep 可以进行过话)
2. systemctl enable 服务名 (设置服务开机启动)
3. systemctl disable 服务名 (关闭服务开机启动)
4. systemctl is-enabled 服务名 (查询某个服务是否是自启动的)



### 2.8.8 f irewall 

==打开或关闭指定的端口==

- 打开端口：firewali-cmd --permanent --add-port=端口号/协议 --permanent 
- 关闭端口：firewall-cmd --permanent --remove-port=端口号/协议 --permanent
- 都需重新载入,才能生效：firewall-cmd --reload
- 查询端口是否开放：firewall-cmd --query-port=端口/协议

### 2.8.9 动态监控

top 和 ps 

- top 执行一段时间会更新正运行的进程

~~~
top [选项]
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718111314674.png" alt="image-20220718111314674" style="zoom:80%;" />

#### 交互操作

在进入top 下：输入

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718114355400.png" alt="image-20220718114355400" style="zoom: 80%;" />

- 监控指定用户：top 回车，在输入u ，输入用户的名称
- 终止进程：top 回车，在输入k ，在输入PID
- 指定系统状态更新时间

#### 查看网络系统状况 netstat 

~~~
netstat [选项]
~~~

- -an ：按一定顺序排序
- -p ：显示哪个进程在调用

~~~
netstat -anp | more
~~~

查看sshd 的服务信息

~~~
netstat -anp | grep sshd
~~~

检测主机链接命令ping 

- 检测远程网络链接是否正常



## 2.9 RPM 和YUM 

- rpm 用于下载包和安装包

### 2.9.1 rpm查询

简单查询：rpm -qa | grep xx 

- rpm -qa 查询安装的rpm软件包
- rpm -qi 软件包名 ：查询软件包信息
- rpm -ql 软件包名：查询软件包中的文件
- rpm -qf 文件全路径名 查询文件所属的软件包 

### 2.9.2 rpm 卸载

语句

~~~
rpm -e RPM包名称
~~~

### 2.9.3 安装 rpm包

~~~
rpm -ivh RPM包全路径名称
~~~

- i = install：安装
- v=verbose  ：提示
- h=hash ：进度条

### 2.9.4 yum

- Shell 前端软件包管理器，自动下载RPM包，一次性安装所有依赖的软件包

基本指令

1. yum查询服务器是否需要的软件

   ~~~
   yum list | grep  XXX
   ~~~

2. 安装

   ~~~
   yum install xxx 下载安装
   ~~~

   







## 2.10 网络配置

虚拟机链接网络

 <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717210111476.png" alt="image-20220717210111476" style="zoom:80%;" />



### 查看IP地址指令

1. Windows下

   ~~~
   ipconfig
   ~~~

2. Linux 下

   ~~~
   ifconfig
   ~~~

IP在同一个网关才可以ping通

~~~
ping ip地址
~~~

### Linux网络环境配置

1. 自动获取

   - Linux启动后会自动获取IP，但是每次获取的IP可能不一样

2. 指定ip

   - 直接修改IP文件来指定IP，并链接到外网

   ~~~
   vim /etc/sysconfig/network-scriipts/ifcfg-ens33
   ~~~

   （1）在里面修改成如下

   ![image-20220717212424940](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717212424940.png)

   添加的内容：

   > #IP
   > IPADDR=192.168.20.132
   > #网关
   > GATEWAY=192.168.20.2
   > #域名服务器
   > DNS1=192.168.20.2

   （2）：修改虚拟机的子网网关，要与Linux一致

![image-20220717212612747](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717212612747.png)

​		网关就上面设置的网关

![image-20220717212838357](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717212838357.png)



（3） 重启网络服务或者重启系统生效

~~~
service network restart 、reboot
~~~

**从Linux链接Windows时需要关闭网络防火墙**



### 设置主机名

~~~
hostname :查看主机名
~~~

- 修改文件在 /etc/hostname 指定
- 重启生效

### 设置hosts映射

1. windows

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717214345842.png" alt="image-20220717214345842" style="zoom:67%;" />

2. linux

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220717214359459.png" alt="image-20220717214359459" style="zoom:67%;" />

- 这样设置之后就可以通过 ping 主机名就可以ping通

### 解析

- Hosts：文本文件，记录IP和Hostname 的映射关系
- DNS：域名系统

# 三、2021高级篇

## 3.1 日志管理

- 检测发生错误的原因，或者被攻击留下的痕迹

### 3.1.1 常用的日志

保存位置

- /var/log/ 该目录就是系统常用的日志文件

- 红色的为重点掌握

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720130608416.png" alt="image-20220720130608416" style="zoom:80%;" />



### 3.1.2 日志管理服务  rsyslogd

CentOS7.6日志服务是rsyslogd，CentOS6.x日志服务是syslogd。rsyslogd功能更强大。rsyslogd的使用、日志文件的格式，和syslogd服务兼容的。原理示意图

- 查询Linux 中的rsyslogd 服务是否启动

  ~~~~
  ps aux | grep "rsyslog" | grep -v "grep"
  ~~~~

  grep -v ：改变匹配的意义，只选择不匹配的行

- 查询 rsyslogd 服务的==自启动状态==

  ~~~
  systemctl list-unit-files | grep rsyslog
  ~~~

#### 配置文件：/etc/rsyslog.conf 

- 编辑文件时的格式：`*.*`  存放日志文件

  - 第一个星表示 日志类型，第二个星表示 日志级别

- 日志类型

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720135430855.png" alt="image-20220720135430855" style="zoom:80%;" />

- 日志级别

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720135527728.png" alt="image-20220720135527728" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720140258172.png" alt="image-20220720140258172" style="zoom:80%;" />

#### 日志服务 rsyslog 记录日志文件

- 事件产生的时间
- 产生事件的服务器的主机名
- 产生事件的服务名或程序名
- 事件的具体信息

查看日志secure

~~~
/var/log/secure 
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720141345571.png" alt="image-20220720141345571" style="zoom:80%;" />



### 3.1.4 自定义日志服务

在 /etc/log/的rsyslog.log 编写自己想要的日志服务信息 

![image-20220720142317025](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720142317025.png)



### 3.1.5 日志轮替

- 日志轮替就是把旧的日志文件移动并改名，同时建立新的空日志文件，当旧日志文件超出保存的范围之后，就会进行删除

  **<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720143816491.png" alt="image-20220720143816491"  />**

配置文件参数：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720144048639.png" alt="image-20220720144048639" style="zoom:80%;" />

#### 把日志文件写入日志轮替

- 第一种方法是直接在/etc/logrotate.conf 配置文件中写入该日志的轮替策略
- 【==推荐==】第二种方法是在/etc/logrotate.d/目录中新建立该日志的轮替文件，在该轮替文件中写入正确的轮替策略，因为该目录中的文件都会被“include”到主配置文件中，所以也可以把日志加入轮替。



#### 日志轮替机制原理

- 依赖系统定时任务，/etc/cron.daily 目录下的logrotate可执行文件

### 3.1.6 查看内存日志

journalctl可以查看内存日志

- journalctl ：查看全部

- journalctl -n 3 ：查看最新3条

- journalctl --since 19:00 --until 19:10:10 ：查看起始时间到结束时间的日志可加日期

- journalctl -p err ：报错日志

- journalctl -o verbose ：日志详细内容

- journalctl _PID=1245 _COMM=sshd ：查看包含这些参数的日志（在详细日志查看)

- ~~~
  journalctl l grep sshd
  ~~~

  注意: journalctl查看的是内存日志,重启清空



## 3.2 定制Linux

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720193756789.png" alt="image-20220720193756789" style="zoom:80%;" />

在Linux的启动流程中,加载内核文件时关键文件：

- kernel文件：vmlinuz-3.10.0-957.el7.x86_64
- initrd文件: initramfs-3.10.0-957.el7.x86_64.img

 【[看文档操作](E:\Linux\take notes\制作自己 mini linux.pdf)】

## 3.3 Linux内核源码& 内核升级

![image-20220720202327800](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720202327800.png)

### 内核升级

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220720204300714.png" alt="image-20220720204300714" style="zoom:80%;" />



## 3.4 Linux备份与恢复



1. 将需要的文件用tar打包，恢复时解压并覆盖就可以

2. 使用dump 和restore 

   - 需先安装好这两个

     ~~~
     yum -y install dump
     yum -y install resrore
     ~~~

### 3.4.1 dump备份

- dump支持分卷和增量备份（所谓的增量备份就是上次备份后 修改/增加过的文件 ,也是差异备份）

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220721093920960.png" alt="image-20220721093920960" style="zoom:80%;" />

案例：

- dump应用案例1

将/boot分区所有内容备份到/opt/boot.bak0.bz2文件中，备份层级为“0"

~~~
dump -0uj -f /opt/boot.bak0.bz2 /boot
~~~

- dump应用案例2

在/boot目录下增加一个文件，备份层级为“1”(只备份上次使用层次“O”备份后发生过改变的数据),注意比较看看这次生成的备份文件boot1.bak有多大

~~~
dump -1uj -f /opt/boot.bak1.bz2 /boot
~~~

==通过dump命令在配合crontab可以实现无人值守备份==

### 3.4.2 dump 其他选项

- dump -W  ：查看备份的文件，以及最后一次备份的层级

-  查看备份时间文件

  ~~~
  cat/etc/dumpdates
  ~~~

dump 备份目录或者文件，是不支持增量备份的，只能使用0级别进行备份，将文件上次到其他服务器



### 3.4.3 恢复restore

基本语法

~~~
restore [模式选项] [选项]
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220721095315543.png" alt="image-20220721095315543" style="zoom: 67%;" />

~~~~
restore -C -f /opt/boot.bak1.bz2   进行恢复比较，和现在当前的文件进行比较

restore -r -f  /opt/boot.bak0.bz2  进行还原恢复

restore -r -f  备份的文件	 还原备份的文件/目录
~~~~





## 3.5 Linux可视化管理

### 3.5.1 webmin 工具

下载地址

~~~
wget http://prdownloads.sourceforge.net/webadmin/webmin-1.997-1.noarch.rpm
~~~

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220721103534765.png" alt="image-20220721103534765" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220721103708687.png" alt="image-20220721103708687" style="zoom:80%;" />

### 3.5.2 bt工具

- 提升运维效率服务器管理软件


安装指令

~~~
yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh 
~~~

安装完成

~~~
==================================================================
Congratulations! Installed successfully!
==================================================================
外网面板地址: http://113.16.28.154:8888/c6d9af34
内网面板地址: http://192.168.20.132:8888/c6d9af34
username: jo4h5ky9
password: 1fd9ba16
If you cannot access the panel,
release the following panel port [8888] in the security group
若无法访问面板，请检查防火墙/安全组是否有放行面板[8888]端口
==================================================================
~~~



 Linux入侵检测& 权限划分&系统优化 



- 审计指令

  - last：这个命令可用于查看我们系统的成功登录、关机、重启等情况；这个命令就是将/var/log/wtmp文件[格式化输出](https://so.csdn.net/so/search?q=格式化输出&spm=1001.2101.3001.7020)。

  - lastb：这个命令用于查看登录失败的情况；这个命令就是将/var/log/btmp文件格式化输出。
  - lastlog：这个命令用于查看用户上一次的登录情况；这个命令就是将/var/log/lastlog文件格式化输出。
  - who：这个命令用户查看当前登录系统的情况；这个命令就是将/var/log/utmp文件格式化输出。
  - w：与who命令一致。

- 日志查看

- 用户查看

- 进程查看

- 其他



权限划分

- r
- w
- x
- u g o 三种用户对文件的操作的权限



系统优化



## 3.6 Linux面试题

### 1 

分析日志t.log(访问量)，将各个ip地址截取，并统计出现次数,并按从大到小排序

http://192.168.200.10/index1.html

http://192.168.200.10/index2.html

http://192.168.200.20/index1.html

http://192.168.200.30/index1.html

http://192.168.200.40/index1.html

http://192.168.200.30/order.html

http://192.168.200.10/order.html

首先把这些网站放入一个文件当中

~~~
vim interview.txt

cat interview.txt | cut -d '/' -f 3 |sort | uniq -c | sort -nr
~~~

### 2

统计连接到服务器的各个ip情况，并按连接数从大到小排序

~~~~
netstat -an | grep ESTABLISHED | awk -F " " '{print $5}' | cut -d ":" -f 1 | sort | uniq -cl sort -nr
~~~~



# 四、定制篇

## 4.1 Linux之JavaEE

### JDK安装

步骤：

1. mdir /opt/jdk

2. 实用xftp7上传到/opt/jdk

3. 解压tar -zxvf jdk1.8.0_333-linux-x64.tar.gz

4. mkdir /usr/local/java

5. mv /opt/jdk/jdk1.8.0_333 /usr/local/java

6. 配置环境变量的配置文件 vim /etc/profile 

   ​	进入了profile 之后，在文件的最后添加以下两句

   - export JAVA_HOME=/usr/local/java/jdk1.8.0_333
   - export PATH=`$JAVA_HOME/bin:  $`PATH

7. source  /etc/profile [让文件生效] (刷新环境变量)
   测试是否安装成功

### idea安装

步骤：

1. 下载地址:https://www.jetbrains.com/idea/download/#section=windows
2. 解压缩到/opt/idea
3. 启动idea bin目录下./idea.sh，配置jdk
4. 编写Hello world程序并测试成功!



### Tomcat安装

步骤：

1. 上传安装文件，并解压缩到/opt/tomcat
2. 进入解压目录/bin,启动tomcat ./startup.sh
3. 开放端口8080（打开端口）

测试：http://linuxip:8080





### MySQL安装

方法一 (https://blog.csdn.net/bai_shuang/article/details/122939884) 

方法二：

https://blog.csdn.net/mqingo/article/details/84974535

https://blog.csdn.net/mqingo/article/details/83866618

开放 3306端口







## 4.2 shell 编程

- shell 是一种命令行解释器，
- 用户可以用Shell来编程、挂起、停止、编写程序

### 4.2.1 Shell脚本执行方式

 格式要求 ：

- 以#!/bin/bash开头
- 具有可执行权限

执行方式

1. 赋予权限 +x 执行权限

   ~~~
   chmod u+x(u用户执行权限、g、o) 文件名
   ~~~

2. sh+脚本

   ~~~
   sh hello.sh
   ~~~

### 4.2.2 Shell变量

1. 系统变量

   `$ HOME`、 `$PWD` 、`$SHELL` 等

   显示当前shell中所有变量：set

2. 用户自定义变量

   定义变量语法：

   ~~~
   变量 = 值
   ~~~

   撤销变量

   ~~~
   unset 变量
   ~~~

   声明静态变量

   ~~~
   readonly 变量
   ~~~

   - 不能unset

#### 规则

- 变量名称可以由字母、数字和下划线组成，但是不能以数字开头。
- 等号两侧不能有空格
- ==变量名称一般大写== 

讲命令的结果返回赋值变量

~~~
C=`date`
D=$(cal)
echo "C=$C"
echo "D=$D"
~~~

### 4.2.3 设置环境变量

语法

~~~
export 变量名=变量值   ：讲shell变量输出为环境变量/全局变量
source 文件名  ：让修改后的配置信息生效
echo $变量名 ：查询环境变量的值
~~~

- 在/etc/profile文件中设置环境变量

shell多行注释语句

~~~
:<<!

代码块

!
~~~



### 4.2.4 位置参数

~~~
./myshell 100 200
~~~

基本语法

- $n ：n为数字，`$`0代表命令本身，`$1-$9`代表第一到第九个参数，十以上的参数，十以上的参数需要用大括号包含：如`${10}` 

- $*：命令行中的所有参数，`$*` 把所有的参数看错一个整体

- $@：命令行中所有的参数，`$@` 把每一个参数区分对待

- $#：代表命令行中所有参数的个数

  ![image-20220718214425907](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718214425907.png)

![image-20220718214336348](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220718214336348.png)



### 4.2.5 预定义变量

基本语法

- $$：当前进程的进程号(PID)
- $!：后台运行的最后一个进程的进程号(PID)
- $?：最后一次执行的命令的返回状态。如果这个变量的值为0，证明上一个命令正确执行;如果这个变量的值为非(具体是哪个数，由命令自己来决定），则证明上一个命令执行不正确了。



### 4.2.6 运算符

基本语法

1. $((运算式))  或 `$[运算式]` 或 expr m + n //expression 表达式

   - expr 运算符之间有空格
   - expr m - n
   - expr \* / % 乘 除 取余

   ~~~bash
    # 计算（2+4）*4
    #方式一
    RES=$(((2+4)*4))
    echo "RES1=$RES"
    
    #方式二
    RES=$[(2+4)*4]
    echo "RES2=$RES"
    
    #方式三
    TEMP=`expr 2 + 3`
    RES=`expr $TEMP \* 4`
    echo "TEMP1=$RES"
    
    # 计算两个参数求和
    SUM=$[$1+$2]
    echo "sum=$SUM"
    
    ./myshell.sh 20 30(传参数)
   ~~~

### 4.2.7 条件控制

基本语法

~~~bash
[ condition ]  #前后有空格
~~~

- 非空返回true，$?验证（0为true ，>1 为false）
- 以 if 开始， 以 fi 结束

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220719111419182.png" alt="image-20220719111419182" style="zoom:80%;" />

判断 "kkk"是否等于"kkk"

~~~bash
if [ "KKK" = "KKK" ]
then
		echo "equal"
fi		
~~~

判断 12是否大于等于15

~~~bash
if [ 12 -ge 15 ]
then
		echo "大于了"
fi		
~~~

判断文件是否存在指定路径

~~~bash
if [ -f /usr/a.txt ]
then
		echo "存在该文件"
fi
~~~

### 4.2.8 流程控制

1. if 判断

   ~~~bash
   if [ 条件判断式 ]
   then 
   	代码块
   fi	
   ~~~

   ~~~bash
   if [ 条件判断式 ]
   then 
   	代码块
   elif [ 条件 ]
   then 
   	代码块
   fi	
   ~~~

   例子

   ~~~bash
   #!/bin/bash
   if [ $1 -ge 60 ]
   then 
   	echo "及格了"
   elif [ $1 -lt 60 ]
   then 
   	echo "不及格"
   fi		
   ~~~

   成绩等级判断：

   ```bash
   # !/bin/bash
   echo "This is Script Five different score levels"
   echo "Input You's Score:"
   read score
   if((score<0 || score >100));then
           echo "输入的成绩范围必须在0~100之间，或者请输入的是整数"
   fi
   # 等级判断
   if ((score>=90 && score<100));then
           echo "You score levels is A"
   elif ((score>=80 && score<90));then
           echo "You score levels is B"
   elif ((score>70 && score<80));then
           echo "You score levels is C"
   elif ((score>60 && score<=70));then
           echo "You score levels is D"
   elif ((score>=0 && score<60));then
           echo "You score levels is E"
   fi
   ```

2. case语句

   ~~~bash
   case $变量名 in
     "值1")
     如果变量的值等于值1，则执行程序1
     ;;
     "值2")
     如果变量的值等于值2，则执行程序2
     ;;
     …省略其他分支.…
     *)
     如果变量的值都不是以上的值，则执行此程序
     ;;
   esac
   ~~~

   实例:

   ~~~bash
   #!/bin/bash
   case $1 in
   "1")
   echo "周一"
   ;;
   "2")
   echo "周二"
   ;;
   *)
   echo "other day ..."
   ;;
   esac
   ~~~

3. for循环

   基本语法1

   ~~~bash
   for 变量 in 值1 值2 值n...
   do
   	程序/代码
   done
   ~~~

   基本语法2

   ~~~bash
   for ((初始值;循环控制条件;变量变化))
   do
   	程序/代码
   done
   ~~~

   案例

   1. 打印命令行输入的参数 （区分`$*` 、`$@`）

   ~~~bash
   #!/bin/bash
   for i in "$*"
   do
   	echo "num is $i"
   done	
   
   #!/bin/bash
   for j in "$@"
   do
   	echo "num is $j"
   done	
   ~~~

   - `$*`  是把所有参数看作一个整体
   - `$@` 把每一个参数分开

   2. 100的累加

      ~~~bash
      # 1-100的累加求和 方式一
      #!/bin/bash
      SUM=0
      for (( i=1;i<=100;i++))
      do
      	SUM=$[$SUM+$i]
      done	
      echo "sum= $SUM"
      
      ~~~
      
      ```bash
      # 1-100的累加求和 方式二
      # !/bin/bash
      echo "Calculate the sum of 1-100"
      echo 
      declare sum=0
      for i in {1..100}
      do
              let sum=$sum+$i
      done
      echo "Calculate the result= $sum"
      ```
      
      ```bash
      # 指定数字的累加求和
      for (( i=1;i<=$1;i++))
      do
      	SUM=$[$SUM+$i]
      done	
      echo "sum= $SUM"
      ```
      
      ```bash
      # 1-n的累加求和
      # !/bin/bash
      echo "Input a Integer n: "
      read n
      sum=0
      for ((i=1;i<=$n;i++))
      do
              let sum=$sum+$i
      done
      echo "Summation result is: $sum"
      ```
      
      

4. while 循环

   基本语法

   ~~~
   while [ 条件判断 ]  # []里面左右两侧有空格
   do
   代码
   done
   ~~~

   ~~~
   #!/bin/bash
   SUM=0
   i=0
   while [ $i -le $1 ]
   do
   	SUM=$[$SUM+$i]
   	i=$[$i+1]
   done
   echo "sum=$SUM"
   ~~~



添加新用户：

```bash
# !/bin/bash
echo "useradd user"

for user in {1..50}
do
        if ((user<10));then
                useradd newuser0${user}
                # 输出的作为每个用户的密码
                echo "123456" | passwd --stdin newuser0${user}
                # 强制每个用户首次登录的时候进行修改密码
                chage -d 0 newuser0#{user}
        else
                useradd newuser${user}
                echo "123456" | passwd --stdin newuser${user}
                chage -d 0 newuser${user}
        fi
done

```



### read 读取控制台输入

基本语法

~~~
read (选项)(参数)
~~~

- -p：指定读取时的提示符
- -t：指定读取时的等待时间，不指定就没有等待时间

~~~
#!/bin/bash
# 读取控制台的输入的一个num1值
read -p "请输入一个数num1=" NUM1
echo "您输入 NUM1 =$NUM1"

# 读取控制台的输入的一个num1值,在10秒内输入
read -t 10 -p "请输入一个数num2=" NUM2
echo "您输入的NUM2=$NUM2"
~~~

### 4.2.9 函数

#### 系统函数

basename基本语法

功能返回完整路径最后 / 的部分，常用于获取文件名

- `basename [pathname] [suffix]`

  `basename [string] [suffix]`

  (功能描述:basename命令会删掉所有的前缀包括最后一个(‘T)字符，然后将字符串显示出来。

- 选项:

  suffix为后缀，如果suffix被指定了,basename会将pathname或string中的suffix去掉。



dirname 

- 返回完整路径最后 / 的前面的部分，常用于==返回部分路径==
- dirname 文件绝对路径 

==不包括文件名字的，只有目录==

#### 自定义函数

~~~
[ function ] funname[()]
{
	Action;
	[retuen int;]
}

# 调用函数名
funname [值]
~~~

案例：计算输入两个参数的和

~~~bash
function getSum(){
	
	SUM=$[$n1+$n2]
	echo "和为：$SUM"
}
# 输入两个数
read -p "请输入一个数n1=" n1
read -p "请输入一个数n2=" n2

#调用自定义函数
getSum $n1 $n2
~~~

### 定时维护MySQL数据库

#### 需求分析

- 每天凌晨2:30备份数据库demo 到/data/backup/db
- 备份开始和备份结束能够给出相应的提示信息
- 备份后的文件要求以备份时间为文件名，并打包成.tar.gz的形式，比如:2021-03-12_230201.tar.gz
- 在备份的同时,检查是否有10天前备份的数据库文件，如果有就将其删除。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220719203239003.png" alt="image-20220719203239003" style="zoom:80%;" />

mysql_db_backup.sh

~~~bash
#!/bin/bash
#备份的目录
BACKUP=/date/backup/db
#当前时间
DATETIME=$(date +%Y-%m-%d_%H:%M:%S)
echo "$DATETIME"
#数据库地址
HOST=localhost
#数据库用户名
DB_USER=root
#数据库密码
DB_PW=123456
#备份的数据库名
DATABASE=studydemo

#创建备份目录，如果不存在就创建
[ ! -d "${BACKUP}/${DATETIME}" ] && mkdir -p "${BACKUP}/${DATETIME}"

#备份数据库
mysqldump -u${DB_USER} -p${DB_PW} --host=${HOST} -q -R --datebases ${DATABASE} | gzip > "${BACKUP}/${DATETIME}/$DATETIME.tar.gz"

#将文件处理成tar.gz
cd ${BACKUP}
tar -zcvf $DATETIME.tar.gz ${DATETIME}

#删除对应的备份目录
rm -rf ${BACKUP}/${DATETIME}
#删除十天以前的备份文件
find ${BACKUP} -atime +10 -name "*.tar.gz" -exec rm {} \;
echo "成功备份数据库 ${DATABASE}!!"
~~~

每天2：30执行文件

crondtab -e 

~~~
30 2 * * * /usr/sbin/mysql_db_backup.sh
~~~



## Linux之Python

（不走这个方向，没有看视频）

Python专业开发平台 -Ubuntu

Ubuntu下开发Python开发环境

APT软件管理和远程登录





