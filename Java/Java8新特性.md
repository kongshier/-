> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 写在最前面

在企业中更多的都是使用 Java8 ，随着 Java8 的普及度越来越高，很多人都提到面试中关于Java 8 也是非常常问的知识点。本文根据 Github 上的文章进行学习，GitHub Java8地址： https://github.com/winterbe/java8-tutorial。



# Java8 新特性 主要内容

~~~mermaid
graph TB
A(Java8 新特性)-->b(Lambda表达式)
A(Java8 新特性)-->c(Stream API)
A(Java8 新特性)-->d(方法引用)
A(Java8 新特性)-->e(接口默认方法)
A(Java8 新特性)-->f(新的日期和时间API)
A(Java8 新特性)-->g(Optional类)
A(Java8 新特性)-->h(并行流)
A(Java8 新特性)-->a1(可重复注解)
A(Java8 新特性)-->a2(类型注解)
A(Java8 新特性)-->a3(Nashorn JavaScript 引擎)
A(Java8 新特性)-->a4(PermGen 空间的移除)
~~~

1. Lambda表达式：Lambda表达式是一种函数式编程的方式，可以使代码更简洁。它允许在方法中传递代码块，从而实现更加灵活的编程方式。
2. Stream API：Stream API提供了一种更简单的方法来处理集合数据。通过使用Stream API，可以轻松地进行==筛选、排序、映射==等操作。
3. 方法引用：方法引用是Lambda表达式的一种简化写法，它允许直接引用已经存在的方法，从而简化代码。
4. 接口默认方法：Java 8允许在接口中定义默认方法，这些方法在实现类中可以被继承和覆盖，从而提供了更多的灵活性。
5. 新的日期和时间API：Java 8引入了一个新的日期和时间API，这个API提供了更多的功能，包括处理时区、时间间隔、日期时间格式化等。
6. Optional类：Optional类是一个容器对象，它可以包含一个值或者为空。它可以==避免空指针异常==的出现，并且可以提供更加清晰的代码。
7. Parallel Stream 并行流：Java 8引入了并行流，它可以在多个线程上并行地处理集合数据，从而提高程序的性能。

以下几种没有上面的那么常见

1. 可重复注解：Java 8允许在同一个地方多次使用同一个注解，从而提供更多的灵活性和可读性。
2. 类型注解：Java 8允许在任何地方使用注解来标记类型，这可以帮助编写更加安全和可靠的代码。
3. Nashorn JavaScript引擎：Java 8引入了Nashorn JavaScript引擎，它可以在Java虚拟机中执行JavaScript代码，从而提供更多的灵活性。
4. Base64编码：Java 8提供了一种更加简单的方法来处理Base64编码，从而使编码和解码更加容易。
5. PermGen空间的移除：Java 8移除了PermGen空间，取而代之的是Metaspace，这使得内存管理更加简单和高效。



下面我们来看看最重要的7种 Java8 新特性



# 1、Lanbda表达式

> Lambda允许把函数作为一个方法的参数，允许在方法中传递代码块，从而实现更加灵活的编程方式。Lambda表达式可以简化代码，减少样板代码的出现，并且使代码更加易读和易于维护。

## 1.1 lambda表达式语法

~~~java
(parameters) -> expression
(parameters) -> { statements; }
~~~

> 其中，parameters是方法的参数列表，->表示将参数列表与方法体分开，expression是单个表达式，statements是多条语句。

Lambda表达式在Java语言中引入了一个操作符`->`，该操作符被称为Lambda操作符或箭头操作符。它将Lambda分为两个部分：

- 左侧：指定了Lambda表达式需要的所有参数
- 右侧：制定了Lambda体，即Lambda表达式要执行的功能。

## 1.2 Lambda代码示例

1. 对比旧版的Java比较器

```java
/**
 * @author Shier 2023/2/19 21:00
 * Lambda表达式
 */
public class LambdaTest {
    public static void main(String[] args) {
        // 1. 创建一个 List 集合，用于存储要排序的怨怒是
        List<String> stringList = Arrays.asList("shier", "xiaoyi", "xiaosan", "zhangsan");
        // 2 使用匿名的比较器对象
        Collections.sort(stringList, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return o2.compareTo(o1);
            }
        });
        System.out.println(stringList.toString()); // [zhangsan, xiaoyi, xiaosan, shier]
    }
}
```

2. 使用Java8的新特性，lambda表达式可以将以上比较器简化成以下：

   首先是可以去掉了传统的匿名对象的方法：

