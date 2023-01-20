> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# 1. 基础篇

==达到的目标：==

- 能够创建SpringBoot工程
- 基于SpringBoot实现ssm整合

## 1.1快速入门 

SpringBoot简介

> SpringBoot设计的目的是用来==简化Spring==应用的==初始搭建==以及==开发过程==

- Spring的程序的缺点
  1. 依赖设置繁琐
  2. 配置繁琐
- SpringBoot程序优点
  1. 起步依赖（简化依赖配置）
  2. 自动配置（简化常用工程相关配置）
  3. 辅助功能（内置服务器，。。。。。。。）



### 1.1.1 idea联网版

1. 创建一个空的工程

2. 创建一个Spring  Initializer （这个就是SpringBoot 的项目创建）选择对应的需求，这里选择了spring web 

3. 新建一个controller包，里面有一个BookController类

   BookController代码如下

   ```java
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   
   //Rest模式
   @RestController
   @RequestMapping("/books")
   public class BookController {
   
       @RequestMapping
       public String getByID(){
           System.out.println("Springboot is running ....");
           return "Springboot is running,,,";
       }
   }
   ```
   

总结：

- 根据向导需要联网进行制作
- jdk8
- 对功能进行选择 打 √ 
- 运行SpringBoot 通过Application程序入口进行

### 1.1.2 官网创建

