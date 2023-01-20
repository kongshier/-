> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿



# 1.MyBatis-Plus简介



## 1.1概念

- 简称MP，是一个MyBatis的增强工具，在MyBatis的基础上只做增强不做改变，为简化开发，提高效率而生。

### 1.1.1MP的特征

1. **无侵入**：只做增强不做改变，引入它不会对现有工程产生影响，如丝般顺滑
2. **损耗小**：启动即会自动注入基本 CURD，性能基本无损耗，直接面向对象操作
3. **强大的 CRUD 操作**：内置通用 Mapper、通用 Service，仅仅通过==少量配置即可实现单表大部分 CRUD 操作==，更有强大的条件构造器，满足各类使用需求
4. **支持 Lambda 形式调用**：通过 Lambda 表达式，方便的编写各类查询条件，无需再担心字段写错
5. **支持主键自动生成**：支持多达 4 种主键策略（内含分布式唯一 ID 生成器 - Sequence），可自由配置，完美解决主键问题
6. **支持 ActiveRecord 模式**：支持 ActiveRecord 形式调用，实体类只需继承 Model 类即可进行强大的 CRUD 操作
7. **支持自定义全局通用操作**：支持全局通用方法注入（ Write once, use anywhere ）
8. **内置代码生成器**：采用代码或者 Maven 插件可快速生成 Mapper 、 Model 、 Service 、 Controller 层代码，支持模板引擎，更有超多自定义配置等您来使用
9. **内置分页插件**：基于 MyBatis 物理分页，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询
10. **分页插件支持多种数据库**：支持 MySQL、MariaDB、Oracle、DB2、H2、HSQL、SQLite、Postgre、SQLServer 等多种数据库
11. **内置性能分析插件**：可输出 SQL 语句以及其执行时间，建议开发测试时启用该功能，能快速揪出慢查询
12. **内置全局拦截插件**：提供全表 delete 、 update 操作智能分析阻断，也可自定义拦截规则，预防误操作



### 1.2MP架构

![image-20220329085339540](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220329085339540.png)



## 1.2整合MyBatis-Plus

- 对于Mybatis整合MP有常常有三种用法，分别是==Mybatis+MP、Spring+Mybatis+MP、Spring Boot+Mybatis+MP==。

1. 创建数据库及表
2. 创建工程
3. MP
   1. 创建子module
   2. MyBatis实现查询User
   3. MyBatis+MP实现查询User
      1. 第一步，将UserMapper继承BaseMapper，将拥有了BaseMapper中的所有方法
      2. 第二步，使用MP中的MybatisSqlSessionFactoryBuilder进程构建（是自己创建生成的）
   4. Spring+MyBatis+MP
      1. 创建子module
      2. 实现查询User
4. SpringBoot+MyBatis+MP
   - 使用SpringBoot将进一步的简化MP的整合，需要注意的是，由于使用SpringBoot需要继承parent，所以需要重新创 建工程，并不是创建子Module。
     1. 创建工程
     1. 导入坐标
     1. 创建编写application.properties
     1. 编写pojo
     1. 编写mapper接口 （加上注解@Runwith，@SpringBootTest：使用的是SpringBoot项目）
     1. 编写启动类
     1. 编写测试类



## 1.3通用CRUD 

- 了解到通过继承BaseMapper就可以获取到各种各样的单表操作，接下来我们将详细讲解这些 操作。

### 1.3.1插入操作

1. 方法定义：int insert(T entity);

2. 测试用例

   ```java
   @RunWith(SpringRunner.class)
   @SpringBootTest
   public class TestUserMapper {
   
       @Autowired
       private UserMapper userMapper;
   
       @Test
       public void testInsert() {
           User user = new User();
           user.setMail("zhugeliang@itcast.cn");
           user.setAge(25);
           user.setUserName("zhugeliang");
           user.setName("诸葛亮");
           user.setPassword("123456");
           user.setAddress("广州");
   
           int result = this.userMapper.insert(user); //result数据库受影响的行数
           System.out.println("result => " + result);
   
           //获取自增长后的id值, 自增长后的id值会回填到user对象中
           System.out.println("id => " + user.getId());
       }
       
   ```

