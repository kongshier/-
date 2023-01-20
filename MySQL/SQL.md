> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 1.SQL service 系统概述

SQL service 是一个可扩展的、高性能的、为分布式客户机 / 服务器计算所设计的数据库管理系统

## 数据库系统组成

1. 数据库
2. 用户
3. 软件系统
4. 硬件系统

~~~mermaid
graph LR
1(数据库)-->2(集成性)
1(数据库)-->3(共享性)
a(用户)-->a1(第一用户)-->a11(最终用户)
a(用户)-->a2(第二用户)-->a21(应用程序员)
a(用户)-->a3(第三用户)-->a31(数据管理员)
b(硬件系统)-->b1(存储和运行数据库的系统)-->b11(CPU 内存 输入 输出设备 外部设等)
d(软件系统)-->d1(数据库管理系统DBMS 操作系统OS)
~~~

## 内部体系结构

### 三级模式结构概念

概念：型 、值

**型：** 某一类数据的结构和属性。

**值：** “型” 的具体赋值。

### 模式结构

从逻辑上分： 1 .外模式 、模式  2.内模式三级抽象模式结构   3.二级映像功能

对用户而言： 用户模式（外模式）  概念模式（模式）  物理模式（内模式） 

三级模式结构和二级映像功能示意图

**模式：** 全体数据的逻辑结构和特征的描述。 不涉及数据的物理存储细节和硬件环境。

**外模式：** （子模式 或者 用户模式）用户允许和看到的那些数据 、与有关的数据逻辑表示，用户的数据视图（用户视图）。一个数据库可以有多个外模式。

**内模式：** （存储模式或者物理模式） 对存储结构的描述，数据库的内部表达形式 。

### 数据库系统三级模式与二级映像的优点

1. 保证数据的独立性
2. 简化用户接口
3. 有利于数据共享
4. 有利于数据的安全保密

## 外部体系结构

由 单用户结构、主从式结构、分布式结构、客户机/服务器结构  浏览器/服务器结构组成

### 单用户结构的数据库系统

> 将应用程序 、 DBMS和数据库在同一个计算机上，独立使用，不能与其他计算机共享数据

### 主从式结构的数据库系统

> 大型主机带多端的多用户结构

**优点**：

1. 结构简单
2. 易于管理与维护

**缺点：** 

1. 性能要求比较高
2. 出故障，则无法使用

### 分布式结构的数据库系统

> 数据在逻辑上是整体的，在物理分布上是在不同的结点上的。结点上分布数据相对独立

**优点：** 多台服务器并发处理数据。

**缺点：** 数据分布式存储数据困难。

### 客户机/服务器结构的数据库系统

**优点：**

1. 网络允许效率提高
2. 由客户机完成应用程序的允许和计算

**缺点：** 

1. 不易于维护升级
2. 客户机要安装客户机程序

### 浏览器/服务器结构的数据库系统

只需按照通用浏览器 实现用户输入输出。

## 4.数据库管理系统DBMS（数据库系统的核心）

**DBMS功能**

>  数据定义功能、 数据操纵功能、数据库运行功能、数据库建立和维护功能、数据通信接口、数据组织存储管理功能。

#### 4.1数据定义功能  DDL

提供查询化语言：SQL 提供Create Drop Alter等语句来执行数据库。

DDL(数据定义语言)  （数据字典 DD　Data　Ｄｉｃｔｉｏｎａｒｙ）

#### 4.2数据操纵功能   DML

DBMS提供：数据操纵语言( DML)   例如一些： 查询（SELECT）、插入语句( INSERT) 、修改（UPDATE）、删除（DELETE）

#### 4.3数据运行管理功能

控制数据库的方法：

1. 数据安全性控制
2. 数据完整性控制
3. 多用户环境下的对数据并发性控制
4. 数据库的回复

#### 4.4数据库的建立和维护功能

​	**建立：** 初始数据装入和数据转换

​	**维护：**  数据库的转储、恢复、重组织与重构造、系统性能监视与分析

#### 4.5数据通信接口

​	与软件系统通信

#### 4.6数据组织、存储和管理

对存放的各种数据的组织、存储、管理 提高利用率

### DBMS的组成

1. 语言编译处理程序：DDL(数据定义) 和 DML（数据操纵） 
2. 系统运行控制程序：系统总控程序(核心)， 安全性控制程序，完整性控制系统，并发控制系统，数据存取和更新系统，通信控制程序 
3. 系统建立、维护程序 ：装配程序，重组程序，系统恢复程序
4. 数据字典  ：帮组管理系统

### DBMS数据存取过程步骤

1. 用户使用特点的数据操纵语言向DBMS发出存取请求
2. DBMS接受请求并将改请求转换成代码指令
3. DBMS依次检查外模式、外模式/模式映像，模式，模式/内模式以及存储结构定义。
4. DBMS对存储数据库执行必要的存取操作
5. 对得到的结果进行处理
6. 将结果返回给用户。

## 数据模型

- 数据模型三要素：数据结构、数据操作和数据约束

- 分类：概念模型 ，逻辑模型 物理模型


### 组成要素

1. 数据结构：描述数据库的组成对象以及对象间的关系
2. 数据操作：数据之间允许执行的操作的集合
3. 数据完整性的约束：规则的集合

## 三个世界

### 现实世界

### 信息世界

1. 实体

2. 属性

3. 实体性  ：有相同属性的实体必然有共同的特征

4. 实体集   ：同型实体的集合

5. 码 ： 在实体型中，能唯一标识一个实体的属性或者属性集

6. 域：一组具有相同数据类型的值的集合
   - 基数：包含值的个数
7. 联系

#### 两个实体型间的关系

1. 一对一联系
2. 一对多联系
3. 多对多联系

#### 两个以上实体型间的联系

#### 单个实体型内部联系

### 计算机世界

> 字段（Field） : 标记实体属性的命名单位
>
> 记录（Record）：字段的有序集合
>
> 文件（File）： 同一类记录的集合
>
> 关键字

## 四种数据模型

### 层次模型：用树形数据结构（有银树）来表示各实体以及实体间的联系

**特点：**

1. 每棵树有且只有一个结点没有双亲 该结点就是跟结点
2. 根结点以外的其他结点有且只有一个双亲结点
3. 父子结点之间的联系是一对多的的联系

#### 层次模型的数据操纵与数据完整性约束

​	**插入：**没有对应的双亲结点不能插入子女结点

​	**删除：**删除双亲结点 子女相应结点也会删除

#### 层次模型优缺点

##### 	优点

1. 结构简单，层次分明，便于实现
2. 结点间联系简单
3. 具有良好的数据完整性支持。

##### 缺点

1. 不能直接表示两以上的实体型间的复杂联系和实体型间的多对多联系
2. 对数据插入和删除限制太对
3. 查询子女节点必须要经过双亲结点

### 网状模型

采用有向图结构表示记录型与记录型之间的数据模型 更直接描述现实世界

**特点**

1. 有一个以上的结点没有双亲结点
2. 允许结点有多个双亲结点
3. 允许两个结点之间有多种联系（复合联系）

#### 网状结构的完整性与约束性

1. 插入数据： 允许插入尚未确定双亲结点值的子女结点值
2. 删除数据：允许数据只删除双亲点值
3. 修改数据：可直接表述非属性结构

#### 网状模型的优缺点

优点

1. 更为直观的描述客观世界，可表述实体间的多种复杂联系
2. 具有良好的性能和存储效率

缺点

1. 数据结构复杂
2. 数据定义和数据操纵极其复杂
3. 加重应用程序负担

### 关系模型

是一张规范化的二维表，由表名、表头和表体构成。

> 关系与关系的实例：一个关系实例对应一张由行和列构成的二维表
>
> 元组： 二维表中的一行
>
> 属性：二维表中的一列
>
> 域 属性的取值范围
>
> 分量 ：每一行元组对应的列的组合
>
> 候选码：（含义解释不清）就是一行一列的交点 一个关系可以有多个候选码
>
> 主码：一个关系中有多个候选码时可以选一个为主码，一个关系只能有一个主码
>
> 关系模式：关系名（属性1 ，属性2 .····属性n）
>
> 关系实例：关系模式的“ 值” 二维表中的数据

关系模式的优缺点

优点：

1. 关系模式与非关系模式不同，有严格的数学理论根据
2. 数据结构简单、清晰、用户易懂、易用，关系描述实体，数据的操纵结果也是关系。
3. 关系模式的存取路劲对用户透明，从而更具有更高的数据独立性，更好的安全保密性，也简化，增加了开发数据库管理系统的负担。

### 面向对象（java）模型

1. 对象和对象标识
2. 类和继承

### 数据库领域新技术