官网创建[SpringBoot](https://start.spring.io/) 

在这个页面中创建SpringBoot 项目

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220418221138765.png" alt="image-20220418221138765" style="zoom:80%;" />

会得到一个压缩包，解压完成，导入idea中进行运行项目

### 1.1.3 阿里云版

设置URL：https://start.aliyun.com  只是为了提高访问的速度，使用阿里云的服务器

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220418221907457.png" alt="image-20220418221907457" style="zoom: 80%;" />

### 1.1.4 手动创建SpringBoot项目

**不需要联网进行** 只是创建的过程，但是maven坐标 必须要手动添加进去

这里不做笔记了，大部分都会在联网的情况下进行项目

本地仓库中有了这些，就不用联网了。



### 1.1.5去除多余的文件

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220418223806311.png" alt="image-20220418223806311" style="zoom:80%;" />



## 1.2 入门案例解析



### 1.2.1parent解析

![image-20220418225829271](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220418225829271.png)



在阿里云创建中是直接使用 dependecies



总结：

1. 继承parent模块可以避免多个依赖使用相同技术时出现依赖版本冲突
2. 继承parent的形式也可以采用引入依赖的形式实现效果



### 1.2.2 starter 解析

starter就是一个包含了若干个坐标的pom文件，还有若干个starter坐标

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

1. parent
   - SpringBoot项目中要继承的项目，定义了若干个坐标版本号，以达到==减少依赖配置==的目的
2. parent
   - 所有的SpringBoot项目要继承的项目，定义了若干个坐标版本号（依赖管理，而不是依赖），以达到==减少依赖冲突==的目的
   - spring-boot-starter-parent各版本号存在着诸多坐标版本不同
3. 实际开发中
   - 使用任意坐标时，仅书写GAV中的G和A，V可以不用写，若是没有书写V，会出现报错，则需要报V写上
   - G：groupId  
   - A：artificial
   - V：version
   - GAV就是对应的坐标信息



### 1.2.3 引导类

xxx Application类

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Springboot1Application {

    public static void main(String[] args) {
        SpringApplication.run(Springboot1Application.class, args);
    }
}
```

- 引导类是Boot 的执行入口，运行main方法就可以启动项目
- 运行后会初始化Spring容器，扫描引导类所在包加载bean



###  1.2.4 内嵌tomcat 

![image-20220419153104805](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220419153104805.png)

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
        <!--排除tomcat 不需要的就把它排除掉-->
        <exclusions>
            <exclusion>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-tomcat</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

    <!--直接在dependency中添加需要的功能-->
    <!--jetty服务器-->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-jetty</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

辅助功能：

- 内嵌Tomcat服务器是Springboot辅助功能之一
- 原理：将Tomcat服务器作为对象运行，并将该对象交给Spring容器管理
- 变更内嵌服务器：去除现有的服务器，添加全新的服务器

内置服务器： 一般都是 tomcat 

- tomcat（默认）：应用面广，负载了较重的组件
- jetty ：更轻量级，负载性能远不及tomcat
- undertow ：undertow 负载性勉强跑赢tomcat



### RESTFul风格

- ==介绍：== （Representational State Transfer） 表现形式状态转换  ==访问网络资源的格式==

- 传统风格资源描述形式：


> ​	http://localhost/user/getById?id=1

- 而Rest风格描述形式：

> ​	http://localhost/user/1

显而易见，Rest风格有以下优势：

1. 隐藏资源的访问行为，无法通过地址得知对资源是哪种操作
2. 简化书写



<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220419224456014.png" alt="image-20220419224456014" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220419224604865.png" alt="image-20220419224604865" style="zoom:80%;" />

- 根据REST风格对资源进行访问称为RESTFUL


Rest风格访问资源时使用行为动作区分对资源进行了哪种操作

|           url           |        作用        |     请求方式      |
| :---------------------: | :----------------: | :---------------: |
|  http://localhost/user  | 查询全部用户的信息 |    GET（查询）    |
| http://localhost/user/1 | 查询指定用户的信息 |    GET（查询）    |
| http://localhost/users  |    添加用户信息    | POST（新增/保存） |
| http://localhost/users  |    修改用户信息    | PUT（修改/更新）  |
| http://localhost/user/1 |    删除用户信息    |  DELETE（删除）   |



> 以上的行为均为约定方式
>
> 所谓约定方式就是大家说好了的，不是规范可以打破，所以称为REST风格，而不是REST规范
>
> 描述模块的名称通常使用复数，也就是加s的格式描述，表示该类资源，而并非单个资源，例如users、books…
>
> ==根据Rest风格对资源的访问称为Restful== 

入门中的注解：

1. @RequestMapping

   - 方法注解

   - 使用在方法上的注解 

   - 作用：设置当前控制器的请求访问路径

     ```java
     @RequestMapping("/{id}", method = RequestMethod.DELETE)
     public String delete(@PathVariable int id){
         System.out.println("user delete...." + id);
         return "{'module':'user delete'}";
     }
     ```

   - 属性：

     - value ：请求的路径，

     - method：http请求动作（GET  \  POST  \  PUT \ DELETE）

2. @PathVariable

   - 形参注解

   - SpringMVC控制器形参定义前面

   - 绑定路径参数与处理器方法形参间的关系，要求路径参数名与形参名一一对应

   - ~~~java
     @RequestMapping("/{id}", method = RequestMethod.DELETE)
     public String delete(@PathVariable int id){
         System.out.println("user delete...." + id);
         return "{'module':'user delete'}";
     }
     ~~~



==REST用到的注解：==@RequestBody 、@RequestParam 、@PathVariable

1. 三者区别：
   - @RequestBody 用于接收json数据
   - @RequestParam 用户接受url地址传参或表单传参
   - @PathVariable 用于接收路径变量，使用 { 参数名称 } 描述路径参数  一个参数使用这个 

REST操作代码：

~~~java
// @Controller
// @ResponseBody
@RestController
@RequestMapping("/books")
public class bookController {

    // @RequestMapping(method = RequestMethod.POST)
    @PostMapping
    public String save(){
        System.out.println("user save....");
        return "{'module':'user save'}";
    }

    // @RequestMapping("/{id}", method = RequestMethod.DELETE)
    @DeleteMapping("/{id}")
    public String delete(@PathVariable int id){
        System.out.println("user delete...." + id);
        return "{'module':'user delete'}";
    }

    // @RequestMapping( method = RequestMethod.PUT)
    @PutMapping
    public String update(@RequestBody User user){
        System.out.println("user update...." + user);
        return "{'module':'user update'}";
    }

    // @RequestMapping(value = "/{id}", method = RequestMethod.GET)
    @GetMapping("/{id}")
    public String getById(@PathVariable int id){
        System.out.println("user getById...." + id);
        return "{'module':'user getById'}";
    }

}
~~~



## 1.3配置

==所有的配置信息都写着properties文件中==

多个SpringBoot模块开发的时候就需要进行 ==复制工程：==  就先搭建好一个环境

1. 保留工程基础结构
2. 抹掉原始工程痕迹



### 1.3.1基础配置

1. 属性配置：

   - 修改服务端口

   ![image-20220420153653107](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220420153653107.png)

   修改配置文件：application.properties,通过键值对配置对应的属性 端口设置为80

   ~~~properties
   server.port=80
   ~~~

2. 基础配置

   - 修改banner

     ```properties
     #修改 banner 就把Spring的那个logo删除掉了
     spring.main.banner-mode=off
     # 设置成图片\文本 显示
     spring.banner.image.location=text.png
     ```

   - <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220420210359088.png" alt="image-20220420210359088" style="zoom:50%;" />

   - 修改日志

     ```properties
     # 日志
     logging.level.root=info
     logging.level.root=debug
     logging.level.root=error
     ```

   - 由于使用到的配置比较多到官网查看： [配置文件](https://docs.spring.io/spring-boot/docs/current/reference/html/application-properties.html#appendix.application-properties)

3. 配置文件类型

   - application.yml （推荐）

     ```yml
     server:
       port: 81
     ```

   - application.yaml :

     ```yaml
     server:
       port: 82
     ```

   - application.proterties

     ```properties
     server.port=80
     ```

4. 配置文件的优先级：

   > properties  >>  yml  >> yaml 
   >
   > 有相同的属性，就会有加载优先级的情况出现，==但是我们开发中一般常用 yml==  
   >
   > 不同配置文件中相同配置按照加载优先级相互覆盖，不同配置文件中不同配置全部保留

   

5. 属性提示消失解决方案：

   >  好像目前的idea都不用自己配置了
   >
   > <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220420213406434.png" alt="image-20220420213406434" style="zoom:67%;" />

### 1.3.2 yaml 数据格式

YAML:是一种数据序列化格式

1. 优点
   - 容易阅读
   - 容易与脚本交互
   - 以数据为核心，重数据轻格式
2. 扩展名
   - .yml (主流)
   - yaml
3. yaml语法规则
   - 大小写敏感
   - 属性层级关系使用多行描述，每行结尾使用冒号结束
   - 使用缩进表示层级关系，同层级左侧对齐，只允许使用空格
   - 属性值前面添加空格（==属性名与属性值之间使用冒号==+空格作为分隔）
   - ‘#’ 表示注释
   - 不能重名

一系列的格式: 

~~~yaml
boolean: TRUE  						#TRUE,true,True,FALSE,false，False均可
float: 3.14    						#6.8523015e+5  #支持科学计数法
int: 123       						#0b1010_0111_0100_1010_1110    #支持二进制、八进制、十六进制
null: ~        						#使用~表示null
string: HelloWorld      			#字符串可以直接书写
string2: "Hello World"  			#可以使用双引号包裹特殊字符
date: 2018-02-17        			#日期必须使用yyyy-MM-dd格式
datetime: 2018-02-17T15:02:31+08:00  #时间和日期之间使用T连接，最后使用+代表时区

subject:         
	- Java
	- 前端
	- 大数据
	
	
enterprise:
	name: itcast
    age: 16
    subject:
    	- Java
        - 前端
        - 大数据
likes: [王者荣耀,刺激战场]			#数组书写缩略格式


users:							 #对象数组格式一
  - name: Tom
   	age: 4
  - name: Jerry
    age: 5
    
    
users:							 #对象数组格式二
  -  
    name: Tom
    age: 4
  -   
    name: Jerry
    age: 5		
    
    
users2: [ { name:Tom , age:4 } , { name:Jerry , age:5 } ]	#对象数组缩略格式


~~~

注意属性名冒号后面与数据之间有一个**空格**



### 1.3.3 yaml数据读取

以下面的方式可以获取到同样的数据

![image-20220420221947749](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220420221947749.png)

- 使用@Value配合SpEl读取单个数据
- 存在多层级就书写多层级，以此书写层级名称

1. yaml中的变量引用

   ```yml
   baseDir: c:\win10
   #使用${属性名} 引用数据
   tempDir: ${baseDir}\temp  # 输出  c:\win10\temp
   # 使用双引号 转移字符 \ 进行了转义
   tempDir2: "${baseDir}\temp \t1 \t2 \t3"  # 输出  c:\win10 emp 1   2  3
   ```

   以上的都是一个属性对应一个变量：当属性多的时候就会有很多的变量 太麻烦

2. 读取yaml的全部属性数据

   ```java
   //使用 自动装配 将所有的数据封装到一个对象Environment中
   //  使用@Autowired自动装配数据到Environment对象中
   @Autowired
   private Environment env;
   System.out.println(env.getProperty("server.port"));  // 80
   System.out.println(env.getProperty("user.name"));   // xxxname
   ```

3. 读取yaml引用类型的属性

   - 使用@ConfigurationProperties注解绑定配置信息到封装类中
   - 封装类需要定义为Spring管理的bean，否则无法进行属性注入

   yml文件：

   ```yml
   # 创建一个类 ，用于封装下面的数据
   # 由spring帮我们去加载数据到对象中，一定要告诉spring加载这组信息
   # 使用时候从spring中直接获取信息使用
   datasource:
     driver: com.mysql.jdbc.Driver
     url: jdbc:mysql://localhost/springboot_db
     username: root
     password: root666123
   ```

   创建的类：

   ```java
   //1.定义数据模型封装yaml文件中对应的数据
   //2.定义为spring管控的bean
   @Component
   //3.指定加载的数据
   @ConfigurationProperties(prefix = "datasource")
   public class MyDataSource {
       private String driver;
       private String url;
       private String username;
       private String password;
   
       @Override
       public String toString() {
           return "MyDataSource{" +
                   "driver='" + driver + '\'' +
                   ", url='" + url + '\'' +
                   ", username='" + username + '\'' +
                   ", password='" + password + '\'' +
                   '}';
       }
   
       public String getDriver() {
           return driver;
       }
   
       public void setDriver(String driver) {
           this.driver = driver;
       }
   
       public String getUrl() {
           return url;
       }
   
       public void setUrl(String url) {
           this.url = url;
       }
   
       public String getUsername() {
           return username;
       }
   
       public void setUsername(String username) {
           this.username = username;
       }
   
       public String getPassword() {
           return password;
       }
   
       public void setPassword(String password) {
           this.password = password;
       }
   }
   ```

   输出：<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220420224723229.png" alt="image-20220420224723229" style="zoom: 80%;" />

## 1.4 整合第三方技术

==整合什么技术，在创建模块时就 √ 选对应的技术集== 

三步骤：

1. 导入对应的坐标
2. 设置相关的配置
3. 使用对应的技术进行开发

### 1.4.1整合JUnit

```java
@SpringBootTest(classes = Springboot04JunitApplication.class) //防止包的位置改变造成报错，写上引导类的包名
//@ContextConfiguration(classes = Springboot04JunitApplication.class)//指定对应的配置文件或者配置类是哪一个
class Springboot04JunitApplicationTests {
    //1.注入你要测试的对象
    @Autowired
    private BookDao bookDao;
    @Test
    void contextLoads() {
        //2.执行要测试的对象对应的方法
        bookDao.save();
        System.out.println("two...");
    }
}
```

- 注解 @SpringBootTest
  - 测试类注解 ，写在测试类的上方
  - 设置JUnit加载的SpringBoot启动类

### 1.4.2整合MyBatis

- 核心配置：数据库连接相关信息
- 映射配置：SQL映射（xml/）简化



1. 设置数据源参数：

```yml
#2.配置相关信息 cj是mysql8.0以后的新加
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
    username: root
    password: 123456
```

2. 定义数据层与映射配置

   ```java
   @Mapper
   public interface BookDao {
       @Select("select * from tbl_book where id = #{id}")
       public Book getById(Integer id);
   }
   ```

3. 测试类中注入dao类

   ```java
   @SpringBootTest
   class Springboot05MybatisApplicationTests {
   
       @Autowired
       private BookDao bookDao;
   
       @Test
       void contextLoads() {
           System.out.println(bookDao.getById(11));
       }
   }
   ```

4. 降低了parent的版本就会出现 时区报错

   ​    url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC   配置时区

   ​    driver-class-name: com.mysql.cj.jdbc.Driver      驱动类过时：添加 cj 新的驱动

### 1.4.3整合MyBatis -plus

1. 使用aliyun的url
2. 只导入Mysql driver 再把M P 的坐标从官网复制导入进来



MP与MyBatis的区别：

1. 导入坐标不同
2. 数据层实现简化

1.导入坐标

```xml
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.3</version>
</dependency>
```

2.只需要继承BaseMapper<实体类>

```java
@Mapper
public interface BookDao extends BaseMapper<Book> {
}
```

3.配置文件

```yml
#设置Mp相关的配置 表的前缀
mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
```

4.测试类：

```java
@SpringBootTest
class Springboot06MybatisPlusApplicationTests {

    @Autowired
    private BookDao bookDao;

    @Test
    void contextLoads() {
        System.out.println(bookDao.selectById(2));// selectXXX的方法是提供好的
    }

    @Test
    void testGetAll() {
        System.out.println(bookDao.selectList(null));
    }

}
```

### 1.4.4整合Druid

1. 导入druid坐标

   ```xml
   <dependency>
       <groupId>com.alibaba</groupId>
       <artifactId>druid-spring-boot-starter</artifactId>
       <version>1.2.6</version>
   </dependency>
   ```

2. 设置相关的配置文件

   ```yml
   spring:
     datasource:
       druid: #druid配置信息
         driver-class-name: com.mysql.cj.jdbc.Driver
         url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
         username: root
         password: root
   ```

3. 使用druid的技术开发

   测试类：

   ```java
   @SpringBootTest
   class Springboot07DruidApplicationTests {
   
       @Autowired
       private BookDao bookDao;
       @Test
       void contextLoads() {
           System.out.println(bookDao.getById(3));
       }
   }
   ```



### 1.5 整合SSMP案例

案例分析：

1. 实体类开发——使用Lombok快速制作实体类
2. Dao开发—整合MyBatisPlus，制作数据层测试类
3. Service开发——基于MyBatisPlus进行增量开发，制作业务层测试类
4. Controller开发——基于Restful开发，使用PostMan测试接口功能
5. Controller开发—-—前后端开发协议制作
6. 页面开发——基于VUE+ElementUI制作，前后端联调，页面数据处理
   - 页面消息处理列表、新增、修改、删除、分页、查询 （CRUD）
7. 项目异常处理
8. 按条件查询——页面功能调整、Controller修正功能、Service修正功能



开发流程：

1. 模块创建 ：不缺分前后端的服务器

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220421224747067.png" alt="image-20220421224747067" style="zoom:67%;" />

   - 导入mp、druid的坐标
   - 修改端口的 80

2. 实体类创建

   - lombok：Java类库，提供一组注解，简化POJO实体类开发 先导入lombok坐标

     ```java
     /**
      * @author Kcs 2022/4/21
      */
     //lombok快速开发
     @Data
     public class Book {
         private Integer id;
         private String type;
         private String name;
         private String description;
     }
     ```

3. 数据层开发

   - MyBatisPlus
   - 数据源：Driud

   

   1. 导入MyBatisPlus和druid坐标

      ```xml
      <!--mp配置-->
      <dependency>
          <groupId>com.baomidou</groupId>
          <artifactId>mybatis-plus-boot-starter</artifactId>
          <version>3.5.1</version>
      </dependency>
      <!--druid配置-->
      <dependency>
          <groupId>com.alibaba</groupId>
          <artifactId>druid-spring-boot-starter</artifactId>
          <version>1.2.9</version>
      </dependency>
      ```

   2. 数据源配置：

      ```yml
      spring:
        datasource:
          druid: #druid配置信息
            driver-class-name: com.mysql.cj.jdbc.Driver
            url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC  #没有创建数据库
            username: root
            password: 123456
            
      mybatis-plus:
        global-config:
          db-config:
            table-prefix: tb_
      ```

   3. 接口

      ```java
      @Mapper
      public interface BookDao extends BaseMapper<Book> {
          
      }
      ```

   4. 测试

      ```java
      @SpringBootTest
      public class BookDaoTestCase {
      
          @Autowired
          private BookDao bookDao;
      
      
          @Test
          void testGetById() {
              System.out.println(bookDao.selectById(1));
          }
      
          @Test
          void testSave() {
              Book book = new Book();
              book.setType("测试1");
              book.setName("测试1");
              book.setDescription("测试111111");
              bookDao.insert(book);
          }
      
          @Test
          void testUpdate() {
              Book book = new Book();
              book.setType("测试1");
              book.setId(1);
              book.setName("测试1");
              book.setDescription("测试111111");
              bookDao.updateById(book);
          }
      
          @Test
          void testDelete() {
              bookDao.deleteById("12");
          }
      
          @Test
          void testGetAll() {
              System.out.println(bookDao.selectList(null));
      
          }
      }    
      ```

   5. MP运行日志

      

      ~~~yml
      configuration:
        log-impl: org.apache.ibatis.logging.stdout.StdOutImpl  # MP 运行日志
      ~~~

   6. 分页

      - 拦截器

   ```java
   import com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor;
   import com.baomidou.mybatisplus.extension.plugins.inner.PaginationInnerInterceptor;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   
   /**
    * @author Kcs 2022/4/22
    */
   /*
   * mp拦截器
   * */
   @Configuration
   public class MPConfig {
       @Bean
       public MybatisPlusInterceptor mybatisConfiguration(){
           //创建拦截器
           MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
           //添加分页拦截器
           interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
           return interceptor;
       }
   }
   ```

   测试：

   ```java
   @Test
       void testGetPage() {
           IPage page = new Page(1,5);
           bookDao.selectPage(page,null);
           page.getRecords();//数据
           page.getCurrent();//当前页数
           page.getSize();//每页的有多少页
           page.getTotal();//总共有多少页
       }
   ```

   7. 数据层标准开发：条件查询

      ```java
      @Test
      void testGetBy() {
          String name = "null";
          //创建QueryWrapper对象
          LambdaQueryWrapper<Book> bw = new LambdaQueryWrapper<>(); //使用lambda 就是防止自己手写 出现书写错我的字段名
          //动态拼写查询条件
          bw.like(name != null, Book::getName, "spring");//按照name进行查找 spring  
          bookDao.selectList(bw);
      }
      ```

4. 业务层开发 

   1. Service层接口定义与数据层接口定义具有较大区别，不要混用

      - selectByUserNameAndPassword (String username , String password)； 数据层
      - login(String username , String password ) ;  业务层

   2. 接口 BookService

      ```java
      import com.baomidou.mybatisplus.core.metadata.IPage;
      import com.example.ssmp.domain.Book;
      
      import java.util.List;
      
      /**
       * @author Kcs 2022/4/22
       */
      public interface BookService {
          //一些常用的方法
          Boolean save(Book book);
      
          Boolean update(Book book);
      
          Boolean delete(Integer id);
      
          Book getById(Integer id);
      
          List<Book> getAll();
      
          IPage<Book> getPage(int currentPage, int pageSize);
      }
      ```

      实现类：

      ```java
      import com.baomidou.mybatisplus.core.metadata.IPage;
      import com.baomidou.mybatisplus.extension.plugins.pagination.Page;
      import com.example.ssmp.dao.BookDao;
      import com.example.ssmp.domain.Book;
      import com.example.ssmp.service.BookService;
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Service;
      
      import java.lang.reflect.ParameterizedType;
      import java.util.List;
      
      /**
       * @author Kcs 2022/4/22
       */
      @Service
      public class BookServiceImpl implements BookService {
      
          //注入数据
          @Autowired
          private BookDao bookDao;
          @Override
          public Boolean save(Book book) {
              return bookDao.insert(book) > 0;
          }
      
          @Override
          public Boolean update(Book book) {
              return bookDao.updateById(book) > 0;
          }
      
          @Override
          public Boolean delete(Integer id) {
              return bookDao.deleteById(id) > 0;
          }
      
          @Override
          public Book getById(Integer id) {
              return bookDao.selectById(id);
          }
      
          @Override
          public List<Book> getAll() {
              return bookDao.selectList(null);
          }
      
          @Override
          public IPage<Book> getPage(int currentPage, int pageSize) {
               Page page =  new Page<>(currentPage, pageSize);
              return bookDao.selectPage(page,null);
          }
      }
      ```

      测试用例： CRUD

      ```java
      @SpringBootTest
      public class BookServiceTestCase {
      
      
          @Autowired
          private BookService bookService;
      
      
          @Test
          void testGetById() {
              System.out.println(bookService.getById(4));
          }
      
          @Test
          void testSave() {
              Book book = new Book();
              book.setType("测试1");
              book.setName("测试1");
              book.setDescription("测试111111");
              bookService.save(book);
          }
      
          @Test
          void testUpdate() {
              Book book = new Book();
              book.setType("测试1");
              book.setId(1);
              book.setName("测试1");
              book.setDescription("测试111111");
              bookService.update(book);
          }
      
          @Test
          void testDelete() {
              bookService.delete(12);
          }
      
          @Test
          void testGetAll() {
              bookService.getAll();
          }
      
          @Test
          void testGetPage() {
              IPage page = bookService.getPage(1, 45);
              page.getRecords();//记录的数
              page.getCurrent();//当前页数
              page.getSize();//每页的有多少页
              page.getTotal();//总共有多少页
          }
      }
      ```

   3. 业务逻辑快速开发（MP）

      - 接口

        ```java
        import com.baomidou.mybatisplus.extension.service.IService;
        import com.example.ssmp.domain.Book;
        
        /**
         * @author Kcs 2022/4/22
         */
        public interface IBookService extends IService<Book> {
        }
        ```

      - 接口实现类

        ```java
        //继承的serviceImpl需要两个泛型接口 数据接口  和实体类
        public class IBookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
        }
        ```

      - 测试类：

        ```java
        @SpringBootTest
        public class BookServiceTestCase {
        
        
            @Autowired
            private IBookService bookService;
        
        
            @Test
            void testGetById() {
                System.out.println(bookService.getById(4));
            }
        
            @Test
            void testSave() {
                Book book = new Book();
                book.setType("测试1");
                book.setName("测试1");
                book.setDescription("测试111111");
                bookService.save(book);
            }
        
            @Test
            void testUpdate() {
                Book book = new Book();
                book.setType("测试1");
                book.setId(1);
                book.setName("测试1");
                book.setDescription("测试111111");
                bookService.updateById(book);
            }
        
            @Test
            void testDelete() {
                bookService.removeById(12);
            }
        
            @Test
            void testGetAll() {
                bookService.list();
            }
        
            @Test
            void testGetPage() {
                IPage page = new Page<Book>(1, 2);
                bookService.page(page, null);
                page.getRecords();//记录的数
                page.getCurrent();//当前页数
                page.getSize();//每页的有多少页
                page.getTotal();//总共有多少页
            }
        }
        ```

      - 在接口的方法没有时就自定义方法

      - 接口中：（根据需要新增方法 新增方法  不能与原有的方法覆盖 ）

        ```java
        public interface IBookService extends IService<Book> {
            //若是里面没有的功能就学要手动添加
        
            boolean savebook(Book book);
        
            boolean modify(Book book);
        
            boolean delete(Integer id);
        }
        ```

      - 接口实现类中

        ```java
        //继承的serviceImpl需要两个泛型接口 数据接口  和实体类
        public class IBookServiceImpl extends ServiceImpl<BookDao, Book> implements IBookService {
        
            // 以下的方法是实现类中的方法没有时 采取自己创建的形式创建方法 
            @Autowired
            private  BookDao bookDao;
        
            @Override
            public boolean savebook(Book book) {
                return bookDao.insert(book)>0;
            }
        
            @Override
            public boolean modify(Book book) {
                return bookDao.insert(book)>0;
            }
        
            @Override
            public boolean delete(Integer id) {
                return bookDao.deleteById(id) > 0;
            }
        }
        ```

5. 表现层开发（标准开发）

   - 基于Restful进行表现层接口开发

   - 使用Postman测试表现层接口功能

     ```java
     @Controller
     @RequestMapping("/books")
     public class BookController {
     
         //注入业务层
         private IBookService bookService;
     
         //查询所有 请求方式都是GET
         //增删改查的方法的注解不一样 并且参数的请求方式也不一样 
         @GetMapping
         public List<Book> getAll(){
             return bookService.list();
         }
     
         //增
         @PostMapping
         public Boolean save(@RequestBody Book book){
             return bookService.save(book);
         }
     
         //改
         @PutMapping
         public Boolean update(@RequestBody Book book){
             return bookService.modify(book);
         }
     
         //删除
         @DeleteMapping("{id}")
         public Boolean delete(@PathVariable Integer id){
             return bookService.delete(id);
         }
     
         //根据id查询
         @GetMapping("{id}")
         public Book getById(@PathVariable Integer id){
             return bookService.getById(id);
         }
         
         @GetMapping("{currentPage}/{pageSize}")
         public IPage<Book> getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
             return bookService.getPage(currentPage, pageSize);
         }
     
     }
     ```

   - 方法的请求方式：xxxMapping

   - 新增：POST

   - 删除：DELETE

   - 修改：PUT

   - 查询：GET

   - 接收参数

   - 实体数据：@RequestBody

   - 路径变量：@PathVariable

6. 表现层一致性处理：

   - 使前端得到的数据格式一样
   - 把数据封装到 data 中 ，使用 flag 表示查询数据成功或者失败

   处理：

   ==设计表现层返回结果的模型类==，用于后端与前端进行数据格式统一，称作==前后端数据协议== 

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220423174625339.png" alt="image-20220423174625339" style="zoom:80%;" />

   ```java
   @Data
   public class R {
       private boolean flag;
       private Object data;
   
       public R() {
       }
   
       public R(Boolean flag) {
           this.flag = flag;
       }
   
       public R(Boolean flag, Object data) {
           this.flag = flag;
           this.data = data;
       }
   }
   ```

   测试代码

   ```java
   @Controller
   @RequestMapping("/books")
   public class BookController2 {
   
       //注入业务层
       private IBookService bookService;
   
       //查询所有 请求方式都是GET
       @GetMapping
       public R getAll() {
           return new R(true,bookService.list());
       }
   
       //增
       @PostMapping
       public R save(@RequestBody Book book) {
           return new R(bookService.save(book));
       }
   
       //改
       @PutMapping
       public R update(@RequestBody Book book) {
           return new R(bookService.modify(book));
       }
   
       //删除
       @DeleteMapping("{id}")
       public R delete(@PathVariable Integer id) {
           return new R(bookService.delete(id));
       }
   
       //根据id查询
       @GetMapping("{id}")
       public R getById(@PathVariable Integer id) {
           return new R(true, bookService.getById(id));
       }
   
       @GetMapping("{currentPage}/{pageSize}")
       public R getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
           return new R(true, bookService.getPage(currentPage, pageSize));
       }
   }
   ```

7. 前后端协议协调

   - 前后端分离结构设计中页面归属前端服务器

   - 单体工程中页面放在resource的static目录中（先clean）

   - created钩子函数用户初始化页面时发起调用

     axois 发送异步请求 前端发送异步请求，调用后端接口  （因为没有数据信息 会报错）

     ```js
     //列表
     getAll() {
         //发送异步请求
         axios.get("/books").then((res)=>{
             console.log(res.data);
         })
     },
     ```

8. 功能

   1. 列表功能 前端双向页面绑定 

      ```js
      //列表
      getAll() {
          //发送异步请求
          axios.get("/books").then((res)=>{
              console.log(res.data);
              this.dataList = res.data.data;//后面的data是我们前面自定义的
          })
      },
      ```

   2. 新增功能

      ```js
      //弹出添加窗口  新增页面
      handleCreate() {
          this.dialogFormVisible = true ;
          //每一次打开窗口 里面的填空要为空
          this.resetForm();
      },
      
      //重置表单
      resetForm() {
          this.formData = {};
      },
      
      //添加
      handleAdd() {
          axios.post("/books",this.formData).then((res)=>{
              //判断当前操作是否成功
              if(res.data.flag){
                  //1.关闭弹层
                  this.dialogFormVisible = false;
                  this.$message.success("添加成功");// 弹窗消息的类型 success、error 、info
              }else{
                  this.$message.error("添加失败");
              }
          }).finally(()=>{
              //2.重新刷新数据
              this.getAll();
          });
      },
      
      //取消
      cancel() {
          this.dialogFormVisible = false;
          //提示信息
          this.$message.info("当前操作取消成功！");
      },
      ```

   3. 删除功能

      - html

        ```html
        <el-table-column label="操作" align="center">
        
            <template slot-scope="scope">
        
                <el-button type="primary" size="mini" @click="handleUpdate(scope.row)">编辑</el-button>
        
                <el-button type="danger" size="mini" @click="handleDelete(scope.row)">删除</el-button>
        
            </template>
        
        </el-table-column>
        ```

      - js：请求方式delete

        ```js
        // 删除
        handleDelete(row) {
            this.$confirm("确定永久删除？", "提示", {type: "info"}).then(() => {
                axios.delete("/books" + this.id).then((res) => {
                    //判断当前操作是否成功
                    if (res.data.flag) {
                        this.$message.success("删除成功");
                    } else {
                        this.$message.error("删除失败");
                    }
                }).finally(() => {
                    //删除后，重新刷新数据 防止删除了 还留在
                    this.getAll();
                });
            }).catch(() => {
                this.$message.info("取消");
            });
        },
        ```

      - 需要传递当前数据对应的id值到后台

      - 根据操作不同，提示对应的提示信息

   4. 修改功能

      1. ```js
         //弹出编辑窗口
         handleUpdate(row) {
             axios.get("/books" + row.id).then((res) => {
                 //判断数据是否查询到
                 if (res.data.flag && res.data.data != null) {
                     this.dialogFormVisible4Edit = true;
                     this.formData = res.data.data;//后面的data是我们前面自定义的
                 } else {
                     this.$message.error("数据同步失败，3秒后刷新...");
                 }
             }).finally(() => {
                 //重新刷新数据
                 this.getAll();
             });
         },
         ```

      2. ```js
         //修改  调用put
         handleEdit() {
             axios.put("/books", this.formData).then((res) => {
                 //判断当前操作是否成功
                 if (res.data.flag) {
                     //1.关闭弹层
                     this.dialogFormVisible4Edit = false;
                     this.$message.success("修改成功");
                 } else {
                     this.$message.error("修改失败，1秒后刷新...");
                 }
             }).finally(() => {
                 //2.重新刷新数据
                 this.getAll();
             });
         },
         ```

      3. 取消添加和修改：

      4. ```js
         //取消
         cancel() {
             this.dialogFormVisible = false;
             this.dialogFormVisible4Edit = false;
             //提示信息
             this.$message.info("当前操作取消成功！");
         },
         ```

   5. 分页功能

      - 使用el分页组件
      - 定义分页组件绑定的数据模型
      - 异步调用获取分页数据
      - 分页数据页面显示

      - ```html
        <!--分页组件-->
        <div class="pagination-container">
            <el-pagination
                    class="pagiantion"
                           
                    @current-change="handleCurrentChange"
                           
                    :current-page="pagination.currentPage"
        
                    :page-size="pagination.pageSize"
        
                    layout="total, prev, pager, next, jumper"
        
                    :total="pagination.total">
        
            </el-pagination>
        
        </div>
        ```

      - 数据模型：

        ```js
        pagination: {//分页相关模型数据
            currentPage: 1,//当前页码
            pageSize: 10,//每页显示的记录数
            total: 0//总记录数
        }
        ```

      - ```js
        //分页查询
        getAll() {
            //发送异步请求
            axios.get("/books/"+this.pagination.currentPage +"/"+ this.pagination.pageSize).then((res) => {
                this.pagination.pageSize = res.data.size;//显示的有多少条数据
                this.pagination.currentPage = res.data.current;//当前页
                this.pagination.total = res.data.total;//总数
                this.dataList = res.data.records;
        
            });
        },
        
        //切换页码
        handleCurrentChange(currentPage) {
            //修改页码值为当前选中的页码值
            this.pagination.currentPage = currentPage;
            // 执行查询
            this.getAll();
        },
        ```

      - 修改存在的bug 在controller中   ==基于业务需求维护删除功能==  不能照搬

        ```java
        @GetMapping("{currentPage}/{pageSize}")
        public R getPage(@PathVariable int currentPage, @PathVariable int pageSize) {
            IPage<Book> page = bookService.getPage(currentPage, pageSize);
            // 如果当前页码值大于总页码值，就重新执行查询操作，使用最大页码值作为当前页码值
            if (currentPage > page.getPages()) {
                bookService.getPage((int) page.getPages(), pageSize);
            }
            return new R(true, page);
        }
        ```

        

   6. 条件查询

      - 数据封装 与当前页码值

        ```js
        pagination: {//分页相关模型数据
            currentPage: 1,//当前页码
            pageSize: 10,//每页显示的记录数
            total: 0,//总记录数
            type: "",
            name: "",
            description: ""
        }
        ```

      - 页面数据模型绑定

        ```html
        <div class="filter-container">
            <el-input placeholder="图书类别" v-model="pagination.type" style="width: 200px;"
                      class="filter-item"></el-input>
            <el-input placeholder="图书名称" v-model="pagination.name" style="width: 200px;"
                      class="filter-item"></el-input>
            <el-input placeholder="图书描述" v-model="pagination.description" style="width: 200px;"
                      class="filter-item"></el-input>
            <el-button @click="getAll()" class="dalfBut">查询</el-button>
            <el-button type="primary" class="butT" @click="handleCreate()">新建</el-button>
        </div>
        ```

      - 组织数据get请求发送数据

        ```js
        getAll() {
            //组织参数，拼接url请求地址
            //有可能填写的为空 就写一个 param = "?q"; 就会把后面查找显示为null
            param = "?type=" + this.pagination.type;
            param += "&name=" + this.pagination.name;
            param += "&description=" + this.pagination.description;
        
            // console.log(param);
            //
        
            //发送异步请求
            axios.get("/books/" + this.pagination.currentPage + "/" + this.pagination.pageSize + param).then((res) => {
                this.pagination.pageSize = res.data.size;//后面的data是我们前面自定义的
                this.pagination.currentPage = res.data.current;//后面的data是我们前面自定义的
                this.pagination.total = res.data.total;//后面的data是我们前面自定义的
                this.dataList = res.data.records;//后面的data是我们前面自定义的
        
            });
        },
        ```

      - Controller接收参数 调用业务层分页条件查询接口

        ```java
        @GetMapping("{currentPage}/{pageSize}")
        public R getPage(@PathVariable int currentPage, @PathVariable int pageSize, Book book) {
        
            IPage<Book> page = bookService.getPage(currentPage, pageSize,book);
            // 如果当前页码值大于总页码值，就重新执行查询操作，使用最大页码值作为当前页码值
            if (currentPage > page.getPages()) {
                bookService.getPage((int) page.getPages(), pageSize,book);
            }
            return new R(true, page);
        }
        ```

      - 添加一个接口方法getpage

        ```java
        IPage<Book> getPage(int currentPage, int pageSize, Book book);
        ```

      - IBookServiceImpl实现类中

        ```java
        @Override
        public IPage<Book> getPage(int currentPage, int pageSize, Book book) {
            LambdaQueryWrapper<Book> lqw = new LambdaQueryWrapper<Book>();
            //条件的组织
            lqw.like(Strings.isNotEmpty(book.getType()),Book::getType,book.getType());
            lqw.like(Strings.isNotEmpty(book.getName()),Book::getName,book.getName());
            lqw.like(Strings.isNotEmpty(book.getDescription()),Book::getType,book.getDescription());
        
            IPage page = new Page<>();
            bookDao.selectPage(page,null);
            return page;
        }
        ```

9. 异常消息处理

   - 后台的bug导致数据格式不一样

     ![image-20220423232337862](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220423232337862.png)

   - 对异常统一处理 出现异常，返回指定的消息 ， 异常处理器必须被扫描加载，否则无法生效

     ```java
     //作为SpringMVC的异常处理器
     @RestControllerAdvice
     public class ProjecExceptionAdvice {
     
         //拦截所有的异常信息  方法
         @ExceptionHandler(Exception.class)
         public R doException(Exception exception) {
             //记录日志
             //通知运维
             //通知开发
             exception.printStackTrace();//异常信息
             //返回的异常内容，是给前端查看异常的内容是什么
             return new R( "服务器故障！！，请稍后再试！");
         }
     }
     ```

   - 添加时异常 全部把消息在后台管理   ==目的：国际化==

     ```js
     //增
     @PostMapping
     public R save(@RequestBody Book book) throws IOException {
         //添加时的异常
         if (book.getName().equals("123")) {
             throw new IOException();
         }
         boolean flag = bookService.save(book);
         return new R(flag ,flag ? "添加成功^_^":"添加失败-_-!");
     }
     ```



**ssmp整合总结**

- 1 - 7 就是后端的内容
- 8 是前端的内容 也是最耗费时间的

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220424182531841.png" alt="image-20220424182531841" style="zoom:80%;" />

# 2. 实用篇



## 2.1 运维实用篇

==达到的目标== :

1. 能够掌握SpringBoot程序多环境开发
2. 能够基于Linux系统发布SpringBoot工程
3. 能够解决线上灵活配置SpringBoot工程的需求

### 2.1.1打包与运行

- 程序打包：先执行clean一下，确保程序的比较干净的  

- 再进行package产生一个jar包

  ![image-20220424221825737](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220424221825737.png)

- 在jar包的文件目录下 进入cmd 执行 命令 java -jar 工程名称



打包插件： 打包成的是jar包

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

==查看端口占用指令：==

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220424223712446.png" alt="image-20220424223712446" style="zoom:67%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220424223859987.png" alt="image-20220424223859987" style="zoom:80%;" />

```java
public static void main(String[] args) {
   // SpringApplication.run(SsmpApplication.class, args);
   // 可以在启动boot程序时断开读取外部临时配置对应的入口，也就是去掉读取外部参数的形参
   // 以下的是为了安全的访问
   SpringApplication.run(SsmpApplication.class);
}
```

### 2.1.2配置高级

4级分类：

1. <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425214617476.png" alt="image-20220425214617476" style="zoom: 67%;" /><img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425214827061.png" alt="image-20220425214827061" style="zoom: 67%;" />
2. 作用：
   - 1级与2级留做系统打包后设置通用属性，1级常用于==运维经理==进行线上整体项目部署方案调控
   - 3级与4级用于==系统开发阶段==设置通用属性，3级常用于==项目经理==进行整体项目属性调控

自定义配置文件：

![image-20220425215710220](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425215710220.png)

![image-20220425215723613](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425215723613.png)

### 2.1.3多环境开发





1. Yaml版

   ```yaml
   # 应用环境
   # 公共配置
   spring:
     profiles:
       active: dev   #设置启动环境
   ---
   # 设置环境
   # 生产环境
   spring:
     profiles: pro   #环境名称
   server:
     port: 80
   ---
   # 开发环境
   spring:
     profiles: dev        
   server:
     port: 81    
   ---
   # 测试环境
   spring:
     config:
       activate:
         on-profile: test  # 不过时的格式
   server:
     port: 82
   ```

   ==用分割线 --- 进行分割，上面的是公共配置，引用下面定义的生产环境、开发环境、测试环境==  

   - 把文件进行拆分：

     ![image-20220425221655514](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425221655514.png)

     主文件中：设置公共配置 ==调用 test文件的  就是 application “-” 后面的名称==

     ```yaml
     # 应用环境
     spring:
       profiles:
         active: test  
     ```

     环境中配置：设置为冲突的配置

2. properties多文件配置

   - ![image-20220425222317835](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425222317835.png)

   - 主文件中：调用和yaml 的格式一样

     ```properties
     spring.profiles.active=dev  
     ```

3. 多环境开发独立配置文件技巧（分组管理）：

   1. 根据功能对配置文件进行拆分，制作成独立的配置文件

      <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220425222855527.png" alt="image-20220425222855527" style="zoom:50%;" />

   2. 使用include属性在激活指定环境的情况下，同时对多个环境进行加载使其生效，多个环境间使用逗号分隔

      ```yml
      spring:
        profiles:
          active: dev  #若需启动dev这个环境，就必须要使用include把相关的也要包括进来：devDB，devMVC ，才能根据对应的路径进行访问 这个是最后才启动的配置，不管include中的那个先后，最终都是执行主文件中的配置信息
          include: devDB,devMVC
      ```

   3. 使用group组

      ```yml
      spring:
        profiles:
          active: dev
          group:
            "dev": devDB,devMVC
            "pro": devDB,proMVC
      ```

   4. 多环境开发控制

      - 导入坐标

        ```xml
        <!--设置多环境-->
        <profiles>
            <profile>
                <id>env_dev</id>
                <properties>
                    <profile.active>dev</profile.active>
                </properties>
                <activation>
                    <activeByDefault>true</activeByDefault>
                </activation>
            </profile>
            <profile>
                <id>env_pro</id>
                <properties>
                    <profile.active>pro</profile.active>
                </properties>
            </profile>
            <profile>
                <id>env_test</id>
                <properties>
                   <profile.active>test</profile.active>
                </properties>
                </profile>
        </profiles>
        ```

      - yml

        ```yaml
        spring:
          profiles:
            active: @profile.active@  # 引用变量值
            group:
              "dev": devDB,devMVC
              "pro": devDB,proMVC
        
        ```

   



### 2.1.4日志

#### 1.日志基础操作

**日志作用：**

1. 编程期调试代码
2. 运营期记录信息
   - 记录日常运营重要信息（峰值流量、平均响应时长···）
   - 记录应用报错信息（错误堆栈）
   - 记录运维过程数据（扩容、宕机、报警····）

导入坐标

```xml
<!--导入日志坐标-->
<dependency>
   <groupId>org.projectlombok</groupId>
   <artifactId>lombok</artifactId>
