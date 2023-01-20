> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# Maven

**资料格式：**

- **配置文件**

> <groupId>com.itheima</groupId>

- **java代码**

  > statement stat = con.createstatement ();

- **示例**

  > <groupId>com.itheima</groupId>

- **命令**

  > mvn test

# Maven简介

## 传统项目管理状态分析

> - jar包不统一，jar包不兼容
> - 工程升级维护过程操作繁琐

## Maven是什么

> Maven的本质是一个项目管理工具，将项目开发和管理过程抽象成一个项目**对象模型**(POM)
>
> POM (Project Object Model) :**项目对象模型**

> ![image-20220123113440744](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123113440744.png)

Maven的作用

> - **项目构建:**提供标准的、跨平台的**自动化项目构建**方式
> - **依赖管理:**方便快捷的**管理**项目依赖的资源**(jar包)**，避免资源间的版本冲突问题
> - **统一开发结构：**提供标准的、统一的项目结构

Maven下载：

> 官网地址：(https://maven.apache.org/)

Maven配置文件

> ![image-20220123142435949](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123142435949.png)
>
> ![image-20220123142444872](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123142444872.png)

## Maven基础概念

### 仓库

> 用于存储资源，包含各种jar包
>
> 中央仓库：是开源/共享的
>
> 私服仓库：公司内部的   **提供访问速度**

![image-20220123143434973](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123143434973.png)

### 坐标

> 用于描述仓库中资源的位置

**Maven坐标主要组成**

- **groupld:**定义当前Maven项目录的包名称(通常是域名反写，例如: org.mybatis)
- **artifactld:**定义当前Maven项目名称(通常是模块名称，例如CRM、SMS)
- **version:**定义当前项目版本号
- **packaging:**定义该项目的打包方式  （较少用）



**Maven坐标作用：**

- 使用唯一标识，唯一性定位资源位置，通过该标识可以将资源的识别与下载工作交由机器完成

### 第一个Maven项目（手工）

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123145845531.png" alt="image-20220123145845531" style="zoom:67%;" />

**在src同层目录下创建pom.xml**

> 包含有groupid、artifactId、version 、[packaging] 标签组成

### Maven项目构建命令

> Maven构建命令使用mvn开头，后面添加功能参数，可以一次执行多个命令，使用空格分隔
> **mvn compile    #编译**
> **mvn clean       #清理**
> **mvn test		  #测试**
> **mvn package  #打包**
> **mvn install	   #安装到本地仓库**
>
> ending

### Maven项目（IDEA生成）

![image-20220123183927683](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123183927683.png)

创建Tomcat运行maven web

## 依赖管理  

**也就是在pom.xml文件里面添加**

### 依赖配置

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123205907570.png" alt="image-20220123205907570" style="zoom:67%;" />

### 依赖传递

引用其他项目的jar包 只需引用jar包的groudId、artifectId、version

> **直接依赖:**在当前项目中通过依赖配置建立的依赖关系
> **间接依赖:**被资源的资源如果依赖其他资源，当前项目间接依赖其他资源

#### 依赖传递冲突问题

> - **路径优先:**当依赖中出现**相同的资源**时，**层级越深，优先级越低，层级越浅，优先级越高**
> - **声明优先:**当资源在**相同层级**被依赖时，**配置顺序靠前的覆盖配置顺序靠后的**
> - **特殊优先:**当同级配置了**相同资源的不同版本**，后配**置的覆盖先配置的**

### 可选依赖

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123211040099.png" alt="image-20220123211040099" style="zoom:67%;" />

~~~xml
<optional>true</optional>  <!--选择隐藏  当别人使用在是发现不了的，不会出现显示依赖-->
~~~

### 排除依赖

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220123211653896.png" alt="image-20220123211653896" style="zoom:67%;" />

~~~xml
<exclusions>需要排除的坐标，不需x</exclusions>
~~~

### 依赖范围

~~~xml
<scope></scope>
~~~

> 依赖的jar默认情况可以在任何地方使用，可以通过scope标签设定其作用范围作用范围
>
> - 主程序范围有效(main文件夹范围内)
> - 测试程序范围有效(test文件夹范围内)
> - 是否参与打包(package指令范围内)

|      scope      | 主代码 | 测试代码 | 打包 | 范例          |
| :-------------: | ------ | -------- | ---- | ------------- |
| compile（默认） | Y      | Y        | Y    | log4j         |
|      test       |        | Y        |      | junit         |
|    provided     | Y      | Y        |      | servlet - api |
|     runtime     |        |          | Y    | jdbc          |

#### 依赖范围传递性

![image-20220124112123154](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220124112123154.png)

## 生命周期与插件

### 项目构建生命周期

一次构建过程经历了多少事件

> cmopile **->** test-compile **->** test **->** packge **->** install

### 三个生命周期阶段

> 1. clean:清理工作
> 2. default:核心工作，例如编译，测试，打包，部署等
> 3. site:产生报告，发布站点等

### default生命周期阶段执行指令

![image-20220124114733993](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220124114733993.png)

### 插件

> - 插件与生命周期内的阶段绑定，在执行到对应生命周期时执行对应的插件功能
> - 默认maven在各个生命周期上绑定有预设的功能
> - 通过插件可以自定义其他功能

# Maven高级

## 分模块开发与设计（重点）

### 工程模块与模块划分

> 新建一个模块进行把整合的进行分类模块拆分

- 分模块开发
  - 模块中仅包含当前模块对应的功能类与配置文件
  - spring核心配置根据模块功能不同进行独立制作
  - ◆当前模块所依赖的模块通过导入坐标的形式加入当前模块后才可以使用
  - web.xml需要加载所有的spring核心配置文件
  
  

#### ssm_pojo拆分

- 新建模块
  - 拷贝原始项目中对应的相关内容到ssm_pojo模块中
    实体类(User)
    配置文件(无)



#### ssm_dao拆分

新建模块

拷贝原始项目中对应的相关内容到ssm_dao模块中

数据层接口(UserDao)

配置文件:保留与数据层相关配置文件(3个)
			注意:分页插件在配置中与SqlSessionFactoryBean绑定，需要保留

- pom.xml:引入数据层相关坐标即可，删除springmvc相关坐标
  - spring
  - mybatis
  - spring整合mybatismysql
  - druid
  - pagehelper
  - **直接依赖ssm_pojo (对ssm_pojo模块执行install指令，将其安装到本地仓库)**



#### ssm_serive拆分

- 新建模块

- 拷贝原始项目中对应的相关内容到ssm_service模块中

  - 业务层接口与实现类(UserService、UserServicelmpl)配置文件:保留与数据层相关配置文件(1个)

  - pom.xml:引入数据层相关坐标即可，删除springmvc相关坐标

  ​		spring

  ​		junit

  ​		spring整合junit

  ​		直接依赖ssm_dao (对ssm_dao模块执行install指令，将其安装到本地仓库)间接依赖ssm_pojo (由ssm_dao模块负责依赖关系的建立)

- 修改service模块spring核心配置文件名，添加模块名称，格式: applicationContext-service.xml
- 修改dao模块spring核心配置文件名，添加模块名称，格式: applicationContext-dao.xml
- 修改单元测试引入的配置文件名称，由单个文件修改为多个文件



#### ssm_conctroller拆分

新建模块（使用webapp模板)

