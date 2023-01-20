> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



## 一微服务技术栈

微服务技术框架

![image-20220725210537787](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220725210537787.png)

# 微服务架构

单体架构：所有功能集中在一个项目种开发，打包部署

- 架构简单
- 部署成本低
- 耦合度高

分布式架构：根据业务功能对系统进行拆分，每个业务模块单独开发

- 降低服务耦合
- 有利于服务升级扩展

微服务：分布式架构的优化设计方案

- 单一职责：拆分粒度更小，每一个服务对应唯一的业务能力
- 面向服务：微服务对外的业务接口
- 自治：团队独立、技术独立、数据独立、部署独立
- 隔离性强：服务调用做好隔离、容错、降级、避免出现级联问题
- 架构赋值、运维、监控、部署难度提高

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726131725096.png" alt="image-20220726131725096" style="zoom:80%;" />

### 微服务技术对比

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726162519337.png" alt="image-20220726162519337" style="zoom:80%;" />



## Springcloud

https://spring.io/projects/spring-cloud



### 服务拆分及远程调用

拆分

- 不同微服务，不要重复开发相同业务
- 微服务数据独立
- 暴露业务接口，让其他微服务调用



RestTemplate 发起远程http请求

```java
/**
 * 创建RestTemplate 并注入容器种
 * @return RestTemplate
 */
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

```java
@Autowired
private RestTemplate restTemplate;

public Order queryOrderById(Long orderId) {
    // 1.查询订单
    Order order = orderMapper.findById(orderId);
    // 2.利用RestTemplate发起http请求，查询用户
    // 2.1.url路径
    String url = "http://userservice/user/" + order.getUserId();
    // 2.2.发送http请求，实现远程调用
    User user = restTemplate.getForObject(url, User.class);
    // 3.封装user到Order
    order.setUser(user);
    // 4.返回
    return order;
}
```



提供者：一次业务种，被其他微服务调用的服务 （提供接口给其他微服务）

消费者：一次业务种，调用其他微服务的服务（调用其他微服务提供的接口）

# Eureka 

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726180838738.png" alt="image-20220726180838738" style="zoom:80%;" />



```xml
<!--eureka服务端-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

添加Eureka注解

```java
@EnableEurekaServer
@SpringBootApplication
public class EurekaApplication {
    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
    }
}
```

```yaml
server:
  port: 10086 # 服务端口
spring:
  application:
    name: eurekaserver # eureka的服务名称
eureka:
  client:
    service-url:  # eureka的地址信息
      defaultZone: http://127.0.0.1:10086/eureka
```



注册

1. 引入pom.xml

   ~~~xml
   <dependency>
          <groupId>org.springframework.cloud</groupId>
          <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
   </dependency>
   ~~~

   

2. 配置文件种，引入客户端配置

   ```yaml
   eureka:
     client:
       service-url:  # eureka的地址信息
         defaultZone: http://127.0.0.1:10086/eureka
   ```

# Ribbon 负载均衡

## 原理

![image-20220726202143074](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726202143074.png)

![image-20220726202931028](Springcloud.assets/image-20220726202931028.png)



IRle接口：

![image-20220726203115222](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726203115222.png)



修改负载均衡规则

 <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220726204812321.png" alt="image-20220726204812321" style="zoom:80%;" />



# nacos 注册中心



## Nacos 配置管理

### 配置的自动刷新（两种方式）

1. @RefreshScope ：自动更新注解 
2. @ConfigurationProperties注解

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728142103043.png" alt="image-20220728142103043" style="zoom:67%;" />

### 多环境配置共享

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728142952131.png" alt="image-20220728142952131" style="zoom:80%;" />

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728143013037.png" alt="image-20220728143013037" style="zoom:67%;" />



## Feign 远程调用

- 实现http请求

定义和实用Fergn

1. 配置依赖pom.xml
2. 开启客客户端服务
   - 配置注解@EnableFeignClients
3. 配置Feign客户端（接口）
   - 注解配置@FeignClient
   - 方法里面实用@GetMapping注解说明路径



### 自定义配置Feign

配置类型：（主要就是配置日志）

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728173236087.png" alt="image-20220728173236087" style="zoom:80%;" />

```java
public class DefaultFeignConfiguration {
    @Bean
    public Logger.Level logLevel(){
        return Logger.Level.BASIC;
    }
}
```

```java
@FeignClient(value = "userservice")  // 注解声明
public interface UserClient {

    @GetMapping("/user/{id}")
    User findById(@PathVariable("id") Long id);
}
```

### 性能优化

- URLConnection：默认实现，不支持连接池

- Apache HttpClient ：支持连接池

  配置连接池

  ~~~yaml
  feign:
    httpclient:
      enabled: true # 支持HttpClient的开关
      max-connections: 200 # 最大连接数
      max-connections-per-route: 50 # 单个路径的最大连接数
  ~~~

- OKHttp：支持连接池

主要的优化点：

1. 使用连接池代替默认的URLConnection
2. 日志级别，最好用basic或者none



### 最佳实践

1. controller和Feigin统一为接口
2. Feign作为独立模块，把POJO、默认的Feign放在这个模块当中

![image-20220728180519885](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728180519885.png)



![image-20220728181336236](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728181336236.png)



## Gateway 服务网关

功能