</dependency>
```

```java
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

//Rest模式
@RestController
@RequestMapping("/books")
public class BookController {
    //麻烦的日志，每个类都要写一句
        private static  final Logger getLog = LoggerFactory.getLogger(BookController.class);
    @GetMapping
    public String getById(){
        //日志级别
        log.debug("debug...");
        log.info("info...");
        log.warn("warn...");
        log.error("error...");
        return "springboot is running...2";
    }
}
```

简化的日志创建形式：==使用日志注解== :  @ Slf4j

```java
import lombok.extern.slf4j.Slf4j;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

//日志注解
@Slf4j
//Rest模式
@RestController
@RequestMapping("/books")
public class BookController {
    @GetMapping
    public String getById(){
        //日志级别
        log.debug("debug...");
        log.info("info...");
        log.warn("warn...");
        log.error("error...");
        return "springboot is running...2";
    }
}
```



日志级别：

- TRACE:运行堆栈信息，使用率低
- ==DEBUG:程序员调试代码使用==
- ==INF:记录运维过程数据==
- ==WARN:记录运维过程报警数据==
- ==ERROR:记录错误堆栈信息==
- FATAL:灾难信息，合并计入ERROR

配置文件里面的配置：

```yaml
# debug: true

logging:
  # 设置分组
  group:
    ebank: com.itheima.controller,com.itheima.service,com.itheima.dao # 把这些包放到到一个iservice包中
    iservice: com.alibaba
  level:
    root: info  # 根路径的日志级别
    # 设置某个包的日志级别  累活（不建议）