3. 修改User对象 ，使id自增长@TableId(type = IdType.AUTO)   不会出现其他的数字

   ```Java
   @TableId(type = IdType.AUTO) //使id自增长
   private Long id;
   ```

4. @TableField   ：在MP中通过@TableField注解可以指定字段的一些属性

   1. 对象中的属性名和字段名不一致的问题（非驼峰） 
   2. 对象中的属性字段在表中不存在的问题

   ```java
   // 插入数据时进行填充
       @TableField(select = false, fill = FieldFill.INSERT) //查询时不返回该字段的值
       private String password;
       private String name;
       private Integer age;
   
   @TableField(value = "email") //指定数据表中字段名
   private String mail;
   
   @TableField(exist = false)
   private String address; //在数据库表中是不存在的
   ```

### 1.3.2更新操作

1. 一种是根据id更新，
2. 一种是根据条件更新

根据id更新：（测试用例） 

```Java
@Test
public void testUpdateById() {
    User user = new User();
    user.setId(1L); //条件，根据id更新 L是数据类型  此处就是id = 1 的信息会被全部修改
    user.setAge(19); //更新的字段
    user.setPassword("666666");

    int result = this.userMapper.updateById(user);
    System.out.println("result => " + result);
}
```

根据条件更新：

第一种方式： QueryWrapper

```Java
@Test
public void testUpdate() {
    User user = new User();
    user.setAge(20); //更新的字段
    user.setPassword("8888888");

    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //两个参数：column：字段，val：字段的值
    wrapper.eq("user_name", "zhangsan"); //匹配user_name = zhangsan 的用户数据

    //根据条件做更新
    int result = this.userMapper.update(user, wrapper);
    System.out.println("result => " + result);
}
```

第二种方式： UpdateWrapper

```java
@Test
public void testUpdate2() { 
    //可以同时设置字段和条件
    UpdateWrapper<User> wrapper = new UpdateWrapper<>();
    wrapper.set("age", 21).set("password", "999999") //更新的字段
    .eq("user_name", "zhangsan"); //更新的条件

    //根据条件做更新
    int result = this.userMapper.update(null, wrapper);
    System.out.println("result => " + result);
}
```



### 1.3.3删除操作

1. 根据id删除：deleteById()

   ```java 
   @Test
   public void testDeleteById(){
       // 根据id删除数据
       int result = this.userMapper.deleteById(2L);
       System.out.println("result => " + result);
   }
   ```

2. 根据columnMap 条件删除记录  deleteByMap()

   ```java
   @Test
   public void testDeleteByMap(){
       Map<String,Object> map = new HashMap<>();
       map.put("user_name", "zhangsan");
       map.put("password", "999999");
   
       // 根据map删除数据，多条件之间是and关系
       int result = this.userMapper.deleteByMap(map);
       System.out.println("result => " + result);
   }
   ```

3. 根据entity 条件删除记录  Wrapper< User> wrapper

   ```Java
   @Test
   public void testDelete(){
       //用法一：
       QueryWrapper<User> wrapper = new QueryWrapper<>();
       wrapper.eq("user_name", "caocao1")
               .eq("password", "123456");
   
       //用法二：推荐
       User user = new User();
       user.setPassword("123456");
       user.setUserName("caocao");
   
       QueryWrapper<User> wrapper = new QueryWrapper<>(user);
   
       // 根据包装条件做删除
       int result = this.userMapper.delete(wrapper);
       System.out.println("result => " + result);
   }
   ```

4. 根据id 批量删除   id 不能为null 已经 empty  deleteBatchIds()

   ```Java
   @Test
   public void  testDeleteBatchIds(){
       // 根据id批量删除数据 传递集合 里面传递是就是id的值 则会删除掉对应的id的数据
       int result = this.userMapper.deleteBatchIds(Arrays.asList(10L, 11L));
       System.out.println("result => " + result);
   }
   ```

### 1.3.4查询操作

- 根据id查询、批量查询、查询单条数据、查询列表、分页查询等操作



1. 根据id查询 selectById

   ```java
   @Test
   public void testSelectById() {
       User user = this.userMapper.selectById(2L);
       System.out.println(user);
   }
   ```