- 身份认证和权限校验
- 服务路由、负载均衡
- 请求限流



技术实现

- gateway：基于WebFlux，响应式编程。
- zuul：基于Servlet的实现，阻塞式编程。



断言：

- 目的为了表示与验证开发者预期的结果

- 当程序执行到断言的位置时，对应的断言应该为真。若断言不为真时，程序会中止执行，并给出错误信息。





搭建网关

1. 引入SpringCloudGateway 和 nacos 依赖

   ```xml
   <dependencies>
       <!--nacos服务注册发现依赖-->
       <dependency>
           <groupId>com.alibaba.cloud</groupId>
           <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
       </dependency>
       <!--网关gateway依赖-->
       <dependency>
           <groupId>org.springframework.cloud</groupId>
           <artifactId>spring-cloud-starter-gateway</artifactId>
       </dependency>
   </dependencies>
   ```

2. 编写路由配置和 nacos 地址

   ```yml
   server:
     port: 10010
   logging:
     level:
       cn.itcast: debug
     pattern:
       dateformat: MM-dd HH:mm:ss:SSS
   spring:
     application:
       name: gateway
     cloud:
       nacos:
         server-addr: nacos:8848 # nacos地址
       gateway:
         routes:
           - id: user-service # 路由标示，必须唯一
             uri: lb://userservice # 路由的目标地址 lb:loadBalance
             predicates: # 路由断言，判断请求是否符合规则
               - Path=/user/** # 路径断言，判断路径是否是以/user开头，如果是则符合
           - id: order-service
             uri: lb://orderservice
             predicates:
               - Path=/order/**  # 路径断言，判断路径是否是以/order开头，如果是则符合
         default-filters: # 默认过滤器，也是全局过滤器
           - AddRequestHeader=Truth,Itkcs is very happy
   ```

### 路由断言工厂 Route Predicate Factory

- 读取用户定义的断言条件，对请求做出判断

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728201747941.png" alt="image-20220728201747941" style="zoom:80%;" />

### 路由过滤器 GatewayFilter

- 对路由的请求或响应做加工处理，比如添加请求头配置
- 在路由下的过滤器只对当前路由的请求生效

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220728202446524.png" alt="image-20220728202446524" style="zoom:80%;" />



### 全局过滤器 GlobalFilter

- 自己写逻辑代码实现

  ```java
  @Component
  public class AuthorizeFilter implements GlobalFilter, Ordered {
      @Override
      public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
          // 1.获取请求参数
          ServerHttpRequest request = exchange.getRequest();
          MultiValueMap<String, String> params = request.getQueryParams();
          // 2.获取参数中的 authorization 参数
          String auth = params.getFirst("authorization");
          // 3.判断参数值是否等于 admin
          if ("admin".equals(auth)) {
              // 4.是，放行 chain的方法filter
              return chain.filter(exchange);
          }
          // 5.否，拦截
          // 5.1.设置状态码
          exchange.getResponse().setStatusCode(HttpStatus.UNAUTHORIZED);
          // 5.2.拦截请求
          return exchange.getResponse().setComplete();
      }
  
      @Override
      public int getOrder() {
          return -1;
      }
  }
  ```



### 过滤器执行顺序

- 每一个过滤器都必须指定一个int类型的order值,==order值越小，优先级越高，执行顺序越靠前==
- GlobalFilter通过实现Ordered接口，或者添加@Order注解来指定order值，由我们自己指定
- 路由过滤器和defaultFilter的order由Spring指定，默认是按照声明顺序从1递增
- 当过滤器的order值一样时，会按照defaultFilter > 路由过滤器 > GlobalFilter 的顺序执行



### 跨域问题

- 域名不同
- 域名相同，端口不同

CORS跨域配置



# Docker

兼容问题

- 将应用Libs（函数库）与应用、配置、依赖一起打包，形成镜像，可以迁移到任意Linux操作系统
- Docker运行在容器中，相互隔离

## Docker架构

- 服务端:接收命令或远程请求，操作镜像或容器
- 客户端:发送命令或者请求到Docker服务端

![image-20220729101503220](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729101503220.png)



## Docker基本操作

- 构建镜像：docker build 
- 拉取镜像：docker pull
- 查看镜像：docker image
- 删除镜像：docker rmi（remove image）
- 推送镜像到服务：docker push
- 保存镜像为压缩包：docker save
- 加载压缩包为镜像：docker load

练习：使用的指令

![image-20220729110232228](Springcloud.assets/image-20220729110232228.png)

### 容器

- 运行：docker run
- 暂停：docker pause
- 暂停到运行：docker unpause
- 运行到停止：docker stop  容器ID
- 停止到运行：docker start
- 查看容器运行日志：docker log
- 查看所有容器运行状态：docker ps
- 进入容器执行命令：docker exce
- 删除指定的容器：docker rm  容器ID

先停止了对应的docker images ，再进行删除images

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729110609838.png" alt="image-20220729110609838" style="zoom: 80%;" />

docker run命令的常见参数

- --name:指定容器名称
- -p：指定端口映射
- -d：让容器后台运行
- 查看容器日志的命令
- docker logs

- 添加-f 参数可以持续查看日志

  查看容器状态:

  docker ps



## 数据卷（volume）