#    com.itheima.controller: debug
    # 设置分组，对某个组设置日志级别
    ebank: warn
```

#### 2.日志输出格式

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426212420616.png" alt="image-20220426212420616" style="zoom:67%;" />



设置日志输出格式控制：

```yaml
  # 设置日志模板格式
  pattern:
#    console: "%d - %m %n"
    console: "%d %clr(%5p) --- [%16t] %clr(%-40.40c){cyan} : %m %n"
```

- %d：日期
- %m：消息
- %n：换行
- %clr ：彩色标注   %clr(%5p) ：对日志级别的添加颜色
- %p：日志的级别    ==%5p：宽度为： 占位符5位==
- [%16t] ：线程名称 16个空格
- %clr(%-40.40c) ：类名 添加颜色 ， 左对齐：-40，左删除处理 .40 ，
- {cyan} ：设置颜色 青色，系统内置的颜色  大概有6个

#### 3.日志文件

生成日志文件：

```yaml
file:
  name: server.log  #日志名称
logback:
  rollingpolicy:  # 滚动的日志文件
    max-file-size: 4KB  #日志大小 超过这个大小，就会创建新的文件
    file-name-pattern: server.%d{yyyy-MM-dd}.%i.log  #创建日志文件的模板 %d：时间格式；%i ：第几个文件
```

## 2.2 实用开发篇

==达到的目标== :

1. 能够基于SpringBoot整合任意第三方技术

### 2.2.1热部署

==不需要重启服务器，修改之后就能立刻显示修改的内容==

####   1 手动启动热部署

导入坐标：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
</dependency>
```

激活热部署  ctrl  +  F9

![image-20220426220627404](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426220627404.png)

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426221000746.png" alt="image-20220426221000746" style="zoom:67%;" />

- 热部署:只有重启,只加载资源文件等,耗时更短 
- 重启:重启+重载,加载资源文件和jar包,耗时更长

####  2 自动启动热部署

<img src="SpringBoot2.assets/image-20220426221533519.png" alt="image-20220426221533519" style="zoom:80%;" />

<img src="SpringBoot2.assets/image-20220426221926390.png" alt="image-20220426221926390" style="zoom:80%;" />

![image-20220426221659716](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426221659716.png)

几秒后就会自动启动热部署

####  3 热部署范围配置

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426222519853.png" alt="image-20220426222519853" style="zoom:67%;" />

```YAML
  devtools:
    restart:
      # 设置不参与热部署的文件或文件夹
      exclude: static/**,public/**,config/application.yml
```

#### 4 关闭热部署

```YAML
enabled: false
```

- true ：可以关闭热部署
- false ：不可以关闭热部署

在Application类中：彻底关闭热部署  在配置文件中的enable ：false就可以不用写

```java
@SpringBootApplication
public class SSMPApplication {
    public static void main(String[] args) {
        System.setProperty("spring.devtools.restart.enabled","false");
        SpringApplication.run(SSMPApplication.class);
    }
}
```

![image-20220426223437613](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426223437613.png)

### 2.2.2配置高级

- @ConfigurationProperties 第三方bean

  在Application类中

  ```java
  import com.alibaba.druid.pool.DruidDataSource;
  import config.ServerConfig;
  import org.springframework.boot.SpringApplication;
  import org.springframework.boot.autoconfigure.SpringBootApplication;
  import org.springframework.boot.context.properties.ConfigurationProperties;
  import org.springframework.boot.context.properties.EnableConfigurationProperties;
  import org.springframework.context.ConfigurableApplicationContext;
  import org.springframework.context.annotation.Bean;
  
  @SpringBootApplication
  @EnableConfigurationProperties(ServerConfig.class)
  public class Springboot13ConfigurationApplication {
  
      //第三方bean
      @Bean
      @ConfigurationProperties(prefix = "dataSource")
      public DruidDataSource datasource(){
          DruidDataSource ds = new DruidDataSource();
  //        ds.setDriverClassName("com.mysql.jdbc.Driver123");
          return ds;
      }
  
      public static void main(String[] args) {
          ConfigurableApplicationContext ctx = SpringApplication.run(Springboot13ConfigurationApplication.class, args);
          ServerConfig bean = ctx.getBean(ServerConfig.class);
          System.out.println(bean);
          DruidDataSource ds = ctx.getBean(DruidDataSource.class);
          System.out.println(ds.getDriverClassName());
      }
  
  }
  ```

  - @EnableConfigurationProperties注解可以将使用@ConfigurationProperties注解对应的类加入spring容器

  - @EnableConfigurationProperties与@Component不能同时存在

  会出现的报错

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220426225547839.png" alt="image-20220426225547839" style="zoom:80%;" />

  

1. 宽松绑定/松散绑定

==使用@ConfigurationProperties绑定属性时，支持属性名称宽松绑定==

配置文件application.yml   中、下划线 都会忽略，大小写都可以被匹配到

```yml
servers:
#  ipAddress: 192.168.0.2       # \u9A7C\u5CF0
#  ipaddress: 192.168.0.2
#  ip_address: 192.168.0.2      # unline
  ip-address: 192.168.0.2       #  烤肉串模式 0-0-0-0---------
#  IPADDRESS: 192.168.0.2
#  IP_ADDRESS: 192.168.0.2      # 常量模式
#  IP_ADD_R-E_SS: 192.168.0.2
```

注意事项：

- ==宽松绑定不支持注解@value引用单个属性的方式==
- 绑定前缀名命名规：仅能使用纯小写字母、数字、下划线作为合法的字符
- prefix里面是小写字母，中划线



1. 常用计量单位绑定

   在实体类中：

   ```java
       @DurationUnit(ChronoUnit.HOURS) //jdk8以后规定超时的  时间范围单位 
       private Duration serverTimeOut;
   //    @DataSizeUnit(DataUnit.MEGABYTES) 存储容量大小
       private DataSize dataSize;
   ```

   配置文件：

   ```yml
   timeout: -1
   serverTimeOut: 3
   dataSize: 10MB
   ```

   

2. bean数据校验

   提高系统安全性

   - 导入坐标

     ```xml
     <!--1.导入JSR303规范   -->
     <dependency>
         <groupId>javax.validation</groupId>
         <artifactId>validation-api</artifactId>
     </dependency>
      <!--使用hibernate框架提供的校验器做实现类-->
     <dependency>
         <groupId>org.hibernate.validator</groupId>
         <artifactId>hibernate-validator</artifactId>
     </dependency>
     
     ```

   - 设置规则 在config实体类中

     ```java
     @Data
     @ConfigurationProperties(prefix = "servers")
     //2.开启对当前bean的属性注入校验 使用注解
     @Validated
     public class ServerConfig {
         private String ipAddress;
         //3.设置具体的规则  给prot设置的值
         @Max(value = 8888,message = "最大值不能超过100")
         @Min(value = 202,message = "最小值不能低于0")
         private int port;
         private long timeout;
         @DurationUnit(ChronoUnit.HOURS) //jdk8以后规定超时的时间单位
         private Duration serverTimeOut;
         private DataSize dataSize;
         private Host host;
     }
     ```

3. 进制数据转换规则

   - 配置文件中：

     ```yml
     datasource:
       driverClassName: com.mysql.jdbc.Driver789
       password: 0127
     ```

     ==输出是 87，就是进制转换的结果==     0 开头是八进制  ，转换成了87十进制的东西 。使用双引号包起来

     <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220502170036158.png" alt="image-20220502170036158" style="zoom: 67%;" />

### 2.2.3测试

#### 1.加载测试专用属性

==在启动测试环境时可以通过properties参数设置测试环境专用的属性== 

- 好处：比多环境开发中的测试环境影响范围小，仅对当前测试类有效

```java
//第一种：properties属性可以为当前测试用例添加临时的属性配置
@SpringBootTest(properties = {"test.prop=testValue1"})

//第二种: args属性可以为当前测试用例添加临时的命令行参数
@SpringBootTest(args={"--test.prop=testValue2"})

//上面两种同时使用  后者的级别高，args会覆盖掉前面的properties的内容
@SpringBootTest(properties = {"test.prop=testValue1"},args={"--test.prop=testValue2"})
public class PropertiesAndArgsTest {

    @Value("${test.prop}")
    private String msg;

    @Test
    void testProperties(){
        System.out.println(msg);
    }
}
```

properties临时配置属性：

```yaml
test:
  prop: testValue
```

#### 2.加载测试专用配置

config类

```java
@Configuration
public class MsgConfig {

    @Bean
    public String msg(){
        return "bean msg";
    }
}
```

config测试类 MsgConfig 类上不加 @Configuration 注解，才需要 @Import

```java
@SpringBootTest
// @Import({MsgConfig.class})
public class ConfigurationTest {

    //自动注入
    @Autowired
    private String msg;

    @Test
    void testConfiguration(){
        System.out.println(msg);
    }
}
```

#### 3.web环境模拟测试

模拟端口：

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class WebTest {

    @Test
    void testRandomPort(){
    }
}    
```

![image-20220502201341259](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220502201341259.png)

BookController：

```java
@RestController
@RequestMapping("/books")
public class BookController {

@GetMapping
 public String getById(){
       System.out.println("getById is running .....");
       return "springboot";
  }
}
```



webTest：

```java
//虚拟环境
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
//开启虚拟MVC调用
@AutoConfigureMockMvc
public class WebTest {

    @Test
    void testRandomPort() {
    }

    @Test
    void testWeb(@Autowired MockMvc mvc) throws Exception {
        // 调用：http://localhost:8080/books
        //创建虚拟请求get()，当前访问/books
        MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
        //执行对应的请求
        mvc.perform(builder);
    }
}
```



1.通过匹配响应执行状态  

```java
@Test
void testStatus(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    //设定预期值 与真实值进行比较，成功测试通过，失败测试失败
    //定义本次调用的预期值
    StatusResultMatchers status = MockMvcResultMatchers.status();
    //预计本次调用时成功的：状态200
    ResultMatcher ok = status.isOk();
    //添加预计值到本次调用过程中进行匹配
    action.andExpect(ok);
}
```

2.匹配响应体

```java
/*
* 匹配响应体
* */
@Test
void testBody(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    //设定预期值 与真实值进行比较，成功测试通过，失败测试失败
    //定义本次调用的预期值
    ContentResultMatchers content = MockMvcResultMatchers.content();
    ResultMatcher result = content.string("springboot2");
    //添加预计值到本次调用过程中进行匹配
    action.andExpect(result);

}
```

测试形式：![image-20220502203830606](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220502203830606.png)

3.匹配json

```java
@RestController
@RequestMapping("/books")
public class BookController {
    @GetMapping
    public Book getById(){
        System.out.println("getById is running .....");
        //模拟的数据，写死
        Book book = new Book();
        book.setId(1);
        book.setName("springboot");
        book.setType("springboot");
        book.setDescription("springboot");
        return book;
    }
}
```

测试：

```java
/*
* json匹配
* */
@Test
void testJson(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    //设定预期值 与真实值进行比较，成功测试通过，失败测试失败
    //定义本次调用的预期值
    ContentResultMatchers content = MockMvcResultMatchers.content();
    ResultMatcher result = content.json("{\"id\":1,\"name\":\"springboot2\",\"type\":\"springboot\",\"description\":\"springboot\"}");
    //添加预计值到本次调用过程中进行匹配
    action.andExpect(result);
}
```

报错形式：![image-20220502204711944](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220502204711944.png)



匹配响应头：

```java
/*
* 匹配响应头
* */
@Test
void testContentType(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);
    //设定预期值 与真实值进行比较，成功测试通过，失败测试失败
    //定义本次调用的预期值
    HeaderResultMatchers header = MockMvcResultMatchers.header();
    ResultMatcher contentType = header.string("Content-Type", "application/json");
    //添加预计值到本次调用过程中进行匹配
    action.andExpect(contentType);
}
```



实际开发的书写形式中：把多个匹配关系写道一个方法中

```java
@Test
void testGetById(@Autowired MockMvc mvc) throws Exception {
    MockHttpServletRequestBuilder builder = MockMvcRequestBuilders.get("/books");
    ResultActions action = mvc.perform(builder);

    //以下三个是并行关系 断言
    
    StatusResultMatchers status = MockMvcResultMatchers.status();
    ResultMatcher ok = status.isOk();
    action.andExpect(ok);

    HeaderResultMatchers header = MockMvcResultMatchers.header();
    ResultMatcher contentType = header.string("Content-Type", "application/json");
    action.andExpect(contentType);

    ContentResultMatchers content = MockMvcResultMatchers.content();
    ResultMatcher result = content.json("{\"id\":1,\"name\":\"springboot\",\"type\":\"springboot\",\"description\":\"springboot\"}");
    action.andExpect(result);
}
```

#### 4.业务层测试事务回滚

```java
@SpringBootTest
//不提交到数据库，但是能执行。就不会把不要的数据保留下来
@Transactional
//测试用例中，提交事务，回滚事务
@Rollback(true)
public class DaoTest {

    @Autowired
    private BookService bookService;

    @Test
    void testSave(){
        Book book = new Book();
        book.setName("springboot3");
        book.setType("springboot3");
        book.setDescription("springboot3");
        bookService.save(book);
    }
}
```



#### 5.测试用例数据设定 设置随机数据

application.yml

```yaml
testcase:
  book:
    id: ${random.int}
    id2: ${random.int(10)} #10以内的整数
    type: ${random.int(5,10)}5~10以内的 开始结束符号不唯一：[1,5] !1,5! 等
    name: ${random.value}
    uuid: ${random.uuid}
    publishTime: ${random.long}
```

```java
package com.itheima.testcase.domain;

import lombok.Data;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@Data
@ConfigurationProperties(prefix = "testcase.book")
public class BookCase {
    private int id;
    private int id2;
    private int type;
    private String name;
    private String uuid;
    private long publishTime;
}
```

### 2.2.4数据层解决方案

先用数据层解决方案选型：

Druid + MyBatis Plus + MySQL

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503152837907.png" alt="image-20220503152837907" style="zoom:50%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503163354913.png" alt="image-20220503163354913" style="zoom:67%;" />



#### 1.SQL

1.内置数据源

- Springboot提供三种内嵌的数据源对象
  - HikariCP：默认内置数据源对象
  - Tomcat提供DataSource： HikariCP不可用的情况下，且在web环境中，将使用tomcat服务器配置的数据源对象
  - Commons DBCP：Hikari不可用，tomcat数据源也不可用，将使用dbcp数据源

==HiKariCP 的 yml配置文件==

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
    hikari:
      driver-class-name: com.mysql.cj.jdbc.Driver
      username: root
      password: 123456
      maximum-pool-size: 50
```

==默认持久化技术：  jdbcTemplate==  （用的比较少）

导入坐标：

```xml
<!--演示JdbcTemplate-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
</dependency>
<!--操作数据库的模板对象-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```

查询

```java
	/*
    * 查询数据
    * */
    @Test
    void testJdbcTemplate(@Autowired JdbcTemplate jdbcTemplate){

        String sql = "select * from tbl_book";
//        List<Map<String, Object>> maps = jdbcTemplate.queryForList(sql);
//        System.out.println(maps);
        //行映射
        RowMapper<Book> rm = new RowMapper<Book>() {
            @Override
            public Book mapRow(ResultSet rs, int rowNum) throws SQLException {
                Book temp = new Book();
                temp.setId(rs.getInt("id"));
                temp.setName(rs.getString("name"));
                temp.setType(rs.getString("type"));
                temp.setDescription(rs.getString("description"));
                return temp;
            }
        };
        List<Book> list = jdbcTemplate.query(sql, rm);
        System.out.println(list);
    }
```

插入（增）：