```java
// 使用lambda表达式:第一次简化
Collections.sort(stringList, (String a, String b) -> {
    return b.compareTo(a);
});
```

> 与旧版的书写明显简短了一些，不过这还不是最简化的

3. 再一次简化成：

```java
Collections.sort(names, (String a, String b) -> b.compareTo(a));
```

4. 但是这样看着还不是足以简化的，对于函数体只有一行的代码，你可以去掉大括号`{}` 以及 `return` 语句，所以下面这个才是比较简化的写法

```java
stringList.sort((a, b) -> b.compareTo(a));
```

由于上面是 `stringList` 是 List 类型，List 本身就有一个 `sort` 方法，而且不要指定数据类型。并且Java编译器可以自动推导出参数类型，所以你可以不用再写一次类型。



### 其他的列子

~~~java
        //语法格式一  无参 无返回值  lambda 只需一条语句
        Runnable runnable = () -> System.out.println("Runnable 运行了！！");
        runnable.run(); //run是Runnable的方法

        //语法格式二  一个参数 无返回值
        Consumer<String> consumer =(x) -> System.out.println(x);
        consumer.accept("运行了？？？？");*/  //consumer 是的 accept

		//语法格式三   有一个参数 参数括号可以省略
        Consumer<String> consumer = x -> System.out.println(x);
        consumer.accept("运行了？？？？");

		//语法格式四  有两个参数 并且里面有多条语句
	       Comparator<Integer> com = (x , y) ->{
           System.out.println("函数式接口！");
           return Integer.compare(x,y);
           };
	        System.out.println(com.compare(45,1));  // x<y 输出-1  x = y 输出 0  x > y 输出 1

		//语法格式五 有两个参数以上有返回值 lambada 只有一个语句 return 和大括号都可以省略不写
        Comparator<Integer> com = (x, y) -> Integer.compare(x, y);
        System.out.println(com.compare(12,45));//输出-1

        //语法格式六 lambda参数列表可以省略不写 JVM会进行”类型推断“
        Comparator<Integer> com = (Integer x, Integer y) -> Integer.compare(x, y);
        System.out.println(com.compare(12,45)); //-1
        //  左右遇一括号省，左侧推断类型省，能省则省
~~~

省略规则：

- 参数类型可以省略不写。  就是上面的格式一
- 如果只有一个参数，参数类型可以省略，同时()也可以省略。
- 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写,同时要省略分号!
- 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写。此时，如果这行代码是return语句，必须省略return不写，同时也必须省略";"不写

> Lambda表达式可以用于各种不同的场景，比如对列表进行过滤、映射和聚合等操作，它可以让代码更加简洁和易于理解。



## 1.3 lambda 表达式作用域（lambda Scopes）

Lambda表达式可以访问其外部作用域中的变量，包括类成员变量、静态变量、方法的参数和局部变量。这些变量被称为自由变量，因为它们不是在Lambda表达式内部定义的。Lambda表达式可以读取自由变量的值，但是不能修改它们的值。如果我们试图在Lambda表达式内部修改一个自由变量的值，那么编译器会报错。

Lambda表达式可以访问三种类型的变量：

1. Lambda表达式外部的变量，也称自由变量。
2. Lambda表达式内部的变量，也称隐式参数。
3. Lambda表达式内部定义的局部变量，也称显示参数。



### 1.3.1 访问外部变量（自由变量）

~~~java
public class LambdaScopeExample {

    private int x = 1;

    public void doSomething() {
        int y = 2;
        Consumer<Integer> lambda = (z) -> System.out.println(x + y + z); // 6
        lambda.accept(3);
    }
}
~~~

在这个例子中，Lambda表达式访问了外部的变量x和y。变量x是类成员变量，变量y是方法的局部变量。Lambda表达式可以读取这些变量的值，但是不能修改它们的值。



### 1.3.2 访问内部变量

Lambda表达式还可以访问自己的参数，也称为隐式参数。==隐式参数可以在Lambda表达式中使用，但是不能在外部使用==。下面是一个Lambda表达式使用隐式参数的例子：

~~~java
Function<Integer, Integer> lambda = x -> x * 2;
~~~

在这个例子中，Lambda表达式的参数x是一个隐式参数，它只能在Lambda表达式内部使用。



### 1.3.3 自定义局部变量

Lambda表达式还可以定义自己的局部变量，也称为显式参数。显式参数==只能在Lambda表达式内部使用，不能在外部使用==。下面是一个Lambda表达式定义显式参数的例子：