- 虚拟目录，指向宿主机文件系统中的某个目录
- 将容器与数据分离，解耦合，方便操作容器内数据，保证数
  据安全

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729140455568.png" alt="image-20220729140455568" style="zoom:80%;" />

~~~~
docker volume create ns

docker volume ls 

docker volume inspect ns

docker volume prune
~~~~



### 挂载数据卷

![image-20220729141139343](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729141139343.png)



## DockerFile自定义镜像



### 镜像结构

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729143658135.png" alt="image-20220729143658135" style="zoom:80%;" />

### DockerFile 

- 通过指令来构建镜像，每一层就会形成一个Layer

 ![image-20220729143941923](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220729143941923.png)

`DockerFile`

~~~dockerfile
# 指定基础镜像
FROM ubuntu:16.04
#FROM java:8-alpine
# 配置环境变量，JDK的安装目录
ENV JAVA_DIR=/usr/local

# 拷贝jdk和java项目的包
COPY ./jdk8.tar.gz $JAVA_DIR/
COPY ./docker-demo.jar /tmp/app.jar

# 安装JDK
RUN cd $JAVA_DIR \
 && tar -xf ./jdk8.tar.gz \
 && mv ./jdk1.8.0_144 ./java8

# 配置环境变量
ENV JAVA_HOME=$JAVA_DIR/java8
ENV PATH=$PATH:$JAVA_HOME/bin

# 暴露端口
EXPOSE 8090
# 入口，java项目的启动命令
ENTRYPOINT java -jar /tmp/app.jar
~~~



## Docker-Compose

- 基于Compose文件快速部署分布式应用
- Compose通过指定定义集群中的每个文件运行



## Docker镜像仓库

- 推送本地镜像到仓库前都必须重命名(docker tag)镜像，以镜像仓库地址为前缀
- 镜像仓库推送前需要把仓库地址配置到docker
- 服务的 daemon.json 文件中，被docker信任
- 推送使用 docker push 命令

- 拉取使用docker pull命令



# 服务异步通讯

## MQ（消息队列）

- 事件驱动架构（Broker）

四种MQ：主要是使用RabbiMQ 、RocketMQ、Kafka

![image-20220730105608442](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730105608442.png)



- 基本消息队列

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730114035227.png" alt="image-20220730114035227" style="zoom:80%;" />

  <img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730115054491.png" alt="image-20220730115054491" style="zoom:50%;" />

- 工作消息队列

- 发布、订阅



### 同步通讯

- 实时调用，存在耦合高问题，存在饥饿问题，吞吐量下降，性能下降，资源浪费，级联失败



### 异步通讯

事件驱动模式（broker）

1. 服务解耦
2. 性能提升（消耗时间减少），吞吐量提高
3. 服务没有强依赖，不担心级联失败问题
4. 流量消峰，降低并发量
5. Broker 的可靠性，吞吐能力，安全性
6. 架构复杂，没有业务流程线不好追踪管理



## SpringAMQP

- 用于应用程序或之间传递业务消息的开放标准。协议与语言和平台无关，符合微服务独立性的要求

发送消息



接收信息

1. 引入依赖
2. 配置地址：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730121616674.png" alt="image-20220730121616674" style="zoom:80%;" />



### WorkQueue 工作队列

- 提高消息处理速度，避免队列消息堆积

preFetch：控制预取的消息上线



### 发布、订阅

- 加入交换机（exchange）
  1. 广播：Fanout
  2. 路由：Direct
  3. 主题：Topic



### 消息转换器





# 分布式搜索

## elasticsearch（ES）

- 搜索引擎

主要是技术栈

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730160916660.png" alt="image-20220730160916660" style="zoom: 50%;" />

### 倒排索引

- 文档（document）：每条数据就是一个文档
- 词条（term）：文档按照语义分成词语，不可以重复
- 面向文档存储，文档数据序列化为 JSON 格式

#### mysql 与 es 对比

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730162521814.png" alt="image-20220730162521814" style="zoom:80%;" />

- 索引:同类型文档的集合
- 映射:索引中文档的约束，比如字段名称、类型



[安装文档指导](E:\Springcloud\study notes\install Step\安装elasticsearch.md)



### IK分词器

- 创建倒序索引时对文档分词
- 用户搜索时，对输入的内容分词

模式：

- ik_smart:智能切分，粗粒度
- ik_max_word:最细切分，细粒度

扩展词汇、禁止敏感词语

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220730193748899.png" alt="image-20220730193748899" style="zoom: 80%;" />

## 索引库操作



### mapping 映射属性

- type：字段数据类型
  - 字符串：text（可分词的文本）、keyword（精确值）
  - 数值：long、integer、short、byte、double
  - 布尔：boolean
  - 日期：date
  - 对象：object
- index：是否创建索引，默认true
- analyzer：分词器
- properties：字段的子字段

### 创建索引库

- ES通过Restful 请求操作索引库

~~~
PUT / 索引库名
~~~

### 查询索引库

~~~
GET /索引库名
~~~

### 删除索引库

~~~】
DELETE /索引库名
~~~

### 添加字段

~~~
PUT /索引库名/_mapping
~~~

## 文档操作



### 新增文档

~~~
POST /索引库名/_doc/文档id
~~~

### 删除文档

~~~
DELETE /索引库名/_doc/文档id
~~~

### 修改文档