```java
/*
* 插入数据
* */
@Test
void testJdbcTemplateSave(@Autowired JdbcTemplate jdbcTemplate){
    String sql = "insert into tbl_book values(3,'springboot1','springboot2','springboot3')";
    jdbcTemplate.update(sql);
}
```

内置数据库：

- H2：
- HSQL：
- Derby：

H2数据库

导入坐标

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
</dependency>
```

设置当前项目为web工程，并配置H2管理控制台参数

```yaml
server:
  port: 80
spring:
  h2:
    console:
      enabled: true  #开启控制台  上线必须关闭
      path: /h2
      
datasource:
    url: jdbc:h2:~/test
    hikari:
#      driver-class-name: org.h2.Driver
      username: sa
      password: 123456

mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
      id-type: auto
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```

![image-20220503162650569](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503162650569.png)

#### 2.NoSQL

常用的NoSQL解决方案：

- Redis  ：
- Mongo ：
- ES：

简单了解上述的NoSQL

##### 1.Redis 

是一款key-value存储结构的==内存级NoSQL数据库==

- 支持多种数据存储格式
- 支持持久化
- 支持集群

安装成功的界面：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503170315743.png" alt="image-20220503170315743" style="zoom: 80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503170614593.png" alt="image-20220503170614593" style="zoom:80%;" />

![image-20220503170937805](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503170937805.png)

**Springboot整合Redis**

1.导入坐标jar包

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

配置对应的内容

```yml
spring:
  redis:
    host: localhost 
    port: 6379 #以上4行可以去掉，默认就是这个
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220503172535952.png" alt="image-20220503172535952" style="zoom:80%;" />

测试类：

```java
@SpringBootTest
class Springboot16RedisApplicationTests {

    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    void set() {
        ValueOperations ops = redisTemplate.opsForValue();
        ops.set("age",41);
    }

    @Test
    void get() {
        ValueOperations ops = redisTemplate.opsForValue();
        Object age = ops.get("name");
        System.out.println(age);
    }

    //hash值   key value
    @Test
    void hset() {
        HashOperations ops = redisTemplate.opsForHash();
        ops.put("info","b","bb");
    }

    @Test
    void hget() {
        HashOperations ops = redisTemplate.opsForHash();
        Object val = ops.get("info", "b");
        System.out.println(val);
    }
}
```

==解决在Java中set和dos窗口不同步==

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.core.StringRedisTemplate;
import org.springframework.data.redis.core.ValueOperations;

@SpringBootTest
public class StringRedisTemplateTest {

    @Autowired
    private StringRedisTemplate stringRedisTemplate;

    @Test
    void get(){
        ValueOperations<String, String> ops = stringRedisTemplate.opsForValue();
        String name = ops.get("name");
        System.out.println(name);
    }
}
```

这样子，在java中设置的也能在dos窗口中查看，在dos窗口中set值也能在java中查看，实现了同步功能。



==redis实现客户端技术切换功能==

导入jedis坐标

```xml
<dependency>
    <groupId>redis.clients</groupId>
    <artifactId>jedis</artifactId>
</dependency>
```

配置jedis

```yaml
spring:
  redis:
    host: localhost
    port: 6379
    #以下的jedis
    client-type: jedis #避免风险
    lettuce:
      pool:
        max-active: 16
    jedis:
      pool:
        max-active: 16
```

- lettcus与jedis区别

  - jedis连接Redis服务器是直连模式，当多线程模式下使用jedis会存在线程安全问题，解决方案可以通过配置连接池使每个连接专用，这样整体性能就大受影响。

  - lettcus基于Netty框架进行与Redis服务器连接，底层设计中采用StatefulRedisConnection。StatefulRedisConnection自身是线程安全的，可以保障并发访问安全问题，所以一个连接可以被多线程复用。当然lettcus也支持多连接实例一起工作。
  - 默认是lettcus。

##### 2.MongoDB

- MongoDB是一个开源、高性能、无模式的文档型数据库。是最新关系数据库的非关系数据库

导入坐标：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-mongodb</artifactId>
</dependency>
```

yml配置文件

```yml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/itheima
      # uri 是写数据库名称的路径
```

创建了一个Book实体对象

```java
@SpringBootTest
class Springboot17MongodbApplicationTests {
    @Autowired
    private MongoTemplate mongoTemplate;
    
    //新增
    @Test
    void contextLoads() {
        Book book = new Book();
        book.setId(2);
        book.setName("springboot2");
        book.setType("springboot2");
        book.setDescription("springboot2");

        mongoTemplate.save(book);
    }
    //查询
    @Test
    void find(){
        List<Book> all = mongoTemplate.findAll(Book.class);
        System.out.println(all);
    }
}
```

##### 3.ES

- Elasticsearch分布式全文搜索引擎  
- ik分词器  
- 倒排索引 ： 数据得到 id
- 创建文档：
- 使用文档：加速搜索

索引操作（略过）

配置文件：

```yml
spring:
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/ssm_db?serverTimezone=UTC
      username: root
      password: 123456
#  elasticsearch:
#    rest:
#      uris: http://localhost:9200

mybatis-plus:
  global-config:
    db-config:
      table-prefix: tbl_
      id-type: auto
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
```



```java
@SpringBootTest
class Springboot18EsApplicationTests {

    @Autowired
    private BookDao bookDao;

//    @Autowired
//    private ElasticsearchRestTemplate template;


    @BeforeEach
    void setUp() {
        HttpHost host = HttpHost.create("http://localhost:9200");
        RestClientBuilder builder = RestClient.builder(host);
        client = new RestHighLevelClient(builder);
    }

    @AfterEach
    void tearDown() throws IOException {
        client.close();
    }

    private RestHighLevelClient client;

//    @Test
//    void testCreateClient() throws IOException {
//        HttpHost host = HttpHost.create("http://localhost:9200");
//        RestClientBuilder builder = RestClient.builder(host);
//        client = new RestHighLevelClient(builder);
//
//        client.close();
//    }

    @Test
    void testCreateIndex() throws IOException {
        CreateIndexRequest request = new CreateIndexRequest("books");
        client.indices().create(request, RequestOptions.DEFAULT);
    }

    @Test
    void testCreateIndexByIK() throws IOException {
        CreateIndexRequest request = new CreateIndexRequest("books");
        String json = "{\n" +
                "    \"mappings\":{\n" +
                "        \"properties\":{\n" +
                "            \"id\":{\n" +
                "                \"type\":\"keyword\"\n" +
                "            },\n" +
                "            \"name\":{\n" +
                "                \"type\":\"text\",\n" +
                "                \"analyzer\":\"ik_max_word\",\n" +
                "                \"copy_to\":\"all\"\n" +
                "            },\n" +
                "            \"type\":{\n" +
                "                \"type\":\"keyword\"\n" +
                "            },\n" +
                "            \"description\":{\n" +
                "                \"type\":\"text\",\n" +
                "                \"analyzer\":\"ik_max_word\",\n" +
                "                \"copy_to\":\"all\"\n" +
                "            },\n" +
                "            \"all\":{\n" +
                "                \"type\":\"text\",\n" +
                "                \"analyzer\":\"ik_max_word\"\n" +
                "            }\n" +
                "        }\n" +
                "    }\n" +
                "}";
        //设置请求中的参数
        request.source(json, XContentType.JSON);
        client.indices().create(request, RequestOptions.DEFAULT);
    }

    @Test
    //添加文档
    void testCreateDoc() throws IOException {
        Book book = bookDao.selectById(1);
        IndexRequest request = new IndexRequest("books").id(book.getId().toString());
        String json = JSON.toJSONString(book);
        request.source(json,XContentType.JSON);
        client.index(request,RequestOptions.DEFAULT);
    }

    @Test
    //添加文档
    void testCreateDocAll() throws IOException {
        List<Book> bookList = bookDao.selectList(null);
        BulkRequest bulk = new BulkRequest();
        for (Book book : bookList) {
            IndexRequest request = new IndexRequest("books").id(book.getId().toString());
            String json = JSON.toJSONString(book);
            request.source(json,XContentType.JSON);
            bulk.add(request);
        }
        client.bulk(bulk,RequestOptions.DEFAULT);
    }

    @Test
    //按id查询
    void testGet() throws IOException {
        GetRequest request = new GetRequest("books","1");
        GetResponse response = client.get(request, RequestOptions.DEFAULT);
        String json = response.getSourceAsString();
        System.out.println(json);
    }

    @Test
    //按条件查询
    void testSearch() throws IOException {
        SearchRequest request = new SearchRequest("books");

        //条件
        SearchSourceBuilder builder = new SearchSourceBuilder();
        builder.query(QueryBuilders.termQuery("all","spring"));
        request.source(builder);

        SearchResponse response = client.search(request, RequestOptions.DEFAULT);
        SearchHits hits = response.getHits();
        for (SearchHit hit : hits) {
            String source = hit.getSourceAsString();
            //System.out.println(source);
            Book book = JSON.parseObject(source, Book.class);
            System.out.println(book);
        }
    }
}
```

### 2.2.5整合第三方技术

#### 1.缓存

作用：

1. 缓存是一种介于数据永久存储介质与数据应用之间的数据临时存储介质
2. 使用缓存可以有效的减少低速数据读取过程的次数提高系统性能
3. 缓存不仅可以用于提高永久性存储介质的数据读取效率，还可以提供临时的数据存储空间

##### **1.快速入门：**

测试一个检验电话号码的验证码 

创建msgService接口

```java
public interface MsgService {
    //得到电话号码
    public String get(String tele);
    //检验电话号码和验证码
    public boolean check(String tele ,String code);
}
```

实现msgService接口msgServiceimpl

```java
import com.itheima.service.MsgService;
import org.springframework.stereotype.Service;

import java.util.HashMap;

@Service
public class MsgServiceImpl implements MsgService {

    //设置缓存  用于临时存储发来的验证码，再进行匹配是否成功
    private HashMap<String ,String> cache = new HashMap<String,String>();

    @Override
    public String get(String tele) {
        String code = tele.substring(tele.length() - 6);
        cache.put(tele,code);
        return code;
    }

    @Override
    public boolean check(String tele, String code) {
        String queryCode = cache.get(tele);
        return code.equals(queryCode);
    }
}
```

控制msgController 

```java
import com.itheima.service.MsgService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/msg")
public class MsgController {
    @Autowired
    private MsgService msgService;

    @GetMapping("{tele}") // 通过传入参数访问 
    public String get(@PathVariable String tele){
        return msgService.get(tele);
    }

    @PostMapping  //传入的电话号码要一致
    public boolean check(String tele,String code){
        return msgService.check(tele,code);
    }
}
```

SpringBoot提供了缓存技术，方便缓存使用

1. 启用缓存
2. 设置进入缓存的数据
3. 设置读取缓存的数据

1.导入坐标 对应的stater

```xml
<!--cache-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-cache</artifactId>
</dependency>
```

启动缓存 在启动类中添加注解@EnableCaching

```java
@SpringBootApplication
//开启缓存功能
@EnableCaching
public class Springboot19CacheApplication {

    public static void main(String[] args) {
        SpringApplication.run(Springboot19CacheApplication.class, args);
    }
}
```

在实现类中 写查询方法  使用注解@Cacheable

解释：

- 若是第一次得到这个id 会执行return 把这个id添加进cacheSpace这个缓存空间 
- 第二次执行同样的操作时，便不会在执行方法里面的return ，会直接从cacheSpace空间中读取首次添加进来相同的那一个 id 

```java
@Override
@Cacheable(value="cacheSpace",key="#id") //#id读取参数值  cacheSpace是自定义 大的缓存空间  还需要根据后面的#id确定缓存的
public Book getById(Integer id) {
    return bookDao.selectById(id);
}
```



- springboot提供的缓存技术除了提供默认的缓存方案，还可以对**==其他缓存技术进行整合，统一接口==**，方便缓存技术的开发与管理
- 官方提供整合的技术
  - Generic
  - JCache
  - Ehcache
  - Hazelcast
  - InfinispanCouchbase
  - Redis
  - Caffenine
  - Simple (默认)
  - memcached

##### **2.案例：**

- 需求

  - 输入手机号获取验证码，组织文档以短信形式发送给用户（页面模拟)

  - 输入手机号和验证码验证结果

- 需求分析

  - 提供controller，传入手机号，业务层通过手机号计算出独有的6位验证码数据，存入缓存后返回此数据
  - 提供controller，传入手机号与验证码，业务层通过手机号从缓存中读取验证码与输入验证码进行比对，返回比对结果

​	1.domain的实体类

```java
@Data
public class SMSCode {
    private String tele;
    private String code;
}
```

​	2.不需要数据层

​	3.业务层：service

1. 业务接口

   ```java
   public interface SMSCodeService {
       public String sendCodeToSMS(String tele);
       public boolean checkCode(SMSCode smsCode);
   }
   ```

2. 实现接口

   ```java
   import com.itheima.domain.SMSCode;
   import com.itheima.service.SMSCodeService;
   import com.itheima.utils.CodeUtils;
   import net.rubyeye.xmemcached.MemcachedClient;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.cache.annotation.CachePut;
   import org.springframework.stereotype.Service;
   
   @Service
   public class SMSCodeServiceImpl implements SMSCodeService {
   
       //注入工具类
       @Autowired
       private CodeUtils codeUtils;
   
       //使用CachePut，每一次的获取的验证码都不一样
      @Override
      @CachePut(value = "smsCode",key="#tele")
      public String sendCodeToSMS(String tele) {
          String code = codeUtils.generator(tele);
          return code;
      }
   
      @Override
      public boolean checkCode(SMSCode smsCode) {
          //取出内存中的验证码与传递过来的验证码对比匹配，如果相同，返回true
          String code = smsCode.getCode();
          String cacheCode = codeUtils.get(smsCode.getTele());
          return code.equals(cacheCode);
      }
   }    
   ```

​	4.controller控制层

```java
@RestController
@RequestMapping("/sms")
public class SMSCodeController {

    @Autowired
    private SMSCodeService smsCodeService;

    //给电话号码获取验证码
    @GetMapping
    public String getCode(String tele){
        String code = smsCodeService.sendCodeToSMS(tele);
        return code;
    }

    //校验验证码
    @PostMapping
    public boolean checkCode(SMSCode smsCode){
        return smsCodeService.checkCode(smsCode);
    }
}
```



​	5.工具类 ：加密

- 生成一个验证码

  ```java
  @Component
  public class CodeUtils {
  
      //补0数组
      private String [] patch = {"000000","00000","0000","000","00","0",""};
  
      public String generator(String tele){
          //电话号码的hash值
          int hash = tele.hashCode();
          //加密码
          int encryption = 525252520;
          //异或
          long result = hash ^ encryption;
          //第二次加密
          long nowTime = System.currentTimeMillis();
          result = result ^ nowTime;
          //使用取模1000000获得 后六位验证码
          long code = result % 1000000;
          code = code < 0 ? -code : code;
          //保证验证码够六位 补零操作
          String codeStr = code + "";
          //获取验证码长度
          int len = codeStr.length();
          //根据验证码的长度进行补零
          return patch[len] + codeStr;
      }
  
      //bean 当前方法是向缓存中获取
      @Cacheable(value = "smsCode",key="#tele")
      public String get(String tele){
          return null;
      }
      
  }
  ```

3.变更缓存供应商

==数据淘汰策略：==

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220507232037868.png" alt="image-20220507232037868" style="zoom:80%;" />