2. 根据id批量查询 selectBatchIds

   ```java
   @Test
   public void testSelectBatchIds(){
       // 根据id批量查询数据 通过集合接受数据 查询 id = 2,3，4,100的数据  没有的id值是查询不到的
       List<User> users = this.userMapper.selectBatchIds(Arrays.asList(2L, 3L, 4L, 100L));
       for (User user : users) {
           System.out.println(user);
       }
   }
   ```

3. 查询一条数据：selectOne

   ```java
   @Test
   public void testSelectOne(){
       //T selectOne(@Param("ew") Wrapper<T> queryWrapper);
       QueryWrapper<User> wrapper = new QueryWrapper<>();
       //查询条件
       wrapper.eq("password", "123456");
       // 查询的数据超过一条时，会抛出异常
       User user = this.userMapper.selectOne(wrapper);
       System.out.println(user);
   }
   ```

4. 查询总记录数 selectCount()

   ```java 
   @Test
   public void testSelectCount(){
       // Integer selectCount(@Param("ew") Wrapper<T> queryWrapper);
       QueryWrapper<User> wrapper = new QueryWrapper<>();
       wrapper.gt("age", 20); // 条件：年龄大于20岁的用户
   
       // 根据条件查询数据条数
       Integer count = this.userMapper.selectCount(wrapper);
       System.out.println("count => " + count);
   }
   ```

5. 查询数据的列表 selectList（）

   ```Java
   @Test
   public void testSelectList(){
       // List<T> selectList(@Param("ew") Wrapper<T> queryWrapper);
       QueryWrapper<User> wrapper = new QueryWrapper<>();
       //设置查询条件    val：模糊查询匹配
       wrapper.like("email", "itcast");
   
       List<User> users = this.userMapper.selectList(wrapper);
       for (User user : users) {
           System.out.println(user);
       }
   }
   ```

6. 分页查询 selectPage()

   1. 配置分页插件：

   2. ```java
      @Configuration
      @MapperScan("cn.itcast.mp.mapper") //设置mapper接口的扫描包
      public class MybatisPlusConfig {
          @Bean //配置分页插件
          public PaginationInterceptor paginationInterceptor(){
              return new PaginationInterceptor();
          }
      }
      ```

   3. 测试用例

      ```java
      // 测试分页查询  要配置一个分页插件
      @Test
      public void testSelectPage(){
          //IPage<T> selectPage(IPage<T> page, @Param("ew") Wrapper<T> queryWrapper);
          Page<User> page = new Page<>(3,1); //查询第一页，查询1条数据
      
          QueryWrapper<User> wrapper = new QueryWrapper<>();
          //设置查询条件
          wrapper.like("email", "itcast");
      
          IPage<User> iPage = this.userMapper.selectPage(page, wrapper);
          System.out.println("数据总条数： " + iPage.getTotal());
          System.out.println("数据总页数： " + iPage.getPages());
          System.out.println("当前页数： " + iPage.getCurrent());
          //getRecords获取数据
          List<User> records = iPage.getRecords();
          for (User record : records) {
              System.out.println(record);
          }
      }
      ```

### 1.3.5SQL注入原理

- 在MP中，ISqlInjector负责SQL的注入工作，它是一个接口，AbstractSqlInjector是它的实现类
- 在AbstractSqlInjector中，主要是由inspectInject()方法进行注入的
- 在实现方法中， methodList.forEach(m -> m.inject(builderAssistant, mapperClass, modelClass, tableInfo)); 是关键，循环遍历方法，进行注入。



## 1.4配置

### 1.4.1基本配置

1. configLocation

   - 单独设置MyBatis配置文档，就讲配置路径配置到configLocation中。

   - SpringBoot配置方式：

     ~~~properties
     mybatis-plus.config-location = classpath:mybatis-config.xml
     ~~~