~~~java
IntStream.range(1, 11)
    .map(x -> {
        int y = x * 2;
        return y;
    })
    .forEach(System.out::println); //  
~~~

在这个例子中，Lambda表达式定义了一个局部变量y，它只能在Lambda表达式内部使用。



# 2、接口默认方法 （Default Methods for Interfaces）

## 2.1 概念

Java 8允许在接口中定义默认方法，这些方法在实现类中可以被继承和覆盖，从而提供了更多的灵活性。默认方法允许我们在接口中添加新的方法，而不会破坏已经实现该接口的现有类。

## 2.2 默认方法语法格式

~~~~java
default returnType methodName(parameterList) {
    // method body
}
~~~~

其中

- default关键字表示这是一个默认方法，
- returnType表示方法的返回类型，
- methodName表示方法名，
- parameterList表示方法的参数列表，
- method body表示方法的实现。



### 2.3 代码示例说明

Java 8使我们能够通过使用 `default` 关键字向接口添加非抽象方法实现。

1. 首先定义一个接口 `Formula` 、里面包括一个默认接口方法、和接口抽象方法
2. 通过匿名内部类进行访问接口方法
3. ==如果是实现了接口，那么该实现类就会默认继承该接口的默认方法== 

```java
/**
 * @author Shier 2023/2/19 21:32
 * 接口默认方法
 */
public class DefaultMethods {
    public static void main(String[] args) {
        // 通过匿名内部类进行访问接口
        Formula formula = new Formula() {
            @Override
            public int add(int a, int b) {
                return a + b;
            }
        };
        System.out.println("接口公共方法：" + formula.add(10, 20)); //接口公共方法：30
        System.out.println("接口默认方法：" + formula.defaultMethods("string1", "string2")); //接口默认方法：string1string2
    }
}

// 定义一个接口
interface Formula {

    // 接口公共方法，必须实现的
    int add(int a, int b);

    // 接口默认方法
    default String defaultMethods(String a, String b) {
        return a + b;
    }
}
```

> 不管是抽象类还是接口，都可以通过匿名内部类的方式访问。不能通过抽象类或者接口直接创建对象。对于上面通过匿名内部类方式访问接口，我们可以这样理解：一个内部类实现了接口里的抽象方法并且返回一个内部类对象，之后我们让接口的引用来指向这个对象。



# 3、函数式接口（Functional Interfaces）

Java 语言设计者们投入了大量精力来思考如何使现有的函数友好地支持Lambda。最终采取的方法是：增加函数式接口的概念。**“函数式接口”是指仅仅只包含一个抽象方法,但是可以有多个非抽象方法(也就是上面提到的默认方法)的接口。** 像这样的接口，可以被隐式转换为lambda表达式。

## 3.1 概念

Java 8引入了函数式接口，它是==只包含一个抽象方法的接口==，这个抽象方法定义了一个函数签名，也就是参数列表和返回值类型。函数式接口可以被用来创建Lambda表达式，从而提供更加灵活的编程方式。

## 3.2 示例代码

通过过滤元素进行演示，使用 Predicate 函数式接口，

```java
/**
 * @author Shier 2023/2/19 22:02
 * Predicate 函数式接口
 */
public class FunctionInterfaceTest {
    public static void main(String[] args) {
        List<String> strings = Arrays.asList("shiera", "yupi", "dsadsan", "zhangsan");
        // 使用过滤，将长度小于 5的元素 收集成一个列表，并返回
        List<String> collect = strings.stream().filter(name -> name.length() < 5).collect(Collectors.toList());
        System.out.println(collect); //[yupi]
    }
}
```

### 使用函数式接口注解

@FunctionalInterface注解  检测它是不是一个函数式接口

~~~java
//一个函数式接口
@FunctionalInterface
interface Run{
    void run();//只有一个抽象方法
}

public static void Sport(Run r){
    System.out.println("开始");
    r.run();//参数构造
    System.out.println("结束");
}
Run run = ()->{ System.out.println("运动员跑");};
System.out.println("-----------------");
Sport(()->{System.out.println("运动员准备跑");});
~~~

### 自定义函数式接口

~~~java
    //自定义一个函数式接口
    @FunctionalInterface
    public interface  MyFuncInterf<T>{
        public T getValue(String origin);
    }

    //定义一个方法 讲函数式接口作为方法参数
    public String toLowerString(MyFuncInterf<String> mf,String origin){
        return mf.getValue(origin);
    }

    //将Lambda表达式实现的接口作为参数传递
    public void test01(){
        String value = toLowerString((str) ->{
            return str.toLowerCase();
        },"abc");
        System.out.println(value);
    }