全量修改

~~~
PUT /索引库名/_doc/文档id
~~~

局部修改

~~~
POST /索引库名/_update/文档id
~~~

### 查询文档

~~~
GET /索引库名/_doc/文档id
~~~



## RestClient操作索引库



### mapping 映射

索引的增删改查方法

```java
@SpringBootTest
class HotelIndexTest {

    private RestHighLevelClient client;

    @Test
    void testCreateIndex() throws IOException {
        // 1.准备Request      PUT /hotel
        CreateIndexRequest request = new CreateIndexRequest("hotel");
        // 2.准备请求参数
        request.source(MAPPING_TEMPLATE, XContentType.JSON);
        // 3.发送请求
        client.indices().create(request, RequestOptions.DEFAULT);
    }

    @Test
    void testExistsIndex() throws IOException {
        // 1.准备Request
        GetIndexRequest request = new GetIndexRequest("hotel");
        // 3.发送请求
        boolean isExists = client.indices().exists(request, RequestOptions.DEFAULT);

        System.out.println(isExists ? "存在" : "不存在");
    }
    @Test
    void testDeleteIndex() throws IOException {
        // 1.准备Request
        DeleteIndexRequest request = new DeleteIndexRequest("hotel");
        // 3.发送请求
        client.indices().delete(request, RequestOptions.DEFAULT);
    }


    @BeforeEach
    void setUp() {
        client = new RestHighLevelClient(RestClient.builder(
                HttpHost.create("http://192.168.150.101:9200") //虚拟机CetOS地址
        ));
    }

    @AfterEach
    void tearDown() throws IOException {
        client.close();
    }
    
}
```



### RestClient 文档操作

```java
@SpringBootTest
class HotelDocumentTest {

    private RestHighLevelClient client;

    @Autowired
    private IHotelService hotelService;

    /**
     * 创建文档
     * @throws IOException
     */
    @Test
    void testAddDocument() throws IOException {
        // 1.查询数据库hotel数据
        Hotel hotel = hotelService.getById(61083L);
        // 2.转换为HotelDoc
        HotelDoc hotelDoc = new HotelDoc(hotel);
        // 3.转JSON
        String json = JSON.toJSONString(hotelDoc);

        // 1.准备Request
        IndexRequest request = new IndexRequest("hotel").id(hotelDoc.getId().toString());
        // 2.准备请求参数DSL，其实就是文档的JSON字符串
        request.source(json, XContentType.JSON);
        // 3.发送请求
        client.index(request, RequestOptions.DEFAULT);
    }

    /**
     * 根据ID查询文档
     * @throws IOException
     */
    @Test
    void testGetDocumentById() throws IOException {
        // 1.准备Request      // GET /hotel/_doc/{id}
        GetRequest request = new GetRequest("hotel", "61083");
        // 2.发送请求
        GetResponse response = client.get(request, RequestOptions.DEFAULT);
        // 3.解析响应结果
        String json = response.getSourceAsString();

        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        System.out.println("hotelDoc = " + hotelDoc);
    }

    /**
     * 根据ID删除文档
     * @throws IOException
     */
    @Test
    void testDeleteDocumentById() throws IOException {
        // 1.准备Request      // DELETE /hotel/_doc/{id}
        DeleteRequest request = new DeleteRequest("hotel", "61083");
        // 2.发送请求
        client.delete(request, RequestOptions.DEFAULT);
    }

    /**
     * 根据ID修改文档
     * @throws IOException
     */
    @Test
    void testUpdateById() throws IOException {
        // 1.准备Request
        UpdateRequest request = new UpdateRequest("hotel", "61083");
        // 2.准备参数
        request.doc(
                "price", "870"
        );
        // 3.发送请求
        client.update(request, RequestOptions.DEFAULT);
    }

    /**
     * 批量导入数据
     * @throws IOException
     */
    @Test
    void testBulkRequest() throws IOException {
        // 查询所有的酒店数据
        List<Hotel> list = hotelService.list();

        // 1.准备Request
        BulkRequest request = new BulkRequest();
        // 2.准备参数
        for (Hotel hotel : list) {
            // 2.1.转为HotelDoc
            HotelDoc hotelDoc = new HotelDoc(hotel);
            // 2.2.转json
            String json = JSON.toJSONString(hotelDoc);
            // 2.3.添加请求
            request.add(new IndexRequest("hotel").id(hotel.getId().toString()).source(json, XContentType.JSON));
        }

        // 3.发送请求
        client.bulk(request, RequestOptions.DEFAULT);
    }

    @BeforeEach
    void setUp() {
        client = new RestHighLevelClient(RestClient.builder(
                HttpHost.create("http://192.168.150.101:9200")//虚拟机地址
        ));
    }

    @AfterEach
    void tearDown() throws IOException {
        client.close();
    }
}
```



# 分布式搜索引擎

## DSL查询文档

### DSL查询分类

1. 查询所有数据：match_all
2. 全文检索（full text）查询：利用分词器对内容进行分词
   - match_query
   - mutl_match_query
3. 精确查询：精确词条查询数据
   - ids
   - range
   - term
4. 地理（geo）查询
   - geo_distance 
   - geo_bounding_box
5. 复合查询：
   - bool
   - function_score

#### 基本语法