1. Ehcache

   - 导入坐标

     ```xml
     <dependency>
         <groupId>net.sf.ehcache</groupId>
         <artifactId>ehcache</artifactId>
     </dependency>
     ```

   - 配置文件

     ```yaml
     --ehcache--
       cache:
         type: ehcache
         ehcache:
           config: ehcache.xml #指向配置文件
     ```

   - 导入ehcache配置文件

     ```xml
     <?xml version="1.0" encoding="UTF-8"?>
     <ehcache xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:noNamespaceSchemaLocation="http://ehcache.org/ehcache.xsd"
              updateCheck="false">
         <diskStore path="D:\ehcache" />
     
         <!--默认缓存策略 -->
         <!-- external：是否永久存在，设置为true则不会被清除，此时与timeout冲突，通常设置为false-->
         <!-- diskPersistent：是否启用磁盘持久化-->
         <!-- maxElementsInMemory：最大缓存数量-->
         <!-- overflowToDisk：超过最大缓存数量是否持久化到磁盘-->
         <!-- timeToIdleSeconds：最大不活动间隔，设置过长缓存容易溢出，设置过短无效果，可用于记录时效性数据，例如验证码-->
         <!-- timeToLiveSeconds：最大存活时间-->
         <!-- memoryStoreEvictionPolicy：缓存清除策略-->
         <defaultCache
             eternal="false"
             diskPersistent="false"
             maxElementsInMemory="1000"
             overflowToDisk="false"
             timeToIdleSeconds="60"
             timeToLiveSeconds="60"
             memoryStoreEvictionPolicy="LRU" />
     <!--使用name区分不同的缓存-->
         <cache
             name="smsCode"
             eternal="false"
             diskPersistent="false"
             maxElementsInMemory="1000"
             overflowToDisk="false"
             timeToIdleSeconds="10"
             timeToLiveSeconds="10"
             memoryStoreEvictionPolicy="LRU" />
     
     </ehcache>
     ```

   - 若是坐标jar包没有导入，但是配置文件写了就会报错

2. Redis

   - 导入坐标

     ```xml
     <dependency>
         <groupId>org.springframework.boot</groupId>
         <artifactId>spring-boot-starter-data-redis</artifactId>
     </dependency>
     ```

   - 配置文件

     ```yaml
     --redis--
       cache:
         type: redis  #使用的技术类型
         redis:
           use-key-prefix: false  #是否使用前缀
           key-prefix: sms_   #指定key前缀
           cache-null-values: false  #是否缓存空值
           time-to-live: 10s  #10秒后过期 查询不到
     
       redis:
         host: localhost
         port: 6379
     ```

3. memcached

   - 安装：管理员运行dos窗口

     ![image-20220508194034485](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220508194034485.png)

   - 客户端选择

     1. Memcache Client for Java :最早的客户端，稳定可靠，用户群广

     2. SpyMemcache ：效率高

     3. Xmenecache ：并发处理更好

        SpringBoot未提供对memcache的整合，需要使用硬编码方式实现客户端初始化管理

   - 快速使用：

     1. 导入坐标（jar包 ）：

        ```xml
        <dependency>
            <groupId>com.googlecode.xmemcached</groupId>
            <artifactId>xmemcached</artifactId>
            <version>2.4.7</version>
        </dependency>
        ```

     2.  配置内容

        ```yaml
        memcached:
          servers: localhost:11211
          poolSize: 10
          opTimeout: 3000
        ```

     3. config类

        properties：属性配置信息类，加载配置

        ```java
        @Component
        @ConfigurationProperties(prefix = "memcached")
        @Data
        public class XMemcachedProperties {
            private String servers;
            private int poolSize;
            private long opTimeout;
        }
        ```

        创建客户端配置类：

        ```java
        @Configuration
        public class XMemcachedConfig {
        
            @Autowired
            private XMemcachedProperties memcachedProperties;
        
            @Bean
            public MemcachedClient getMemcachedClient() throws IOException {
                //获取端口
                MemcachedClientBuilder memcachedClientBuilder = new XMemcachedClientBuilder(memcachedProperties.getServers());
               //链接的数量
                memcachedClientBuilder.setConnectionPoolSize(memcachedProperties.getPoolSize());
                //超时时间
                memcachedClientBuilder.setOpTimeout(memcachedProperties.getOpTimeout());
                MemcachedClient memcachedClient = memcachedClientBuilder.build();
                return memcachedClient;
            }
        }
        ```

     4. 业务实现类：

        ```java
        import com.itheima.domain.SMSCode;
        import com.itheima.service.SMSCodeService;
        import com.itheima.utils.CodeUtils;
        import net.rubyeye.xmemcached.MemcachedClient;
        import org.springframework.beans.factory.annotation.Autowired;
        import org.springframework.cache.annotation.CachePut;
        import org.springframework.stereotype.Service;
        
        @Service
        public class SMSCodeServiceImpl implements SMSCodeService {
            //以下是springboot中使用xmemcached
            @Autowired
            private MemcachedClient memcachedClient;
        
            @Override
            public String sendCodeToSMS(String tele) {
                String code = codeUtils.generator(tele);
                try {
                    memcachedClient.set(tele,10,code);//10 超时时间
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return code;
            }
        
            @Override
            public boolean checkCode(SMSCode smsCode) {
                String code = null;
                try {
                    code = memcachedClient.get(smsCode.getTele()).toString();
                } catch (Exception e) {
                    e.printStackTrace();
                }
                return smsCode.getCode().equals(code);
            }
        
        }
        ```

4. jetcache远程缓存 

   - jetCache对SpringCache进行了封装，在原有功能基础上实现了多级缓存、缓存统计、自动刷新、异步调用、数据报表等功能
   - 属于底层框架，整合了以下cache
     - 本地缓存
       1. LinkHashMaP
       2. Caffeine   ：
     - 远程缓存
       1. Redis
       2. Tair

   导入坐标

   ```xml
   <dependency>
       <groupId>com.alicp.jetcache</groupId>
       <artifactId>jetcache-starter-redis</artifactId>
       <version>2.6.2</version>
   </dependency>
   ```

   配置文件

   ```yaml
   jetcache:
     statIntervalMinutes: 1
     #本地
     local:
       default:
         type: linkedhashmap
         keyConvertor: fastjson  #key类型转换器
     #远程
     remote:
       default:
         type: redis
         host: localhost
         port: 6379
         keyConvertor: fastjson
         valueEncode: java
         valueDecode: java
         poolConfig:
           maxTotal: 50
       sms:
         type: redis
         host: localhost
         port: 6379
         poolConfig:
           maxTotal: 50
   ```

   启动类注解：

   ```java
   @SpringBootApplication
   //jetcache启用缓存的主开关
   @EnableCreateCacheAnnotation
   public class Springboot20JetCacheApplication {
       public static void main(String[] args) {
           SpringApplication.run(Springboot20JetCacheApplication.class, args);
       }
   
   }
   ```

   业务实现类

   ```java
   @Service
   public class SMSCodeServiceImpl implements SMSCodeService {
   
       @Autowired
       private CodeUtils codeUtils;
       //remote area指定使用的配置，默认有下划线
   //    @CreateCache(area="sms",name="jetCache_",expire = 10,timeUnit = TimeUnit.SECONDS)
       
   // local：在启动类中使用了@EnableCreateCacheAnnotation注解就可以使用下面的CreateCache注解
       @CreateCache(name="jetCache_",expire = 1000,timeUnit = TimeUnit.SECONDS)
       private Cache<String ,String> jetCache;
   
       @Override
       public String sendCodeToSMS(String tele) {
           String code = codeUtils.generator(tele);
           jetCache.put(tele,code);
           return code;
       }
   
       @Override
       public boolean checkCode(SMSCode smsCode) {
           String code = jetCache.get(smsCode.getTele());
           return smsCode.getCode().equals(code);
       }
   
   }
   ```

   jetcache方法缓存

   ```java
   @SpringBootApplication
   //jetcache启用缓存的主开关
   @EnableCreateCacheAnnotation
   //开启方法注解缓存
   @EnableMethodCache(basePackages = "com.itheima")
   public class Springboot20JetCacheApplication {
   
       public static void main(String[] args) {
           SpringApplication.run(Springboot20JetCacheApplication.class, args);
       }
   
   }
   ```

   序列化对象 实现Serializable

   ```java
   @Data
   public class Book implements Serializable {
       private Integer id;
       private String type;
       private String name;
       private String description;
   }
   ```

5. j2cache

   - 缓存整合框架，可以提供缓存的整合方案，使用各种缓存搭配使用 但是自身不提供缓存功能
   - 基于ehcache +redis整合

   导入坐标

   ```xml
   <dependency>
       <groupId>net.oschina.j2cache</groupId>
       <artifactId>j2cache-core</artifactId>
       <version>2.8.4-release</version>
   </dependency>
   
   <dependency>
       <groupId>net.oschina.j2cache</groupId>
       <artifactId>j2cache-spring-boot2-starter</artifactId>
       <version>2.8.0-release</version>
   </dependency>
    <dependency>
        <groupId>net.sf.ehcache</groupId>
        <artifactId>ehcache</artifactId>
   </dependency>
   ```

   配置文件

   ```yaml
   j2cache:
     config-location: j2cache.properties  #要创建 j2cache.properties
   ```

   j2cache.properties

   ```properties
   # 1级缓存
   j2cache.L1.provider_class = ehcache
   ehcache.configXml = ehcache.xml
   
   # 设置是否启用二级缓存
   j2cache.l2-cache-open = false
   
   # 2级缓存
   j2cache.L2.provider_class = net.oschina.j2cache.cache.support.redis.SpringRedisProvider
   j2cache.L2.config_section = redis
   redis.hosts = localhost:6379
   
   # 1级缓存中的数据如何到达二级缓存
   j2cache.broadcast = net.oschina.j2cache.cache.support.redis.SpringRedisPubSubPolicy
   
   redis.mode = single
   
   redis.namespace = j2cache
   ```

   业务实现

   ```java
   @Service
   public class SMSCodeServiceImpl implements SMSCodeService {
   
       @Autowired
       private CodeUtils codeUtils;
   
       @Autowired
       private CacheChannel cacheChannel;
   
       @Override
       public String sendCodeToSMS(String tele) {
           String code = codeUtils.generator(tele);
           cacheChannel.set("sms",tele,code);
           return code;
       }
   
       @Override
       public boolean checkCode(SMSCode smsCode) {
           String code = cacheChannel.get("sms",smsCode.getTele()).asString();
           return smsCode.getCode().equals(code);
       }
   
   }
   ```

#### 2. 任务

- 定时任务技术
  1. Quartz
  2. Spring Task
- 工作(Job)∶用于定义具体执行的工作
- 工作明细(JobDetail):用于描述定时工作相关的信息
- 触发器（Trigger ):用于描述触发工作的规则，通常使用cron表达式定义调度规则
- 调度器(Scheduler) :描述了工作明细与触发器的对应关系



2.1整合Quart

1. 导入坐标

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-quartz</artifactId>
   </dependency>
   ```

2. 定义具体执行的任务，基础QuartzJobBean

   ```java
   public class MyQuartz extends QuartzJobBean {
       @Override
       protected void executeInternal(JobExecutionContext context) throws JobExecutionException {
           System.out.println("quartz task run...");
       }
   }
   ```

   定义工作明细与触发器，绑定关系

   ```java
   @Configuration
   public class QuartzConfig {
   
       //具体工作明细
       @Bean
       public JobDetail printJobDetail(){
           //绑定具体的工作
           return JobBuilder
                   .newJob(MyQuartz.class)
                   .storeDurably()
                   .build();
       }
   
       //触发器
       @Bean
       public Trigger printJobTrigger(){
           ScheduleBuilder schedBuilder = CronScheduleBuilder.cronSchedule("0/5 * * * * ?");
           //绑定对应的工作明细
           return TriggerBuilder.newTrigger().forJob(printJobDetail()).withSchedule(schedBuilder).build();
       }
   }
   ```

   简化形式： 

   1.开启定时任务功能

   ```java
   @SpringBootApplication
   //开启定时任务功能
   @EnableScheduling
   public class Springboot22TaskApplication {
   
       public static void main(String[] args) {
           SpringApplication.run(Springboot22TaskApplication.class, args);
       }
   }
   ```

   2.指定时间

   ```
   @Component
   public class MyBean {
   
       //指定多久时间执行一次
       //                  秒 分 小时 日 月 星期
       //每一秒执行一次
       @Scheduled(cron = "0/1 * * * * ?")
       public void print(){
           System.out.println(Thread.currentThread().getName()+" :spring task run...");      
       }
   }
   ```

   配置属性

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220508224917793.png" alt="image-20220508224917793" style="zoom:67%;" />

   ```yaml
   spring:
     task:
       scheduling:
         thread-name-prefix: spring_tasks_
         shutdown:
           await-termination: false
           await-termination-period: 10s
   ```



#### 3.邮件

==SpringBoot整合JavaMail== ：

- SMTP (Simple Mail Transfer Protocol)︰简单邮件传输协议，用于发送电子邮件的传输协议
- POP3 ( Post Office Protocol - Version 3):用于接收电子邮件的标准协议  （不同步）
- IMAP ( Internet Mail Access Protocol) :互联网消息协议，是POP3的替代协议 （同步）





整合要点：

1. 导入坐标

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-mail</artifactId>
   </dependency>
   ```

2. 配置文件

   ```yaml
   spring:
     mail:
       host: smtp.126.com  #邮箱的类型 供应商
       username: test@126.com
       password: test
   ```

3. 定义一个接口

   ```java
   public interface SendMailService {
       void sendMail();
   }
   ```

   实现类

   ```java
   //@Service
   public class SendMailServiceImpl implements SendMailService {
   
       @Autowired
       private JavaMailSender javaMailSender;
   
       //发送人
       private String from = "test@qq.com";
       //接收人
       private String to = "test@126.com";
       //标题
       private String subject = "测试邮件";
       //正文
       private String context = "测试邮件正文内容";
   
       @Override
       public void sendMail() {
           //简单邮件信息
           SimpleMailMessage message = new SimpleMailMessage();
           message.setFrom(from+"(小甜甜)");
           message.setTo(to);
           message.setSubject(subject);
           message.setText(context);
           javaMailSender.send(message);
       }
   }
   ```

发送多部邮件

```java
@Service
public class SendMailServiceImpl2 implements SendMailService {

    @Autowired
    private JavaMailSender javaMailSender;

    //发送人
    private String from = "test@qq.com";
    //接收人
    private String to = "test@126.com";
    //标题
    private String subject = "测试邮件";
    //正文
    private String context = "<img src='https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fbkimg.cdn.bcebos.com%2Fpic%2F8326cffc1e178a82b9018131e84f648da97739124247&refer=http%3A%2F%2Fbkimg.cdn.bcebos.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1645001879&t=f4d8895e53576eacf54605dcc63c6861'/><a href='https://www.itcast.cn'>点开有惊喜</a>";

    @Override
    public void sendMail() {

        try {
            MimeMessage message = javaMailSender.createMimeMessage();
            //封装到一个类helper中
            MimeMessageHelper helper = new MimeMessageHelper(message,true);
            helper.setFrom(to+"(小甜甜)");
            helper.setTo(from);
            helper.setSubject(subject);
            helper.setText(context,true);

            //添加附件
            File f1 = new File("D:\\workspace\\springboot\\springboot_23_mail\\target\\springboot_23_mail-0.0.1-SNAPSHOT.jar");
            File f2 = new File("E:\\Spring-boot 2\\springboot源代码（完整版）\\springboot_23_mail\\src\\main\\resources\\logo.png");

            helper.addAttachment(f1.getName(),f1);
            helper.addAttachment("最靠谱的培训结构.png",f2);

            javaMailSender.send(message);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### 4.信息

- 消息发送方
  - 生产者

- 消息接收方
  - 消费者

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220513212041957.png" alt="image-20220513212041957" style="zoom: 50%;" />

- 同步消息
  - 需要等到回应才接着发送下一个消息
- 异步消息
  - 不需要等到回应，可以直接把消息发完



- 异步消息传递技术

  1. JMS （Java Message Service）：一个规范，等同于JDBC规范，提供了与消息服务相关的API接口

     - JMS消息模型
       1. peer-2-peer:点对点模型，消息发送到一个队列中，队列保存消息。队列的消息只能被一个消费者消费，或超时
       2. publish-subscribe:发布订阅模型，消息可以被多个消费者消费，生产者和消费者完全独立，不需要感知对方的存在
     - JMS消息种类
       - TextMessage
       - MapMessage
       - ==BytesMessage==
       - StreamMessage
       - objectMessage
       - Message (只有消息头和属性)

     JMS实现：ActiveMQ、Redis、HornetMQ、RabbitMQ、RocketMQ（没有完全遵守JMS规范)

  2. AMQP (advanced message queuing protocol)：一种协议（高级消息队列协议，也是消息代理规范），规范了网络交换的数据格式，兼容JMS

     - 优点：具有跨平台星，服务器供应商，生产者，消费者可以使用不同的语言来实现
     - AMOP消息类型
       - ==direct exchange==
       - fanout exchange
       - ==topic exchange==
       - headers exchange
       - system exchange
     - AMOP消息种类：byte[]
     - AMOP实现：RabbitMQ、StormMQ、RocketMQ

  3. MQTT(Message Queueing Telemetry Transport）：消息队列遥测传输，专为小设备设计，是物联网（IOT）生态系统中主要成分之一
     心

     - 小型设备

     

  4. Kafka：一种高吞吐量的分布式发布订阅消息系统，提供实时消息功能

     

##### 1.SpringBoot整合ActiveMQ

- 安装ActiveMQ

1.导入坐标

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-activemq</artifactId>
</dependency>
```