1. 分布式数据库
2. 数据仓库与数据挖掘技术
3. 多媒体数据库
4. 大数据技术

# 2.关系数据库



## 2.1关系模型的数据结构及其形式化定义



### 2.1.1关系形式化定义及其概念

**1.域**

> 定义2.1 ：域是一组相同数据类型的集合，又称值域。域中所包含的值的个数称为**基数**；

**2.笛卡尔积**

> 定义2.2 ：给定一组域（D~1~,D~2~，····，D~n~）（可以是部分或者全部相同元素，也可以全部不同元素）记为：D~1~ *D~2~ * ····*D~n~ = {d~1~,d~2~,····d~n~ }
>
> d~i~ 是分量；{d~1~,d~2~,····d~n~ } 是一个元组；

可以用一个**二维表**表示出来

D~1~ * D~2~ = {(丽丽，女)，（娜娜，男），（boy,女）}

| 姓名 | 性别 |
| :--: | :--: |
| 丽丽 |  女  |
| 娜娜 |  男  |
| boy  |  女  |



例题：

笛卡尔积R由4个域组成，若每个域的基数均为2，则R的基数为（16）

- 2^4^   

- 笛卡尔积是：A×B×C×D

- 也就是想这样的一个二维表

- | A    | B    | C    | D    |
  | ---- | ---- | ---- | ---- |
  |      |      |      |      |
  |      |      |      |      |







**3.关系**

> 定义2.3：笛卡尔积D~1~ *D~2~ * ····*D~n~的任一子集称为定义在域D~1~,D~2~，····，D~n~上的**n元关系**，用R(D~1~,D~2~，····，D~n~) 表示  R:关系名字；n是关系的目或度
>
> 

注意

1. 关系R中 ，n = 1 时 是单元关系，n = 2  为二元关系依次类推；
2. 关系中的每个元素是关系中的元组；
3. 关系是笛卡尔积的一个子集   每一行为元组  每一列为域；
4. 在数学上，关系是笛卡尔积的子集，实际应用中，关系是有意义的笛卡尔积的子集；

> 定义2.4：定义在域D~1~ *D~2~ * ····*D~n~ 上的关系由关系头和关系体组成。

### 2.1.2关系的性质  

1. 列是同质的，每一列中的分量必须来自同一个域，必须是同一个类型的数据
2. 不同的属性可来自同一个域，但不同的属性必须有不同的名字（属性是列）
3. 列的顺序可以任意交换（属性）
4. 关系中元组的顺序可任意 交换（行）
   - 记录也表示行
5. 关系中不允许出现 相同的元组（行）
6. 关系中每一分量必须是不可分的数据项 ，所有的属性值都是原子的 ，一个确定的值。

### 2.1.3关系模式

关系模式是型 ，关系是值，关系模式是对关系的描述

1. 定义2.5：关系的描述称为关系模式，形式化表示为 R (U，D,DOM,F)


- R：关系名

- U：组成该关系的属性名集合

- D：属性组U中属性所带来的域

- DOM：属性向域的映像集合；

- F：属性间数据的依赖关系集合。

- 简记为：R(U) R:关系名 U：属性名的集合



- 关系模式：是关系的框架(表框架)，是对关系结构的描述，是稳定的，静态的
- 关系：动态的、随时间不断变化、它关系模式在某一时刻的状态或内容   ，关系中的操作不断更新数据库中的数据



### 2.1.4关系数据库与关系数据库模式

- 在一个给定的领域中，所有实体以及实体之间的联系所对应的关系的集合构成一个关系数据库。

- 关系数据库的型为关系数据库模式，是对关系数据库的描述

## 2.2关系的码与关系完整性

### 2.2.1候选码与主码

**1.候选码**

> 能够唯一标识关系中元组的一个属性或属性集  也称为（候选关键字，候选键）；
>
> 定义2.6：设关系R有属性 A~1~,A~2~,A~3~,···A~n~,其属性集K=（ A~1~,A~2~,A~3~,···A~n~），当且仅当满足以下条件时，则K称为候选码
>
> 1. 唯一性：关系R的任意两个不同元组，其属性集K的值是不同的；
> 2. 最小性：组成关系建的 （ A~1~,A~2~,A~3~,···A~n~）中，任一属性都不能从属性集K中删掉，否则破坏唯一性。

**2.主码**

> 若一个关系中有多个候选码，则从中选择一个作为查询、插入、删除元素的操作变量，选中的为主码，也称主关系建、主键、关系键、关键字等。
>
> **每个关系中必须要选中一个主码，选中则不能修改**

**3.主属性与非主属性**

> **主属性：** 包含在主码中的各个属性
>
> **非主属性：**不包含在任何候选码中的属性；
>
> **例题：**假设有教师授课关系TCS,分别有三个属性教师(T)、课程(C)和学生(S)。-个教师可以讲授多门课程，- 门课程可以有多个教师讲授，同样一个学生可以选听多门课程，一门课程可以为多个学生选听。在这种情况下，T, c, s三者之间是多对多关系，(T, C, S)三个属性的组合是关系TCS的候选码，称为全码，T, C, S都是主属性。

### 2.2.2外码（外部关系键）

> 若关系R~2~ 的一个或一组属性X不是R~2~ 的主码，而是另一个关系R~1~ 的主码，则该属性或属性组X称为关系R~2~ 的外码或外部关系键，并成关系R~2~
>
> 为参照关系，关系R~1~ 为被参照关系。

### 2.2.3关系的完整性

关系模型中三类完整性：实体完整性，参照完整性，用户自定义 ，其中实体完整性，参照完整性，必须满足完整性约束条件，称为关系两个不变性；

由于不同的应用环境，还需要一些约束条件，就用户自定义完整性。

1.完整实体型

- 指主码的值不能为空或部分为空

- 关系模型中，一个元组对应一个实体，一个关系则对应一个实体集。

2.参照完整性

- 如果关系R~2~ 的外码X与关系R~1~ 的主码相符，则X的每个值或者等于R~1~ 主码中的某一个值，或者取空值
- 也就是R~1~(X) 、 R~2~   

3.用户自定义完整性

- 针对某一具体关系数据库的约束条件，反映某一具体应用所涉及的数据必须满足的语义要求。

## 2.3关系代数

- 关系模型由关系数据库、关系操作、关系完整性越苏三部分组成。


- 常用的关系操作：查询操作，更新操作

### 2.3.1关系代数运算符

**集合运算符**

| 运算符 | 含义     | 英文              |
| ------ | -------- | ----------------- |
| ∪      | 并       | Union             |
| −      | 差       | Difference        |
| ∩      | 交       | Intersection      |
| ×      | 笛卡尔积 | Cartesian Product |

**比较运算符**

| 运算符 | 含义     |
| ------ | -------- |
| >      | 大于     |
| ≥      | 大于等于 |
| <      | 小于     |
| ≤      | 小于等于 |
| =      | 等于     |
| ≠      | 不等于   |



**关系运算符**

| 运算符 | 含义 | 英文       |
| :----- | :--- | :--------- |
| σ      | 选择 | Selection  |
| π      | 投影 | Projection |
| ⋈      | 链接 | Join       |
| ÷      | 除   | Division   |

**逻辑运算符**

| 运算符 | 含义 |
| :----- | :--- |
| ∧      | 与   |
| ∨      | 或   |
| ¬      | 非   |



**5 种基本的关系代数运算**

- **并（Union）**
  - 关系 R 与 S 具有相同的关系模式，即 R 与 S 的元数相同（结构相同），R 与 S 的并是属于 R 或者属于 S 的元组构成的集合，记作 R ∪ S，定义如下：
  - R∪S={t|t∈R∨t∈S}R∪S={t|t∈R∨t∈S}
  - 相同算一个 ，不同则并起来

- **差（Difference）**
  - 关系 R 与 S 具有相同的关系模式，关系 R 与 S 的差是属于 R 但不属于 S 的元组构成的集合，记作 R − S，定义如下：
  - R−S={t|t∈R∨t∉S}R−S={t|t∈R∨t∉S}

- **广义笛卡尔积（Extended Cartesian Product）**
  - 两个无数分别为 n 目和 m 目的关系 R 和 S 的 笛卡尔积是一个 (n+m) 列的元组的集合。组的前 n 列是关系 R 的一个元组，后 m 列是关系 S 的一个元组，记作 R × S，定义如下：
  - R×S={t|t=<(t~n~ ,t~m~)∧t~n~∈R∧tm∈S}R×S={t|t=<(t~n~,t~m~)∧t~n~∈R∧t~m~∈S}
  - $(t^n,t^m)$ 表示元素 $t^n$ 和 $t^m$ 拼接成的一个元组