~~~



将数字字符串转换为整数类型

```java
@FunctionalInterface
public interface Converter<F, T> {
    T convert(F from);
}
```

```java
Converter<String, Integer> converter = (from) -> Integer.valueOf(from);
Integer converted = converter.convert("123");
System.out.println(converted.getClass()); //class java.lang.Integer
```



### 内置四大函数式接口

|       函数式接口        | 参数类型 | 返回类型 |                             用途                             |
| :---------------------: | :------: | :------: | :----------------------------------------------------------: |
| Consumer<T>消费类型接口 |    T     |   void   |       对类型为T的对象应用操作，包含方法：void  accpt()       |
|  Suppiler<T>函数式接口  |    无    |    R     |             放回类型为T的对象 ，包含方法 T:get()             |
|      Function<T,R>      |    T     |    R     | 对类型为T的对象应用操作并返回结果。结果是R类型的对象。包含方法：R apply（T t） |
| Predicate<T>断定型接口  |    T     | boolean  | 确定类型为T 的对象是否满足某约束条件，并返回boolean值包含方法：boolean test (T t) |

Java 8提供了许多预定义的函数式接口，比如Function、Consumer、Predicate等。这些接口中的方法可以用Lambda表达式来实现，从而实现更加简洁的代码。

#### Predicate

Predicate 接口是只有一个参数的返回布尔类型值的 **断言型** 接口。该接口包含多种默认方法来将 Predicate 组合成其他复杂的逻辑（比如：与，或，非）：

源码解析

```java
package java.util.function;
import java.util.Objects;

@FunctionalInterface
public interface Predicate<T> {
    
    // 该方法是接受一个传入类型,返回一个布尔值.此方法应用于判断.
    boolean test(T t);

    //and方法与关系型运算符"&&"相似，两边都成立才返回true
    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }
    // 与关系运算符"!"相似，对判断进行取反
    default Predicate<T> negate() {
        return (t) -> !test(t);
    }
    //or方法与关系型运算符"||"相似，两边只要有一个成立就返回true
    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }
   // 该方法接收一个Object对象,返回一个Predicate类型.此方法用于判断第一个test的方法与第二个test方法相同(equal).
    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
```

示例

```java
Predicate<String> predicate = (s) -> s.length() > 0;

predicate.test("foo");              // true
predicate.negate().test("foo");     // 取反了，所以是false

Predicate<Boolean> nonNull = Objects::nonNull;
Predicate<Boolean> isNull = Objects::isNull;

Predicate<String> isEmpty = String::isEmpty;
Predicate<String> isNotEmpty = isEmpty.negate();
```

#### Function 

Function 接口接受一个参数并生成结果。默认方法可用于将多个函数链接在一起（compose, andThen）：

```java
package java.util.function;
 
import java.util.Objects;
 
@FunctionalInterface
public interface Function<T, R> {
    
    //将Function对象应用到输入的参数上，然后返回计算结果。
    R apply(T t);
    //将两个Function整合，并返回一个能够执行两个Function对象功能的Function对象。
    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }
    // 
    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }
 
    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```

#### Supplier

Supplier 接口产生给定泛型类型的结果。 与 Function 接口不同，Supplier 接口不接受参数。

```java
Supplier<Person> personSupplier = Person::new;
personSupplier.get();   // new Person
```

#### Consumer

Consumer 接口表示要对单个输入参数执行的操作。

```java
Consumer<Person> greeter = (p) -> System.out.println("Hello, " + p.firstName);
greeter.accept(new Person("Luke", "Skywalker")); // Hello luke
```

#### Comparator

Java中的经典老接口。

```java
Comparator<Person> comparator = (p1, p2) -> p1.firstName.compareTo(p2.firstName);

Person p1 = new Person("John", "Doe");
Person p2 = new Person("Alice", "Wonderland");

comparator.compare(p1, p2);             // > 0
comparator.reversed().compare(p1, p2);  // < 0
```



# 4、方法和构造函数引用(Method and Constructor References)

## 4.1 介绍

Java 8中引入了方法和构造函数的引用，它们是一种新的语法，可以使得代码更加简洁、易于理解。方法和构造函数的引用允许我们直接引用一个已经存在的方法或构造函数，而不需要重新实现它们。

## 4.2 方法引用

方法引用是一种通过方法的名称来引用已经存在的方法的语法。在Lambda表达式中，我们可以通过::符号来引用一个已经存在的方法。

### 4.2.1 方法引用格式

