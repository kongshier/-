> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# Nginx概述

- Nginx是一款轻量级的Web服务器/[反向代理](https://so.csdn.net/so/search?q=反向代理&spm=1001.2101.3001.7020)服务器及电子邮件（IMAP/POP3）代理服务器。其特点是占有内存少，并发能力强，事实上nginx的并发能力在同类型的网页服务器中表现较好.



## 下载与安装

1. 创建安装路径文件夹 

   ~~~
   mkdir -p /usr/local/nginx 
   ~~~

2. 安装依赖包：

   ~~~
   yum -y install gcc pcre-devel zlib-devel openssl openssl-devel
   ~~~

3. 下载Nginx安装包：

   ~~~
   wget https://nginx.org/download/nginx-1.22.0.tar.gz
   ~~~

4. 解压

   ~~~
   tar -zxvf nginx-1.22.0.tar.gz
   ~~~

5. 进入 nginx-1.22.0

   ~~~
   cd nginx-1.22.0
   ~~~

6. 安装前检查工作

   ~~~
   ./configure --prefix=/usr/local/nginx
   ~~~

7. 编译并安装

   ~~~
   make && make install
   ~~~

8. 进入目录

   ~~~
   cd /usr/local/nginx
   ~~~

![image-20221017092700899](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017092700899.png)

| Nginx目录文件   | 说明                                |
| --------------- | ----------------------------------- |
| conf/nginx.conf | nginx配置文件                       |
| html            | 存放静态文件(html、css、Js等)       |
| logs            | 日志目录，存放日志文件              |
| sbin/nginx      | 二进制文件，用于启动、停止Nginx服务 |



### 树形结构展示：

~~~
yum install yum

tree
~~~

![image-20221017093145093](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017093145093.png)

# Nginx命令

==都是在sbin目录下执行以下的命令==

1. 查看版本

   ~~~
   cd sbin
   ./nginx -v
   ~~~

   ![image-20221017093425102](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017093425102.png)

2. 检查配置文件是否有错误

   ~~~
   ./nginx -t
   ~~~

   ![image-20221017093532789](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017093532789.png)

3. 启动Nginx

   ~~~
   sbin/nginx
   ~~~

4. 停止Nginx

   ~~~
   ./nginx -s stop
   ~~~

5. 查看进程

   ~~~
   ps -ef |grep nginx
   ~~~

6. 重新加载配置文件 配置文件修改都要重新加载文件

   ~~~
   ./nginx -s reload
   ~~~

# Nginx配置文件结构

Nginx配置文件（conf/nginx.conf）整体分为三部分(逻辑划分)

## 一、全局块

- 和nginx运行相关的全局配置

![image-20221017113536546](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017113536546.png)



## 二、events块

- 和网络链接相关的配置

![image-20221017113632522](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017113632522.png)



## 三、http块

-  代理、缓存、日志记录、虚拟主机配置

1. http全局块
2. server块（server全局块和location块）

注意：http块中可以配置多个server块，每个server块中可以配置多个location块

![image-20221017114617675](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017114617675.png)

# Nginx应用



Nginx可以作为静态web服务器来部署静态资源。静态资源指在服务端真实存在并且能够直接展示的一些文件，比如常见的html页面、css文件、js文件、图片、视频等资源。相对于Tomcat，Nginx处理静态资源的能力更加高效，所以在生产环境下，一般都会将静态资源部署到Nginx中。将静态资源部署到Nginx非常简单，只需要将文件复制到Nginx安装目录下的html目录中即可。



![image-20221017145158531](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017145158531.png)

## 反向部署

### 正向代理

是一个位于客户端和原始服务器（origin server)之间的服务器，为了从原始服务器取得内容，客户端向代理发送一个请求并指定目标（原始服务器），然后代理向原始服务器转交请求并将获得的内容返回给客户端。



- 正向代理的典型用途是为在防火墙内的局域网客户端提供访问internet的途径。 
- 正向代理一般是在客户端设置代理服务器，通过[代理服务器](https://so.csdn.net/so/search?q=代理服务器&spm=1001.2101.3001.7020)转发请求，最终访问到目标服务器。

![image-20221017145959538](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017145959538.png)

### 反向代理

反向代理服务器位于用户与目标服务器之间，但是对于用户而言，反向代理服务器就相当于目标服务器，即用户直接访问反向代理服务器就可以获得目标服务器的资源，反向代理服务器负责将请求转发给目标服务器。

用户不需要知道目标服务器的地址，也无须在用户端作任何设定。

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017150237000.png" alt="image-20221017150237000" style="zoom:67%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017150629810.png" alt="image-20221017150629810" style="zoom:80%;" />

## 负载均衡

- 应用集群：将同一应用部署到多台机器上，组成应用集群，接收负载均衡器分发的请求，进行业务处理并返回响应数据。
- 负载均衡器：将用户请求根据对应的负载均衡算法分发到应用集群中的一台服务器进行处

### 配置

![image-20221017151021958](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017151021958.png)



### 负载均衡策略

| 名称       | 说明             |
| :--------- | :--------------- |
| 轮询       | 默认方式         |
| weight     | 权重方式         |
| ip_hash    | 依据ip分配方式   |
| least_conn | 依据最少连接方式 |
| url_hash   | 依据url分配方式  |
| fair       | 依据响应时间方式 |

 



# Nginx特点

1. 跨平台：Nginx可以在大多数操作系统中运行，而且也有Windows的移植版本
2. 配置异常简单：非常容易上手。配置风格跟程序开发一样，神一般的配置
3. 非阻塞、高并发：数据复制时，磁盘I/O的第一阶段是非阻塞的。官方测试能够支撑5万并发连接，在实际生产环境中跑到2-3万并发连接数（这得益于Nginx使用了最新的epoll模型）
4. 事件驱动：通信机制采用epoll模式，支持更大的并发连接数
5. 内存消耗小：处理大并发的请求内存消耗非常小。在3万并发连接下，开启的10个Nginx进程才消耗150M内存（15M*10=150M）
6. 成本低廉：Nginx作为开源软件，可以免费试用。而购买F5 BIG-IP、NetScaler等硬件负载均衡交换机则需要十多万至几十万人民币
7. 内置健康检查功能：如果Nginx Proxy后端的某台Web服务器宕机了，不会影响前端访问。
8. 节省带宽：支持GZIP压缩，可以添加浏览器本地缓存的Header头。
9. 稳定性高：用于反向代理，宕机的概率微乎其微



# Nginx与Tomcat区别

![image-20221017152224445](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20221017152224445.png)

