~~~q
GET /indexName/_search
{
	"query":{
		"查询类型":{
			"查询条件":"条件值"
		}
	}
}


//查询所有
GET /test/_search
{
	"query":{
		"match_all":{
		}
	}
}
~~~

### 全文检索查询

> 对用户输入内容分词，用于搜索框搜索

#### match_query

推荐使用

~~~q
GET /indexName/_search
{
	"query":{
		"match":{
			"FIELD":"TEXT"
		}
	}
}
~~~

#### mutl_match_query

性能较差

~~~GET /indexName/_search
GET /indexName/_search
{
	"query":{
		"mutl_match":{
			"query":"搜索内容"
			"FIELD":["字段1","字段2","字段n"]
		}
	}
}
~~~

### 精准查询

- 一般是查找不需要分词的内容

term：根据词条精确值查询 （输入的内容和查询的内容完全一致才可以得到搜索结果）

~~~q
GET /indexName/_search
{
	"query":{
		"term":{
			"FIELD":{
				"value":"VALUE"
			}
		}
	}
}
~~~

range：根据值的范围查询

~~~q
GET /indexName/_search
{
	"query":{
		"range":{
			"FIELD":{
					"gte":100  //大于等于	
					"lte":200  //小于等于
			}
		}
	}
}
~~~

### 地理坐标查询

geo_bounding_box ：查询geo_point值落在某个矩形范围的所有文档

~~~q
GET /indexName/_search
{
	"query":{
		"geo_bounding_box":{
			"FIELD":{
				"top_left":{
					"lat":31.1,
					"lon":123.1
				},
				"bottom_right":{
					"lat":33.1,
					"lon":113.1
				}				
			}
		}
	}
}
~~~

geo_distance ：查询到指定中心点小于某个距离值的所有文档

~~~
GET /indexName/_search
{
	"query":{
		"geo_distance":{
			"distance":"1KM"
			"FIELD":"31.5,45.5"  //中心点坐标
		}
	}
}
~~~

### 复合查询（compound）

- function score：算分函数查询，控制文档相关性算分

相关性算分

![image-20220731155409713](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731155409713.png)

![image-20220731155600427](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731155600427.png)

![image-20220731155725439](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731155725439.png)



![image-20220731160206053](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731160206053.png)



Boolean Query

- must：必须匹配每个子查询 "与"
- should：选择性匹配子查询 “或”
- must_not：必须不匹配，不参与算分 “非”
- filter：必须匹配，不参与算分

## 搜索结果处理

### sort：排序

- 正序：ASC
- 倒叙：DESC

![image-20220731161730339](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731161730339.png)



### 分页

- from
- size

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731162345686.png" alt="image-20220731162345686" style="zoom:80%;" />



### 深度分页

- search after：分页时需要排序，原理是从上一个的排序值开始，查询**下一页**数据
- scroll：原理排序数据形成快照，保存在内存。消耗内存大

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731163101658.png" alt="image-20220731163101658" style="zoom:80%;" />



### 高亮

- 搜索结果中，搜索关键字突出显示

原理

- 在页面中的标签添加css样式



## RestClient 查询文档

基本步骤：

1. 创建SearchRequest对象

2. 准备Request.source()，也就是DSL。

   ① QueryBuilders来构建查询条件

   ② 传入Request.source() 的 query() 方法

3. 发送请求，得到结果

4. 解析结果（参考JSON结果，从外到内，逐层解析）

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731170956218.png" alt="image-20220731170956218" style="zoom:80%;" />

~~~java
@Test
void testMatchAll() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    request.source()
        .query(QueryBuilders.matchAllQuery());
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
 
    // 4.解析响应
    handleResponse(response);
}
 
private void handleResponse(SearchResponse response) {
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        System.out.println("hotelDoc = " + hotelDoc);
    }
}
~~~

### 全文检索查询

~~~java
@Test
void testMatch() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    request.source()
        .query(QueryBuilders.matchQuery("all", "如家"));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
 
}

~~~

==抽取相同的代码 ：Ctrl + Alt + m==

### 布尔查询

~~~java
@Test
void testBool() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.准备BooleanQuery
    BoolQueryBuilder boolQuery = QueryBuilders.boolQuery();
    // 2.2.添加term
    boolQuery.must(QueryBuilders.termQuery("city", "杭州"));
    // 2.3.添加range
    boolQuery.filter(QueryBuilders.rangeQuery("price").lte(250));
 
    request.source().query(boolQuery);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
 
}
~~~



### 精确查询

~~~java
 		/*
     * term精确查询测试
     * */
    @Test
    void testMatchTerm() throws IOException {
        //1:准备request
        SearchRequest request = new SearchRequest("hotel");
        //2:组织DSL参数
        request.source()
                .query(QueryBuilders.termQuery("all","如家"));
        //3:发送请求，得到响应结果
        SearchResponse search = client.search(request, RequestOptions.DEFAULT);
        //4:输出响应结果
        handleResponse(search);
    }
~~~



### 排序、分页

~~~java
@Test
void testPageAndSort() throws IOException {
    // 页码，每页大小
    int page = 1, size = 5;
 
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.query
    request.source().query(QueryBuilders.matchAllQuery());
    // 2.2.排序 sort
    request.source().sort("price", SortOrder.ASC);
    // 2.3.分页 from、size
    request.source().from((page - 1) * size).size(5);
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleResponse(response);
 
}