拷贝原始项目中对应的相关内容到ssm_controller模块中

- 表现层控制器类与相关设置类(UserController、异常相关……)

- 配置文件:保留与表现层相关配置文件(1个)、服务器相关配置文件(1个)

- - pom.xml:引入数据层相关坐标即可，删除springmvc相关坐标

  - spring

  - springmvcjacksonservlet

  - tomcat服务器插件

  - 直接依赖ssm_service (对ssm_service模块执行install指令，将其安装到本地仓库)

  - 间接依赖ssm_dao、ssm_pojo

- 修改web.xml配置文件中加载spring环境的配置文件名称，使用*通配，加载所有applicationContext-开始的配置文件



## 聚合（重点）

### 多模块构建维护

![image-20220124140213357](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220124140213357.png)

~~~xml
<!--定义该工程用于进行构建管理 在pom文件下添加下列代码-->  
<packing>pom</packing>

<!--管理工程列表-->
<modules>
   <!--具体的工程名称  顺序无关  运行结果的顺序只与模块间的依赖关系有关-->
	<module>    </module>
    <module>    </module>
    <module>    </module>
    <module>    </module>
</modules>
~~~

> **若工程没有写pacaking 打包方式 默认是jar包**，

#### 模块类型

> pom
>
> war
>
> jar

## 继承（重点）

 模块依赖维护

**继承的作用：**

通过继承可以在子工程中用父工程中的配置

- 在子工程中配置继承关系



**制作方式：**

- 在**子工程**中**声明其父工程**坐标与对应的位置 

~~~xml
<!--定义父工程 parent标签-->
<parent>
    <groupId>com.kcs</groupId>
    <artifactId>ssm</artifactId>
    <version>1.0-SNAPSHOT</version>
    <!-- 父工程的pom文件 -->
    <relativePath>../ssm/pom.xml  (父工程的pom文件,y用相对路径)</relativePath>
</parent>
~~~





### 继承依赖定义

- 在**父工程**中定义依赖关系  定义子工程坐标


~~~xml
<!--此处的依赖管理内容-->
<dependencyManagement>
    <!--所有具体的依赖-->
    <dependencies>
        <!--spring环境 -->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
            <version>5.1.9.RELEASE</version>
        </dependency>
    <dependencies>