- **投影（Projection） ** 单目运算
  - 投影运算是从关系的垂直方向进行运算，在关系 R 中选出若干属性列 A 组成新的关系，记作 $π_A(R)$，其形式如下：
  - πA(R)={t[A]|t∈R}πA(R)={t[A]|t∈R}

- **选取（Selection）**  单目运算

  - 选择运算是从关系的水平方向进行运算，是从关系 R 中选择满足给定条件的元组，记作 $σ_F(R)$，其形式如下：

  - σF(R)={t|t∈R∧F(t)=True}σF(R)={t|t∈R∧F(t)=True}


- **交（Intersection）**

  - 关系 R 和 S 具有相同的关系模式，交是由属于 R 同时双属于 S 的元组构成的集合，记作 R∩S，形式如下：

  - R∩S={t|t∈R∧t∈S}R∩S={t|t∈R∧t∈S}

- 链接（Join）

  注：下面的 θ 链接应该记作：

- **θ 链接**  二目运算

  - 从 R 与 S的笛卡尔积中选取属性间满足一定条件的元组，可由基本的关系运算笛卡尔积和选取运算导出，表示为：

  - R⋈XθYS=σXθY(R×S)R⋈XθYS=σXθY(R×S)

  - XθY 为链接的条件，θ 是比较运算符，X 和 Y 分别为 R 和 S 上度数相等且可比的属性组

- **等值链接**
  - 当 θ 为「=」时，称之为等值链接，记为： $R\Join_{X=Y}S$

- **自然链接**
  - 自然链接是一种特殊的等值链接，它要求两个关系中进行比较的分量必须是 相同的属性组，并且在结果集中将 重复的属性列 去掉

- **除法（division）**  二目运算

​		关系R(X , Y) 与关系 S（Y，Z）其中 X,Y,Z为属性集合，R中的Y与S中的Y可以有不同的属性名，但对应属性必须出自相同的域。

​		关系R除以关系S得一个新关系P(X,Y)；P 是R中满足下列条件的元组在X上的投影：元组在X上分量值x的像集Y~x~ 包含S在Y上投影的集合。

​		R÷S={t~r~[X] t~r~∈R ∩Π~y~ (S)∈Y~x~}

​		Y~x~  为x在R上的像集 x=t~r~ [X]

在S中找出与R的像集对应的元素 则对应的元组则为R÷S的结果

![image-20220110112904608](C:\Users\86177\AppData\Roaming\Typora\typora-user-images\image-20220110112904608.png)

### 2.3.2传统的集合运算

1. 设给定两个关系 R  S，若满足

   - 具有相同的列数（或称度数）n；
   - R中第 i  个属性和S中的 第 i  个属性必须来自同一个域（列同质）

   则说关系 R ,S 是相容的

   **除了笛卡尔积运算外，其他的集合运算要求参加运算的关系必须满足上述的相容性定义**

### 2.3.3

## 2.4关系演算

> 元组关系演算
>
> 域关系演算

### 2.4.1演算语言

> **1.ALPHA语言**
>
> > 谓词公式定义要求
> >
> > ALPHA格式：<操作符> <工作空间名> (<目标表>)[ :<操作条件>]
> >
> > 操作符有：GET ， PUT ， HOLD ，UPDATE ，DELETE， DROP
>
> > **数据查询**
> >
> > > 1. 简单查询   ： GET W (S) 把数据库中的数据读入内存空间 W ;目标表 S 
> > >
> > >    ~~~sql
> > >    GET W (SC.CNo)
> > >    /*目标表为选课关系 SC中的属性CNo */
> > >    ~~~
> > >
> > > 2. 条件查询:使用运算符进行筛选
> > >
> > > 3. 排序查询：规定顺序
> > >
> > > 4. 定额排序：规定查询出元组的个数 在括号后面加定额数量
> > >
> > > 5. 带元组变量的查询  ：元组变量代表关系中的元组  取值在规定范围内变化的  
> > >
> > >    **两个用途**
> > >
> > >    > 1. 定义短变量
> > >    > 2. 使用**量词**用到元组变量
> > >
> > > 6. 带存在量词的查询
> > >
> > > 7. 库函数查询
> >
> > **数据更新**
> >
> > **修改**  ：使用UPDATE 语句实现
> >
> > > 1. 读数据  ：使用HOLD语句将要修改的元组从数据库中读到工作空间中
> > > 2. 修改：利用宿主语言修改
> > > 3. 返回：使用UPDATE语句修改
> >
> > **插入**  ：使用PUT语句
> >
> > > 1. 建立新元祖
> > > 2. 写数据：利用PUT语句将元组写入到指定的关系中
> >
> > **删除**  :使用DELETE语句实现
> >
> > > 1. 读数据
> > > 2. 删除：使用delete语句删除该元组

**2.QUEL语言**