~~~~java
方法的持有者::方法名称
~~~~

比如上面的类型转换案例中，就能将其改成静态方法的引用

```java
// 例子一
Converter<String, Integer> converter = Integer::valueOf; // 静态方法引用
Integer converted = converter.convert("123");
System.out.println(converted.getClass());
```

~~~java
// 例子二
public class MethodsReferences {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
        names.forEach(System.out::print); // 不换行
        names.forEach(System.out::println); // 换行
    }
}
~~~

> 我们使用方法引用的语法来引用了System.out的println()方法。在Lambda表达式中，我们将`System.out::println`作为参数传递给了names集合的forEach()方法。这个语法与Lambda表达式的语法非常相似，但是使用了`::`符号来引用方法。

Java 8允许您通过`::`关键字传递方法或构造函数的引用。 上面的示例显示了如何引用静态方法。 但我们也可以引用对象方法：

```java
/**
 * @author Shier 2023/2/19 22:46
 */
public class ConstructReferences {
    public static void main(String[] args) {
        Something something = new Something();
        Converter<String, String> converter = something::startsWith; // 对象方法的引用
        String converted = converter.convert("Java");
        System.out.println(converted);    // "J"
    }
}
class Something {
    String startsWith(String s) {
        return String.valueOf(s.charAt(0)); // 
    }
}
```



## 4.3 构造函数的引用

构造函数引用是一种通过构造函数的名称来引用已经存在的构造函数的语法。在Lambda表达式中，我们可以通过类名::new的方式来引用一个已经存在的构造函数。

### 4.3.1 语法格式：

~~~java
类名::new
~~~

### 4.3.2 实现案例

接下来看看构造函数是如何使用`::`关键字来引用的，首先我们定义一个包含多个构造函数的简单类：