2.配置文件

```yaml
server:
  port: 80


spring:
  activemq:
    broker-url: tcp://localhost:61616 #链接的端口
  jms:     #默认的保存位置
    pub-sub-domain: true
    template:
      default-destination: itheima  
```

3.实现activemq

接口：

```java
public interface MessageService {
    void sendMessage(String id);
    String doMessage();
}
```

实现类：

```java
@Service
public class MessageServiceActivemqImpl implements MessageService {

    @Autowired
    private JmsMessagingTemplate messagingTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列，id："+id);
        messagingTemplate.convertAndSend("order.queue.id",id); //
    }

    @Override
    public String doMessage() {
        String id = messagingTemplate.receiveAndConvert("order.queue.id",String.class);
        System.out.println("已完成短信发送业务，id："+id);
        return id;
    }
}
```

监听器  ：自动处理掉订单

```java
@Component
public class MessageListener {
    //监听消息队列
    @JmsListener(destination = "order.queue.id")
    //转发
    @SendTo("order.other.queue.id")
    public String receive(String id){
        System.out.println("已完成短信发送业务，id："+id);
        return "new:"+id;
    }
}
```



##### 2.SpringBoot整合RabbitMQ

- RabbitMQ基于Erlang语言编写，需要暗转Erlang
- Erlang：
  - 配置环境变量
    - ERLANG_HOME
    - PATH

- 安装RabbitMQ
  - 使用cmd管理员运行
  - 开启Rabbit服务



direct模式：

1.导入坐标

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-amqp</artifactId>
</dependency>
```

2.配置文件

```yaml
rabbitmq:
  host: localhost
  port: 5672
```

实现类：

```java
//@Service
public class MessageServiceRabbitmqDirectImpl implements MessageService {

    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列（rabbitmq direct），id："+id);
        //
        amqpTemplate.convertAndSend("directExchange","direct",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

配置类 ：消息队列（direct）

```java
@Configuration
public class RabbitConfigDirect {

    //两个消息队列
    @Bean
    public Queue directQueue(){
        return new Queue("direct_queue");
    }

    @Bean
    public Queue directQueue2(){
        return new Queue("direct_queue2");
    }

    @Bean
    public DirectExchange directExchange(){
        return new DirectExchange("directExchange");
    }

    //交换机
    @Bean
    public Binding bindingDirect(){
        return BindingBuilder.bind(directQueue()).to(directExchange()).with("direct");
    }
    @Bean
    public Binding bindingDirect2(){
        return BindingBuilder.bind(directQueue2()).to(directExchange()).with("direct2");
    }

}
```



监听器：两个消息队列

```java
@Component
public class MessageListener {

    @RabbitListener(queues = "direct_queue")
    public void receive(String id){
        System.out.println("已完成短信发送业务(rabbitmq direct)，id："+id);
    }

}
```



```java
@Component
public class MessageListener2 {

    @RabbitListener(queues = "direct_queue")
    public void receive(String id){
        System.out.println("已完成短信发送业务(rabbitmq direct two)，id："+id);
    }

}
```



topic模式： 主题交换机

1.导入坐标

2.配置文件

1和2 都和direc一样

3.消息队列类

```java
//@Configuration
public class RabbitConfigTopic {

    @Bean
    public Queue topicQueue(){
        return new Queue("topic_queue");
    }

    @Bean
    public Queue topicQueue2(){
        return new Queue("topic_queue2");
    }

    //主题交换机
    @Bean
    public TopicExchange topicExchange(){
        return new TopicExchange("topicExchange");
    }

    @Bean
    public Binding bindingTopic(){
        return BindingBuilder.bind(topicQueue()).to(topicExchange()).with("topic.*.id");//模糊查询
    }
    @Bean
    public Binding bindingTopic2(){
        return BindingBuilder.bind(topicQueue2()).to(topicExchange()).with("topic.orders.*");
    }

}
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220513223505754.png" alt="image-20220513223505754" style="zoom:67%;" />

定义队列类：

```java
@Component
public class MessageListener {

    @RabbitListener(queues = "topic_queue")
    public void receive(String id){
        System.out.println("已完成短信发送业务(rabbitmq topic 1)，id："+id);
    }

    @RabbitListener(queues = "topic_queue2")
    public void receive2(String id){
        System.out.println("已完成短信发送业务(rabbitmq topic 22222222)，id："+id);
    }

}
```

实现类：

```java
//@Service
public class MessageServiceRabbitmqTopicImpl implements MessageService {

    @Autowired
    private AmqpTemplate amqpTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列（rabbitmq topic），id："+id);
        amqpTemplate.convertAndSend("topicExchange","topic.orders.id",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```



##### 3.SpringBoot整合RocketMQ

- 安装RocketMQ
- 默认端口：9876
- 配置环境变量
  - PATH
  - ROCKET-HOME
  - NAMESRV-ADDR : 127.0.0.1:9876  （建议配上）



- 命名服务器与broker

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220513224244519.png" alt="image-20220513224244519" style="zoom:67%;" />



1.导入坐标

```xml
<dependency>
    <groupId>org.apache.rocketmq</groupId>
    <artifactId>rocketmq-spring-boot-starter</artifactId>
    <version>2.2.1</version>
</dependency>
```

2.配置文件

```yaml
rocketmq:
  name-server: localhost:9876
  producer:
    group: group_rocketmq  # 对生产者进行分组
```

实现类：

```java
@Service
public class MessageServiceRocketmqImpl implements MessageService {

    @Autowired
    private RocketMQTemplate rocketMQTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列（rocketmq），id："+id);
//        rocketMQTemplate.convertAndSend("order_id",id);
        //异步发送消息
        SendCallback callback = new SendCallback() {
            @Override
            public void onSuccess(SendResult sendResult) {
                System.out.println("消息发送成功");
            }

            @Override
            public void onException(Throwable e) {
                System.out.println("消息发送失败！！！！！");
            }
        };
        rocketMQTemplate.asyncSend("order_id",id,callback);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

监听器：

```java
@Component
@RocketMQMessageListener(topic = "order_id",consumerGroup = "group_rocketmq")
public class MessageListener implements RocketMQListener<String> {
    @Override
    public void onMessage(String id) {//返回的值都在id中
        System.out.println("已完成短信发送业务(rocketmq)，id："+id);
    }
}
```



##### 4.SpringBoot 整合Kafka

- 安装Kafka

1.导入坐标

```xml
<dependency>
    <groupId>org.springframework.kafka</groupId>
    <artifactId>spring-kafka</artifactId>
</dependency>
```

2.配置文件

```yaml
kafka:
  bootstrap-servers: localhost:9092
  consumer:
    group-id: order
```

3.实现类

```java
@Service
public class MessageServiceKafkaImpl implements MessageService {

    @Autowired
    private KafkaTemplate<String,String> kafkaTemplate;

    @Override
    public void sendMessage(String id) {
        System.out.println("待发送短信的订单已纳入处理队列（kafka），id："+id);
        kafkaTemplate.send("itheima2022",id);
    }

    @Override
    public String doMessage() {
        return null;
    }
}
```

监听器：

```java
@Component
public class MessageListener {

    @KafkaListener(topics = "itheima2022")
    public void onMessage(ConsumerRecord<String,String> record){
        System.out.println("已完成短信发送业务(kafka)，id："+record.value());
    }
}
```



### 2.2.6监控

**意义：**

监控操作系统当前处于什么状态，执行什么程序

1. 监控服务状态是否宕机
2. 监控服务运行指标（内存、虚拟机、线程、请求）
3. 监控日志
4. 管理服务（服务下线）



**监控实施方式：**

开始拉取，宕机上报

- 显示监控信息的服务器：用于获取服务信息，并显示对应的信息
- 运行的服务：启动时主动上报，告知监控服务器自己需要受到监控

![image-20220514225006630](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514225006630.png)



**可视化监控平台**

spring-boot-admin：



1.创建服务端

先导入坐标

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-server</artifactId>
    <version>2.5.4</version>
</dependency>
```

配置端口：

```yaml
server:
  port: 8080
```

在启动类中添加注解：@EnableAdminServer 启动服务端

2.创建客户端

导入坐标：

```xml
<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
    <version>2.5.4</version>
</dependency>
```

配置文件：

```yaml
server:
  port: 80

spring:
  boot:
    admin:
      client:
        url: http://localhost:8080  # 指定本机端口
# 健康指标的明细
management:
  endpoint:
    health:
      show-details: always  #启动指定端点
  # 查看全部的健康信息 *    
  endpoints:
    web:
      exposure:
        include: "*" #启动所有的端点
```



**Actuator**：

- Actuator提供了SpringBoot生产就绪功能，通过端点的配置与访问，获取端点信息
- 端点描述了一组监控信息，SpringBoot提供了多个内置端点，也可以根据需要自定义端点信息
- 访问当前应用所有端点信息：/actuator
- 访问端点详细信息：/actuator/端点名称

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514232250648.png" alt="image-20220514232250648" style="zoom: 67%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514232310637.png" alt="image-20220514232310637" style="zoom:67%;" />

暴露端点功能：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514232814245.png" alt="image-20220514232814245" style="zoom:67%;" />

**端点指标控制**

1. info端点指标控制

2. ![image-20220514233440089](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514233440089.png)

3. <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514233434746.png" alt="image-20220514233434746" style="zoom:67%;" />

4. health端点指标控制

   ==health表示整个健康系统的指标==  加入的是重要信息

   <img src="SpringBoot2.assets/image-20220514233609146.png" alt="image-20220514233609146" style="zoom:67%;" />

   

5. metrics端点指标控制

   

   <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514233726851.png" alt="image-20220514233726851" style="zoom:67%;" />

6. 自定义端点

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220514234111015.png" alt="image-20220514234111015" style="zoom:67%;" />



# 3.原理篇

==达到的目标 :==

1. 掌握SpringBoot内部工作流程

2. 理解SpringBoot整合第三方技术的原理

3. 实现自定义开发整合第三方技术的组件

## 3.1 自动配置

### 3.1.1 bean的加载方式



1 . xml方式声明bean

导入坐标：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>5.3.9</version>
    </dependency>

    <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>druid</artifactId>
        <version>1.1.16</version>
    </dependency>

</dependencies>
```

xml配置bean

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--xml方式声明自己开发的bean-->
    <bean id="cat" class="com.itheima.bean.Cat"/>
    <bean class="com.itheima.bean.Dog"/>

    <!--xml方式声明第三方开发的bean-->
    <bean id="dataSource" class="com.alibaba.druid.pool.DruidDataSource"/>
    <bean class="com.alibaba.druid.pool.DruidDataSource"/>
    <bean class="com.alibaba.druid.pool.DruidDataSource"/>
</beans>
```



2 . xml + 注解定义bean

![image-20220515203315518](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220515203315518.png)

xml ：bean指定文件加载路径

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:context="http://www.springframework.org/schema/context"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="
       http://www.springframework.org/schema/beans
       http://www.springframework.org/schema/beans/spring-beans.xsd
       http://www.springframework.org/schema/context
       http://www.springframework.org/schema/context/spring-context.xsd
    ">

    <!--指定加载bean的位置，组件component，命名空间context-->
    <context:component-scan base-package="com.itheima.bean,com.itheima.config"/>
</beans>
```



加载第三方bean

```java
@Configuration //配置类
public class DbConfig {
    //使用第三方的bean 返回值就是那个bean的返回值类型
    @Bean
    public DruidDataSource dataSource(){
        DruidDataSource ds = new DruidDataSource();
        return ds;
    }
}
```



3 . 配置类加载bean

```java
@ComponentScan({"com.itheima.bean","com.itheima.config"})  //磁盘扫描 扫描指定包路径下的配置类
public class SpringConfig3 {
}
```

加载bean类

```java
public class App3 {
    public static void main(String[] args) {
        //加载配置类对象 AnnotationConfigApplicationContext  就会把配置类自动加载成一个bean
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig3.class);
        String[] names = ctx.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
    }
}
```



4 .  Factorybean

bean对象：

```java
//创建 dog对象
public class DogFactoryBean implements FactoryBean<Dog> {
    //实现三个方法
    //指定FactoryBean的对象
    @Override
    public Dog getObject() throws Exception {
        Dog d = new Dog();
        //可以做一系列的初始化的工作
        return d;
    }

    //对象的类型
    @Override
    public Class<?> getObjectType() {
        return Dog.class;
    }

    //是否是单利
    @Override
    public boolean isSingleton() {
        return true;
    }
}
```

config对象

```java
@ComponentScan({"com.itheima.bean","com.itheima.config"})
public class SpringConfig3 {

    @Bean
    public DogFactoryBean dog(){
        return new DogFactoryBean();
    }


```

加载factorybean

```java
public class App3 {
    public static void main(String[] args) {
        //加载配置类对象 AnnotationConfigApplicationContext
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig3.class);
        String[] names = ctx.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println(ctx.getBean("dog"));
    }
}
```



5 proxyBeanMothod属性

加载配置类并加载配置文件（系统迁移)：

```java
@Configuration

@Component
//系统迁移时就把配置文件导入进来
@ImportResource("applicationContext1.xml")
public class SpringConfig32 {
}
```

使用proxyBeanMethods=true可以保障调用此方法得到的对象是从容器中获取的而不是重新创建的

```java
@Configuration(proxyBeanMethods = true)  //默认true 代理形式
// true 时出来的是同一个bean类 也就是创建一个代理对象 
// false 时出来的是不同的 就不要代理对象，出现的类也不一样
public class SpringConfig33 {
    //定义一个bean
    @Bean
    public Cat cat(){
        return new Cat();
    }
}
```



6 import 导入bean

- 使用@lmport注解导入要注入的bean对应的字节码
- 被导入的bean无需使用注解声明为bean
- 此形式可以有效的降低源代码与Spring技术的耦合度，在spring技术底层及诸多框架的整合中大量使用

```java
//@Import({Dog.class,DbConfig.class})  
@Import(DogFactoryBean.class)
public class SpringConfig4 {

}
```

得到全路径类名



7 . 使用上下文对象在容器初始化完毕后注入bean

```java
public class App5 {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig4.class);
        //上下文容器对象已经初始化完毕后，手工加载bean
        ctx.registerBean("tom", Cat.class,0);
        ctx.registerBean("tom", Cat.class,1);
        ctx.registerBean("tom", Cat.class,2);
        //只是要注册一个bean
        ctx.register(Mouse.class);
        String[] names = ctx.getBeanDefinitionNames();
        for (String name : names) {
            System.out.println(name);
        }
        System.out.println("----------------------");
        System.out.println(ctx.getBean(Cat.class));
    }
}
```



8 导入实现了ImportSelector接口的类，实现对导入源的编程式处理

bean对象：

```java
public class MyImportSelector implements ImportSelector {
    @Override
    public String[] selectImports(AnnotationMetadata metadata) {
//        System.out.println("================");
//        System.out.println("提示："+metadata.getClassName());
//        System.out.println(metadata.hasAnnotation("org.springframework.context.annotation.Configuration"));
//        Map<String, Object> attributes = metadata.getAnnotationAttributes("org.springframework.context.annotation.ComponentScan");
//        System.out.println(attributes);
//        System.out.println("================");

        //各种条件的判定，判定完毕后，决定是否装在指定的bean
        boolean flag = metadata.hasAnnotation("org.springframework.context.annotation.Configuration");
        if(flag){
            return new String[]{"com.itheima.bean.Dog"};
        }
        return new String[]{"com.itheima.bean.Cat"}; //全路径类名
    }
}
```

config类：

```java
@Configuration

@Import(MyImportSelector.class)
public class SpringConfig6 {
}
```



9 . 导入实现了ImportBeanDefinitionRegistrar接口的类，通过BeanDefinition的注册器注册实名bean，实现对容器中bean的裁定，例如对现有bean的覆盖，进而达成不修改源代码的情况下更换实现的效果

bean对象：

```java
public class MyRegistrar implements ImportBeanDefinitionRegistrar {
    @Override
    public void registerBeanDefinitions(AnnotationMetadata importingClassMetadata, BeanDefinitionRegistry registry) {
        //1.使用元数据去做判定

        // 后面获得的方式很多
        BeanDefinition beanDefinition = BeanDefinitionBuilder.rootBeanDefinition(BookServiceImpl2.class).getBeanDefinition();
        registry.registerBeanDefinition("bookService",beanDefinition);
    }
}
```

config对象：

```java
@Import(MyRegistrar.class)
public class SpringConfig7 {
}
```



10 . 导入实现了BeanDefinitionRegistryPostProcessor接口的类，通过BeanDefinition的注册器注册实名bean,实现对容器中bean的最终裁定

config对象

```java
@Import({BookServiceImpl1.class, MyPostProcessor.class, MyRegistrar2.class, MyRegistrar.class}) // 导入了一些列的类，使用数组注入多个类
public class SpringConfig8 {
}
```

bean对象：实现 BeanDefinitionRegistryPostProcessor ， 对bean的后处理操作

```java
public class MyPostProcessor implements BeanDefinitionRegistryPostProcessor {
    @Override
    public void postProcessBeanDefinitionRegistry(BeanDefinitionRegistry registry) throws BeansException {
         //最后处理的是BookServiceImpl4的这个类。后执行的覆盖先执行的  后处理机制：
        BeanDefinition beanDefinition = BeanDefinitionBuilder.rootBeanDefinition(BookServiceImpl4.class).getBeanDefinition();
        registry.registerBeanDefinition("bookService",beanDefinition);
    }

    @Override
    public void postProcessBeanFactory(ConfigurableListableBeanFactory beanFactory) throws BeansException {

    }
}
```

运行程序中：

```java
public class App8 {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig8.class);
        BookSerivce bookService = ctx.getBean("bookService", BookSerivce.class);
        bookService.check();
    }
}
```

实现类中：

```java
@Service("bookService")
public class BookServiceImpl1 implements BookSerivce {
    @Override
    public void check() {
        System.out.println("book service 1..");
    }
}
```



**总结：** 

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220515220907551.png" alt="image-20220515220907551" style="zoom:67%;" />



### 3.1.2 bean的加载控制

 （一）

- bean的加载控制根据指定情况对bean进行==选择性加载==以达到使用于项目的目标

  以上的10种中有以下可以达到选择性的bean

  1. 使用上下文对象在容器初始化完毕后注入bean
  2. 导入实现了ImportSelector接口的类，实现对导入源的编程式处理
  3. 导入实现了ImportBeanDefinitionRegistrar接口的类，通过BeanDefinition的注册器注册实名bean，实现对容器中bean的裁定
  4. 导入实现了BeanDefinitionRegistryPostProcessor接口的类，通过BeanDefinition的注册器注册实名bean,实现对容器中bean的最终裁定

演示：

​	运行：

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);
        String[] beans = ctx.getBeanDefinitionNames();
        for (String bean : beans) {
            System.out.println(bean);
        }
    }
}
```

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220516222730773.png" alt="image-20220516222730773" style="zoom:67%;" />



（二）

猫和老鼠案例：

- 使用@Conditional注解的==派生注解设置各种组合条件控制bean的加载== 

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220516224637816.png" alt="image-20220516224637816" style="zoom: 67%;" />

匹配指定环境：

```java
//加载druid的dataSource
@Bean
@ConditionalOnClass(name="com.mysql.jdbc.Driver")
public DruidDataSource dataSource(){
    return new DruidDataSource();
}
```

（三）bean依赖属性的配置：

案例：

1.导入坐标：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
        <version>2.5.4</version>
    </dependency>
    <dependency>
        <groupId>org.projectlombok</groupId>
        <artifactId>lombok</artifactId>
        <version>1.18.22</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
        <version>2.5.4</version>
    </dependency>
</dependencies>
```



配置文件 ：通过配置文件设置信息  配置文件中使用固定格式为属性类注入数据

```yml
cartoon:
  cat:
    name: "图多盖洛"
    age: 5
  mouse:
    name: "泰菲"
    age: 1
```

配置类： 将业务功能bean运行需要的资源抽取成独立的属性类（******Properties)，设置读取配置文件信息