> 1. **数据定义**  **使用 CREATE语句定义新关系**
>
>    > CREATE<关系名> （<属性名 = 数据类型及长度 >，[ ,<属性名 = 数据类型及长度  ······>）
>
> 2. 数据查询
>
>    > 格式：
>    >
>    > ~~~sql
>    > RANGE OF t1 IS  R1
>    > RANGE OF t2 IS  R2
>    > ···
>    > RANGE OF tk IS  RK
>    > RETRIEVE(目标表)
>    > WHERE<条件>
>    > /*
>    > t1  t2 是定义在 R1 R2 上的元组变量
>    > */
>    > ~~~
>
> 3. 数据更新
>
>    > 1. 修改：使用REPLACE语句实现
>    >
>    >    ~~~sql
>    >    RANGE OF TX IS T 
>    >    REPLACE (TX.Dept ='信息')
>    >    WHERE TX,TN='刘伟'
>    >    ~~~
>    >
>    > 2. 插入：使用APPEND语句实现
>    >
>    >    ~~~sql
>    >    APPEND TO SC (SNc = 'ss',CNo = 'C2',Score = 90)
>    >    ~~~
>    >
>    > 3. 删除：使用DELETE语句实现
>    >
>    >    ~~~sql
>    >    RANGE OF SX IS S 
>    >    DELETE SX 
>    >    WHERE SX.SNo='S6'
>    >    ~~~

2.4.2域关系演算语言QBE (Query By  Example)  

> QBE ： 示例查询  屏幕编辑语言 
>
> **特点**
>
> 1. 以表格形式进行操作  ：以一个表格或者多个表格进行操作
>
> 2. 通过例子进行查询
>
> 3. 查询顺序自由
>
>    **使用QBE步骤**
>
>    1. 用户根据要求向系统申请一张或几张表格 这些表格显示在终端上。
>    2. 用户在空白表格在左上角的一栏内输入关系名
>    3. 系统根据用户输入的关系名，将在第一行从左至右自动填写各个属性名
>    4. 用户在关系名或属性名下方的一个内填写相应的操作指令，操作命令包括 P.(打印或显示)、U（修改）、I.(插入)、D.(删除)
>
> **数据查询** 
>
> 1. 简单查询 ：使用操作符  P. 完成数据查询。  用作示例的元素下方有下划线
> 2. 条件查询
> 3. 排序查询
> 4. 库函数查询
>
> **数据更新**
>
> 1. 修改 U.
> 2. 插入 I.
> 3. 删除 D.

# 3.关系数据库标准语言 -SQL

## 3.1符号意义

~~~sql
@ 表示局部变量

@@ 表示全局变量

# 表示本地临时表的名称，以单个数字符号打头；它们仅对当前的用户连接是可见的

## 表示全局临时表
-- 注释
/**/ 代码块注释
~~~





> 数据库存储数据占用空间小，容易持久保存 存储安全，容易维护和升级，数据库容易移植，简化对数据的操作。

文件

> 主文件：.mdf 扩展名
>
> 日志文件：.ldf 扩展名  log日志

##  3.2数据库的修改和删除

### 使用脚本修改  TSQL

~~~sql
exec sp_helpdb testdb(数据库名称)  /*exec sp_helpdb  数据库名称 就是查看这个数据库的内容*/
/*修改  修改对象 ，修改对象名称*/
alter database testdb01
/*固定的编辑语法 修改name = XXX */
modify name = testdb02;只是修改了名称，但是逻辑文件名称没有修改
/*修改数据文件的名称*/
alter database testdb02 这个是修改后的名称
modify file {
name = 'testdb01',这个是原来库的名称
size = 15MB,
maxsize =50MB,
filegrowth = 10MB
};
~~~

修改逻辑名称：

~~~sql
--修改逻辑文件名  
--MDF
   alter database 数据库名称 modify file(name=原逻辑文件名, newname=新逻辑文件名)  
--Log
   alter database 数据库名称 modify file(name=原逻辑文件名, newname=新逻辑文件名)   
~~~





### 使用较本删除数据库

~~~sql
drop database testdb;/*使用drop语句删除自己创建的数据库 一般不能删除系统的数据库，*/ 
~~~

## 3.3数据库的备份和还原

> 差异备份  （differential backup）在上一次基础上再备份一个
>
> 完整备份（full backup）  整个备份下来

> 执行备份  .bak 后缀名
>
> 还原：通过bak备份文件进行还原

## 3.4数据类型

> 数据类型就是属性 ，有一些常用的，例如：整数数据 ，字符数据，日期数据，货币数据等

### 数字类型

| 数据类型 | 范围                | 占用的字节 |
| -------- | ------------------- | ---------- |
| bigint   | -2^63^ ~2^63^ -1    | 8字节      |
| int      | -2^31^~2^31^-1      | 4字节      |
| smallint | - 2^15^ ~ 2^15^-1   | 2字节      |
| tinyint  | 0~255               | 1字节      |
| float    | -1.79E+308~3.40E+38 | 4或者8字节 |

### 时间类型

| 数据类型      | 输出                                                   |
| ------------- | ------------------------------------------------------ |
| time          | 12：35：29.123 （精确度到秒后面三位）时分秒            |
| date          | 2007-05-08 （年月日）                                  |
| smalldatetime | 2007-05-08 12:35:00                                    |
| datetime      | 2007-05-08 12:35:29.123(精确到后面 就是小数点后面三位) |
| datetime      | 2007-05-08 12:35:29.1234567(精确到小数点后面三七位)    |

### 字符串类型

| 类型              | 说明                                                         |
| ----------------- | ------------------------------------------------------------ |
| char[(n)]         | 固定长度 。 n用于定义字符串长度，**必须**在1~8000之间。      |
| varchar[(n\|max)] | 可变长度。n用于定义字符串长度，**可以**在1~8000之间。        |
| nchar[(n)]        | 固定长度的Unicode字符串数据。n用于定义字符串长度，**必须**在1~4000之间。 |
| nvarchar          | 可变长度的Unicode字符串数据。n用于定义字符串长度，**必须**在1~4000之间。 |

## 3.5创建表

> 关键：表名称，列名称，数据类型，每个是否为空值，
>
> 表中的主键：由表的一列或多列组成，主键始终是唯一的，主键值不可以重复。

### SSMS创建表



### Transcat-SQL创建表

~~~sql
CREATE TABLE dbo.Products/*创建一个Products表*/ (ProductlD int PRIMARY KEYNOT NULL/*主键*/,ProductName varchar(25) NOT NULL, Pricemoney NULL,ProductDescription text NULL)Go

~~~



括号里面不同属性之间用 英文逗号 “， ” 隔开

### 修改表结构

**字段名就是列名称**

> 1. 更改**字段类型**长度
>
>    ~~~sql
>    alter table 表名称
>    alter column 字段名 类型长度 -- varchar(10)
>    ~~~
>
> 2. 更改**字段类型**
>
>    ~~~sql
>    alter table 表名称
>    alter column 字段名 更改后的类型
>    ~~~
>
> 3. 添加 not null 约束
>
>    ~~~sql
>    alter table 表名称
>    alter column 字段名 int not null 
>    ~~~
>
> 4. 设置主键
>
>    ~~~sql
>    alter table 表名称
>    ADD constraint 逐渐名 primary key(字段名)   -- 不是修改主键名称 他是唯一的不能修改的
>    ~~~
>
> 5. 更待字段名
>
>    ~~~sql
>    EXEC sp_rename '表名. 字段名'  -- 修改前的字段名
>    '修改后的字段名','COLUMN' -- 修改后的字段名
>    ~~~
>
> 6. 添加字段名
>
>    ~~~sql
>    ALTER TABLE 表
>    ADD 字段名 字段类型 DEFAULT null  
>    				 默认值
>    ~~~
>
> 7. 删除表
>
>    ~~~sql
>    DROP TABLE table_name [,....n]
>    ~~~

### 定义表主键、外键

> 主关键字：一个只有一个，唯一的；
>
> 外键：两个关系之间的相关联系   保持数据的一致性，完整性，主要是控制存储在外键表中的数据

> 1. 设置主键
>
>    ~~~sql
>    alter table 表 add constraint 主键名称 primary key (需要的主键字段)
>    alter table Stu_PkFk_S add constraint PK_S primary key (sno)
>    ~~~
>
> 2. 删除主键
>
>    ~~~sql
>    alter table Stu_PkFk_S drop constraint PK_S
>    ~~~

> 1. 添加 SQL SERVICE外键  从表建立外键
>
>    > 就是另外一张表的主键 关系到本表的外键
>    >
>    > **例如：**A表中的一个字段，是B表的主键，那他就可以是A表的外键。
>
>    ~~~SQL
>    alter table 表名 add constraint 外键 foreign key references 外键的表名(字段名)
>    references 关联的表名(关联的字段名) --注意’关联的表名’和’关联的字段名’
>    ~~~
>
> 2. 删除SQL SERVICE外键
>
>    ~~~sql
>    alter table Stu_PkFk_S drop constraint FK_S 
>    ~~~
>
>    设置外键时 A表中的主键可以是B表的外键建立联系 ，可以有多个外键
>
>    ~~~sql
>     --这是SQL中的注释信息，使用两个减号来注释。
>    drop table sc    --删除表sc
>    create table sc  --创建表sc
>    (sno char(4) foreign key references student(sno),  --加外键约束
>    cno char(4) foreign key references course(cno),  --加外键约束
>    grade int,
>    primary key(sno, cno)  --设置sno和cno的属性组为主键
>    )
>    ~~~
> 
> 



## 3.6数据表的增删改查

> **记录由表中的列和行组成**。**字段**是**列和行**的**交集**：某种类型的**单个值。**

### 增（插入）

> 1. 插入单行数据
>
>    ~~~sql
>    INSERT INTO "表名"("栏位1","栏位2".....)
>    VALUES ("值1","值2".....)
>    -- 简化
>    INSERT INTO "表格名" VALUES("值1","值2".....);
>    ~~~
>
> 2. 插入多行数据
>
>    ~~~SQl
>    INSERT INTO "表格名"("栏位1","栏位2".....)
>    VALUES ("值1","值2".....),("值1","值2".....),("值1","值2".....),("值1","值2".....);
>    -- 一个括号的值对应一个栏位
>    
>    -- 简化
>    INSERT INTO "表格名" VALUES("值1","值2".....),("值1","值2".....),("值1","值2".....),("值1","值2".....);
>    ~~~
>
> 3. 从其他表copy数据
>
>    ~~~sql
>    INSERT INTO "表格名1"("栏位1","栏位2".....)
>    SELECT "栏位3","栏位4",..... -- select 查询语句
>    FROM "表格2"
>    -- 把表格2中的数据copy到表格1的 栏位1 。。上
>    ~~~
>
>    
>
> ~~~sql
> select * from [dbo].[uerinfo]--使用脚本插入记录
> 
> insert into uerinfo(userid ,eamil,name) 
> values ('zhangsan','456413@qq,com','张三');--插入单行的数据
> 
> --插入多行数据
> insert into uerinfo(userid ,eamil,name) 
> values ('lisi','ddsad@qq.com','李四'),('wangba','laoba@qq.com','老八'),('wangba01','laoba01@qq.com','老八一号'),('wangban','laoban@qq.com','老八n号');
> --在values中一个括号就是一行数据就是一个记录
> ~~~
>
> ~~~sql
> -- 从其他的数据文件中copy到指定的位置中 
> insert into uerinfo(userid ,eamil,name) 
> select sno,sage,ssex from [dbo].[student]
> ~~~

### 查

> 使用关键字 SELECT select __list 查询的字段名称 有*是查询所有名称
>
> FROM table_source  从哪一张表查询

> Distinct/Top用法
>
> **distinct 去重** 
>
> ~~~sql
> select distinct select_list
> from table_source
> -- 在table_source 中查询，并且去掉重复的内容
> ~~~
>
> TOP
>
> ~~~sql
> select Top 行数 select_list  -- 在table _source 查询表的前 n 行数据
> from table_source 
> ~~~
>
> ~~~sql
> select *from [dbo].[uerinfo] -- 查询整个数据表
> 
> select userid, eamil from [dbo].[uerinfo] -- 查询指定的列
> 
> select distinct id from  [dbo].[student] -- 去掉id例中重复的值
> 
> select top 10 *from [dbo].[student] -- 只查询前十行数据
> 
> ~~~
>

### 改

> **关键字：** UPDATE   TABLE_NAME   
>
> SET 字段 = 值  设置字段  和   值

~~~sql
select *from [dbo].[uerinfo]
where id = 10  --查询 id = 10 的行

update [dbo].[uerinfo]
set userid = 'laoba01'  -- 对应 字段 = 值  （要修改成为的值）
where id =10  --要限定的修改行的数据 不然全部都会被修改
~~~

### 删除

> **关键字：** DELECE FROM TABLE_list
>
> ~~~sql
> -- 例如：
> select *from [dbo].[uerinfo]  -- from可省略
> 
> delete from [dbo].[uerinfo]
> where id = 2  -- 只删除 id = 2 的行数据 
> ~~~
>





## 3.7条件限制where

> 分类
>
> 1. 精确限制条件
>
>    ~~~sql
>    WHERE 字段 = 值  -- 只能查看限定的内容
>    ~~~
>
> 2. 模糊限制条件
>
>    ~~~sql
>    WHERE 字段 like ‘%值%’  -- % 在值的前面 ，模糊掉前面的内容 只匹配 值 对应内容  ； 若 % 在值的后面则 先匹配 值 把后面的模糊掉  ；再者就是 % 值 % 对值的前后都进行模糊掉
>    ~~~
>
>    ~~~sql
>    -- 例题
>    select *from   [dbo].[uerinfo]
>                                                 
>    delete [dbo].[uerinfo]  -- 精确删除
>    where id = 18
>                                                 
>    delete [dbo].[uerinfo]
>    where userid like '%z%' -- 模糊删除
>                                                 
>    ~~~
>
>    

### BETWEEN 语法

> 限制条件表达式 ，指定表达式范围值
>
> ~~~sql
> [NOT] BETWEEN begin  开始数 and 结束数   -- 起始到结束范围值
> ~~~
>
> ~~~sql
> -- 例题
> where id between 10 and 45 -- 查看 id = 10 ~ 45 之间 的 内容
> where id not between 10 and 45 -- 查看 id = 10 ~ 45 之外 的 内容
> ~~~
>
> ~~~SQL
> select GETDATE() 方法是服务器的当前的时间
> ~~~
>
> 

## 3.8子查询

> **IN表达式**
>
> 用于限制条件表达式，指定表达式范围值
>
> ~~~sql
> [NOT] IN(subquery|expression[,...n])
> ~~~
>
> 结构是指定 所在的行的内容
>
> ~~~sql
> select *from [dbo].[stu]
> where number in (1,4);-- 指定number值为 1 和4 的 行结果
> where number not in (1,4);-- 指定number值为 1 和4 之外的行结果
> ~~~
>
> ~~~sql
> select *from [dbo].[stu]
> where number in (select number from [dbo].[student]) -- 子查询 就是在括号里面的是子类的，查询出对应的number 在和第一行的数据表的number进行查询有共同的number则有结果出来，
> where number not in (select number from [dbo].[student])-- 除了括号里面的 其他都要显示出结果/。
> -- 子查询只是一个条件范围，返回的是主查询的记录
> ~~~
>
> **EXISTS表达式** 
>
>  ~~~sql
>  select a.num, a.age,a.sex from [dbo].[student] a  -- 给表取一个名为a， a表中查询的 是num（学号）、age(年龄)、sex 。 a 就是student 这个表
>  where exists (select ID from [dbo].[student_course]b  -- 在 b（student_course） 表中是否存在 ID 与a 中的 num、age等属性相同 存在则返回true 否则返回false 
>  where a.num = b. num) -- num 代表学号，  
>  EXISTS 指定一个子查询，检测行的存在。 
>  ~~~
>
> ~~~sql
> -- 例题
> select a.number ,a.name,  from [dbo].[stu]  as a -- a 就是代表stu这个表
> where exists (select *from [dbo].[stu_course] b where a.number =b.number);-- 子查询中所有的字段，若a表和b表中的number相同则返回结果
> where not exists (select *from [dbo].[stu_course] b where a.number =b.number); -- 不存在 就是返回false就是返回不存在b表中的值
> ~~~
>
> 

## 3.9排序

### 放回纪律排序

> 关键字：ORDER BY 
>
> ~~~sql
> order_by_experssion [ASC | DESC][..n] 排序的字段要在表中存在才能进行排序，否则不能排序  ASC是升序  DESC是降序  
> ~~~
>
> ~~~sql
> select *from [dbo].[stu]
> order by id asc  -- 升序  asc可省略
> 
> order by number desc   -- 降序
> 
> select *from [dbo].[stu]
> order by id,number -- 多个一起排序 升序
> 
> select *from [dbo].[stu]
> order by id, number desc -- 多个一起排序前个是升序 后面一个是降序  书写字段的优先级进行排序，在前的先优先排序
> 
> -- 也可以对字符串进行排序，就是根据字符串对应的编码 进行排序， 日期等等都可以进行排序
> ~~~

## 3.10关联查询 （多表查询）

> 1. inner join (交叉关联) 只返回两个表中连接字段相等的行 
>
> ~~~sql
> select *from 表1 inner join 表2 on 表1 .字段号 = 表2 .字段号  -- on是两个表中的关联关系控制字段  on 后面是关联条件
> ~~~
>
> 1. left join(左关联) 返回包括**左表中所有的记录** 和**右表中联结字段相等**的记录 （就是在on条件控制相等的字段）
>
>    ~~~sql
>    select *from 表1 left join 表2 on 表1 .字段号 = 表2 .字段号
>    ~~~
>
> 2. right join 返回包括右表中的所有记录和左表中的联结字段相等的记录
>
>    ~~~sql
>    select *from 表1 right join 表2 on 表1 .字段号 = 表2 .字段号
>    ~~~
>
>    ~~~sql
>    -- 例题
>    -- 交叉关联
>    select *from [dbo].[stu]  a
>    inner join [dbo].[stu_course] b  
>    on a.number = b.number -- inner 中返回学号相等的所有（*）字段  
>    -- 左关联
>    select *from [dbo].[stu]  a
>    left join [dbo].[stu_course] b  
>    on a.number = b.number -- left 中返回a 表中所有字段的内容 ，b表中的满足on条件里面的字段的内容，不满足的返回null
>    -- 右关联
>    select *from [dbo].[stu]  a
>    右 join [dbo].[stu_course] b  
>    on a.number = b.number -- left 中返回b 表中所有字段的内容 ，a表中的满足on条件里面的字段的内容，不满足的返回null
>                                              
>    -- 多表关联 
>    -- 右三张表  [dbo].[stu] [course] [stu_course] 分别是学生表 、课程表、 学生选课表
>    select *from [dbo].[stu]  a
>    inner join [dbo].[stu_course] b  
>    on a.number = b.number -- 学号相等返回 
>    inner join [dbo].[course] c
>    on b.coursenum = c.coursenum -- 课程号相同的返回 
>    -- 返回所有的字段
>                                              
>    select  a. name , a.number ,c.name ,c.number from [dbo].[stu]  a
>    inner join [dbo].[stu_course] b  
>    on a.number = b.number -- 学号相等返回 
>    inner join [dbo].[course] c
>    on b.coursenum = c.coursenum -- 课程号相同的返回
>    where a.number = 11
>    -- 返回指定的字段,并且能直看某一给学生(通过where限制条件进行筛选出来)
>    -- 也可以用 left right join 进行关联
>    ~~~
>
>    

## 3.11函数



> 1. 聚合函数
>
> AVG()  : 返回各值的 平均值。忽略null
>
> ~~~sql
> select avg(字段名)
> From 表1
> ~~~
>
> SUM():
>
> ~~~sql
> 返回表达式的所有值的和，忽略null；sum()只能用于数字列
> select Sum(字段名) FROM 表名
> ~~~
>
> ~~~sql
> -- 例题 
> select AVG(score) from [dbo].[stu]; -- 求平均
> select SUM(score) as sum_score from [dbo].[stu]; -- 求和  as 为字段取名字为 ：sum_score
> select name+' - '+number as name_num   from [dbo].[stu]; -- 把两列结合起来并命名为：name_num
> ~~~
>
> MIN() :   返回表达式的最小值  字段类型为：数字型或字符型
>
> ~~~sql
> select MIN(字段名) FROM 表名
> ~~~
>
> MAX：返回表达式的最小值，字符类型为：数字型或字符型
>
> ~~~sql
> select MAX(字段名) FROM 表名
> ~~~
>
> ~~~sql
> -- 例题
> select MIN(score) from [dbo].[stu]; -- 求平均
> select MAX(score) as sum_score from [dbo].[stu]; 
> ~~~



### COUNT()函数

> 返回组中的项数 并且**返回的类型**为**整型** 
>
> ~~~sql
> select COUNT(字段名) FROM 表名
> ~~~
>
> ~~~SQL
> -- 例题
> select count(number) as '共有学号'  from [dbo].[stu]; -- 忽略掉null的不计算进内
> select COUNT_BIG(age)  from [dbo].[stu] ;-- COUNT_BIG 用于大于2^23-1内  COUNT用于2^23-1内
> ~~~

### LEN()函数

> 1. **返回字符串表达式占用的字符数大小**  并不是字符串的长度 
>
> 2. 起哄不包含尾随空格  
>
> 3. 若要返回表达式的字节数，使用DATELENGTH()函数
>
>    ~~~sql
>    select LEN(字段名) FROM 表名
>    ~~~
>
>    ~~~sql
>    -- 例题
>    select LEN(age) from [dbo].[stu];  -- 2 个字符 因为年龄中都是只用两个数字 
>    select datalength(name)as len_name from [dbo].[stu]; -- 4个字节因为datalength是计算字节数
>    ~~~

### 随机数的产成 RAND（）

> 1. 查询分析器中执行：select rand()  
>
> 2. 可以随机生成整数，小数很少。
>
>    ~~~sql
>    select floor(rand()*N) -- 返回小于或等于所给表达式的最大整数  向下取整
>    select ceiling(rand()*N) -- 返回大于等关于所给表达式的最小整数  向上取整
>    ~~~
>
>    > floor（4.45） = 4  ；ceiling（4.45）= 5
>
>    ~~~sql
>    select rand();-- 随机数不大于1
>    select floor(rand()*10); -- 0~9之间的整数
>    select CEILING(rand()*10); -- 1~10之间的整数
>    select floor(8.456); -- 结果是 8 
>    select ceiling(8.456); -- 结果是 9
>    ~~~
>
>    

### 时间函数

> 1. **GETDATE() :** 返回**数据库系统**的时间值 返回类型是datetime()
>
>    ~~~SQL
>    SELECT GETDATE()	
>    ~~~
>
> 2. **GETUTCDATE()**:返回**当前国际标准**时间值，返回类型为datetime
>
> ~~~sql
> select GETUTCDATE()
> ~~~

### 时间转换格式

> 1. **CONVENT()** 函数把日期转换为新的数据类型；
>
> 2. **CONVENT()**可以用不同格式显示日期/时间数据
>
> 3. CONVENT(data_type(length),date_to_be_converted(),style)  三个参数分别是 1.要转换**成**的数据类型(长度)，2.要转换的时间值，3.要转换的时间格式
>
>    | Style ID      | style                                 |
>    | ------------- | ------------------------------------- |
>    | 100或0        | mon dd yyyy hh:miAM(PM)               |
>    | **101**       | **mm/dd/yy**                          |
>    | 102           | yy.mm.dd                              |
>    | **103**       | **dd/mm/yy**                          |
>    | **104**       | **dd.mm.yy**                          |
>    | **105**       | **dd-mm-yy**                          |
>    | **106**       | **dd mon yy**                         |
>    | 107           | Mon dd,yy                             |
>    | 108           | hh:mm:ss                              |
>    | 109或者9      | mon dd yyyy  hh:mi：ss: mmmAM（PM）   |
>    | **110**       | **mm-dd-yy**                          |
>    | **111**       | **yy/mm/dd**                          |
>    | 112           | yymmdd                                |
>    | 113或者13     | dd mon yyyy hh:mm:ss.mmm(24h)         |
>    | 114           | hh:mi:ss:mmm(24h)                     |
>    | **120或者20** | **yyyy-mm-dd hh:mi:ss.mmm(24h)**      |
>    | **121或者21** | **yyyy-mm-dd hh:mm:ss.mmm**           |
>    | 126           | yyyy-mm-ddThh:mm:ss.mmm(没有小数空格) |
>    | 130           | dd mon yyyy hh:mi:ss.mmmAM（PM）      |
>    | 131           | dd/mm/yy hh:mi:ss.mmmAM（PM）         |
>
>    ~~~sql
>    -- 时间格式
>    select GETDATE();--格式是 2022-01-14 16:27:59.137
>    --只取年月日
>    select CONVERT(varchar(10),GETDATE(),110) as '月 日 年'; -- 01-14-2022 月 日 年
>    select CONVERT(varchar(23),GETDATE(),109) as '月日年时分秒'; -- 01 14 2022  4:31:24:417  月 日 年 时 分 秒
>    ~~~
>
>    

### 时间计算

> **DATEDIFF()  :放**回两个日期之间的天数
>
> ~~~sql
> DATEDIFF(datepart, startdate ,enddate) 
> -- startdate\enddate是合法的日期表达式  开始和结束时间
> -- datepart 计算日期的哪一部分 比如 ：单独计算 年 或者 月
> ~~~
>
> **DATEADD()函数**在日期中**添加或减去**指定**的时间间隔**
>
> ~~~sql
> DATEADD(datepart, number ,date) 
> -- datepart增加或减去日期的部分
> -- number 为增加或减去数 可以是负数  
> -- date 指定的日期
> ~~~
>
> ~~~sql
> 
> --计算天数
> select DATEDIFF(DAY,'2022-1-12','2021-12-23'); --这两个时间的天数之差 后面的减去前面的时间 end - start 
> select DATEDIFF(DAY,'2021-12-23','2022-1-12');  
> 
> --计算月份
> select DATEDIFF(MONTH,'2021-12-23 16:27:59.137','2022-01-14 16:27:59.137');   --只计算月份，不计算年 日  时间
> 
> select DATEDIFF(MINUTE,'2021-12-23 16:27:59.137','2022-01-14 16:27:59.137'); --只计算分钟，不计算年 月 日 小时 秒
> -- 增加年月日时分秒
> select DATEADD(YEAR,10,'2022-01-14 16:27:59.137') -- 加10年
> select CONVERT(varchar(10), DATEADD(YEAR,10,'2022-01-14 16:27:59.137'),110); -- 加10年
> 
> select DATEADD(MONTH,-10,'2022-01-14 16:27:59.137') -- 减10个月
> 
> select DATEADD(DAY,10,'2022-01-14 16:27:59.137') -- 加10day
> 
> select DATEADD(HOUR,-10,'2022-01-14 16:27:59.137') -- 减10小时
> 
> select DATEADD(MiNUTE,10,'2022-01-14 16:27:59.137') -- 加10分
> 
> ~~~

### 日期的某一部份的获取或计算

> DATEPART():用于返回日期/时间的单独部分，比如年 月 日 小时 分钟，秒  返回类似是INT类型
>
> DATENAME();这个也是用于返回日期的单独部分 返回类是VARCHAR型
>
> day() month() year()
>
> ~~~sql
> select DATEPART(YEAR, GETDATE()) as '年'; -- 只要年
> 
> select DATEPART(Day, GETDATE()) as 'day'; -- 只日
> 
> select DATENAME(YEAR,GETDATE());-- 返回类型是varcahr类型
> 
> select YEAR(GETDATE());--年 
> 
> select MONTH(GETDATE());-- 月
> 
> select DAY(GETDATE());-- 日
> 
> ~~~
>
> 

### 字符串函数

> **CAHRINDEX()**
>
> 1. CAHRINDEX(experssion1 ，expression2[,start_location])  expression1是到expression2中寻找的字符，start_location是expr2 在expre1中的位置。
>
> start不写也可以,默认从0开始,返回一个index索引值，没有找到则返回 0  
>
> **PATINDEX()**
>
> 返回字符或者字符串在**另一个字符串**或者表达式中的**起始位置**，PATINDEX函数**支持搜索字符串中使用通配符**，这使PATINDEX函数对于变化的搜索字符串很有价值
> 和 CHARINDEX函数一样，PATINDEX函数返回搜索字符串在被搜索字符串中的起始位置。假如有这样一个PATINDEX函数:
> PATINDEX(%BC%,'ABCD')
> 这个PATINDEX函数返回的结果是2，这和 CHARINDEX函数一样。这里的%标记告诉PATINDEX函数去找字符串“BC"，不管被搜字符前后的是什么。
>
> ~~~SQL
> select CHARINDEX('s','dasdsadsadsadsas',4); -- 在后面的字符串中找出第一次出现s的索引值，找不到返回0  后面是4 表示从第四个字符开始查找
> 
> select PATINDEX('%s%','sdasas'); -- 不加通配符是不能查找到的，必须要有通配符  
> -- 如果通配符只有单边的只能匹配字符串中第一个或者最后一个是不是改字符，是就返回索引值，不是则返回0
> -- 单边的通配符是表示以什么字符(开头/结尾)
> ~~~
>
> **STUFF函数：**用于删除指定长度的字符，并可以在制定的起点出插入另一组字符，返回类型是字符串类型
>
> ~~~sql
> stuff(列名，开始位置，长度，替代字符串)
> ~~~
>
> ~~~sql
> select STUFF('aabbccdd',5,2,'截取'); -- aabb截取dd   在第五个位置开始截取，截取两位，并且用“截取”代替
> select *,STUFF(name,1,2,'wsnimm') as 'newname'from [dbo].[stu];
> where number = 1
> ~~~
>
> **SUBSTRING()** :用于截取指定长度的字符串
>
> ~~~sql
> substring('字符串',开始位置，长度);
> -- 例题
> select substring('sadsds',1,3); -- sad 下标从1开始 返回截取的内容
> 
> select *,SUBSTRING(cmath,2,2)as new from [dbo].[course1]
> where con = 1002;
> ~~~
>
> **LEFT() 、RIGHT()**
>
> ~~~SQL
> LEFT() -- 返回字符串中从左边开始指定个数的字符。
> LEFT ( 字符串 , 长度 ) -- 后面的参数不能为负数 
> RIGHT()-- 返回字符串中从 右边 开始指定个数的字符。
> RIGHT( 字符串 , 长度 )
> 
> select left ('sadsds',3); -- sad   长度不能为负数
> select right ('sadmlkdls',4); -- sds 顺序还是从左到右，但是只要右边的四个字符
> 
> select *,LEFT(cmath,2)as new from [dbo].[course1]
> 
> select *,right(cend,2)as new from [dbo].[course1]
> ~~~
>
> **LTRIM() ,RTTIM() 去除首尾的空格**
>
> ~~~sql
> LTRIM()-- 删除起始空格后返回字符表达式。
> LTRIM( 字符串 )
> RTTIM()-- 截断所有尾随空格后返回一个字符串。
> RTTIM( 字符串 )
> --字符去除空格
> 
> select LTRIM('  s d a  '); --去除左边的空格s d a  
> select RTRIM('  s d a  '); --去除右边的空格   s d a
> 
> select *,LTRIM(cend)as new from [dbo].[course1]
> 
> select *,RTRIM(cend)as new from [dbo].[course1]
> ~~~
>
> **UPPER() LOWER()：大小写转换**
>
> ~~~sql
> UPPER()-- 返回小写字符数据转换为大写的字符表达式。
> UPPER (字符串)
> LOWER()-- 返回大写字符数据转换为小写的字符表达式。
> LOWER(字符串)
> select UPPER('dsad') -- DSAD
> select LOWER('DSAD') -- dsad
> 
> select *,UPPER(cend)as new from [dbo].[course1]
> select *,LOWER(cend)as new from [dbo].[course1]
> ~~~
>
> **REPLACE()替换字符串**
>
> ~~~sql
> 用另一个字符串值替换出现的所有指定字符患值。
> REPLACE ( 源字符串, 源字符串中要被替换的字符串, 要替换的字符串 )
> select replace('abdsad','ds','kl'); -- abklad 全部替换的
> select *，replace(name,'张三','王八是你') from  [dbo].[student] 要替换的长度不需要相等
> ~~~
>
> **REPLICATE()  SPACE()**
>
> ~~~SQL
> REPLICATE以指定的次数重复字符表达式。
> REPLICATE ( 字符串 ,重复次数（int） )
> SPACE返回指定个数的空格表达示
> SPACE( 个数（int） )  -- 返回空格数
> 
> select REPLICATE('SS',4) -- SSSSSSSS重复4次
> select 's'+SPACE(4)+'s'; -- s    s
> 
> select *,REPLICATE(cend)as new from [dbo].[course1]
> select name +space(1)+number from [dbo].[course1] -- 把两个连接起来显示
> ~~~
>
> **REVERSE()：倒置**
>
> ~~~sql
> select reverse('dsadlm') -- mldasd 
> select *,reverse(cend)as new from [dbo].[course1]
> ~~~
>
> **CAST()数据类型转换** ：
>
> ~~~sql
> CAST函数用于将某种数据类型的表达式显式转换为另一种数据类型
> CAST( string_expression as data_type) 
> select cast(123 as varchar); -- 123(varchar(10))
> 
> select cast('你' as varchar(10)); -- 你 (varchar(10))
> 
> select 'da'+CAST(1 as varchar(10)); -- da1
> 
> select CAST(2.5 as int);  -- 2
> 
> select CAST('2012-12-02' as datetime); -- 2012-12-02 00:00:00.000
> 
> select  cast(age as decimal(5,1)) from [dbo].[stu]  -- 显示小数的位数 1位
> ~~~
>
> **CASE()函数**  : 条件判断转换 ，把**满足条件的表达示转换为对应的结果** 
>
> **简单case（）**  有一定的限制
>
> ~~~sql
> case 字段 WHEN '条件' THEN '值'  WHEN '条件' THEN '值'  ELSE '值' END 
> -- fe
> case 字段 WHEN '1' THEN '男'  WHEN '2' THEN '女'  ELSE '其他' END 
> 
> -- 简单case函数
> select *,case sex when '男' then 'man'
> when '女' then 'woman'
> end
> as 'engsex'
> from [dbo].[stu] 
> ~~~
>
> **CASE（） 搜索函数**
>
> ~~~sql
> case  WHEN 字段 = '条件' THEN '值'  WHEN 字段 =  '条件' THEN '值'  ELSE '值' END 
> -- 例如
> select  *,
> case when age>10 and age<15  then '小孩子' 
> -- in(10,11,12,13,14,15)   then '小孩子' 
> when age>30 and age<35  then '中年人'
> when  age>60  then '老人' 
> else  '非人类 '  end 
> from [dbo].[stu]
> ~~~
>
> 

# 4.视图

## 4.1概念

> 1. 视图是一张**虚拟表**，并**不**在数据库中**以存储数据值集的形式存在**。在引用过程中依据**基表动态**生成。

## 4.2视图的优缺点

> 1. **安全：**有的数据是需要保密的，如果直接把表给出来进行操作会造成泄密，那么可以通过创建视图把相应视图的权限给出来即可保证数据的安全。
> 2. **高效：**复杂的连接查询，每次执行时效率比较低，可以考虑新建视图，每次从视图中获取，将会提高效率。
> 3. **定制数据：**将常用的字段放置在视图中。

## 4.3使用视图

> 1. 创建视图
>
>    ~~~sql
>    #查看10号部门所有的员工信息
>    create view v_emp as select * from emp where deptno=10;
>     -- 创建一个名为 v_emp 的视图 
>    ~~~
>
> 2. 查询视图
>
>    ~~~sql
>    select * from v_emp;
>    ~~~
>
>    
>
> 3. 修改视图
>
>    ~~~sql
>    # 将基表的ename字段修改了
>    update v_emp set ename='kitty' where empno=7839;
>    # 将视图包含的deptno均修改为20，在基表中修改
>    update v_emp set deptno=20;
>    # 结果集为空，基表中不存在10号部门了
>    select * from v_emp;
>    # with check option保证视图查询条件不被修改，但其他字段可以修改
>    create view v_emp as select * from emp where deptno=10 with check option;
>    ~~~
>
>    
>
> 4. 删除视图
>
>    ~~~sql
>    #删除视图（DDL操作）
>    drop view v_emp;
>    ~~~
>
>    

## 4.3 要注意的问题

- 通过视图可以修改基表数据，但视图一般只做查询。

- with check option关键词词用于保证视图的查询条件不被修改，但其他字段可以修改。

# 5.索引

## 5.1什么是索引

> 索引是供服务器快速在表中查询一行数据的数据结构，可以比作书籍的目录。mysql中的索引的默认数据结构是B-Tree。

## 5.2使用索引好处

### 5.2.1性能指标

> 性能从高到低依次是：
>
> system>const>eq_ref>ref>fulltext>ref_or_null>index_merge>unique_subquery>index_subquery>range>index>ALL，其中all表示全表扫描。一般来说，查询至少达到range级别，最好能达到ref级别。否则，sql的查询性能会很慢。

### 5.2.2 查询语句性能比较

关键词explain：查看sql执行性能

~~~sql
#解释计划任务
#explain：查看sql执行性能
#性能级别：const，查询1row
explain select * from emp where empno=7788;
#性能级别：all（全表扫描），查询14row
explain select * from emp where ename='scott';
-- 第1条语句的条件字段是主键，主键自动创建索引，根据记录地址查找；而第2条语句的条件是普通字段，做的是全表扫描。
~~~

## 5.3使用索引

1. 普通索引

   ~~~sql
   create index index_name on tname(fie1...);
   #创建普通单列索引，多个列用逗号隔开
   create index index_name on emp(ename);
   #性能级别：ref，查询1row
   explain select * from emp where ename='scott';
   #删除索引
   drop index index_name on emp;
   ~~~

2. 唯一索引

   ~~~sql
   #创建唯一索引，唯一约束也会添加唯一索引
   create unique index index_name on tname(fie);
   ~~~

## 5.4使用场景

> 表数据量足够大；
>
> 增删改较少的表；
>
> 高基数列。什么意思？该列的数据大多数都不一样。

### 5.5注意

> - 索引需要单独开辟空间进行维护，对数据进行增删改，都需要维护索引。所以索引不易添加过多；
> - 将条件列设置索引（经常作为条件的列）；
> - 索引失效的状况：比如or关键字会导致索引失效。

# 6.关键字

## 6.1SQL语句

|        类型        |         含义         |
| :----------------: | :------------------: |
|    create table    |      创建一张表      |
| insert into…values |    想表中插入数据    |
|    delete from     |    删除表中的信息    |
| update …set …where | 在where位置更新数据  |
|     drop table     |        删除表        |
|  alter table …add  |  向表中添加某个属性  |
|  alter table…drop  | 将表中的某个属性删除 |

## 6.2特殊关键字

|          类型          |                    含义                    |                示例                 |
| :--------------------: | :----------------------------------------: | :---------------------------------: |
|        primary         |      主键，后面括号中是作为主键的属性      |          primary  key (ID)          |
| foregin key references | 外键，括号中为外键，references后为外键的表 | foregin key(stu_id) references(stu) |
|        not null        |          不为空，前面为属性的定义          |     name varchar(10 ) not  null     |

## 6.3单关系查询

| 类型     | 含义                                      |
| -------- | ----------------------------------------- |
| select   | 查找出的表所含有的属性                    |
| from     | 要操作代表                                |
| where    | 判断条件，根据判断条件选择信息            |
| distinct | 在select中加入distinct 得到的结果**去重** |
| all      | 在select中加入all得到的结果是**不去重**   |
| and      | 在where中使用and将判断条件**连接起来**    |
| or       | 在where中使用or表示判断条件**多选一**     |
| not      | 在where中使用not表示判断条件**取反**      |

## 6.4多关系查询

| 类型              | 含义                                                       |
| ----------------- | ---------------------------------------------------------- |
| A，B              | 在from后面通过逗号连接多张表，表示将这些表进行笛卡儿积运算 |
| natural join      | 将natural join关键字**前后的两张表进行自然连接运算**       |
| A join B using(c) | 将A和B通过c属性**自然连接**                                |

## 6.5附加运算查询

| 类型                    | 含义                                                         |
| ----------------------- | ------------------------------------------------------------ |
| as                      | 将as**前的关系**起一个**别名**，在此语句中，可以用**别名来代指这个表** |
| *                       | 在select中通过: “**表名.***” 来表示查找出这个表中**所有的属性** |
| order by                | 让查询结果中的信息按照给定的**属性排序**（默认升序，上小下大） |
| desc                    | 在order by之后的属性后使用，表示采用**降序**排序             |
| asc                     | 在order by之后的属性后使用，表示采用**升序**排序（默认）     |
| between                 | 在where中使用between表示一个数在**两个数值之间取值**         |
| not between             | between的反义词，在两个数**之外**取值                        |
| union/union all         | 将两个SQL语句**做并**运算，并且自动去重，添加all表示不去重   |
| intersect/intersect all | 将两个SQL语句**做交**运算，并且自动去重，添加all表示不去重   |
| except/except all       | 将两个SQL语句**做差**运算，并且自动去重，添加all表示不去重   |
| is null                 | 在where中使用is null表示这个值是空值                         |
| is not null             | 在where中使用is not null表示这个值不是空值                   |

## 6.6聚集函数运算查询

|   类型   |                      含义                      |
| :------: | :--------------------------------------------: |
|   avg    |                     平均值                     |
|   min    |                     最小值                     |
|   max    |                     最大值                     |
|   sum    |                      总和                      |
|  count   |                      计数                      |
| distinct |           表示将distinct后的属性去重           |
| group by |    将在group by上取值相同的信息分在一个组里    |
|  having  | 对group by产生的分组进行筛选，可以使用聚集函数 |

# 7.存储过程与触发器

## 7.1存储过程

### 7.1.1概念

> 存储过程是独立于数据库之外的数据库对象，是SQL service 服务器上一组预编译的Transact-SQL语句，用于完成某任务，它可以接收参数，输出参数，返回单个或多个结果、返回状态值和参数值，存储过程独立于程序源代码，可单独修改。

#### 创建存储过程

~~~~sql
CREATE PROCEDURE 存储过程名
	[@变量名 数据类型] 
   [ = 默认值 ]
   [WITH ENCRYPTION|RECOMPILE] 	
   [FOR REPLICATION]	
as
	<sql语句>
~~~~

- WITH ENCRYPTION：存储过程加密，任何人都无法查看存储过程定义。WITH RECOMPILE:该过程在运行时编译
- FOR REPLICATION：指定不能再订阅服务器上执行为复制创建的存储过程。
- SQL语句：存储过程要执行的操作，但不能使用CREATE DEFAULT / CREATE TRIGGER / CREATE PROCEDURE / CREATE VIEW / CREATE RULE
- []  可省略

~~~sql
 # 示例
 use Student  /*指定数据库,创建的存储过程会保存在数据库文件中*/  -- ues 的student是一个数据库
CREATE PROCEDURE cjjicx
	@name varchar(50)
	WITH ENCRYPTION    --加密
as
	select sno from S where sname=@name
go  /*go作为批处理结束标志*/

~~~

#### 执行存储过程

~~~sql
EXEC | EXECUTE
    [@返回状态= ] [schema_name.] 存储过程名
    [@形参 = ] [value]
    WITH RECOMPILE]