```java
class Person {
    String name;
    String age;

    Person() {}

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

接下来我们指定一个用来创建Person对象的对象工厂接口：

```java
interface PersonFactory<P extends Person> {
    P create(String name, int age);
}
```

这里我们使用构造函数引用来将他们关联起来，而不是手动实现一个完整的工厂：

```java
public class ConstructReferences {
    public static void main(String[] args) {
        PersonFactory<Person> personFactory = Person::new;
        personFactory.add("shier", 19);
    }
}
```

我们只需要使用 `Person::new` 来获取Person类构造函数的引用，Java编译器会自动根据`PersonFactory.create`方法的参数类型来选择合适的构造函数。

> 需要注意的是，方法和构造函数的引用只能用于符合特定签名的方法和构造函数。也就是说，如果我们想要使用方法或构造函数的引用，必须确保它们的参数列表和返回值类型与Lambda表达式的参数列表和返回值类型一致。



# 5、Optional

Optional不是函数式接口，而是用于防止/避免 NullPointerException 的漂亮工具。

> Optional是一个容器对象，可以包含一个非空对象或者一个空对象。如果包含了非空对象，则`isPresent()`方法会返回true，调用`get()`方法会返回该对象。如果包含了空对象，则`isPresent()`方法会返回false，调用`get()`方法会抛出NoSuchElementException异常。

Optional 中提供一系列处理空指针异常的方法。

1. `of(T value)`：返回一个包含指定非空值的Optional对象，如果value为空，则抛出NullPointerException异常。
2. `ofNullable(T value)`：返回一个包含指定值的Optional对象，如果value为空，则返回一个空Optional对象。
3. `empty()`：返回一个空的Optional对象。
4. `isPresent()`：如果包含非空对象，则返回true，否则返回false。
5. `get()`：如果包含非空对象，则返回该对象，否则抛出NoSuchElementException异常。
6. `orElse(T other)`：如果包含非空对象，则返回该对象，否则返回指定的默认值other。
7. `orElseGet(Supplier<? extends T> other)`：如果包含非空对象，则返回该对象，否则返回由Supplier提供的默认值。
8. `map(Function<? super T, ? extends U> mapper)`：如果包含非空对象，则对其进行转换并返回包含转换结果的Optional对象，否则返回空Optional对象。
9. `flatMap(Function<? super T, Optional<U>> mapper)`：如果包含非空对象，则对其进行转换并返回转换结果，否则返回空Optional对象。

示例说明

~~~java
/**
 * @author Shier
 */
public class OptionalExample {
    public static void main(String[] args) {
        // 返回一个非空的Optional对象，为空则会出现NPE异常
        Optional<String> optional1 = Optional.of("hello");
        // 返回一个包含指定对象的Optional对象，为空则返回Optional对象
        Optional<String> optional2 = Optional.ofNullable(null);
        // 判断Optional实例对象是否为空
        System.out.println(optional1.isPresent()); // true
        System.out.println(optional2.isPresent()); // false

        // 包含非空对象则返回非空对象，否则就是NPE
        System.out.println(optional1.get()); // hell
        System.out.println(optional2.orElse("world")); // world

        // 非空则进行转换，返回的是一个转换后的Optional对象
        Optional<String> optional3 = optional1.map(s -> s.toUpperCase());
        System.out.println(optional3.get()); // HELLO
        // 如果包含非空对象，则对其进行转换并返回转换结果
        Optional<Integer> optional4 = optional1.flatMap(s -> Optional.of(s.length()));
        System.out.println(optional4.get()); // 5
    }
}
~~~

[关于Optional的更多介绍](https://blog.kaaass.net/archives/764)

# 6、Stream介绍

## 6.1. Stream流的作用是什么？

> Stream API 用于处理集合数据。Stream可以用于对集合进行筛选、排序、聚合等操作，它的使用方式和SQL语句类似。Stream不会修改源数据，而是通过生成一个新的Stream来执行操作，因此它是一个惰性求值的操作。只有在需要返回结果时才会执行实际操作。
>
> 又或者可以说是Stream 操作将分为中间操作或者最终操作两种，最终操作返回一特定类型的计算结果，而中间的操作则返回的是Stream本身，这样就可以将多个Stream操作串起来。

## 6.2. Stream流的思想和使用步骤

- 先得到集合或者数组的Stream流（就是一根传送带）
- 把元素放上去
- 然后就用这个Stream流简化的API来方便的操作元素

## 6.3. Stream流常用API方法

1. `filter(Predicate<T> predicate)`：用于对Stream进行筛选，保留符合条件的元素。（过滤掉，只要符合的内容）
2. `map(Function<T, R> mapper)`：用于对Stream进行映射，将元素进行转换。
3. `sorted(Comparator<T> comparator)`：用于对Stream进行排序。
4. `distinct()`：用于对Stream进行去重，去掉重复的元素。
5. `limit(long maxSize)`：用于对Stream进行截取，只保留前maxSize个元素。
6. `skip(long n)`：用于对Stream进行跳过，跳过前n个元素。
7. `forEach(Consumer<T> action)`：用于对Stream进行遍历，对每个元素执行指定的操作。
8. `collect(Collector<T, A, R> collector)`：用于对Stream进行聚合，将元素收集到一个容器中并返回。Stream流操作后的结果数据==转回到集合或者数组==中去。
9. `reduce(T identity, BinaryOperator<T> accumulator)`：用于对Stream进行聚合，将元素逐个应用给定的累加器函数，并返回累加结果。



Collectors工具类提供具体的收集方式

| 方法                                                         | 说明                   |
| ------------------------------------------------------------ | ---------------------- |
| public static <T> Collector taList(）                        | 把元素收集到List集合中 |
| public static <T> Collector toet()                           | 把元素收集到Set集合中  |
| public static collector oap(Function kexMlapper , Function valueMappe.) | 把元素收集到Map集合中  |

## 6.5 示例并对API解释

首先创建一个动态数组，也就是ArrayList集合，并对里面添加一些数据

```java
List<String> stringList = new ArrayList<>();
stringList.add("ddd2");
stringList.add("aaa2");
stringList.add("bbb1");
stringList.add("aaa1");
stringList.add("bbb3");
stringList.add("ccc");
stringList.add("bbb2");
stringList.add("ddd1");
```

### 6.5.1 Filter（过滤）

过滤通过一个predicate接口来过滤并只保留符合条件的元素，该操作属于**中间操作**，所以我们可以在过滤后的结果来应用其他Stream操作（比如forEach）。forEach需要一个函数来对过滤后的元素依次执行。forEach是一个最终操作，所以我们==不能在forEach之后来执行其他Stream操作==。

```java
// 测试 Filter(过滤)
stringList
        .stream()
        .filter((s) -> s.startsWith("a"))// 以a开头的
        .forEach(System.out::println);//aaa2 aaa1 使用了函数式接口中方法的引用

