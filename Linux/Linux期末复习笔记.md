> Linux三大题型：命令简答题，脚本程序，服务器配置文件



# 一、文件操作（项目1、2）

1. 创建文件
   - 方式一：`touch` 文件名（P47）
   - 方式二：`vim` 文件名
   - 方式三：`cat` 文件名 ，再使用 `cat >> 文件名` 进行追加内容 （P41）

2. 文件复制、移动
   - 复制：`cp` 源文件名 目标文件名 （P45）
   - 移动：`mv` 源文件名 目标文件名（P47）
3. 修改文件权限 （P119）==项目7==
   - 方式一：使用 `rwx` 设定权限
     - `chmod u/g/o+r/w/x 文件名`
   - 方式二：使用数字 r =4 , w = 2 , x = 1
     - `chmod 777 文件名`
4. 文件查找（1.找文件内容grep，2.找文件find）（P52~53）
   - `grep 内容 文件名`
   - `find [路径] 匹配表达式`
5. 文件打包、解压 （P50）
   - 打包： `tar -cvzf xxx.tar.gz 打包目标文件夹路径 ` 
   - 解压：`tar xzvf xxx.tar.gz -C 解压到的路径`
6. 统计文件 （P）
   1. 行数：wc -n
   2. wc-c：统计字节数
   3. wc-w：统计字数



# 二、用户和组管理（项目3、4）

1. 创建用户 useradd 用户名（P95~96）
2. 组创建 groupadd 组名（P100）
3. 用户加入组群：gpasswd -a 用户名 组名 （P100）



# 三、文件系统和磁盘管理（项目7、8）

1. 磁盘分区管理 fdisk /dev/sba （P122）
2. LVM（P135） RAID（P131） quota（P139）
3. 创建文件系统 mkfs -t ext4 /dev/sda （P126）
4. 挂载：mount 区块 挂载路径 （P129）



# 四、进程管理（项目5、6）

1. 查看进程运行状态：ps（P56） 动态查看进程状态： top（P59）
2. 进程前后台切换 （P59）
   - `bg` ：将进程切换至后台运行
   - `fg` ：将进程切换至前台进行
   - &：进程的后台运行
   - Ctrl + z：可以将一个正在前台执行的命令放到后台，并且暂停。
3. 查看后台进程 jobs（P59）



# 五、shell脚本编程（项目9）

（P80）

1. 分支结构

   ```bash
   if [条件表达式];then
   	代码块
   elif [条件表达式];then
   	代码块
   else
   	代码块
   fi  
   ```

2. 循环结构

   ==while循环==

   ```bash
   while (条件表达式)
   do
       执行的代码块
   done
   ```

   ==for循环==

   ```bash
   for i in (条件表达式)
   do
       执行代码块
   done
   ```



# 六、服务器配置

（P157）

1. 读懂配置文件（考怎么写配置文件）



# 七、其他的命令

1. 查看当前系统的内存使用情况 free （P55）

2. 查看操作系统信息 uname （P60）

3. 修改主机名 hostname （P）

   ```bash
   sudo hostname 新主机名
   ```

4. 修改 `ip ifconfig`

5. 重启网络服务 

   - `systemctl restart network` （Centos7）
   - `service network restart `（Centos6）

6. 软件包查询 `rpm -qa |grep dhcp`