~~~

~~~sql
# 示例
use Student
exec cjjicx @name = 'xiaoming'
go /*批量处理结束标志*/
~~~

#### 修改存储过程

~~~sql
ALTER PROCEDURE 存储过程名
   [@变量名 数据类型] 
   [ = 默认值 ]
   [WITH ENCRYPTION] 	
   [FOR REPLICATION]	
as
	<sql语句>

~~~

删除存储过程

~~~sql
DROP PROCEDURE 存储过程名
~~~

#### 查看存储过程定义

- 显示存储过程的**参数及数据类型**：sp_help 存储过程名
- 显示存储过程**源代码**：sp_helptext 存储过程名
- 显示与存储过程相关的**数据库对象**：sp_depends ’ 存储过程名 ’
- 显示当前数据库中存储**过程列表**：sp_stored_prodedure ’ 存储过程名 ’

~~~sql
use Student 
sp_helptext cjjicx
~~~

#### 重命名存储过程

~~~sql
SP_RENAME 原存储过程名，新存储过程名
~~~

示例

~~~sql
use Student
SP_RENAME cjjicx,cjjicx2 --将存储过程cjjicx更名为cjjicx2
go
~~~

## 7.2触发器

### 7.2.1概念

> 触发器是特殊的存储过程，它也定义了一组SQL语句，用于完成某项任务。存储过程的执行是通过过程名字直接调用，而触发器是**通过事件（如insert，update）进行触发而被执行**。