stringList.stream().filter((str) -> str.endsWith("1")).forEach(System.out::println);// bbb1 aaa1 ddd1
```

forEach 是为 Lambda 而设计的，保持了最紧凑的风格。而且 Lambda 表达式本身是可以重用的，非常方便。



### 6.5.2 Sorted（排序）

排序也是一个 **中间操作**，返回的是排序好后的 Stream。**如果你不指定一个自定义的 Comparator 则会使用默认排序（升序）。**

```java
  		// 排序
        stringList.stream().sorted()
                .filter((s) -> s.startsWith("a"))// 以a开头的
                .forEach(System.out::println); //aaa1 aaa2 使用了函数式接口中方法的引用
        System.out.println("Sorted倒序排序:");
        stringList.stream().sorted((a, b) -> b.compareTo(a))
                .filter((s) -> s.startsWith("a"))
                .forEach(System.out::println); //aaa2 aaa1
```

需要注意的是，排序只创建了一个排列好后的Stream，而不会影响原有的数据源，排序之后原数据stringList是不会被修改的



### 6.5.3 Map (映射)

中间操作 map 会将元素根据指定的 Function 接口来依次将元素转成另外的对象。

示例

```java
// 测试映射
stringList.stream().map(s -> s.toUpperCase()).sorted().forEach(System.out::println);
stringList.stream().map(String::toUpperCase).sorted().forEach(System.out::println);
```



### 6.5.4 Match (匹配)

Stream提供了多种匹配操作，允许检测指定的Predicate是否匹配整个Stream。所有的匹配操作都是 **最终操作** ，并返回一个 boolean 类型的值。

1. anyMatch 方法：如果集合中至少有一个元素满足Predicate条件，返回true，否则返回false。

   ```java
   List<Integer> numbers1 = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
   List<Integer> numbers2 = Arrays.asList(1, 3, 5, 7, 9);
   boolean hasEven1 = numbers1.stream().anyMatch(n -> n % 2 == 0);
   boolean hasEven2 = numbers2.stream().anyMatch(n -> n % 2 == 0);
   System.out.println("number1: " + hasEven1); // true
   System.out.println("number2: " + hasEven2); // false
   ```

2. allMatch方法：如果集合中所有元素都满足Predicate条件，返回true，否则返回false。

   ```java
   List<Integer> numbers1 = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
   boolean hasEven1 = numbers1.stream().allMatch(n -> n % 2 == 0);
   System.out.println("number1: " + hasEven1); // true
   ```

3. noneMatch方法：如果集合中没有元素满足Predicate条件，返回true，否则返回false。

   ```java
    List<Integer> numbers1 = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
    List<Integer> numbers2 = Arrays.asList(1, 3, 5, 7, 9);
    boolean hasEven1 = numbers1.stream().noneMatch(n -> n % 2 == 0);
    boolean hasEven2 = numbers2.stream().noneMatch(n -> n % 2 == 0);
    System.out.println("number1: " + hasEven1); // false
    System.out.println("number2: " + hasEven2); // true
   ```



### 6.5.5 Count (计数)

计数是一个 **最终操作**，返回Stream中元素的个数，**返回值类型是 long**。

```java
// 测试计数 Count 操作
long count = stringList.stream().filter(s -> s.startsWith("a")).count();
System.out.println(count); // 2
```

### 6.5.6 Reduce （规约）

这是一个 **最终操作** ，允许通过指定的函数来将stream中的多个元素规约为一个元素，规约后的结果是通过Optional 接口表示的

```java
// 规约
Optional<String> reduce = stringList.stream().sorted().reduce((a, b) -> a + "-" + b);
System.out.println(reduce);
```

这个方法的主要作用是把 Stream 元素组合起来。它提供一个起始值（种子），然后依照运算规则（BinaryOperator），和前面 Stream 的第一个、第二个、第 n 个元素组合。从这个意义上说，字符串拼接、数值的 sum、min、max、average 都是特殊的 reduce。例如 Stream 的 sum 就相当于`Integer sum = integers.reduce(0, (a, b) -> a+b);`也有没有起始值的情况，这时会把 Stream 的前面两个元素组合起来，返回的是 Optional。

```java
        // 字符串连接
        String concat = Stream.of("A", "B", "C", "D").reduce("", String::concat);
        System.out.println(concat); //ABCD
        // 求最小值
        double minValue = Stream.of(-1.5, 1.0, -3.0, -2.0).reduce(Double.MAX_VALUE, Double::min);
        System.out.println(minValue); // -3.0
        // 求和
        int sumValue = Stream.of(1, 2, 3, 4).reduce(0, Integer::sum);
        System.out.println(sumValue);// sumValue = 10, 有起始值
        // 求和
        sumValue = Stream.of(1, 2, 3, 4).reduce(Integer::sum).get();
        System.out.println(sumValue);// sumValue = 10, 无起始值
        // 过滤
        concat = Stream.of("a", "B", "c", "D", "e", "F")
                .filter(x -> x.compareTo("Z") > 0)
                .reduce("", String::concat);
        System.out.println(concat);//字符串连接，concat = "ace"