2. mapperLocations

   - 在 Mapper 中有自定义方法（XML 中有自定义实现），需要进行该配置，指定Mapper 所对应的 XML 文件位置

   - SpringBoot配置方式：

     ~~~properties
     mybatis-plus.mapper-locations = classpath*:mybatis/*.xml
     ~~~

3. typeAliasesoPackge

   - MyBaits 别名包扫描路径，通过该属性可以给包中的类注册别名，注册后在 Mapper 对应的 XML 文件中可以直接使 用类名，而不用使用全限定的类名（即 XML 中调用的时候不用包含包名）。

   - ~~~properties
     mybatis-plus.type-aliases-package = cn.itcast.mp.pojo
     ~~~

### 1.4.2进阶配置

- MyBatis的原生支持配置，通过MyBatis xml配置文件的形式进行配置

1. mapUnderscoreToCamelCase

   - 类型：boolean

   - 默认值：true

   - 是否开启自动驼峰命名规则（camel case）映射，即从经典数据库列名 A_COLUMN（下划线命名） 到经典 Java 属 性名 aColumn（驼峰命名） 的类似映射。

     ~~~properties
     #关闭自动驼峰映射，该参数不能和mybatis-plus.config-location同时存在
     mybatis-plus.configuration.map-underscore-to-camel-case=false
     ~~~

2. cacheEnable

   - 类型：booolean

   - 默认值：true

   - 全局地开启或关闭配置文件中的所有映射器已经配置的任何缓存，默认为 true。

   - ~~~properties
     mybatis-plus.configuration.cache-enabled=false
     ~~~

### 1.4.3 DB策略配置

1. ==idType==

   - 类型: com.baomidou.mybatisplus.annotation.IdType
   - 默认值：ID_WORKER

2. ==tablePrefix==

   - 类型:String

   - 默认值:null

     表示前缀，全局配置后可以省略@Tablename()配置

   - SpringBoot：

   - ~~~properties
     mybatis-plus.global-config.db-config.id-type=auto
     ~~~



## 1.5条件构造器

在Mp中 wrapper 中重要的实现类有：==AbstractWrapper==   AbstractChainWrapper是重点实现 ，前者重点学习

> QueryWrapper(LambdaQueryWrapper) 和 UpdateWrapper(LambdaUpdateWrapper) 的父类 用于生成 sql 的 where 条件, entity 属性也用于生成 sql 的 where 条件 注意: entity 生成的 where 条件与 使用各个 api 生成 的 where 条件没有任何关联行为



### allEq

- 说明：
- allEq(Map params) 
- allEq(Map params, boolean null2IsNull) 
- allEq(boolean condition, 
- Map params, boolean null2IsNull)

测试用例：

```Java
    @Test
    public void testAllEq(){

        Map<String,Object> params = new HashMap<>();
        params.put("name", "李四");
        params.put("age", "20");
        params.put("password", null);

        QueryWrapper<User> wrapper = new QueryWrapper<>();
        //  生成的sql语句：SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE password IS NULL AND name = ? AND age = ?
//        wrapper.allEq(params);
        //生成的sql语句：SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? AND age = ?
//        wrapper.allEq(params, false);

        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE age = ?
        //过滤    满足条件才能进行过滤
//        wrapper.allEq((k, v) -> (k.equals("age") || k.equals("id")) , params);
        //SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? AND age = ?
        wrapper.allEq((k, v) -> (k.equals("age") || k.equals("id") || k.equals("name")) , params);
        List<User> users = this.userMapper.selectList(wrapper);
        for (User user : users) {
            System.out.println(user);
        }
    }
```

### 基本比较操作：

1. eq 

  - 等于 = 

2. ne 

  - 不等于 <> 

3. gt 

  - 大于 > 

4. ge 

  - 大于等于 >= 

5. lt 

  - 小于 <  

6. le

  - 小于等于 <= 

7. between 

  - BETWEEN 值1 AND 值2 

8. notBetween

  - NOT BETWEEN 值1 AND 值2 

9. in 字段 

  - IN (value.get(0), value.get(1), ...) 

10. notIn 字段 

  - NOT IN (v0, v1, ...)

  测试用例：

  ```Java
  @Test
  public void testEq() {
      QueryWrapper<User> wrapper = new QueryWrapper<>();
  
      // 生成的sql语句：SELECT id,user_name,password,name,age,email FROM tb_user WHERE password = ? AND age >= ? AND name IN (?,?,?)
      wrapper.eq("password", "123456")
              .ge("age", 20)
              .in("name", "李四", "王五", "赵六");
  
      List<User> users = this.userMapper.selectList(wrapper);
      for (User user : users) {
          System.out.println(user);
      }
  
  }
  ```

### 模糊查询

- like   ==模糊前后的值==

  - LIKE '%值%' 
  - 例: like("name", "王") ---> name like '%王%' 

- notLike ==不模糊==

  - NOT LIKE '%值%

  - 例: notLike("name", "王") ---> name not like '%王%'

- likeLeft  ==左模糊==

  - LIKE '%值' 
  - 例: likeLeft("name", "王") ---> name like '%王' 

- likeRight ==右模糊==

  - LIKE '值%' 
  - 例: likeRight("name", "王") ---> name like '王%'

- 测试用例：

- ```Java
  @Test
  public void testLike(){
      QueryWrapper<User> wrapper = new QueryWrapper<>();
      //生成的sql语句：  SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name LIKE ?
      // 传入参数：%五(String)
      wrapper.likeLeft("name", "五");//就把五前面的 字 或者  其他内容 给忽略掉  就是查询以 五 结尾的
  
      List<User> users = this.userMapper.selectList(wrapper);
      for (User user : users) {
          System.out.println(user);
      }
  }
  ```



### 排序

- orderBy
  - 排序 ORDER BY 字段
- orderByAsc   ==降序==
  - 排序：ORDER BY 字段, ... ASC 
  - 例: `orderByAsc("id", "name") ---> order by id ASC,name ASC `
- orderByDesc   ==升序==
  - 排序：ORDER BY 字段, ... DESC 
  - 例: `orderByDesc("id", "name") ---> order by id DESC,name DESC`

测试用例：

```java
@Test
public void testOrderByAgeDesc(){
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //按照年龄倒序排序
    //生成的sql语句：  SELECT id,user_name,name,age,email AS mail FROM tb_user ORDER BY age DESC
    wrapper.orderByDesc("age");

    List<User> users = this.userMapper.selectList(wrapper);
    for (User user : users) {
        System.out.println(user);
    }
}
```

### 逻辑查询

- or
  - 拼接OR
  - 主动调用OR表示紧接着下一个方法不是用and链接
- and 
  - AND嵌套

测试用例：

```Java
@Test
public void testOr(){
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //生成的sql语句： SELECT id,user_name,name,age,email AS mail FROM tb_user WHERE name = ? OR age = ?
    //若是中间没有or()操作，则是用and链接 返回的结果就会不一样
    //or不走索引 用 Union拼接
    wrapper.eq("name", "王五").or().eq("age", 21);

    List<User> users = this.userMapper.selectList(wrapper);
    for (User user : users) {
        System.out.println(user);
    }
}
```

### select 操作

- 在MP中查询中，默认查询所有的字段，可以通过指定字段进行查询

测试用例：

```Java
@Test
public void testSelect(){
    QueryWrapper<User> wrapper = new QueryWrapper<>();
    //生成的sql语句：SELECT id,name,age FROM tb_user WHERE name = ? OR age = ?
    wrapper.eq("name", "王五")
            .or()
            .eq("age", 21)
            .select("id","name","age"); //指定查询 id name  age 的字段
    List<User> users = this.userMapper.selectList(wrapper);
    for (User user : users) {
        System.out.println(user);
    }
}
```







# 2.Active Record  （AR）

- 动态语言（PHP 、Ruby等）
- 属于ORM（对象关系层）， 表映射到记录，记录映射到对象，字段映射到对象属性。遵循的命名和配置惯例 ，可以快速实现模型的操作。

ActiveRecord的主要思想：

- 每一个数据表对应创建一个类，类的每一个对象实例对应于数据库中表的一行记录；表的每个字段在类中都有相应的Field
- ActiveRecord同时负责把自己持久化，在ActiveRecore中封装了对应的数据库的访问，即CRUD；
- ActiveRecord的一种领域模型，封装了部分业务逻辑

## 2.1开启AR

- 将实体对象继承Model即可

```java
import cn.itcast.mp.enums.SexEnum;
import com.baomidou.mybatisplus.annotation.*;
import com.baomidou.mybatisplus.extension.activerecord.Model;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class User extends Model<User> {
    //继承Model类
    private Long id;
    private String userName;
    private String password;
    private String name;
    private Integer age;
    private String mail;
}
```



## 2.2根据主键查询

```Java
@RunWith(SpringRunner.class)
@SpringBootTest
public class TestUserMapper2 {

    @Test
    public void testSelectById(){
        User user = new User();
        user.setId(16L);

        User user1 = user.selectById();
        System.out.println(user1);
    }
}
```



## 2.3插入(新增)数据

```java
@Test
public void testInsert(){
    User user = new User();
    user.setUserName("diaochan");
    user.setPassword("123456");
    user.setAge(20);
    user.setName("貂蝉");
    user.setMail("diaochan@itcast.cn");
    user.setVersion(1);
    user.setSex(SexEnum.WOMAN); //使用的是枚举

    // 调用AR的insert方法进行插入数据
    boolean insert = user.insert();
    System.out.println("result => " + insert);
}
```



## 2.4更新操作

```java
@Test
public void testUpdate(){
    User user = new User();
    user.setId(13L);// 查询条件
    user.setAge(31); // 更新的数据 在13中设置年龄为31岁

    boolean result = user.updateById();
    System.out.println("result => " + result);
}
```

## 2.5删除操作

```java
@Test
public void testDelete(){
    User user = new User();
    user.setId(13L);//删除id为13行的数据
    boolean delete = user.deleteById();
    System.out.println("result => " + delete);
}
```



## 2.6根据条件查询

```java
@Test
    public void testSelect(){
        User user = new User();

        QueryWrapper<User> wrapper  = new QueryWrapper<>();
        wrapper.ge("age", 30); //大于等于30岁的用户查询出来  使用ge 这个比较运算符 比较运算符在上面有笔记

        List<User> users = user.selectList(wrapper);
        for (User user1 : users) {
            System.out.println(user1);
        }
    }
```



# 3.Oracle主键Sequence



# 4.插件



## 4.1 MyBatis的插件机制

MyBatis 允许在已映射语句执行过程中的某一点进行==拦截调用==  （拦截器）

1. Executor (update, query, flushStatements, commit, rollback, getTransaction, close, isClosed) 
2.  ParameterHandler (getParameterObject, setParameters) 
3. ResultSetHandler (handleResultSets, handleOutputParameters) 
4. StatementHandler (prepare, parameterize, batch, update, query)

拦截了Executor接口部分方法（update、query、commit、rollback）

对上面的方法概述：

1. 拦截执行器的方法
2. 拦截参数的处理
3. 拦截结果集的处理
4. 拦截sql语法构建的处理



插件的方法

```java
import org.apache.ibatis.executor.Executor;
import org.apache.ibatis.mapping.MappedStatement;
import org.apache.ibatis.plugin.*;

import java.util.Properties;

@Intercepts({@Signature(
        type= Executor.class,//指定拦截的类型 Executor
        method = "update",//拦截的是update方法
        args = {MappedStatement.class,Object.class})})
public class MyInterceptor implements Interceptor {

    @Override
    public Object intercept(Invocation invocation) throws Throwable {
        //拦截方法，具体业务逻辑编写的位置
        return invocation.proceed();
    }

    @Override
    public Object plugin(Object target) {
        //这次方法会执行多次，因为要执行上面的四个点(Executor、ParameterHandler 、ResultSetHandler 、StatementHandler )总共执行四次
        //创建target对象的代理对象,目的是将当前拦截器加入到该对象中
        return Plugin.wrap(target, this);
    }

    @Override
    public void setProperties(Properties properties) {
        //属性设置
    }
}
```





## 4.2执行分析插件

- 在MP中提供了对SQL执行的分析的插件，可用作阻断全表更新、删除的操作，
- ==注意：该插件仅适用于开发环境，不 适用于生产环境。==  主要是由于性能不行

SpringBoot配置：

```java
@Bean //SQL分析插件
public SqlExplainInterceptor sqlExplainInterceptor(){

    SqlExplainInterceptor sqlExplainInterceptor = new SqlExplainInterceptor();

    List<ISqlParser> list = new ArrayList<>();
    list.add(new BlockAttackSqlParser()); //全表更新、删除的阻断器

    sqlExplainInterceptor.setSqlParserList(list);

    return sqlExplainInterceptor;
}
```



测试用例 ： 查询结构是错误的 被拦截了才会出错 ，说明拦截器生效了

```java
/**
 * 测试全表更新，SQL分析器阻断效果
 */