### 创建触发器

~~~sql
CREATE TRIGGER 触发器名 ON 表名
       [WITH ENCRYPTION] -- 文本加密
       {FOR | AFTER | INSTESD OF}
       		[delete][,insert][update]
as
[sql语句]
~~~

- 触发器名不能以 # 或 ## 开头
- 视图只能被INSTEAD OF触发器引用
- AFTER：指定触发器只有在SQL所有操作以及所有引用级联操作和约束条件成功完成过后才触发。
- FOR：与AFTER等价。不能在视图上定义AFTER触发器。
- SQL语句：多于一个语句时用begin和end包括

~~~sql
/*该触发器的作用是：当用户向SC表中插入记录时，如果插入了在S表中没有的学生学号sno，
则提示用户不能插入记录，否则提示记录插入成功。
*/
use Student
CREATE TRIGGER insert_xh on SC
	AFTER INSERT
as
begin
	if(exists(select * from inserted join S on inserted.sno=S.sno))
	begin
		rollback tran   /*取消insert操作*/
		select '不能插入记录'
	end
	if(not exists(select * from inserted join S on inserted.sno=S.sno))
	begin
		select '插入记录成功'
	end
end
go	

~~~

### 修改触发器

~~~sql
ALTER TRIGGER  触发器名  ON 表名|视图
	[WITH ENCRYPTION]
	{FOR | AFTER | INSTESD OF} 
        [delete][,insert][,update]
as
	[SQL语句]
~~~

### 删除触发器

~~~sql
DROP TRIGGER 触发器名
~~~

### 重命名触发器

~~~sql
SP_RENAME  原触发器名 , 新触发器名
~~~



# 8.数据库的安全管理