```

上面代码例如第一个示例的 reduce()，第一个参数（空白字符）即为起始值，第二个参数（String::concat）为 BinaryOperator。这类有起始值的 reduce() 都返回具体的对象。而对于第四个示例没有起始值的 reduce()，由于可能没有足够的元素，返回的是 Optional，请留意这个区别。



# 7、Parallel Streams （并行流）

上一章提到过Stream有串行和并行两种，串行Stream上的操作是在一个线程中依次完成，而并行Stream则是在多个线程上同时执行。

下面开始介绍并行流如何提高性能：

首先创建一个没有重复的大表：

```java
int max = 1000000;
List<String> values = new ArrayList<>(max);
for (int i = 0; i < max; i++) {
    UUID uuid = UUID.randomUUID();
    values.add(uuid.toString());
}
```

分别使用串行和并行进行排序，看看执行的时间；

```java
/**
 * @author Shier 2023/2/20 14:19
 */
public class ParallelStreamTest {
    public static void main(String[] args) {
        int max = 1000000;
        List<String> values = new ArrayList<>(max);
        for (int i = 0; i < max; i++) {
            UUID uuid = UUID.randomUUID();
            values.add(uuid.toString());
        }
        // 串行排序
        long startTime = System.currentTimeMillis();
        long count = values.stream().sorted().count();
        long endTime = System.currentTimeMillis();
        System.out.println("串行执行时间：" + (endTime - startTime) + "ms"); // 665ms

        // 并行排序
        long startParallelTime = System.currentTimeMillis();
        long count2 = values.parallelStream().sorted().count();
        long endParallelTime = System.currentTimeMillis();
        System.out.println("并行执行时间：" + (endParallelTime - startParallelTime) + "ms"); // 332ms
    }
}
```

上面的串并行排序的代码几乎是一样的，但是并行排序的效率块了50%左右。可见性能提高了不少。与普通的串行流相比，并行流可以充分利用多核CPU的优势，加速集合的处理速度。

> 需要注意的是，并行流在某些情况下并不一定比串行流更快，甚至有可能比串行流更慢。这是因为并行流需要将数据分成多个部分，分别在不同的线程上进行处理，而这个过程本身也需要一定的时间和资源。因此，在使用并行流时，需要根据具体的情况进行测试和优化。



# 8、 可重复注解

在 Java 8 中，可以使用@Repeatable注解来定义可重复注解，这使得我们可以将同一种注解多次应用于同一元素上。在使用可重复注解时，需要先定义一个包含@Repeatable注解的容器注解，再在容器注解中定义注解的值，如果想要给同一个类型的注解使用多次，只需要给该注解标注一下`@Repeatable`即可。

例如，假设我们要定义一个@Author注解，用于标记一篇文章的作者，我们可以按照以下步骤进行操作：

1. 定义容器注解Authors：

   ~~~java
   /**
    * 定义一个容器注解类Authors
    */
   public @interface Authors {
       Author[] value();
   }
   ~~~

2. 定义一个包含@Repeatable注解的容器注解Authors：

   ~~~java
   /**
    * @author Shier 2023/2/20 14:39
    * 使用容器注解类的注解@Repeatable说明是可重复的
    */
   @Repeatable(Authors.class)
   public @interface Author {
       String name();
   }
   ~~~

   > 第一步和第二步都是在创建一个包装类，将Authors作为注解

3. 使用@Author注解时，可以将多个作者名字传递给容器注解Authors：

   ~~~java
   /**
    * 第一种写完整的
    * 在使用容器注解来声明值，最外层的为复数形式的注解类，也就是第一个步骤创建的类，里面的Author是第二步创建的可重复的注解类
    */
   @Authors({
           @Author(name = "shier"),
           @Author(name = "小十二"),
   })
   public class Article {}
   
   
   /**
    * 第二种简单写法
    */
   @Author(name = "shier")
   @Author(name = "小十二")
   public class Article {}
   ~~~

在上面的例子中，@Author注解表示一篇文章的作者，使用@Repeatable注解来定义可重复注解。然后定义一个容器注解Authors，包含一个Author类型的数组。最后，在定义一篇文章时，可以将多个作者名字传递给@Authors注解。

通过使用可重复注解，我们可以更加灵活地定义和使用注解，使代码更加简洁和易读。