@Test
public void testUpdateAll(){
    User user = new User();
    user.setAge(110); // 更新的数据

    boolean result = user.update(null); // 条件为null 则是全表更新
    System.out.println("result => " + result);
}
```

当执行全表更新时，会抛出异常，这样有效防止了一些误操作





## 4.3性能分析插件

- 性能分析拦截器，用于输出每条 SQL 语句及其执行时间，可以设置最大执行时间，超过时间会抛出异常。 

- 注意：该插件只用于开发环境，不建议生产环境使用。（性能问题）



mybatis-config.xml配置文件

```xml
<!-- 性能分析插件 -->
<plugin interceptor="com.baomidou.mybatisplus.extension.plugins.PerformanceInterceptor">
    <!--最大的执行时间，单位为毫秒-->
    <property name="maxTime" value="100"/>
    <!--对输出的SQL做格式化，默认为false-->
    <property name="format" value="true"/>
</plugin>
```



## 4.4乐观锁插件



### 4.4.1主要适用的场景

**目的：** 当要更新一条记录的时候，希望这条记录没有被别人更新

==并发操作==

实现方式：

1. 取出记录时，获取当前的版本（version）
2. 更新时，带上这个版本（version）
3. 执行更新时，set version = newVersion where version = oldVersion
4. 如果版本（version）不对，则更新失败



乐观锁防止多个事务对同一个数据同时修改



### 4.4.2配置方式：

1. Spring .xml

   ~~~xml
   <bean class="com.baomidou.mybatisplus.extension.plugins.OptimisticLockerInterceptor"/>
   ~~~

2. Spring boot 

   ~~~java
   @Bean
   public OptimisticLockerInterceptor optimisticLockerInterceptor() {
   return new OptimisticLockerInterceptor();
   }
   ~~~

3. MyBatis 全局配置

   

4. 注解实体字段

   为实体添加@Version注解

   1. 添加@version注解，设置初始值为1

      ~~~sql
      ALTER TABLE `tb_user`
      ADD COLUMN `version` int(10) NULL AFTER `email`;
      UPDATE `tb_user` SET `version`='1';
      ~~~

      

   2. 为User实体对象添加version字段，并且添加@version注解

      ~~~java
          @Version //乐观锁的版本字段
          private Integer version;
      ~~~

   测试：

   ```java
   @Test
   public void testUpdateVersion(){
       User user = new User();
       user.setId(2L);// 查询条件
   
       //先拿到版本 再设置id
       User userVersion = user.selectById();
   
       user.setAge(23); // 更新的数据
       user.setVersion(userVersion.getVersion()); // 当前的版本信息
   
       boolean result = user.updateById();
       System.out.println("result => " + result);
   }
   ```



特别说明：

- 支持的数据类型：==int== 、Integer、long、Long、Date、Timestamp、LocalDateTime
- 整数类型下 newVersion = oldVersion  + 1
- newVersioni 会回写到entity中
- 仅支持两种操作
  1. updateById(id)
  2. update(entity wrapper)
- 在update（entity ，warpper） 方法下，==wrapper不能复用！！==



# 5.Sql注入器



## 5.1编写MyBaseMapper 泛型里面传入的类不知道是哪一个 T 代表全部 类

```java
import com.baomidou.mybatisplus.core.mapper.BaseMapper;