~~~

### 高亮

解析

![image-20220731173645428](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731173645428.png)

代码

~~~java
@Test
void testHighlight() throws IOException {
    // 1.准备Request
    SearchRequest request = new SearchRequest("hotel");
    // 2.准备DSL
    // 2.1.query
    request.source().query(QueryBuilders.matchQuery("all", "如家"));
    // 2.2.高亮
    request.source().highlighter(new HighlightBuilder().field("name").requireFieldMatch(false));
    // 3.发送请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析响应
    handleHighResponse(response);
 
} 

public void handleHighResponse(SearchResponse response){
    // 4.解析响应
    SearchHits searchHits = response.getHits();
    // 4.1.获取总条数
    long total = searchHits.getTotalHits().value;
    System.out.println("共搜索到" + total + "条数据");
    // 4.2.文档数组
    SearchHit[] hits = searchHits.getHits();
    // 4.3.遍历
    for (SearchHit hit : hits) {
        // 获取文档source
        String json = hit.getSourceAsString();
        // 反序列化
        HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
        // 获取高亮结果
        Map<String, HighlightField> highlightFields = hit.getHighlightFields();
        if (!CollectionUtils.isEmpty(highlightFields)) {
            // 根据字段名获取高亮结果
            HighlightField highlightField = highlightFields.get("name");
            if (highlightField != null) {
                // 获取高亮值
                String name = highlightField.getFragments()[0].string();
                // 覆盖非高亮结果
                hotelDoc.setName(name);
            }
        }
        System.out.println("hotelDoc = " + hotelDoc);
    }
 }
~~~



## 数据聚合

聚合（aggregations）

- 桶（Bucket）集合：用来对文档做分组
  - TermAggregations：安装字段值分组
  - DateHistogram：按照日期阶梯分组
- 度量（Metric）集合：数值类
  - Avg
  - Max
  - Min
  - Stats：求max、min、avg、sum等
- 管道（pipeline）聚合

参与集合的字段类型

- keyword
- 数值
- 日期
- 布尔

### DSL实现Bucket聚合

聚合三要素

- 聚合名称
- 聚合类型
- 聚合字段

聚合可配置属性

1. size：结果数量
2. order：排序方式
3. field：字段

term类型

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731175238544.png" alt="image-20220731175238544" style="zoom:80%;" />

 升序 

~~~
"order":{
	"字段":ASC / DESC
}
~~~

限定范围

~~~q
"range":{
	"字段":{
		lte:
		gte:
	}
}
~~~



### DSL实现Metrics聚合

- Avg
- Max
- Min
- Stats：求max、min、avg、sum等

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220731205325649.png" alt="image-20220731205325649" style="zoom:80%;" />





## 自动补全

### 分词器

- character filters：在tokenizer之前对文本进行处理。例如删除字符、替换字符
- tokenizer：将文本按照一定的规则切割成词条(term)。例如keyword，就是不分词;还有ik_smart
- tokenizer filter：将tokenizer输出的词条做进一步处理。例如大小写转换、同义词处理、拼音处理等

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801094800352.png" alt="image-20220801094800352" style="zoom:80%;" />



### RestAPI实现自动补全

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801100415247.png" alt="image-20220801100415247" style="zoom:80%;" />

```java
@Test
void testSuggest() throws IOException {
    // 1.准备请求
    SearchRequest request = new SearchRequest("hotel");
    // 2.请求参数
    request.source().suggest(new SuggestBuilder()
            .addSuggestion(
                    "hotelSuggest",
                    SuggestBuilders
                            .completionSuggestion("suggestion")
                            .size(10)
                            .skipDuplicates(true)
                            .prefix("s")  //根据拼音首字母来补全查询内容
            ));
    // 3.发出请求
    SearchResponse response = client.search(request, RequestOptions.DEFAULT);
    // 4.解析
    Suggest suggest = response.getSuggest();
    // 4.1.根据名称获取结果
    CompletionSuggestion suggestion = suggest.getSuggestion("hotelSuggest");
    // 4.2.获取options
    for (CompletionSuggestion.Entry.Option option : suggestion.getOptions()) {
        // 4.3.获取补全的结果
        String str = option.getText().toString();
        System.out.println(str);
    }
}
```

## 数据同步

方案一：同步调用

- 简单粗暴
- 业务耦合高

![image-20220801101255766](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801101255766.png)

方案二：异步通知

- 低耦合
- 依赖mq的可靠性

![image-20220801101525792](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801101525792.png)

方案三：监听binlog

- 耦合低、实现复杂

![image-20220801101629422](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801101629422.png)



### MQ实现数据同步





## ES集群

- 海量数据存储问题：将索引库从逻辑上分为N个分片（shard），存储到多个节点
- 单点故障问题：将分片数据在不同节点备份（replica）

### 节点角色

![image-20220801112122603](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801112122603.png)



# 微服务保护



## 雪崩问题及解决方案



### 雪崩问题

服务器支持的线程和并发数有限，请求一直阻塞，会导致服务器资源耗尽，从而导致所有其它服务都不可用，那么当前服务也就不可用了。

那么，依赖于当前服务的其它服务随着时间的推移，最终也都会变的不可用，形成级联失败，雪崩就发生了：