<dependencyManagement>
~~~

### 继承依赖使用

- 在**子工程**中定义依赖关系**，无需邪出版本号**，版本在父工程中控制，维护时只要对父工程中的版本进行修改就可以了


~~~xml
<dependencies>
        <!--spring环境-->
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-context</artifactId>
        </dependency>
</dependencies>
~~~

### 继承的资源

![image-20220124193048050](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220124193048050.png)

### 继承与聚合比较

- **作用**
  	     聚合用于快速**构建项目**

  ​	     继承用于快速**配置**

  **相同点**

  ​          聚合与继承的pom.xml文件打包方式均为pom，可以将两种关系制作到同一个pom文件中

  ​      	聚合与继承均属于设计型模块，并无实际的模块内容

- **不同点:**
            聚合是在**当前**模块中配置关系，聚合可以感知到参与聚合的模块有哪些

  ​          继承是在**子模块**中配置关系，父模块无法感知哪些子模块继承了自己



## 属性

### 属性统一的重要性

#### 属性类别

1. 自定义属性

   > **作用：** 等同于定义变量，方便统一维护
   >
   > ~~~xml
   > <!--定义自定义属性格式  properties标签中-->
   > <properties>
   >     <spring.version>5.1.9.RELEASE</spring.version>
   >     <!--标签名就是变量名 也就是 spring.version和junit.version-->
   >     <junit.version>4.12</junit.version>
   > </properties>
   > <!--调用格式 ${变量名}-->
   > <dependency>
   >     <groupId>org.springframework</groupId>
   >     <artifactId>spring-context</artifactId>
   >     <version>${spring.version}</version>
   > </dependency>
   > ~~~

2. 内置属性

   > **作用：** 使用maven内置属性，快速配置
   >
   > ~~~xml
   > <!--调用格式-->
   > ${basedir}
   > ${version}
   > ~~~

3. Setting属性

   > **作用：** 使用maven配置文件setting.xml中的标签属性，用于动态配置
   >
   > ~~~xml
   > <!--调用格式-->
   > ${settings.localRepository}
   > ~~~

4. Java系统属性

   > **作用：** 读取java系统属性
   >
   > ~~~xml
   > <!--调用格式-->
   > ${user.home}
   > <!--系统属性查询方式-->
   > mvn help:system
   > ~~~

5. 环境变量属性

   > **作用：** 使用maven配置文件setting.xml中的标签属性，用于动态配置
   >
   > ~~~xml
   > <!--调用格式-->
   > ${env.JAVA_HOME}
   > <!--环境变量属性查询方式-->
   > mvn help:system
   > ~~~

## 版本管理

### 工程版本

- SNAPSHOT（测试阶段版本）

  项目开发过程中，为方便团队成员合作，解决模块间相互依赖和时时更新的问题，开发者对每个模块进行构建的时候，输出的临时性版本叫快照版本（测试阶段版本)
  快照版本会随着开发的进展不断更新

- RELEASE（发布版本）

  项目开发到进入阶段里程碑后，向团队外部发布较为稳定的版本，这种版本所对应的构件文件是稳定的，即便进行功能的后续开发，也不会改变当前发布版本内容，这种版本称为发布版本



### 工程版本号约定

> - **约束规范**
>
>   ​	<主版本>.<次版本>.<增量版本>.<里程碑版本>
>   ​	主版本:表示项目重大架构的变更，如: spring5相较于spring4的迭代
>
>   ​	次版本:表示有较大的功能增加和变化，或者全面系统地修复漏洞
>
>   ​	增量版本:表示有重大漏洞的修复
>   ​	里程碑版本:表明一个版本的里程碑（版本内部)。这样的版本同下一个正式版本相比，相对来说不是很稳定，有待更多的测试>
>
> 示例：5.1.1.RELEASE

## 资源配置

### 资源配置多文件维护

配置文件应用pom属性

> **作用：** 在任意配置文件中加载pom文件中定义的属性
>
> ~~~xml
> <!--调用格式-->
> ${jdbc.url}
> 
> <!--开启配置文件加载pom属性-->
> 
> <!-- 配置资源文件对应的信息-->
> <!--在bulid标签中-->
> <resources>
>     <resource>
>         <!--指定配置文件对应的位置目录，使用相对路径（../） ${project.basedir}x  -->
>         <directory>${project.basedir}/src/main/resources</directory>
>         <!--开启对配置文件的资源加载过滤-->
>         <filtering>true</filtering>
>     </resource>
> </resources>
> ~~~

- 配置文件中读取pom属性值
  - 在pom文件 中设定配置文件路径
  - 开启加载pom属性过滤功能
  - 使用${属性名}格式引用pom属性

## 多环境开发配置