```java
@ConfigurationProperties(prefix = "cartoon")
@Data
public class CartoonProperties {
    private Cat cat;
    private Mouse mouse;
}
```

主类：定义业务bean，通常使用@import导入，解耦强制加载bean

使用@EnableConfigurationProperties注解设定使用属性类时加载bean

```java
@Data
@ConditionalOnClass(name="org.springframework.data.redis.core.RedisOperations") //
@EnableConfigurationProperties(CartoonProperties.class) //强制把CartoonProperties类加载成bean
public class CartoonCatAndMouse implements ApplicationContextAware {
    private Cat cat;
    private Mouse mouse;

    private CartoonProperties cartoonProperties;

    //构造方法
    public CartoonCatAndMouse(CartoonProperties cartoonProperties){
        this.cartoonProperties = cartoonProperties;
        //确保每次修改能得到新的值，若是没有修改则使用旧的设置
        cat = new Cat();
        cat.setName(cartoonProperties.getCat()!=null && StringUtils.hasText(cartoonProperties.getCat().getName()) ? cartoonProperties.getCat().getName() : "tom");
        cat.setAge(cartoonProperties.getCat()!=null && cartoonProperties.getCat().getAge()!=null ? cartoonProperties.getCat().getAge() : 10);

        mouse = new Mouse();
        mouse.setName(cartoonProperties.getMouse()!=null && StringUtils.hasText(cartoonProperties.getMouse().getName()) ? cartoonProperties.getMouse().getName() : "jerry");
        mouse.setAge(cartoonProperties.getMouse()!=null && cartoonProperties.getMouse().getAge()!=null ? cartoonProperties.getMouse().getAge() : 8);
    }

    //播放动画片
    public void play(){
        String[] beans = applicationContext.getBeanDefinitionNames();
        for (String bean : beans) {
            System.out.println(bean);
        }
        System.out.println(cat.getAge()+"岁的"+cat.getName()+"和"+mouse.getAge()+"岁的"+mouse.getName()+"在互打小鸡鸡");
    }

    private ApplicationContext applicationContext;
}
```

猫和老鼠实体类：

```java
@Data
public class Cat {
    private String name;
    private Integer age;
}
```

```java
@Data
public class Mouse {
    private String name;
    private Integer age;
}
```



启动类：

```java
@SpringBootConfiguration
@Import(CartoonCatAndMouse.class)
public class App {
    public static void main(String[] args) {
        ConfigurableApplicationContext ctx = SpringApplication.run(App.class);
        CartoonCatAndMouse bean = ctx.getBean(CartoonCatAndMouse.class);
        bean.play();
    }
}
```



### 3.1.3 bean的依赖属性配置



自动配置思想：

1. 收集Spring开发者的编程习惯，整理开发过程使用的常用技术列表—>(==技术集A==)
2. 收集常用技术(技术集A)的使用参数，整理开发过程中每个技术的常用设置列表-->(==设置集B==)
3. 初始化SpringBoot基础环境，加载用户自定义的bean和导入的其他坐标，形成==初始化环境==
4. 将==技术集A==包含的所有技术都定义出来，在Spring/SpringBoot启动时默认全部加载
5. 将==技术集A==中具有使用条件的技术约定出来，设置成按条件加载，由开发者决定是否使用该技术（与==初始化环境==比对)
6. 将==设置集B==作为默认配置加载（约定大于配置），减少开发者配置工作量
7. 开放==设置集B==的配置覆盖接口，由开发者根据自身需要决定是否覆盖默认配置



**查看源码** ：

```java
 @SpringBootApplication(excludeName = "org.springframework.boot.autoconfigure.context.LifecycleAutoConfiguration")

@SpringBootConfiguration      
    @Configuration            
        @Component            
    @Indexed          //加载bean时 加速加载        
@EnableAutoConfiguration      
    @AutoConfigurationPackage     
        @Import(AutoConfigurationPackages.Registrar.class)    
    @Import(AutoConfigurationImportSelector.class)            
@ComponentScan(excludeFilters = { 
        @ComponentScan.Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class), 类型排除过滤器
        @ComponentScan.Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) 配置类型过滤器
    })


   @Import(AutoConfigurationPackages.Registrar.class)    设置当前配置所在的包作为扫描包，后续要针对当前的包进行扫描
   @Import(AutoConfigurationImportSelector.class)        
```

注解层次：



~~~mermaid
graph LR
a(SpringBootConfiguration) -->a1(Configuration)-->a12(Component) 
a(SpringBootConfiguration) -->a2(Indexed)
b(EnableAutoConfiguration) -->b1(AutoConfigurationPackage)-->b12(Import AutoConfigurationPackages.Registrar.class) 
b(EnableAutoConfiguration) -->b2(Import AutoConfigurationImportSelector.class)
c(ComponentScan) -->c1(ComponentScan.Filter)
~~~

### 3.1.4 自动配置原理

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220520215501306.png" alt="image-20220520215501306" style="zoom:67%;" />







### 自定义Starter



#### 案例  ：统计独立ip访问次数

1. 每次访问网站行为均进行统计
2. 后台每10秒输出一次监控信息 （格式：IP + 访问次数）

**需求分析：** 

1. 数据记录位置：Map / Redis     （本次使用Map）
2. 功能触发位置：每次Web请求（拦截器）
   1. 一：降低难度，主动请求，仅统计单一操作访问次数（查询等）
   2. 二：开发拦截器
3. 业务参数  （ 配置顶 ）
   1. 输出频度：默认10秒
   2. 数据特征：累计数据 / 阶段数据，默认累计数据
   3. 输出格式：详细模式 / 极简模式   

**自定义starter**

完成业务定时功能显示报表



**开启yml提升功能：**

1. 导入配置处理器坐标：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
</dependency>
```

2. 进行自定义提示功能开发

   ```json
   "hints": [
     {
       "name": "tools.ip.model",
       "values": [
         {
           "value": "detail",
           "description": "详细模式."
         },
         {
           "value": "simple",
           "description": "极简模式."
         }
       ]
     }
   ```





## 3.2核心原理

### 3.2.1启动流程

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220522110829463.png" alt="image-20220522110829463" style="zoom: 80%;" />

1. 初始化数据
2. 创建容器



```java
Springboot30StartupApplication【10】->SpringApplication.run(Springboot30StartupApplication.class, args);
    SpringApplication【1332】->return run(new Class<?>[] { primarySource }, args);
        SpringApplication【1343】->return new SpringApplication(primarySources).run(args);
            SpringApplication【1343】->SpringApplication(primarySources)
            # 加载各种配置信息，初始化各种配置对象
                SpringApplication【266】->this(null, primarySources);
                    SpringApplication【280】->public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources)
                        SpringApplication【281】->this.resourceLoader = resourceLoader;
                        # 初始化资源加载器
                        SpringApplication【283】->this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
                        # 初始化配置类的类名信息（格式转换）
                        SpringApplication【284】->this.webApplicationType = WebApplicationType.deduceFromClasspath();
                        # 确认当前容器加载的类型
                        SpringApplication【285】->this.bootstrapRegistryInitializers = getBootstrapRegistryInitializersFromSpringFactories();
                        # 获取系统配置引导信息
                        SpringApplication【286】->setInitializers((Collection) getSpringFactoriesInstances(ApplicationContextInitializer.class));
                        # 获取ApplicationContextInitializer.class对应的实例
                        SpringApplication【287】->setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
                        # 初始化监听器，对初始化过程及运行过程进行干预
                        SpringApplication【288】->this.mainApplicationClass = deduceMainApplicationClass();
                        # 初始化了引导类类名信息，备用
            SpringApplication【1343】->new SpringApplication(primarySources).run(args)
            # 初始化容器，得到ApplicationContext对象
                SpringApplication【323】->StopWatch stopWatch = new StopWatch();
                # 设置计时器
                SpringApplication【324】->stopWatch.start();
                # 计时开始
                SpringApplication【325】->DefaultBootstrapContext bootstrapContext = createBootstrapContext();
                # 系统引导信息对应的上下文对象
                SpringApplication【327】->configureHeadlessProperty();
                # 模拟输入输出信号，避免出现因缺少外设导致的信号传输失败，进而引发错误（模拟显示器，键盘，鼠标...）
                    java.awt.headless=true
                SpringApplication【328】->SpringApplicationRunListeners listeners = getRunListeners(args);
                # 获取当前注册的所有监听器
                SpringApplication【329】->listeners.starting(bootstrapContext, this.mainApplicationClass);
                # 监听器执行了对应的操作步骤
                SpringApplication【331】->ApplicationArguments applicationArguments = new DefaultApplicationArguments(args);
                # 获取参数
                SpringApplication【333】->ConfigurableEnvironment environment = prepareEnvironment(listeners, bootstrapContext, applicationArguments);
                # 将前期读取的数据加载成了一个环境对象，用来描述信息
                SpringApplication【333】->configureIgnoreBeanInfo(environment);
                # 做了一个配置，备用
                SpringApplication【334】->Banner printedBanner = printBanner(environment);
                # 初始化logo
                SpringApplication【335】->context = createApplicationContext();
                # 创建容器对象，根据前期配置的容器类型进行判定并创建
                SpringApplication【363】->context.setApplicationStartup(this.applicationStartup);
                # 设置启动模式
                SpringApplication【337】->prepareContext(bootstrapContext, context, environment, listeners, applicationArguments, printedBanner);
                # 对容器进行设置，参数来源于前期的设定
                SpringApplication【338】->refreshContext(context);
                # 刷新容器环境
                SpringApplication【339】->afterRefresh(context, applicationArguments);
                # 刷新完毕后做后处理
                SpringApplication【340】->stopWatch.stop();
                # 计时结束
                SpringApplication【341】->if (this.logStartupInfo) {
                # 判定是否记录启动时间的日志
                SpringApplication【342】->    new StartupInfoLogger(this.mainApplicationClass).logStarted(getApplicationLog(), stopWatch);
                # 创建日志对应的对象，输出日志信息，包含启动时间
                SpringApplication【344】->listeners.started(context);
                # 监听器执行了对应的操作步骤
                SpringApplication【345】->callRunners(context, applicationArguments);
                #
                SpringApplication【353】->listeners.running(context);
                # 监听器执行了对应的操作步骤
```



容器选择类型





监听器

![image-20220522153759448](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220522153759448.png)