![image-20210715172710340](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715172710340.png)



解决雪崩问题的四种方式：

### 1 超时处理

- 超时处理：设定超时时间，请求超过一定时间没有响应就返回错误信息，不会无休止等待


![image-20210715172820438](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715172820438.png)



### 2 仓壁模式

仓壁模式来源于船舱的设计：船舱都会被隔板分离为多个独立空间，当船体破损时，只会导致部分空间进入，将故障控制在一定范围内，避免整个船体都被淹没。

![image-20210715172946352](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715172946352.png)



- 限定每个业务能使用的线程数，避免耗尽整个tomcat的资源，因此也叫线程隔离。


![image-20210715173215243](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715173215243.png)



### 3 断路降级

断路器模式：由**断路器**统计业务执行的异常比例，如果超出阈值则会**熔断**该业务，拦截访问该业务的一切请求。

断路器会统计访问某个服务的请求数量，异常比例：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715173327075.png" alt="image-20210715173327075" style="zoom:80%;" />

当发现访问服务D的请求异常比例过高时，认为服务D有导致雪崩的风险，会拦截访问服务D的一切请求，形成熔断：

<img src="https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715173428073.png" alt="image-20210715173428073" style="zoom: 80%;" />



### 4 限流

**流量控制**：限制业务访问的QPS，避免服务因流量的突增而故障。

![image-20210715173555158](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715173555158.png)







### 总结

- 微服务之间相互调用，因为调用链中的一个服务故障，引起整个链路都无法访问的情况。

解决方案：

**限流**是对服务的保护，==避免因瞬间高并发流量==而导致服务故障，进而避免雪崩。是一种**预防**措施。

**超时处理、线程隔离、降级熔断**是在部分服务故障时，将故障控制在一定范围，避免雪崩。是一种**补救**措施。





## 服务保护技术对比

在SpringCloud当中支持多种服务保护技术：