**多环境配置**

~~~xml
<!--创建多环    在project标签下-->
<profiles>
    <!--定义具体的环境，生产环境-->
    <profile>
        <!--定义环境对应的唯一名称，名称不能重复-->
        <id>pro_env</id>
        <!--定义环境中专用的属性值-->
        <properties>
            <jdbc.url>jdbc:mysql://127.0.0.1:3306/ssm_db</jdbc.url>
        </properties>
        <!--设置默认启动-->
        <activation>
       		<activeByDefault>true</activeByDefault>
        </activation>
    </profile>
    <!--定义具体的环境，开发环境-->
    <profile>
        <id>dev_env</id>
          <properties>
            <jdbc.url>jdbc:mysql://127.2.2.2:3306/ssm_db</jdbc.url>
        </properties>
    </profile>
</profiles>
~~~

### 加载指定环境

> **作用：** 加载指定环境配置   
>
> 执行构建命令并指定加载对应环境配置信息
>
> ~~~xml
> <!--调用格式-->
> mvn 指令 –P 环境定义id
> <!--示例-->
> mvn install -p pro_env
> ~~~

## 跳过测试

### 应用场景

- 整体模块功能未开发
- 模块中某个功能未开发完毕
- 单个功能更新调试导致其他功能失败
- 快速打包
- ……



命令

~~~xml
mvn 指令 -D skipTests
~~~

**ps:**  执行的指令生命周期必须包含测试环节



**操作按钮**

![image-20220124201921414](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220124201921414.png)

~~~xml
<!--在build中的plugins中-->
<plugin>
    <artifactId>maven-surefire-plugin</artifactId>
    <version>2.22.1</version>
    <!--配置跳过测试-->
    <configuration>
        <skipTests>true</skipTests><!--设置跳过测试 -->
        <includes> <!--包含指定测试的用例-->
            <include>**/User*Test.java</include>
        </includes>
        <excludes><!--排除指定测试用例-->
       		<exclude>**/User*TestCase.java</exclude>
              <!--**是通配符 -->
        </excludes>
    </configuration>
</plugin>

~~~

## 私服（重点）

安装

**Nexus**

~~~xml
<!--启动服务器-->
nexus.exe /run nexus
<!--访问服务器 本机端口是：6060-->
http://localhost:8081
~~~

- 修改基础配置信息

  安装路径下etc目录中nexus-default.properties文件保存有nexus基础配置信息，例如默认访问端口  ，修改端口号

- 修改服务器运行配置信息

  安装路径下bin目录中nexus.vmoptions文件保存有nexus服务器启动对应的配置信息，例如默认占用内存空间

### 私服获取资源

- **宿主仓库**（自己的仓库）

  ​	保存无法从中央仓库获取的资源

  ​	自主研发

  ​	第三方非开源项目

- **代理仓库 proxy**

  ​	代理远程仓库，通过nexus访问其他公共仓库

- **仓库组group**

  ​	将若干个仓库组成一个群组，方便获取数据

  ​	仓库组不能保存资源，设计型仓库

### 资源上传

上传的信息

- 保存的位置
- 资源文件
- 对应坐标

### idea上传资源和下载资源

#### 本地仓库访问私服仓库

-  访问私服的用户名和密码

- 上传的位置（宿主地址）

  ~~~xml
  <!--配置本地仓库访问私服的权限（setting.xml）每个人都要使用里面的-->
  <servers>
      <server>
          <id>heima-release</id>
          <username>用户名</username>
          <password>密码</password>
      </server>
      <server>
          <id>heima-snapshots</id>
          <username>用户名</username>
          <password>密码</password>
      </server>
  </servers>
  <!--配置本地仓库资源来源（setting.xml）-->
  <mirrors>
      <mirror>
          <id>nexus-heima</id>
          <mirrorOf>*</mirrorOf>  <!--所有信息来源-->
          <url>http://localhost:8081/repository/maven-public/</url>  <!--这个是仓库组的地址-->
      </mirror>
  </mirrors>
  ~~~



#### 下载资源时

> -  访问私服的用户名和密码
> - 下载的仓库组地址

> - **下载的地址配置到本地地址**
> - **上传的地址配置到工程地址**

### 访问私服配置（项目工程访问私服）

标签：distributionManagement

~~~xml
<!--配置当前项目访问私服上传资源的保存位置-->
<distributionManagement>
    <!--配置release-->
    <repository>
        <id>heima-release</id>
        <url>http://localhost:8081/repository/heima-release/</url>
    </repository>
    <!--配置snapshout-->
    <snapshotRepository>
        <id>heima-snapshots</id>
        <url>http://localhost:8081/repository/heima-snapshots/</url>
    </snapshotRepository>
</distributionManagement>
~~~

#### 发布指令：deploy