import java.util.List;

public interface MyBaseMapper<T> extends BaseMapper<T> {

    List<T> findAll();

    // 扩展其他的方法

}
```

然后其他的Mapper类就继承这个MyBaseMapper接口  相当于嵌套

```java
import cn.itcast.mp.pojo.User;

public interface UserMapper extends MyBaseMapper<User> {
    User findById(Long id);
}
```



## 5.2编写MySallnjector

==继承DefaultSqlInjector 进行扩展== ，不能直接继承 AbstractSqlInjector  因为继承了这个 导致BaseMapper中的方法失效

```java
import com.baomidou.mybatisplus.core.injector.AbstractMethod;
import com.baomidou.mybatisplus.core.injector.DefaultSqlInjector;

import java.util.ArrayList;
import java.util.List;

public class MySqlInjector extends DefaultSqlInjector {

    @Override
    public List<AbstractMethod> getMethodList() {
        List<AbstractMethod> list = new ArrayList<>();

        // 获取父类中的集合
        list.addAll(super.getMethodList());

        // 再扩充自定义的方法
        list.add(new FindAll());

        return list;
    }
}
```



## 5.3编写FindAll

```java
import com.baomidou.mybatisplus.core.injector.AbstractMethod;
import com.baomidou.mybatisplus.core.metadata.TableInfo;
import org.apache.ibatis.mapping.MappedStatement;
import org.apache.ibatis.mapping.SqlSource;