- [Netfix Hystrix](https://github.com/Netflix/Hystrix)
- [Sentinel](https://github.com/alibaba/Sentinel)
- [Resilience4J](https://github.com/resilience4j/resilience4j)

早期比较流行的是Hystrix框架，但目前国内实用最广泛还是Sentinel框架，对比如下：

|                | **Sentinel**                                   | **Hystrix**                   |
| -------------- | ---------------------------------------------- | ----------------------------- |
| 隔离策略       | 信号量隔离                                     | 线程池隔离 / 信号量隔离       |
| 熔断降级策略   | 基于慢调用比例或异常比例                       | 基于失败比率                  |
| 实时指标实现   | 滑动窗口                                       | 滑动窗口（基于 RxJava）       |
| 规则配置       | 支持多种数据源                                 | 支持多种数据源                |
| 扩展性         | 多个扩展点                                     | 插件的形式                    |
| 基于注解的支持 | 支持                                           | 支持                          |
| 限流           | 基于 QPS，支持基于调用关系的限流               | 有限的支持                    |
| 流量整形       | 支持慢启动、匀速排队模式                       | 不支持                        |
| 系统自适应保护 | 支持                                           | 不支持                        |
| 控制台         | 开箱即用，可配置规则、查看秒级监控、机器发现等 | 不完善                        |
| 常见框架的适配 | Servlet、Spring Cloud、Dubbo、gRPC  等         | Servlet、Spring Cloud Netflix |





## Sentinel介绍和安装



### 初识Sentinel

Sentinel是阿里巴巴开源的一款微服务流量控制组件。官网地址：https://sentinelguard.io/zh-cn/index.html

Sentinel 具有以下特征：

- **丰富的应用场景**：例如秒杀（即突发流量控制在系统容量可以承受的范围）、消息削峰填谷、集群流量控制、实时熔断下游不可用应用等。
- **完备的实时监控**：Sentinel 同时提供实时的监控功能。
- **广泛的开源生态**：Sentinel 提供开箱即用的与其它开源框架/库的整合模块
- **完善的** **SPI** **扩展点**：Sentinel 提供简单易用、完善的 SPI 扩展接口。定制规则管理、适配动态数据源等。



### 安装Sentinel

1）下载

sentinel官方提供了UI控制台，方便我们对系统做限流设置。[GitHub](https://github.com/alibaba/Sentinel/releases)下载。

2）运行

将jar包放到任意非中文目录，执行命令：

```sh
java -jar sentinel-dashboard-1.8.1.jar
```

如果要修改Sentinel的默认端口、账户、密码，可以通过下列配置：

| **配置项**                       | **默认值** | **说明**   |
| -------------------------------- | ---------- | ---------- |
| server.port                      | 8080       | 服务端口   |
| sentinel.dashboard.auth.username | sentinel   | 默认用户名 |
| sentinel.dashboard.auth.password | sentinel   | 默认密码   |

```sh
java -Dserver.port=8090 -jar sentinel-dashboard-1.8.1.jar  # 修改端口
```

3）访问

访问http://localhost:8080页面，就可以看到sentinel的控制台了：需要输入账号和密码，默认都是：sentinel

![image-20220801180604676](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220801180604676.png)





## 微服务整合Sentinel

我们在order-service中整合sentinel，并连接sentinel的控制台，步骤如下：

1）引入sentinel依赖

```xml
<!--sentinel-->
<dependency>
    <groupId>com.alibaba.cloud</groupId> 
    <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
</dependency>
```



2）配置控制台

修改application.yaml文件，添加下面内容：

```yaml
server:
  port: 8088
spring:
  cloud: 
    sentinel:
      transport:
        dashboard: localhost:8080
```



3）访问order-service的任意端点

打开浏览器，访问http://localhost:8088/order/101，这样才能触发sentinel的监控。

然后再访问sentinel的控制台，查看效果：

![image-20210715191241799](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210715191241799.png)



流量控制

隔离和降级

授权规则

规则持久化

分布式事务

多级缓存



分布式缓存

## Redis持久化

### RDB持久化

- Redis数据快照，把内存中的所有数据都记录到磁盘中。当Redis实例故障重启后，从磁盘读取快照文件，恢复数据。

执行命令

- 执行save命令
- 执行bgsave命令
- Redis停机时
- 触发RDB条件时



#### RDB原理

bgsave开始时会fork主进程得到子进程，子进程共享主进程的内存数据。完成fork后读取内存数据并写入 RDB 文件。

fork采用的是copy-on-write技术：

- 当主进程执行读操作时，访问共享内存
- 当主进程执行写操作时，则会拷贝一份数据，执行写操作

![image-20210725151319695](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210725151319695-16594423534471.png)





### AOF持久化

> Append Only File （追加文件）
>
> 执行每一条命令都会得到一个命令日志文件

![image-20210725151543640](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210725151543640.png)



#### AOF配置

AOF默认是关闭的，需要修改redis.conf配置文件来开启AOF：

```properties
# 是否开启AOF功能，默认是no
appendonly yes
# AOF文件的名称
appendfilename "appendonly.aof"
```



AOF的命令记录的**频率**也可以通过redis.conf文件来配：

```properties
# 表示每执行一次写命令，立即记录到AOF文件
appendfsync always 
# 写命令执行完先放入AOF缓冲区，然后表示每隔1秒将缓冲区数据写到AOF文件，是默认方案
appendfsync everysec 
# 写命令执行完先放入AOF缓冲区，由操作系统决定何时将缓冲区内容写回磁盘
appendfsync no
```

三种策略对比：

![image-20210725151654046](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210725151654046.png)



#### AOF文件重写

通过执行 bgrewriteaof 命令，可以让AOF文件执行重写功能，用最少的命令达到相同效果。

![image-20210725151729118](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20210725151729118.png)

AOF原本有三个命令，但是`set num 123 和 set num 666`都是对num的操作，第二次会覆盖第一次的值

重写命令后，AOF文件内容就是：`mset name jack num 666`



Redis也会在触发阈值时自动去重写AOF文件。阈值也可以在redis.conf中配置：

```properties
# AOF文件比上次文件 增长超过多少百分比则触发重写
auto-aof-rewrite-percentage 100
# AOF文件体积最小多大以上才触发重写 
auto-aof-rewrite-min-size 64mb 
```



### RDB与AOF对比

![image-20220802203015847](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802203015847.png)



## Redis主从

- 搭建主从集群，进一步提高Redis的并发能力

![image-20220802203315176](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220802203315176.png)

### 主从数据同步原理

#### 全量同步

- 消耗性能
- repid ：数据集标记，id一致则是相同数据集
- offset：偏移量，随 repl_baklog 增多而增多

![image-20220803154635252](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803154635252.png)

判断第一个同步

![image-20220803155158752](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803155158752.png)



流程：

1. slave节点请求增量同步
2. master 节点判断 replid ，发现不一致，拒绝增量同步
3. master 将完整内存数据生成 RDB，发送 RDB 到slave 
4. slave 清空本地数据，加载master 的RDB
5. master 将RDB期间的命令记录在repl_baklog，并持续将log 中的命令发送给slave
6. slave 执行接收到的命令，保持与 master 之间的同步





#### 增量同步

- slave 重启后同步，执行增量同步

![image-20220803162316353](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803162316353.png)

优化Redis主从集群

- 在master中配置repl-diskless-sync yes启用无磁盘复制，避免全量同步时的磁盘IO
- Redis单节点上的内存占用不要太大，减少RDB导致的过多磁盘IO
- 适当提高repl_baklog的大小，发现slave宕机时尽快实现故障恢复，尽可能避免全量同步
- 主 - 从 - 从 链式结构，减少master 压力

repl_backlog原理



## Redis哨兵

- 监控集群

### 哨兵作用、原理

提供Sentinel 机制 进行监控

- 监控： Sentinel会不断检查您的 master 和 slave 是否按预期工作
- 自动故障恢复：如果 master 故障，Sentinel 会将一个 slave 提升为 master。当故障实例恢复后也以新的master为主
- 通知：Sentinel 充当Redis客户端的服务发现来源，当集群发生故障转移时，会将最新消息推送给Redis 的客户端



服务状态监控

- 主管下线：超过响应时间
- 客观下线：大部分的sentinel 实例下线

故障转移

- 首先选定一个slave作为新的master，执行slaveof no one
- 让所有节点都执行slaveof 新master
- 修改故障节点配置，添加slaveof 新master

哨兵集群



RedisTemplate 哨兵

![image-20220803201637573](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803201637573.png)

![image-20220803201552805](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220803201552805.png)





















































