public class FindAll extends AbstractMethod {

    @Override
    public MappedStatement injectMappedStatement(Class<?> mapperClass, Class<?> modelClass, TableInfo tableInfo) {

        String sql = "select * from " + tableInfo.getTableName();
        SqlSource sqlSource = languageDriver.createSqlSource(configuration,sql, modelClass);

        return this.addSelectMappedStatement(mapperClass, "findAll", sqlSource, modelClass, tableInfo);
    }
}
```

5.4注册到Spring容器中

在MyBatisPlusConfig中

```java
@Bean
public MySqlInjector mySqlInjector(){
    return new MySqlInjector();
}
```



测试：

```java
@Test
public void testFindAll(){
    List<User> userlist = this.userMapper.findAll();
    for (User user : users) {
        System.out.println(user);
    }
}
```



# 6.自动填充功能

## 6.4添加注解@TableFiled注解



为password添加自动填充功能，在新增数据时有效



FieldFill提供了多种模式选择



## 6.5编写MyMetaObjectHandler





测试：





# 7.逻辑删除



> 删除操作需要实现逻辑删除 ，所谓逻辑删除就是将数据标记为删除，而并非真正 的物理删除（非DELETE操作），查询时需要携带状态条件，确保被标记的数据不被查询到。这样做的目的就是避免 数据被真正的删除。
>



## 7.1修改表结构

- 为tb_user表增加deleted字段，用于表示数据是否被删除，1代表删除，0代表未删除。



## 7.2配置

application.properties



7.3测试



# 8.通用的枚举

解决繁琐的配置 ，通常表示一些固定的属性 比如：性别（男、女），学历：（小、初、高、大）

## 8.1修改表结构

~~~sql
ALTER TABLE `tb_user`
ADD COLUMN `sex` int(1) NULL DEFAULT 1 COMMENT '1-男，2-女' AFTER `deleted`;
~~~

## 8.2定义枚举

~~~java
package cn.itcast.mp.enums;
import com.baomidou.mybatisplus.core.enums.IEnum;
import com.fasterxml.jackson.annotation.JsonValue;
public enum SexEnum implements IEnum<Integer> {
MAN(1,"男"),
WOMAN(2,"女");
private int value;
private String desc;
SexEnum(int value, String desc) {
this.value = value;
this.desc = desc;
}
@Override
public Integer getValue() {
return this.value;
}
@Override
public String toString() {
return this.desc;
}
}

~~~

## 8.3配置

application.properties文件





# 9.代码生成器

- AutoGenerator 是 MyBatis-Plus 的代码生成器，通过 AutoGenerator 可以快速生成 Entity、Mapper、Mapper XML、Service、Controller 等各个模块的代码，极大的提升了开发效率。





# 10.MyBatisX快速开发插件



MyBatisX 是一款基于 IDEA 的快速开发插件，为效率而生。



- 功能： 
  - Java 与 XML 调回跳转 
  - Mapper 方法自动生成 XML













