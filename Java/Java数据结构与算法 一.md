> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：**猫十二懿**

Java数据结构与算法的整体框架：

![image-20220904224759881](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220904224759881.png)



算法 先简单 ==》做复杂，把复杂算法拆分成简单的问题 ==》解决问题

# 经典算法



## 1 字符串匹配  

> str1 = "nihdisoadisaoidhi"  str2="aoi"

str1 是否包含有 str2 

- 暴力破解
- KMP算法

## 2 汉诺塔游戏

> 将A塔的所有圆盘移动到C塔。并且规定小盘上不能有大盘，三根柱子之间一次只能移动一个圆盘

- 分治算法

## 3 八皇后问题（92种）

> 在一个8 × 8 的国际象棋摆放 8个皇后，使其不能互相攻击
>
> 任意两个皇后都不能处于同一列、同一行或者同一斜线上，问有多少种摆法

- 回溯算法

## 4 马踏棋盘算法（骑士周游）

> 马放在 8 × 8 的国际象棋的棋盘中，board[0~7] [0~7] 某一个格中，马走日，要求每个格子只进入一次，走完64个格子 

- 使用图的深度优化遍历算法 (DFS) + 贪心算法优化



# 数据结构与算法简介

- 算法是程序的灵魂
- 程序使用内存计算框架（Spark）和缓存技术（Redis）优化程序

## 数据结构与算法的关系

- 数据结构（Data Structure）：研究组织数据方式的学科
- 程序  = 算法 + 数据结构
- 结合实际生活问题

 

## 实际编程遇到的问题

- 约瑟夫问题（丢手帕问题）：单向环形链表【数据结构】
- 修路问题：最小生成树（普利姆算法）
- 最短路径问题：弗洛伊德算法
- 汉诺塔：分治算法
- 八皇后问题：回溯算法



## 数据结构

数据结构：线性结构和非线性结构

### 线性结构

1. 元素之间存在**一对一**的线性关系
2. 存储结构
   1. 顺序存储结构：顺序存储的线性表为顺序表，**存储元素是连续的**
   2. 链式存储结构：链式存储的线性表为链表，**链表中元素不一定连续**，元素节点中存放数据元素以及**相邻元素的地址信息**
3. 常见的线性结构：数据、队列、链表、栈

### 非线性结构

- 非线性结构：二维数组、多维数组、广义表、树结构、图结构

# 稀疏数组和队列



## 稀疏数组

当一个数组中大部分元素为 0 ，或者为同一个值的数组时，可以使用稀疏数组来保存该数组

处理方法：

1. 记录数组一共有几行几列，有多少个不同的值
2.  把具有不同值的元素的行列及值记录在一个小规模的数组中，从而缩小程序的规模

原始二维数组 ==》稀疏数组

![image-20220805195210067](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220805195210067.png)   ===》<img src="Java数据结构与算法 一.assets/image-20220805195243076.png" alt="image-20220805195243076" style="zoom:80%;" />

### 应用实例

1. 使用稀疏数组，来保留类似前面的二维数组
2. 把稀疏数组存盘，并且可以重新恢复到原来的二维数组



二维数组==>稀疏数组：

1. 遍历原始的二维数组，得到有效数据的个数 sum
2. 根据sum 就可以创建 稀疏数组 sparseArr  int[sum + 1] [3]
3. 将二维数组的有效数据数据存入到 稀疏数组

稀疏数组==>原始的二维数组：

1. 先读取稀疏数组的第一行，根据第一行的数据，创建原始的二维数组，比如上面的 chessArr2 = int [ 11 ] [ 11 ]
2. 在读取稀疏数组后几行的数据，并赋给 原始的二维数组 即可

![image-20220805200850843](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220805200850843.png)

```java
package com.sparse;

/**
 * @author Kcs 2022/8/5
 */
public class SparseArray {
    public static void main(String[] args) {
        //创建一个原始的数组 11 * 11
        // 0 ：无棋子 ，1：黑子 ，2：白子
        int chessArr[][] = new int[11][11];
        //黑子位置
        chessArr[1][2] = 1;
        // 白子位置
        chessArr[2][3] = 2;
        chessArr[6][5] = 2;
        // 遍历原始数组
        System.out.println("原始的二维数组：");
        for (int[] row : chessArr) {
            //每一个元素数据
            for (int data : row) {
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

        // 将二维数组 转 稀疏数组
        // 统计非零的个数
        int sum = 0;
        for (int i = 0; i < 11; i++) {
            for (int j = 0; j < 11; j++) {
                if (chessArr[i][j] != 0) {
                    sum++;
                }
            }
        }

        //2创建对应的稀疏数组
        int sparseArr[][] = new int[sum + 1][3];
        // 稀疏数组赋值
        sparseArr[0][0] = 11;
        sparseArr[0][1] = 11;
        sparseArr[0][2] = sum;

        // 遍历二维数组，将非零的值存放到sparseArr中
        //用于记录非零的元素个数
        int count = 0;
        for (int i = 0; i < 11; i++) {
            for (int j = 0; j < 11; j++) {
                if (chessArr[i][j] != 0) {
                    count++;
                    //列位置
                    sparseArr[count][0] =i;
                    //行位置
                    sparseArr[count][1] =j;
                    sparseArr[count][2] =chessArr[i][j];
                }
            }
        }
        //输出稀疏数组的格式
        System.out.println();
        System.out.println("稀疏数组：");
        System.out.printf("%s\t%s\t%s\n","列","行","值");
        for (int i = 0; i < sparseArr.length; i++) {
            System.out.printf("%d\t%d\t%d\n",sparseArr[i][0],sparseArr[i][1],sparseArr[i][2]);
        }

        //稀疏数组 转 原始数组
        //1.先读取稀疏数组的第一行，根据第一行的数据，创建原始的二维数组
        int chessArr2[][] = new int[sparseArr[0][0]][sparseArr[0][1]];

        //遍历稀疏数组，从第二行开始,并且重新赋值给原始数组
        for (int i = 1; i < sparseArr.length; i++) {
            chessArr2[sparseArr[i][0]][sparseArr[i][1]] = sparseArr[i][2];
        }
        //输出原始数组
        System.out.println();
        System.out.println("稀疏数组转原始二维数组：");
        for (int[] row : chessArr2) {
            //每一个元素数据
            for (int data : row) {
                System.out.printf("%d\t", data);
            }
            System.out.println();
        }

    }
}
```



## 队列

- ==有序列表==，用数组或链表来实现
- ==先进先出== ：存入队列的数据，要先取出

![image-20220807200406341](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220807200406341.png)

- front 随着数据**出队**而改变
- rear 随着数据**入队**而改变

### 队列操作

1. 队空条件：front == rear == null，rear + 1
2. 队满条件：rear = maxSize - 1，则继续入队，否则队满：rear = maxSize - 1

```java
import java.util.Scanner;

/**
 * @author Kcs 2022/8/7
 */
public class ArrayQueueDemo1 {
    public static void main(String[] args) {
        //创建一个队列对象
        ArrayQueue queue = new ArrayQueue(3);
        //接收用户输入
        char key = ' ';
        Scanner scanner = new Scanner(System.in);
        boolean loop = true;
        //输入一个菜单
        while (loop) {
            System.out.println("s(show):显示队列");
            System.out.println("e(exit):退出程序");
            System.out.println("a(add):向队列添加数据");
            System.out.println("g(get):获取队列数据");
            System.out.println("h(head):查看用户头的数据");
            //接收一个字符
            key = scanner.next().charAt(0);

            switch (key) {

                case 's':
                    queue.showQueue();
                    break;

                case 'a':
                    System.out.println("输入数字：");
                    int value = scanner.nextInt();
                    queue.addQueue(value);
                    break;

                case 'g':
                    try {
                        int res = queue.getQueue();
                        System.out.println("取出的数据是：" + res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                //查看队列头数据
                case 'h':

                    try {
                        int res = queue.headQueue();
                        System.out.println("队列头的数据：" + res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                //程序退出
                case 'e':
                    scanner.close();
                    loop = false;
                    break;

                default:
                    break;
            }
        }
        System.out.println("程序退出");
    }
}
//使用数据模拟队列编写一个ArrayQueue类

class ArrayQueue {

    /**
     * 表示数组的最大容量
     */
    private int maxSize;
    /**
     * 队列头
     */
    private int front;
    /**
     * 队列尾
     */
    private int rear;
    /**
     * 存放数据数组
     */
    private int[] array;

    /**
     * 构造器
     */
    public ArrayQueue(int arrMaxSize) {
        maxSize = arrMaxSize;
        array = new int[maxSize];
        //指向队列头部，队列头的前一个位置
        front = -1;
        //指向队列尾部，队列尾的数据（队列的最后一个数据）
        rear = -1;
    }

    /**
     * 判断队列是否满
     */
    public boolean isFull() {
        return rear == maxSize - 1;
    }

    /**
     * 判断队列是否为空
     */
    public boolean isEmpty() {
        return rear == front;
    }

    /**
     * 入队操作
     */
    public void addQueue(int n) {
        //判断是否队满
        if (isFull()) {
            System.out.println("队满，不可以添加数据");
            return;
        }
        // rear后移
        rear++;
        array[rear] = n;
    }

    /**
     * 出队操作
     */
    public int getQueue() {
        //判断是否为空
        if (isEmpty()) {
            throw new RuntimeException("队列为空，没有数据可取");
        }
        // front后移
        front++;
        return array[front];
    }

    /**
     * 显示队列数据
     */
    public void showQueue() {
        // 遍历队列
        if (isEmpty()) {
            System.out.println("队列为空，没有数据！！");
            return;
        }
        for (int i = 0; i < array.length; i++) {
            System.out.printf("array[%d] = %d\n", i, array[i]);
        }

    }

    /**
     * 显示队列头部数据,不是取数据
     */
    public int headQueue() {
        if (isEmpty()) {
            throw new RuntimeException("队列为空，没有数据~~");
        }
        return array[front + 1];
    }

}
```

此时把内容取出完，但也不能添加入数据，还在占用空间



### 环形队列

分析

1. front 变量的含义做一个调整：front 指向队列的第一个元素，array[front] ，front 的初始值 = 0
2. rear 变量的含义做一个调整：rear 指向队列的最后一个元素的后一个位置，空出一个空间作为约定，rear 初始值 = 0
3. 队列==满==条件：(rear + 1) % maxSize = front 
4. 队列为==空==的条件：rear =  front 
5. 队列中有效数据的个数：( rear +maxSize - front ) % maxSize // rear =1 , front = 0

```java
import java.util.Scanner;

/**
 * @author Kcs 2022/8/7
 */
public class CircleArrayQueueDemo {
    public static void main(String[] args) {
        //创建一个环形队列对象
        // 队列有效数据最多只有3个
        CircleQueue queue = new CircleQueue(4);
        //接收用户输入
        char key = ' ';
        Scanner scanner = new Scanner(System.in);
        boolean loop = true;
        //输入一个菜单
        while (loop) {
            System.out.println("s(show):显示队列");
            System.out.println("e(exit):退出程序");
            System.out.println("a(add):向队列添加数据");
            System.out.println("g(get):获取队列数据");
            System.out.println("h(head):查看用户头的数据");
            //接收一个字符
            key = scanner.next().charAt(0);
            switch (key) {
                case 's':
                    queue.showQueue();
                    break;

                case 'a':
                    System.out.println("输入数字：");
                    int value = scanner.nextInt();
                    queue.addQueue(value);
                    break;

                case 'g':
                    try {
                        int res = queue.getQueue();
                        System.out.println("取出的数据是：" + res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;

                //查看队列头数据
                case 'h':

                    try {
                        int res = queue.headQueue();
                        System.out.println("队列头的数据：" + res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                //程序退出
                case 'e':
                    scanner.close();
                    loop = false;
                    break;

                default:
                    break;
            }
        }
        System.out.println("程序退出");
    }
}
//使用数据模拟队列编写一个ArrayQueue类

class CircleQueue {

    /**
     * 表示数组的最大容量
     */
    private int maxSize;
    /**
     * front 指向队列的第一个元素，array[front] ，front 的初始值 = 0
     */
    private int front;
    /**
     * 1. rear 指向队列的最后一个元素的后一个位置，空出一个空间作为约定，rear 初始值 = 0
     */
    private int rear;
    /**
     * 存放数据数组
     */
    private int[] array;

    /**
     * 构造器
     */
    public CircleQueue(int arrMaxSize) {
        maxSize = arrMaxSize;
        array = new int[maxSize];
    }

    /**
     * 判断队列是否满 (rear + 1) % maxSize == front
     */
    public boolean isFull() {
        return (rear + 1) % maxSize == front;
    }

    /**
     * 判断队列是否为空 rear =  front
     */
    public boolean isEmpty() {
        return rear == front;
    }

    /**
     * 入队操作,添加数据
     */
    public void addQueue(int n) {
        //判断是否队满
        if (isFull()) {
            System.out.println("队满，不可以添加数据");
            return;
        }
        // 直接将数据加入
        array[rear] = n;
        //将rear后移，取模，判断队满,防止地址溢出
        rear = (rear + 1) % maxSize;
    }

    /**
     * 出队操作，取数据
     */
    public int getQueue() {
        //判断是否为空
        if (isEmpty()) {
            throw new RuntimeException("队列为空，没有数据可取");
        }
        // front直接指向队列的第一个元素
        //1. front 对应的值保存到临时变量
        int value = array[front];
        //2. front 后移,取模，防止地址溢出
        front = (front + 1) % maxSize;
        //3.将临时保存的变量返回
        return value;
    }

    /**
     * 显示队列数据
     */
    public void showQueue() {
        // 遍历队列
        if (isEmpty()) {
            System.out.println("队列为空，没有数据！！");
            return;
        }
        //从front开始遍历，有效个数:( rear +maxSize - front ) % maxSize
        for (int i = front; i < front + effectiveValue(); i++) {
            System.out.printf("array[%d] = %d\n", i % maxSize, array[i % maxSize]);
        }

    }

    /**
     * 求出当前队列有效数据的个数
     */
    public int effectiveValue() {
        return (rear + maxSize - front) % maxSize;
    }

    /**
     * 显示队列头部数据,不是取数据
     */
    public int headQueue() {
        //判断为空
        if (isEmpty()) {
            throw new RuntimeException("队列为空，没有数据~~");
        }
        return array[front];
    }

}
```



# 链表

Linked List

1. 带头节点的链表
2. 没有头节点的链表



- 有序的列表，链表以节点方式存储，链式存储
- 每个节点包含 data 域 ，next 域：指向下一个节点
- 链表的节点之间不一定是连续的

 

## 单链表

带头结点（单链表）逻辑结构示意图

![image-20220807215722911](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220807215722911.png)

内存布局图

![image-20220807215621747](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220807215621747.png)

水浒传英雄排行榜管理

分析

1. 完成CRUD功能

2. 添加英雄方式

   1. 直接添加到链表尾部
   2. 根据排名将英雄插入到指定位置（英雄存在，则无效）

3. 单链表创建示意图

   ![image-20220807221131311](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220807221131311.png)

### 单链表添加节点

1. 先创建一个head头节点，单链表的头
2. 每添加一个节点，就直接加入到链表的最后遍历

遍历

1. 通过一个变量遍历，帮助遍历整个链表

```java
package com.linkedlist;

/**
 * @author Kcs 2022/8/7
 */
public class SingleLinkedListDemo {

    public static void main(String[] args) {
        //测试
        //创建节点
        HeroNode hero1 = new HeroNode(1, "宋江", "及时雨");
        HeroNode hero2 = new HeroNode(2, "卢俊义", "玉麒麟");
        HeroNode hero3 = new HeroNode(3, "吴用", "智多星");
        HeroNode hero4 = new HeroNode(4, "林冲", "豹子头");

        //添加进入链表
        SingleLinkedList singleLinkedList = new SingleLinkedList();
        singleLinkedList.add(hero1);
        singleLinkedList.add(hero2);
        singleLinkedList.add(hero3);
        singleLinkedList.add(hero4);

        //显示
        singleLinkedList.list();
    }

}

/**
 * 定义一个SingleLinkedList管理英雄
 */
class SingleLinkedList {
    /**
     * 初始化一个头节点
     */
    private HeroNode head = new HeroNode(0, "", "");

    /**
     * 添加节点到单向链表
     * 找当前链表的最后节点
     * 最后节点的next 指向新的节点
     */
    public void add(HeroNode heroNode) {

        //添加一个临时变量temp
        HeroNode temp = head;
        //遍历链表，找到最后
        while (true) {
            //找到链表的最后
            if (temp.next == null) {
                break;
            }
            //如果没有找到，temp后移
            temp = temp.next;

        }
        //退出循坏，temp就指向链表的最后
        temp.next = heroNode;
    }

    //显示链表,遍历
    public void list() {
        //判断链表是否为空
        if (head.next == null) {
            System.out.println("链表为空");
            return;
        }
        //头节点不能动，辅助变量遍历
        HeroNode temp = head.next;
        while (true) {
            //判断是否到链表最后
            if (temp == null) {
                break;
            }
            //输出节点信息
            System.out.println(temp);
            //将temp后移,不然就是死循环
            temp = temp.next;
        }
    }
}


/**
 * 定义一个HeroNode，每个heroNode对象就是一个节点
 */
class HeroNode {
    /**
     * 编号
     */
    public int no;
    /**
     * 姓名
     */
    public String name;
    /**
     * 昵称
     */
    public String nickname;
    /**
     * 指向下一个节点
     */
    public HeroNode next;

    /**
     * 构造器
     * @param no
     * @param name
     * @param nickname
     */
    public HeroNode(int no, String name, String nickname) {
        this.no = no;
        this.name = name;
        this.nickname = nickname;
    }


    /**
     * 重写toString
     */
    @Override
    public String toString() {
        return "Heroes{" +
                "no=" + no +
                ", name='" + name + '\'' +
                ", nickname='" + nickname + '\'' +
                '}';
    }
}
```

以上代码，添加的顺序改变是无序的，就按添加的代码进行排序（也就是第一种方式）

方式二添加英雄方式

- 根据排名（编号）将英雄插入到指定位置（英雄存在，则无效）

分析

1. 首先找到新添加的节点的位置，通过辅助变量（指针），通过遍历
2. 新的节点.next = temp.next 
3. temp.next = 新的接点

```java
package com.linkedlist;

import com.sun.xml.internal.ws.util.StreamUtils;

/**
 * @author Kcs 2022/8/7
 */
public class SingleLinkedListDemo {

    public static void main(String[] args) {
        //测试
        //创建节点
        HeroNode hero1 = new HeroNode(1, "宋江", "及时雨");
        HeroNode hero2 = new HeroNode(2, "卢俊义", "玉麒麟");
        HeroNode hero3 = new HeroNode(3, "吴用", "智多星");
        HeroNode hero4 = new HeroNode(4, "林冲", "豹子头");

        //添加进入链表
        SingleLinkedList singleLinkedList = new SingleLinkedList();
        // singleLinkedList.add(hero1);
        // singleLinkedList.add(hero2);
        // singleLinkedList.add(hero3);
        // singleLinkedList.add(hero4);

        //根据编号添加
        singleLinkedList.addHeroByOrder(hero4);
        singleLinkedList.addHeroByOrder(hero1);
        singleLinkedList.addHeroByOrder(hero3);
        singleLinkedList.addHeroByOrder(hero2);
        
        
        //显示
        singleLinkedList.list();
    }

}

/**
 * 定义一个SingleLinkedList管理英雄
 */
class SingleLinkedList {
    /**
     * 初始化一个头节点
     */
    private HeroNode head = new HeroNode(0, "", "");
    
    /**
     * 根据排名(编号)将英雄插入到指定位置（英雄存在，则无效）
     */
    public void addHeroByOrder(HeroNode heroNode) {
        //设置一个临时遍历，找到要添加的位置 ，temp位于添加位置的前一个节点，否则插入失败
        HeroNode temp = head;
        //标志编号是否存在
        boolean flag = false;

        while (true) {
            //到链表的最后，为空
            if (temp.next == null) {
                break;
            }
            //确定添加位置
            if (temp.next.no > heroNode.no) {
                break;
            } else if (temp.next.no == heroNode.no) {
                //添加的编号已存在，无效
                flag = true;
                break;
            }
            //后移，继续遍历
            temp = temp.next;
        }

        //判断flag
        if (flag) {
            //已存在编号
            System.out.printf("该英雄编号%d已存在,不能添加\n", heroNode.no);
        } else {
            //插入链表中，temp的后面
            heroNode.next = temp.next;
            temp.next = heroNode;
        }

    }


    /**
     * 显示链表,遍历
     */
    public void list() {
        //判断链表是否为空
        if (head.next == null) {
            System.out.println("链表为空");
            return;
        }
        //头节点不能动，辅助变量遍历
        HeroNode temp = head.next;
        while (true) {
            //判断是否到链表最后
            if (temp == null) {
                break;
            }
            //输出节点信息
            System.out.println(temp);
            //将temp后移,不然就是死循环
            temp = temp.next;
        }
    }
}


/**
 * 定义一个HeroNode，每个heroNode对象就是一个节点
 */
class HeroNode {
    /**
     * 编号
     */
    public int no;
    /**
     * 姓名
     */
    public String name;
    /**
     * 昵称
     */
    public String nickname;
    /**
     * 指向下一个节点
     */
    public HeroNode next;

    /**
     * 构造器
     * @param no
     * @param name
     * @param nickname
     */
    public HeroNode(int no, String name, String nickname) {
        this.no = no;
        this.name = name;
        this.nickname = nickname;
    }


    /**
     * 重写toString
     */
    @Override
    public String toString() {
        return "Heroes{" +
                "no=" + no +
                ", name='" + name + '\'' +
                ", nickname='" + nickname + '\'' +
                '}';
    }
}
```



### 单链表修改节点

修改英雄的信息

```java
/**
 * 修改节点信息，根据编号修改，编号不能修改
 * 根据newHeroNode 的 no 来修改信息
 */
public void update(HeroNode updateHeroNode) {
    //判断链表是否空
    if (head.next == null) {
        System.out.println("链表为空！！！");
        return;
    }
    //找到修改的节点，根据no
    HeroNode temp = head.next;
    //判断是否找到节点
    boolean flag = false;
    while (true) {
        if (temp == null) {
            break;
        }
        //找到
        if (temp.no == updateHeroNode.no) {
            flag = true;
            break;
        }

        //后移
        temp = temp.next;
    }
    //判断是否为要修改的节点
    if (flag) {
        temp.name = updateHeroNode.name;
        temp.nickname = updateHeroNode.nickname;
    } else {
        //没有找到
        System.out.printf("没有找到编号 %d的信息，不能修改\n", updateHeroNode.no);
    }
}
```



### 单链表删除节点

1. 找到要删除节点的前一个节点temp
2. temp.next = temp.next.next （跳过的节点，就是直接删除掉，被垃圾回收了）

```java
/**
 * 删除节点，不能改变head 节点，通过temp找到待删除的节点的前一个节点
 * temp.next.no 与删除节点的no比较
 */

public void delete(int no) {
    HeroNode temp = head;
    //标志是否找到待删除的节点
    boolean flag = false;
    while (true) {
        //temp到链表最后
        if (temp.next == null) {
            break;
        }
        if (temp.next.no == no) {
            //找到要删除节点的前一个节点
            flag = true;
            break;
        }
        //后移
        temp = temp.next;
    }
    //判断flag
    if (flag) {
        //找到 ，删除
        temp.next = temp.next.next;
    } else {
        System.out.println("要删除的节点%d不存在\n" + no);
    }
}
```

### 单链表查询节点

~~~java

/**
 * 查找英雄信息
 */
public void search(int no) {
    //判断链表是否为空
    HeroNode temp = head;
    if (temp.next == null) {
        System.out.println("链表为空！！！");
        return;
    }
    //判断是否找到节点
    boolean flag = false;
    while (true) {
        //temp到链表最后
        if (temp.next == null) {
            break;
        }
        if (temp.no == no) {
            //找到要查找节点的前一个节点
            flag = true;
            break;
        }
        //后移
        temp = temp.next;
    }
    //判断flag
    if (flag) {
        //查找到
        System.out.println(temp);
    } else {
        System.out.println("要查找的节点%d不存在\n" + no);
    }
}
~~~

### 单链表面试题

- 单链表（节点）反转

  1. 定义一个节点 reverse = new HeroNode（）
  2. 从头到尾遍历原来的链表，每遍历一个节点，并放在新的链表的最前端，最前端的next域指向上一个最前端的地方，原来的链表的第一个就没有next
  3. 原来的链表的 head.next = reverseHead.next

  ```java
  //将链表反转
  public static void reverseList(HeroNode head) {
      //如果链表为空，或者只有一个节点，无须反转，直接返回
      if (head.next == null || head.next.next == null) {
          return;
      }
      //辅助变量
      HeroNode cur = head.next;
      //指向当前节点（cur节点）的下一个节点，
      HeroNode next = null;
      HeroNode reverseHead = new HeroNode(0, "", "");
  
      //遍历原来的链表,每遍历一个新的节点，就将其取出，放在新的链表reverseHead 的最前端
      while (cur != null) {
          //暂存当前节点的下一个节点
          next = cur.next;
          //将cur的下一个节点的指向新的链表的最前端
          cur.next = reverseHead.next;
          //cur链接到新的链表上
          reverseHead.next = cur;
          //cur后移,不能是cur.next 因为反转后的next以及不存在了
          cur = next;
      }
      //将原始链表的head.next指向reverseHead.next 实现反转
      head.next = reverseHead.next;
  }
  ```

## 双向链表

单链表存在问题：

1. 只有一个方向，而双向链表可以向前或前后查找
2. 单向链表不能自我删除，要有临时变量，双向链表可以实现自我删除

双向链表结构：

![image-20220808220745643](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220808220745643.png)



### 分析双向链表的CRUD

1. 遍历：
   - 和单链表一样，向前或向后查找
2. 添加：默认添加到双向链表的最后
   1. 先找到双向链表的最后的这个节点（temp）
   2. temp. next =newHeroNode
   3. newHeroNode.pre = temp
3. 修改
   1. 和单向链表一样
4. 删除
   1. 自我删除某个节点
   2. 直接找到要删除的这个节点（temp）
   3. temp.pre.next = temp.next (temp前一个直接指向temp的后一个节点)
   4. temp.next.pre = temp.pre

## 单向环形链表

### 应用场景

> Josephu(约瑟夫、约瑟夫环) 问题 Josephu 问题为：设编号为1，2，… n的n个人围坐一圈， 约定编号为k（1<=k<=n）的人从1开始报数，数到m 的那个 人出列，它的下一位又从1开始报数，数到m的那个人又出 列，依次类推，直到所有人出列为止，由此产生一个出队 编号的序列.

​														单向环形链表结构

![image-20220810205120664](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220810205120664.png)

### Josehu 问题 分析

> 先构成一个有n个结点的单循环链表， 然后由k结点起从1开始计数，计到m时，对应结点从链表中删除，然后再从被删除结点 的下一个结点又从1开始计数，直到最后一个结点从链表中删除算法结束

- n = 5 ：有五个人
- k = 1：从第一个人开始报数
- m = 2 ，数两次

![image-20220810210002148](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220810210002148.png)

出队列报数顺序：

> 2 =》4 =》1=》5 =》3

### 分析思路

1. 先创建第一个节点，让first指向该节点，并形成环形
2. 后面让我们每创建一个新的节点，把该节点，加入到已经有的环形链表中

#### 遍历环形链表

1. 先让一个指针（变量）curBoy ，指向first节点
2. 通过while循环遍历该环形链表curBoy.next = first

#### 出队顺序

1. 创建一个指针（变量）helper，开始指向环形链表的最后一个节点
2. 报数前，先让 first 和 helper 移动 k - 1 次
3. 报数时，让first 和 helper 指针同时移动 m - 1 次
4. 将 first 指向这个小孩节点出圈 
   - first = first.next
   - helper.next = first
5. 原来的节点没有了任何的指向就会被垃圾回收

```java
package com.linkedlist;

/**
 * @author Kcs 2022/8/10
 */
public class Josepfu {
    public static void main(String[] args) {
        //环形链表测试

        CircleSingleLinkedList circleSingleLinkedList = new CircleSingleLinkedList();

        //创建五个小孩节点
        circleSingleLinkedList.addBoy(100);
        //显示
        circleSingleLinkedList.showBoy();

        //出圈
        circleSingleLinkedList.countBoy(1, 2, 100);
    }
}

/**
 * 创建一个单向的环形链表
 */
class CircleSingleLinkedList {
    /**
     * 创建first节点
     */
    private Boy first = new Boy(-1);

    /**
     * 添加节点，构成环形链表
     */
    public void addBoy(int nums) {
        //数据判断
        if (nums < 1) {
            System.out.println("nums值需要大于1");
            return;
        }
        //临时变量
        Boy curBoy = null;

        //使用for创建环形链表
        for (int i = 1; i <= nums; i++) {
            //根据编号，创建节点
            Boy boy = new Boy(i);
            //第一个小孩节点
            if (i == 1) {
                first = boy;
                //形成环形
                first.setNext(first);
                //curBoy 指向第一个小孩节点
                curBoy = first;
            } else {
                //指向新建的节点
                curBoy.setNext(boy);
                boy.setNext(first);
                curBoy = boy;
            }
        }
    }

    /**
     * 遍历当前的环形链表
     */
    public void showBoy() {
        //判断链表是否为空
        if (first == null) {
            System.out.println("链表为空！！");
            return;
        }
        //first 节点不能移动，创建临时指针
        Boy curBoy = first;
        while (true) {
            System.out.printf("小孩的编号:%d\n", curBoy.getNo());
            //遍历结束
            if (curBoy.getNext() == first) {
                break;
            }
            //curBoy后移
            curBoy = curBoy.getNext();
        }
    }

    /**
     * 根据输入，计算出圈的顺序
     * @param startNo 开始的节点
     * @param countNum 数几下
     * @param nums 圈内总共有几个节点
     */
    public void countBoy(int startNo, int countNum, int nums) {
        //校验
        if (first == null || startNo < 1 || startNo > nums) {
            System.out.println("输入的数字有误。请重新输入");
            return;
        }
        //临时指针
        Boy helper = first;
        while (true) {
            //遍历借结束
            if (helper.getNext() == first) {
                break;
            }
            //helper后移
            helper = helper.getNext();
        }
        //报数前，先让 first 和 helper 移动 k - 1 次
        for (int i = 0; i < startNo - 1; i++) {
            first = first.getNext();
            helper = helper.getNext();
        }
        //报数时，让first 和 helper 指针同时移动 m - 1 次,循环操作，直到圈中只有一个人
        while (true) {
            //判断圈中只有一个人
            if (helper == first) {
                System.out.println("最后一个人了");
                break;
            }
            //让first 和 helper 指针同时移动 countNum - 1 ,出圈
            for (int i = 0; i < countNum - 1; i++) {
                first = first.getNext();
                helper = helper.getNext();
            }
            //first指向出圈的节点
            System.out.printf("小孩 %d 出圈\n", first.getNo());
            //first指向出圈小孩的节点
            first = first.getNext();
            helper.setNext(first);
        }
        System.out.printf("最后圈中的小孩的编号是%d", helper.getNo());
    }
}


/**
 * 创建一个Boy类，表示一个节点
 */
class Boy {
    /**
     * 编号
     */
    private int no;
    /**
     * 下一个节点
     */
    private Boy next;

    public Boy(int no) {
        this.no = no;
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    public Boy getNext() {
        return next;
    }

    public void setNext(Boy next) {
        this.next = next;
    }
}
```

# 栈 stack

- 先入后出的有序列表
- 栈(stack)是限制线性表中元素的插入和删除只能在线性表的同一端进行的一 种特殊线性表。**允许插入和删除的一端，为变化的一端，称为栈顶(Top)，另 一端为固定的一端，称为栈底(Bottom)**
- 最先放入栈中元素在栈底，最后放入的元素在栈顶，而 删除元素刚好相反，最后放入的元素最先删除，最先放入的元素最后删除

## 出栈（pop） 、入栈（push）结构

![image-20220811211410996](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220811211410996.png)

## 应用场景

1. 子程序的调用：在跳往子程序前，会先将下个指令的地址存到堆栈中，直到 子程序执行完后再将地址取出，以回到原来的程序中
2. 处理递归调用：和子程序的调用类似，只是除了储存下一个指令的地址外， 也将参数、区域变量等数据存入堆栈中
3. 表达式的转换 [ 中缀表达式转后缀表达式 ] 与求值(实际解决) 
4. 二叉树的遍历
5. 图形的深度优先( depth一first )搜索法

## 栈的快速入门

1. 用数组模拟栈
2. 栈顶：定义变量初始值 top = -1
3. 入栈：top++，stack[top] = data
4. 出栈：int value = stack[top] ,top -- ,return value

```java
package com.stack;

import java.util.Scanner;

/**
 * 栈
 * @author Kcs 2022/8/11
 */
public class ArrayStackDemo {
    public static void main(String[] args) {
        //测试
        ArrayStack stack = new ArrayStack(4);
        String key = "";
        //控制菜单是否退出
        boolean loop = true;
        Scanner scanner = new Scanner(System.in);
        while (loop) {
            System.out.println("show:显示栈内所有的数据");
            System.out.println("push:添加数据到栈(入栈)");
            System.out.println("pop:从栈中取出数据(出栈)");
            System.out.println("exit:退出栈");
            System.out.println("你的选择是：");

            key = scanner.next();
            switch (key) {
                case "show":
                    stack.list();
                    break;
                case "push":
                    System.out.println("请输入一个数字：");
                    int value = scanner.nextInt();
                    stack.push(value);
                    break;
                case "pop":
                    try {
                        int res = stack.pop();
                        System.out.printf("出栈的数据%d\n", res);
                    } catch (Exception e) {
                        System.out.println(e.getMessage());
                    }
                    break;
                case "exit":
                    scanner.close();
                    loop = false;
                    break;
                default:
                    break;

            }
        }
        System.out.println("程序退出,欢迎下次再来！！！");
    }
}


/**
 * 定义一个ArrayStack 表示栈
 */
class ArrayStack {
    /**
     * 栈的的大小
     */
    private int maxSize;
    /**
     * 数组模拟栈
     */
    private int[] stack;
    /**
     * 初始化栈顶
     */
    private int top = -1;

    /**
     * 构造方法
     */
    public ArrayStack(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    /**
     * 栈满
     */
    public boolean isFull() {
        return top == maxSize - 1;
    }

    /**
     * 栈空
     */
    public boolean isEmpty() {
        return top == -1;
    }

    /**
     * 入栈
     */
    public void push(int value) {
        //判断是否栈满
        if (isFull()) {
            System.out.println("栈满");
            return;
        }
        top++;
        stack[top] = value;
    }

    /**
     * 出栈
     */
    public int pop() {
        //判断是否栈满
        if (isEmpty()) {
            throw new RuntimeException("栈空,没有存储数据");
        }
        int value = stack[top];
        top--;
        return value;
    }

    /**
     * 遍历栈,遍历时从栈顶开始
     */
    public void list() {
        if (isEmpty()) {
            System.out.println("栈空,没有存储数据");
            return;
        }
        //从栈顶显示数据
        for (int i = top; i >= 0; i--) {
            System.out.printf("stack[%d] = %d\n", i, stack[i]);
        }
    }

}
```

## 栈实现综合案例-计算器

![image-20220812210831649](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220812210831649.png)

### 思路分析 （使用中缀表达式）

计算式：7 * 2 * 2 - 5 + 1- 5 * 3 - 3

1. 首先创建两个栈
   1. 数栈（numStack）：存放数
   2. 符号栈（operStack）：存放运算符
2. 通过一个index 值，来遍历表达式
3. 扫描到一个数字，就直接加入数栈
4. 扫描到一个运算符，则有两种情况
   1. 若当前符号栈为空，就直接入栈
   2. 若符号栈不为空，就进行比较，如果当前的操作符的优先级 小于 或 等于 栈中的操作符，则从数栈中pop数两个数，再从符号栈中pop出一个符号，进行运算，将其结果进入数栈，将当前的操作符入符号栈
   3. 如果当前的操作符的优先级大于栈中的操作符，就直接入符号栈
5. 当表达式扫描完毕，就顺序的从数栈和符号栈中pop出相应的数和符号，并运行
6. 最后在数栈只有一个数字，既是结果
7. 处理多位数问题
   1. 不能发现一个数就立即入栈，可能是多位数
   2. 处理数式，需要项expression的表达式的index，后看一位，若是数九进行扫描，若是符号才入栈
   3. 定义一个字符串变量，进行拼接

```java
package com.stack;

/**
 * @author Kcs 2022/8/12
 */
public class Calculator {
    public static void main(String[] args) {
        //扫描表达式
        String expression = "5456*2+5";
        //创建两个栈，数栈，符号栈
        ArrayCalStack numStack = new ArrayCalStack(10);
        ArrayCalStack operStack = new ArrayCalStack(10);

        //扫描变量
        int index = 0;
        int num1 = 0;
        int num2 = 0;
        int oper = 0;
        int res = 0;

        //用于每次扫描得到的char保存到ch
        char ch = ' ';

        //用于拼接多位数
        String keyNum = "";

        //循环扫描
        while (true) {
            //依次得到每一个字符
            ch = expression.substring(index, index + 1).charAt(0);
            //判断是否为符号
            if (operStack.isOper(ch)) {
                //判断符号栈是否为空
                if (!operStack.isEmpty()) {
                    //如果当前的操作符的优先级 小于 或 等于 栈中的操作符，则从数栈中pop数两个数，再从符号栈中pop出一个符号，进行运算，
                    //将其结果进入数栈，将当前的操作符入符号栈
                    if (operStack.priority(ch) <= operStack.priority(operStack.peek())) {
                        num1 = numStack.pop();
                        num2 = numStack.pop();
                        oper = operStack.pop();
                        res = numStack.cal(num1, num2, oper);
                        //运算结构入数栈
                        numStack.push(res);
                        //当前操作符入符号栈
                        operStack.push(ch);
                    } else {
                        //如果当前的操作符的优先级大于栈中的操作符，就直接入符号栈
                        operStack.push(ch);
                    }
                } else {
                    //为空，直接入符号栈
                    operStack.push(ch);
                }
            } else {
                //如果是数字就直接入数栈(存在多位数问题)

                //处理多位数
                keyNum += ch;

                //如果ch为expression最后的一位
                if (index == expression.length()-1){
                    numStack.push(Integer.parseInt(keyNum));
                }else {
                    //判断下一位是否为数字，若为数字，则进行扫描，若是运算符，则入符号栈
                    if (operStack.isOper(expression.substring(index + 1, index + 2).charAt(0))){
                        //如果后一位为运算符则入栈，keepNum ="112"
                        numStack.push(Integer.parseInt(keyNum));
                        //清空keepNum
                        keyNum = "";

                    }
                }
            }
            //让index + 1 ,判断是否扫描到最后
            index++;
            if (index >= expression.length()) {
                break;
            }
        }
        //当表达式扫描完毕，就顺序的从数栈和符号栈中pop出相应的数和符号，并运行
        while (true) {
            //若符号栈为空，则计算最后的结果，数栈中只有一个数字
            if (operStack.isEmpty()) {
                break;
            }
            num1 = numStack.pop();
            num2 = numStack.pop();
            oper = operStack.pop();
            res = numStack.cal(num1, num2, oper);
            //运算结果入数栈
            numStack.push(res);
        }
        //将数栈最后的结果pop
        int result = numStack.pop();
        System.out.printf("表达式%s = %d", expression, result);
    }
}


/**
 * ArrayCalStack
 */
class ArrayCalStack {
    /**
     * 栈的的大小
     */
    private int maxSize;
    /**
     * 数组模拟栈
     */
    private int[] stack;
    /**
     * 初始化栈顶
     */
    private int top = -1;

    /**
     * 构造方法
     */
    public ArrayCalStack(int maxSize) {
        this.maxSize = maxSize;
        stack = new int[this.maxSize];
    }

    /**
     * 返回当前栈顶的值，但并不pop
     */
    public int peek() {
        return stack[top];
    }

    /**
     * 栈满
     */
    public boolean isFull() {
        return top == maxSize - 1;
    }

    /**
     * 栈空
     */
    public boolean isEmpty() {
        return top == -1;
    }

    /**
     * 入栈
     */
    public void push(int value) {
        //判断是否栈满
        if (isFull()) {
            System.out.println("栈满");
            return;
        }
        top++;
        stack[top] = value;
    }

    /**
     * 出栈
     */
    public int pop() {
        //判断是否栈满
        if (isEmpty()) {
            throw new RuntimeException("栈空,没有存储数据");
        }
        int value = stack[top];
        top--;
        return value;
    }

    /**
     * 遍历栈,遍历时从栈顶开始
     */
    public void list() {
        if (isEmpty()) {
            System.out.println("栈空,没有存储数据");
            return;
        }
        //从栈顶显示数据
        for (int i = top; i >= 0; i--) {
            System.out.printf("stack[%d] = %d\n", i, stack[i]);
        }
    }

    /**
     * 饭后运算符的优先级，自定义优先级：数字越大优先级就越高
     */
    public int priority(int oper) {
        if (oper == '*' || oper == '/') {
            return 1;
        } else if (oper == '+' || oper == '-') {
            return 0;
        } else {
            //只有 + - * /
            return -1;
        }
    }

    /**
     * 判断是否是一个优先级
     */
    public boolean isOper(char var) {
        return var == '+' || var == '-' || var == '*' || var == '/';
    }

    /**
     * 计算方法
     */
    public int cal(int num1, int num2, int oper) {
        //用于保存计算结果
        int res = 0;
        switch (oper) {
            case '+':
                res = num1 + num2;
                break;
            case '-':
                res = num2 - num1;
                break;
            case '*':
                res = num1 * num2;
                break;
            case '/':
                res = num2 / num1;
                break;
            default:
                break;
        }
        return res;
    }
}
```

## 前缀(波兰表达式)

- 前缀表达式的运算符位于操作数之前

> (3+4)×5-6 对应的前缀表达式就是 - × + 3 4 5 6

### 计算机求职

- 从右至左扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个 数，用运算符对它们做相应的计算（栈顶元素 和 次顶元素），并将结果入栈；重复上 述过程直到表达式最左端，最后运算得出的值即为表达式的结果

(3+4)×5-6 对应的前缀表达式就是 - × + 3 4 5 6 的表达式的求值步骤

1. 从右至左扫描，将6、5、4、3压入堆栈
2. 遇到+运算符，因此弹出3和4（3为栈顶元素，4为次顶元素），计算出3+4的值，得7， 再将7入栈
3. 接下来是×运算符，因此弹出7和5，计算出7×5=35，将35入栈
4. 最后是-运算符，计算出35-6的值，即29，由此得出最终结果

## 中缀

- 最常见的运算规则

## 后缀

- 运算符位于操作数之后

> (3+4)×5-6 对应的后缀表达式就是 3 4 + 5 × 6 –

### 计算规则

​	从左至右扫描表达式，遇到数字时，将数字压入堆栈，遇到运算符时，弹出栈顶的两个 数，用运算符对它们做相应的计算（次顶元素 和 栈顶元素），并将结果入栈；重复上 述过程直到表达式最右端，最后运算得出的值即为表达式的结果

1. 从左至右扫描，将3和4压入堆栈；
2. 遇到+运算符，因此弹出4和3（4为栈顶元素，3为次顶元素），计算出3+4的值，得7，再将7入 栈；
3. 将5入栈； 
4.  接下来是×运算符，因此弹出5和7，计算出7×5=35，将35入栈； 
5. 将6入栈；
6. 最后是-运算符，计算出35-6的值，即29，由此得出最终结果

### 逆波兰计算器

1. 输入一个逆波兰表达式（后缀表达式）使用栈（Stack）计算其结果
2. 支持小括号和多位数，只对整数计算

#### 分析

1. 定义一个逆波兰表达式
2. 依次将逆波兰表达式的数据和运算符存入到ArrayList中
3. ArrayList 传递给一个方法，遍历ArrayList,配合栈，完成计算

```java
package com.stack;

import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

/**
 * @author Kcs 2022/8/13
 */
public class PolandNotation {
    public static void main(String[] args) {


        //定义一个逆波兰表达式 (3+4)×5-6 ,4 5 * 8 - 60 + 8 2 / +,存在空格符号
        String suffixExpression = "4 5 * 8 - 60 + 8 2 / +";


        //将ArrayList传递给一个方法，遍历

        List<String> list = getListString(suffixExpression);
        System.out.println("list=" + list);

        int res = calculate(list);
        System.out.println("result = " + res);
    }

    /**
     * 表达式 存入ArrayList中
     * @param suffixExpression
     * @return String[]
     */
    public static List<String> getListString(String suffixExpression) {
        //将表达式分割
        String[] spilt = suffixExpression.split(" ");
        List<String> list = new ArrayList<String>();
        for (String ele : spilt) {
            list.add(ele);
        }
        return list;
    }

    // 逆波兰表达式的运算
    public static int calculate(List<String> ls) {

        //创建给栈，只需要一个栈
        Stack<String> stack = new Stack<String>();

        // 遍历 ls
        for (String item : ls) {
            //判断是否位数，正则表达式
            //匹配多位数
            if (item.matches("\\d+")) {
                //入栈
                stack.push(item);
            } else {
                //pop出两个数，并运算,再入栈
                int num2 = Integer.parseInt(stack.pop());
                int num1 = Integer.parseInt(stack.pop());
                //判断前的符号
                int res = 0;
                if (item.equals("+")) {
                    res = num1 + num2;
                } else if (item.equals("-")) {
                    //用后出栈的减去先出栈的
                    res = num1 - num2;
                } else if (item.equals("*")) {
                    res = num1 * num2;
                } else if (item.equals("/")) {
                    //用后出栈的 除以 先出栈的
                    res = num1 / num2;
                } else {
                    throw new RuntimeException("运算符有问题，不属于四则运算符号");
                }
                stack.push("" + res);
            }
        }
        //最后留在栈里的数据是运算结果
        return Integer.parseInt(stack.pop());
    }
}
```



## 中缀转后缀

 将这个中缀表达式：1 + (( 2 + 3) × 4 ) - 5 ===》后缀表达式

### 分析步骤

1. 初始化两个栈：运算符栈 s1 和 储存中间 结果的栈 s2；
2. 从左至右扫描中缀表达式； 
3. 遇到操作数时，将其压s2；
4. 遇到运算符时，比较其与s1栈顶运算符的优先级： 
   1. 如果s1为空，或栈顶运算符为左括号“(”，则直接将此运算符入栈； 
   2. 否则，若优先级比栈顶运算符的高，也将运算符压入s1； 
   3. 否则，将s1栈顶的运算符弹出并压入到s2中，再次转到(4.1)与s1中新的栈顶运算 符相比较；
5. 遇到括号时：
   1. 如果是左括号 “(” ，则直接压入s1 
   2. 如果是右括号 “)” ，则依次弹出s1栈顶的运算符，并压入s2，直到遇到左括号为止，此时将这一对括号丢弃 
6. 重复步骤2至5，直到表达式的最右边  
7. 将s1中剩余的运算符依次弹出并压入s2 
8. 依次弹出s2中的元素并输出，结果的逆序即为中缀表达式对应的后缀表达式。

```java
package com.stack;

import java.util.ArrayList;
import java.util.List;
import java.util.Stack;

/**
 * @author Kcs 2022/8/13
 */
public class PolandNotation {
    public static void main(String[] args) {

        // 中缀 ===》后缀
        // 1 + (( 2 + 3) * 4 ) - 5 ===》1 2 3 + 4 * + 5 –
        String expression = "1+((2+3)*4)-5";
        List<String> infixExpressionList = toInfixExpressionList(expression);
        System.out.println("中缀表达式：" + infixExpressionList);

        List<String> suffixExpressionList = parseSuffixExpressionList(infixExpressionList);
        System.out.println("后缀表达式：" + suffixExpressionList);

        System.out.println("后缀表达式的结果 = " + calculate(suffixExpressionList));
    /**
     * 将中缀表达式转为List 上面的中缀表达式存入List得到的结果:[1, +, (, (, 2, +, 3, ), ×, 4, ), -, 5]
     */
    public static List<String> toInfixExpressionList(String s) {
        //存放中缀表达式内容
        ArrayList<String> list = new ArrayList<>();
        //定义指针，遍历中缀表达式
        int i = 0;
        //多位拼接
        String str;
        char c;
        do {
            //c为非数字
            if ((c = s.charAt(i)) < 48 || (c = s.charAt(i)) > 57) {
                list.add("" + c);
                //后移
                i++;
            } else {
                //多位数
                str = "";
                while (i < s.length() && (c = s.charAt(i)) >= 48 && (c = s.charAt(i)) <= 57) {
                    str += c;
                    i++;
                }
                list.add(str);
            }
        } while (i < s.length());
        return list;
    }


    /**
     * 将得到的中缀表达式转换成 后缀表达式
     */
    public static List<String> parseSuffixExpressionList(List<String> list) {
        // 定义栈 符号栈
        Stack<String> s1 = new Stack<String>();
        //存储中间结果的栈，使用List方便操作
        List<String> s2 = new ArrayList<String>();

        //遍历list
        for (String item : list) {
            //为数，入s2
            if (item.matches("\\d+")) {
                s2.add(item);
            } else if (item.equals("(")) {
                s1.push(item);
            } else if (item.equals(")")) {
                //依次弹出s1栈顶的运算符，并压入s2，直到遇到左括号为止，此时将这一对括号丢弃
                while (!s1.peek().equals("(")) {
                    s2.add(s1.pop());
                }
                //将左括号弹出，消除小括号
                s1.pop();
            } else {
                //item的优先级比s1栈顶的优先级小,将s1栈顶的运算符弹出并压入到s2中，再次转到与s1中新的栈顶运算符相比较
                while (s1.size() != 0 && Operation.getValue(s1.peek()) >= Operation.getValue(item)) {
                    s2.add(s1.pop());
                }
                //将item 压入栈顶
                s1.push(item);
            }
        }
        //将s1中剩余的运算符依次弹出并加入s2
        while (s1.size() != 0) {
            s2.add(s1.pop());
        }
        //存放到list，正常输入就是逆波兰表达式
        return s2;
    }


    /**
     * 表达式 存入ArrayList中
     * @param suffixExpression
     * @return String[]
     */
    public static List<String> getListString(String suffixExpression) {
        //将表达式分割
        String[] spilt = suffixExpression.split(" ");
        List<String> list = new ArrayList<String>();
        for (String ele : spilt) {
            list.add(ele);
        }
        return list;
    }

    // 逆波兰表达式的运算
    public static int calculate(List<String> ls) {

        //创建给栈，只需要一个栈
        Stack<String> stack = new Stack<String>();

        // 遍历 ls
        for (String item : ls) {
            //判断是否位数，正则表达式
            //匹配多位数
            if (item.matches("\\d+")) {
                //入栈
                stack.push(item);
            } else {
                //pop出两个数，并运算,再入栈
                int num2 = Integer.parseInt(stack.pop());
                int num1 = Integer.parseInt(stack.pop());
                //判断前的符号
                int res = 0;
                if (item.equals("+")) {
                    res = num1 + num2;
                } else if (item.equals("-")) {
                    //用后出栈的减去先出栈的
                    res = num1 - num2;
                } else if (item.equals("*")) {
                    res = num1 * num2;
                } else if (item.equals("/")) {
                    //用后出栈的 除以 先出栈的
                    res = num1 / num2;
                } else {
                    throw new RuntimeException("运算符有问题，不属于四则运算符号");
                }
                stack.push("" + res);
            }
        }
        //最后留在栈里的数据是运算结果
        return Integer.parseInt(stack.pop());
    }
}


/**
 * 优先级高低,返回运算符对应的优先级
 */

class Operation {
    private static int ADD = 1;
    private static int SUB = 1;
    private static int MUL = 2;
    private static int DIV = 2;

    //返回对应的优先级数字
    public static int getValue(String operation) {
        int result = 0;
        switch (operation) {
            case "+":
                result = ADD;
                break;
            case "-":
                result = SUB;
                break;
            case "*":
                result = MUL;
                break;
            case "/":
                result = DIV;
                break;
            default:
                System.out.println("不存在该运算符！！！");
                break;
        }
        return result;
    }
}
```

# 递归

- 自己调用自己，每次的变量都不一样

## 规范

1. 执行一个方法时，就创建一个新的受保护的独立空间(栈空间)
2. 方法的局部变量是独立的，不会相互影响, 比如n变量
3. 如果方法中使用的是引用类型变量(比如数组)，就会共享该引用类型的数据
4. 递归必须向退出递归的条件逼近，否则就是无限递归,出现StackOverflowError（栈溢出）， 死龟了
5. 当一个方法执行完毕，或者遇到return，就会返回，遵守谁调用，就将结果 返回给谁，同时当方法执行完毕或者返回时，该方法也就执行完毕

## 递归 - 迷宫回溯问题

![image-20220825153332671](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220825153332671.png)

1. 小球得到的路径，和程序员 设置的找路策略有关即：找 路的上下左右的顺序相关 
2. 再得到小球路径时，可以先 使用(下右上左)，再改成(上 右下左)，看看路径是不是有变化 
3. 测试回溯现象

```java
package com.recursion;

/**
 * @author Kcs 2022/8/25
 */
public class MiGong {
    public static void main(String[] args) {

        //二维数组模拟迷宫
        int[][] map = new int[8][7];
        //1.表示墙
        //上下两行置为 1
        for (int i = 0; i < 7; i++) {
            map[0][i] = 1;
            map[7][i] = 1;
        }
        //左右两侧的列置为 1
        for (int i = 0; i < 8; i++) {
            map[i][0] = 1;
            map[i][6] = 1;
        }
        //挡板
        map[3][1] = 1;
        map[3][2] = 1;

        System.out.println("原地图：");
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 7; j++) {
                System.out.print(map[i][j] + " ");
            }
            System.out.println();
        }

        //设置起点
        // setWay(map, 1, 1);
        setWay2(map, 1, 1);

        //新的地图，标识过的
        System.out.println("走过的路径：");
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 7; j++) {
                System.out.print(map[i][j] + " ");
            }
            System.out.println();
        }
    }

    /**
     * @param map 地图
     * @param i 起始位置
     * @param j
     * @return true ,false
     * 当 map[i][j]为 0：还没有走的点，1：墙，2：走过的路径，3：走不通的点，(6,5)为终点
     * 策略一: 下 → 右 → 上 → 左，走不通，再回溯
     * 策略二：下 → 左 → 上 → 右
     * 策略三：上 → 右 → 下 → 左
     * 策略很多，可以自己尝试修改，本次使用的策略为策略一，但是存在最优路径
     */
    public static boolean setWay(int[][] map, int i, int j) {
        if (map[6][5] == 2) {
            return true;
        } else {
            if (map[i][j] == 0) {
                // 假设可以走
                map[i][j] = 2;
                //对应策略的顺序进行修改
                if (setWay(map, i + 1, j)) {
                    //向下走
                    return true;
                } else if (setWay(map, i, j + 1)) {
                    //向右走
                    return true;
                } else if (setWay(map, i - 1, j)) {
                    //向上走
                    return true;
                } else if (setWay(map, i, j - 1)) {
                    //向左走
                    return true;
                } else {
                    //走不通的起点
                    map[i][j] = 3;
                    return false;
                }
            } else {
                return false;
            }
        }
    }

    /**
     * 策略三：上 → 右 → 下 → 左
     * @param map
     * @param i
     * @param j
     * @return
     */
    public static boolean setWay2(int[][] map, int i, int j) {
        if (map[6][5] == 2) {
            return true;
        } else {
            if (map[i][j] == 0) {
                // 假设可以走
                map[i][j] = 2;
                //对应策略的顺序进行修改
                if (setWay2(map, i - 1, j)) {
                    //向上走
                    return true;
                } else if (setWay2(map, i, j + 1)) {
                    //向右走
                    return true;
                } else if (setWay2(map, i + 1, j)) {
                    //向下走
                    return true;
                } else if (setWay2(map, i, j - 1)) {
                    //向左走
                    return true;
                } else {
                    //走不通的起点
                    map[i][j] = 3;
                    return false;
                }
            } else {
                return false;
            }
        }
    }
}
```



## 八皇后问题（92种）

问题描述：在一个8 × 8 的国际象棋摆放 8个皇后，使其不能互相攻击

要求：任意两个皇后都不能处于同一列、同一行或者同一斜线上，问有多少种摆法



### 分析

1. 第一个皇后先放第一行第一列
2. 第二个皇后放在第二行第一列、然后判断是否OK， 如果不OK，继续放在 第二列、第三列、依次把所有列都放完，找到一个合适
3. 继续第三个皇后，还是第一列、第二列……直到第8个皇后也能放在一个 不冲突的位置，算是找到了一个正确解
4. 当得到一个正确解时，在栈回退到上一个栈时，就会开始回溯，即将第 一个皇后，放到第一列的所有正确解，全部得到.
5. 然后回头继续第一个皇后放第二列，后面继续循环执行 1,2,3,4的步骤

说明：

- 理论上应该创建一个二维数组来表示棋盘，但是实际上可以通过算法， 用一个一维数组即可解决问题. arr[8] = {0 , 4, 7, 5, 2, 6, 1, 3} 
- 对应arr 下标表示第几行，即第几个皇后，arr[i] = val , val 表示第 i + 1 个皇后，放在第 i + 1行的 第val+1列

~~~java
package com.recursion;

/**
 * @author Kcs 2022/8/28
 */
public class Queue8 {

    /**
     * 皇后总数
     */
    int max = 8;

    /**
     * 定义数组array，保留皇后放置的位置
     */
    int[] array = new int[max];

    /**
     * 统计一共有多少种解法
     */
    static int count = 0;

    public static void main(String[] args) {
        //测试
        Queue8 queue8 = new Queue8();
        queue8.check(0);
        System.out.printf("共有解法：%d", count);
    }

    /**
     * 放置第n个皇后
     * check每一次递归时，都会进入到for循环
     */
    private void check(int n) {
        //8皇后已经放完
        if (n == max) {
            print();
            return;
        }
        //依次放入皇后，并判断是否冲突
        for (int i = 0; i < max; i++) {
            //本皇后n，放置行的首列
            array[n] = i;
            //皇后放置第i列，判断是否与前面的皇后的列是否冲突

            if (judge(n)) {
                //不冲突，接着下一个皇后， 递归
                check(n + 1);
            }
            //冲突，回去到上一行 array[n] = i，将第n个皇后，放置在本行的后移一个位置
        }
    }


    /**
     * 查看放置的皇后是否与前面放置的皇后是否产生冲突
     * n: 第n个皇后
     */
    private boolean judge(int n) {
        for (int i = 0; i < n; i++) {
            //判断皇后是否在同一列上，或者统一斜线上(Math.abs(n - i) == Math.abs(array[n] - array[i] n:表示列上，
            // 比如 n = 1 时，array[n] = array[1] = 1 ,arr[i] = val , val 表示第i+1个皇后，放在第i+1行的第val+1列
            // 同一行就不要判断， n不断在增加
            if (array[i] == array[n] || Math.abs(n - i) == Math.abs(array[n] - array[i])) {
                return false;
            }
        }
        return true;
    }

    /**
     * 输出皇后的位置
     */
    public void print() {
        count++;
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i] + " ");
        }
        System.out.println();
    }
}

~~~



# 排序算法



- 排序是一种数据结构，不是算法，指定的顺序进行排序的过程。



## 内部排序

- 将需要处理的所有数据都加载到内存处理器中去进行排序



## 外部排序

- 数据量过大，无法全部加载到内 存中，需要借助外部存储进行 排序



## 常见排序算法

~~~mermaid
graph LR
a(排序) -->b1(内部排序 : 使用内存)
a(排序) -->b2(外部排序:内存外存结合)
b1(内部排序:使用内存)-->c1(插入排序)
b1(内部排序:使用内存)-->c2(选择排序)
b1(内部排序:使用内存)-->c3(交换排序)
b1(内部排序:使用内存)-->c4(归并排序)
b1(内部排序:使用内存)-->c5(基数排序)
c1(插入排序)-->c11(直接插入排序)
c1(插入排序)-->c12(希尔排序)
c2(选择排序)-->c21(简单选择排序)
c2(选择排序)-->c22(堆排序)
c3(交换排序)-->c31(冒泡排序)
c3(交换排序)-->c32(快速排序)
~~~

## 算法时间复杂度

### 度量一个程序(算法)执行时间的两种方法



1. 事后统计的方法

   存在两个问题：一是要想对设计的算法的运行性能进行评测，需要实际运行该程序；

   ​					     二是所得时间的统计量依赖于计算机的硬件、软件等环境因素, 要在同一台计算机的相同状态下运行，才能比较那个算法速度更快。

   

2. 事前估算的方法

   通过分析某个算法的时间复杂度来判断哪个算法更优



### 时间频率

一个算法花费的时间与算法中语句的执行次数成正比例，哪个算法 中语句执行次数多，它花费时间就多。一个算法中的语句执行次数称为语句频 度或时间频度。记为T(n)。



####  举例

![image-20220828222143139](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220828222143139.png)

![image-20220828222124713](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220828222124713.png)

![image-20220828221828310](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220828221828310.png)

### 时间复杂度

1. 一般情况下，算法中的基本操作语句的重复执行次数是问题规模n的某个函 数，用T(n)表示，若有某个辅助函数f(n)，使得当n趋近于无穷大时，T(n) / f(n)  的极限值为不等于零的常数，则称f(n)是T(n)的同数量级函数。记作 T(n)=Ｏ ( f(n) )，称Ｏ( f(n) ) 为算法的渐进时间复杂度，简称时间复杂度。
2. T(n) 不同，但时间复杂度可能相同。 如：T(n)=n²+7n+6 与 T(n)=3n²+2n+2 它 们的T(n) 不同，但时间复杂度相同，都为O(n²)。
3. 计算时间复杂度
   - 用常数1代替运行时间中的所有加法常数 T(n)=n²+7n+6 => T(n)=n²+7n+1
   - 修改后的运行次数函数中，只保留最高阶项 T(n)=n²+7n+1 => T(n) = n²
   - 去除最高阶项的系数 T(n) = n²=> T(n) = n² => O(n²)

![image-20220828223739873](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220828223739873.png)

- 平方阶：2个 for 循环

常见的算法时间复杂度由小到大依次为：Ο(1)＜Ο(log2^n^)＜Ο(n)＜Ο(nlog2^n^)＜Ο(n ^2^ )＜ Ο(n^3^ )＜ Ο(n^k^ ) ＜Ο(2n ) ，随着问题规模n的不断增大，上述时间复杂度不断增大，算法的 执行效率越低



1. 常数阶

   无论代码执行了多少行，只要是没有循环等复杂结构，那这个代码的时间复杂度就都是O(1)

   ~~~java
   int i = 2;
   int j = 3;
   ++i;
   j++;
   int m = i+j;
   ~~~

   它消耗的时候并不随着某个变量的增长而增长，那么无论这类代 码有多长，即使有几万几十万行，都可以用O(1)来表示它的时间复杂度

2. 对数阶O(log2^n^)

   ~~~java
   int i = 1;
   while(i<n){
   	i = i*2;
   }
   ~~~

   在while循环里面，每次都将 i 乘以 2，乘完之后，i 距离 n 就越来越近了。假设循环 x次之后，i 就大于 2 了，此时这个循环就退出了，也就是说 2 的 x 次方等于 n，那么 x =  log2n也就是说当循环 log2n 次以后，这个代码就结束了。因此这个代码的时间复杂度为： O(log2n) 。 O(log2n) 的这个2 时间上是根据代码变化的，i = i * 3 ，则是 O(log3n) 

3. 线性阶O(n)

   ~~~java
   for(i=1,i<=n,i++){
   	j =i;
   	j++;
   }
   ~~~

   这段代码，for循环里面的代码会执行n遍，因此它消耗的时间是随着n的变化而变 化的，因此这类代码都可以用O(n)来表示它的时间复杂度

4. 线性对数阶O(nlogN)

   ~~~java
   for(i=1,i<=n,i++){
   	i = 1;
   	while(i<n){
   		i = i*2;
   	}
   }
   ~~~

   将时间复杂度为O(logn)的代码循环N遍的 话，那么它的时间复杂度就是 n * O(logN)，也就是了O(nlogN)

5. 平方阶O(n^2^)

   ~~~java
   for(i=1,i<=n,i++){
   	for(j=1,j<=n,j++){
   		j = i;
   		j++;
   	}
   }
   ~~~

   如果把 O(n) 的代码再嵌套循环一遍，它的时间复杂 度就是 O(n²)，这段代码其实就是嵌套了2层n循环，它的时间复杂度就是 O(n * n)， 即 O(n²) 如果将其中一层循环的n改成m，那它的时间复杂度就变成了 O(m * n)

6. 立方阶O(n³)、K次方阶O(n^k^)

### 平均时间复杂度和最坏时间复 杂度

- 平均时间复杂度是指所有可能的输 入实例均以等概率出现的情况下， 该算法的运行时间。
- 最坏情况下的时间复杂度称最坏时 间复杂度。一般讨论的时间复杂度 均是最坏情况下的时间复杂度。 原因是：最坏情况 下的时间复杂度是算法在任何输入实例上运行时间的界限，这就保证 了算法的运行时间不会比最坏情况更长。

![image-20220901092550077](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220901092550077.png)

## 空间复杂度

- 一个算法的空间复杂度(Space Complexity)定义为该 算法所耗费的存储空间，它也是问题规模 n 的函数
- 空间复杂度(Space Complexity)是对一个算法在运行过程中临时占用存储空间大 小的量度。有的算法需要占用的临时工作单元数与解决问题的规模n有关，它 随着n的增大而增大，当n较大时，将占用较多的存储单元

## 一、冒泡排序 Bubble Sorting

### 基本思想

​	通过对待 排序序列从前向后（从下标较小的元素开始）,依次比较 相邻元素的值，若发现逆序则交换，使值较大 的元素逐渐从前移向后部，就象水底下的气泡一样逐渐 向上冒。

### 优化

​	因为排序的过程中，各元素不断接近自己的位置，如果一趟比较下 来没有进行过交换，就说明序列有序，因此要在排序过程中设置 一个标志flag判断元素是否进行过交换。从而减少不必要的比较

![image-20220902085505920](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220902085505920.png)

### 分析

冒泡数组：3 ，9， -1， 10， -5

- 使用冒泡排序法将其排成一个从小到大的有序数列
- 相邻元素逆序就交换

### 结论

1. 循环次数：数组长度 - 1 次
2. 每一趟排序的次数不断减少
3. 某一趟排序中，没有进行一次交换，则说明是有序排序（优化）

```java
import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Date;

/**
 * @author Kcs 2022/9/2
 */
public class BubbleSorting {
    public static void main(String[] args) {
        //排序数组
        int[] array = {3, 9, -1, 10, 20};
        System.out.println("原始冒泡数组：" + Arrays.toString(array));
        bubbleSort(array);
        System.out.println("排序结果：" + Arrays.toString(array));

        // 测试冒泡排序的时间复杂度, 用一个较大的数据进行测试
        int[] test = new int[8000];
        for (int i = 0; i < 8000; i++) {
            test[i] = (int) (Math.random() * 80000);

        }
        Date beforeDate = new Date();
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String formatBefore = simpleDateFormat.format(beforeDate);
        System.out.println("排序前时间" + formatBefore);

        bubbleSort(test);

        Date afterDate = new Date();
        String afterDateformat = simpleDateFormat.format(afterDate);
        System.out.println("排序前时间" + afterDateformat);
    }


    //封装冒泡方法
    public static void bubbleSort(int[] arr) {

        //表示是否进行交换
        boolean flag = false;

        int temp;
        //第一趟排序
        for (int i = 0; i < arr.length - 1; i++) {
            for (int j = 0; j < arr.length - 1 - i; j++) {
                //前面的比后面的数大，就进行交换
                if (arr[j] > arr[j + 1]) {
                    flag = true;
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                }
            }

            // System.out.println("第" + (i + 1) + "次排序结果：" + Arrays.toString(arr));

            if (!flag) {
                //没有发生交换
                break;
            } else {
                //重置flag ,进行下次交换
                flag = false;
            }
        }
    }

}
```

## 二、选择排序 （Select Sorting）

​	选择式排序也属于内部排序法，是从欲排序的数据中，按指定的规则选出某一 元素，再依规定交换位置后达到排序的目的。

### 思路

第 一次从arr[0] ~ arr[n-1]中选取最小值，与arr[0]交换，第二次从 arr[1] ~ arr[n-1]中选取最小值，与arr[1]交换，第三次从arr[2]~ arr[n-1]中 选取最小值，与arr[2]交换，…，第i次从arr[i-1] ~ arr[n-1]中选取最小值， 与arr[i-1]交换，…, 第n-1次从arr[n-2]~arr[n-1]中选取最小值，与arr[n-2] 交换，总共通过n-1次，得到一个按排序码从小到大排列的有序序列。

![image-20220902220027274](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220902220027274.png)

### 分析

原始数组 ： 101，34，119，1，要求：**由小到大**

每次执行的得到的结果：

1. 1，34，119，101
2. 1，34，119，101
3. 1，34，101，119



### 结论

1. 需要执行数组大小 -1轮排序
2. 每一轮都是一个循环，循环的规则（代码）
   1. 先假定当前数为最小数，
   2. 然后和后面的数进行比较，若当前数更小，重新得到最小数，并得到下标
   3. 遍历到数组的最后时，就得到本轮的最小数和下标
   4. 交换

```java
import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Date;

/**
 * @author Kcs 2022/9/2
 */
public class SelectSorting {
    public static void main(String[] args) {
        int[] arr = {101, 34, 119, 1};
        System.out.println("排序前：" + Arrays.toString(arr));
        selectSort(arr);
        System.out.println("排序后：" + Arrays.toString(arr));

        //测试时间
        int[] test = new int[8000];
        for (int i = 0; i < 8000; i++) {
            test[i] = (int) (Math.random() * 80000);

        }
        Date beforeDate = new Date();
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String formatBefore = simpleDateFormat.format(beforeDate);
        System.out.println("排序前时间" + formatBefore);

        selectSort(test);

        Date afterDate = new Date();
        String afterDateformat = simpleDateFormat.format(afterDate);
        System.out.println("排序前时间" + afterDateformat);

    }

    /**
     * 选择排序
     * 时间复杂度 O(n^2)
     * @param arr
     */
    public static void selectSort(int[] arr) {

        //原始数组 ： 101，34，119，1，要求：由小到大

        for (int i = 0; i < arr.length - 1; i++) {
            //起始索引
            int minIndex = i;
            int min = arr[i];
            for (int j = i + 1; j < arr.length; j++) {
                //由大到小：>  由小到大：< ；当前值进行比较，找出索引
                if (min > arr[j]) {
                    min = arr[j];
                    // 得到最小值索引
                    minIndex = j;
                }
            }

            //最小值放在arr[0]
            if (minIndex != i) {
                arr[minIndex] = arr[i];
                arr[i] = min;
            }
            // System.out.println("第" + (i + 1) + "轮排序结果：" + Arrays.toString(arr));

        }
    }
}
```



## 三、插入排序

​	插入式排序属于内部排序法，是对于欲排序的元素以插入的方式找寻该元素的 适当位置，以达到排序的目的

### 基本思想

​	把n个待排序的元素看成为 一个有序表和一个无序表，开始时有序表中只包含一个元素，无序表中 包含有n-1个元素，排序过程中每次从无序表中取出第一个元素，把它 的排序码依次与有序表元素的排序码进行比较，将它插入到有序表中的 适当位置，使之成为新的有序表。

![image-20220902231718276](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220902231718276.png)

### 分析

原始数组：101, 34, 119, 1



```java
import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Date;

/**
 * @author Kcs 2022/9/3
 */
public class InsertSort {
    public static void main(String[] args) {
        int[] arr = {101, 34, 119, 1, 45, 78};
        System.out.println("排序前结果：" + Arrays.toString(arr));
        insertSort(arr);
        System.out.println("排序后结果：" + Arrays.toString(arr));


        // 测试冒泡排序的时间复杂度, 用一个较大的数据进行测试
        int[] test = new int[8000];
        for (int i = 0; i < 8000; i++) {
            test[i] = (int) (Math.random() * 80000);

        }
        Date beforeDate = new Date();
        SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String formatBefore = simpleDateFormat.format(beforeDate);
        System.out.println("排序前时间" + formatBefore);

        insertSort(test);

        Date afterDate = new Date();
        String afterDateformat = simpleDateFormat.format(afterDate);
        System.out.println("排序后时间" + afterDateformat);
    }

    /**
     * 插入排序
     */
    public static void insertSort(int[] arr) {
        int insertValue = 0;
        int insertIndex = 0;

        for (int i = 1; i < arr.length; i++) {
            //定义待插入的数
            insertValue = arr[i];

            //arr[1] 前面这个数的索引
            insertIndex = i - 1;

            //insertValue 找到插入的位置  由小到大 < ；由大到小：<
            // insertIndex >= 0 放置越界
            // insertValue < arr[insertIndex] : 带插入的数字
            // arr[insertIndex] 后移
            while (insertIndex >= 0 && insertValue < arr[insertIndex]) {
                arr[insertIndex + 1] = arr[insertIndex];
                insertIndex--;
            }
            //找到插入的位置
            if (insertIndex + 1 == i) {
                arr[insertIndex + 1] = insertValue;
            }
            // System.out.println("第" + i + "轮排序结果：" + Arrays.toString(arr));
        }
    }
}
```



## 四、希尔排序



### 基本思想

​	希尔排序是把记录按下标的一定增量分组，对每组使用直接插入排序算法排序；随着增量逐渐减少，每组包含的关键词越来越多，当增量减至1时，整个文件恰 被分成一组，算法便终止



### 分析

初始数组 {8,9,1,7,2,3,5,4,6,0} 

1. 希尔排序时， 对有序序列在插入时采用交换法, 并测试排序速度.
2. 希尔排序时， 对有序序列在插入时采用移动法, 并测试排序速度

![image-20220903094604723](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903094604723.png)

交换法：

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/3
 */
public class ShellSort {
    public static void main(String[] args) {
        int[] arr = {8, 9, 1, 7, 2, 3, 5, 4, 6, 0};
        shellSort(arr);
    }

    /**
     * 希尔排序
     */
    public static void shellSort(int[] arr) {

        int temp = 0;
        int count = 0;
        // 循环处理 希尔排序
        for (int gap = arr.length / 2; gap > 0; gap /= 2) {
            for (int i = gap; i < arr.length; i++) {
                //遍历各组中所有的元素
                for (int j = i - gap; j >= 0; j -= gap) {
                    //当前元素大于加上步长后的元素，则进行交换
                    if (arr[j] > arr[j + gap]) {
                        temp = arr[j];
                        arr[j] = arr[j + gap];
                        arr[j + gap] = temp;
                    }
                }
            }
            System.out.println("第" + (++count) + "轮希尔排序结果：" + Arrays.toString(arr));
        }
    }
}
```



移步法

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/3
 */
public class ShellSort {
    public static void main(String[] args) {
        int[] arr = {8, 9, 1, 7, 2, 3, 5, 4, 6, 0};
        shellSort(arr);
        System.out.println("交换法：" + Arrays.toString(arr));

        shellSort2(arr);
        System.out.println("移位法：" + Arrays.toString(arr));
        
    }
    /**
     * 移位法
     * @param arr
     */
    public static void shellSort2(int[] arr) {
        for (int gap = arr.length / 2; gap > 0; gap /= 2) {
            //从gap个元素，逐个对其所在组进行之直接插入排序
            for (int i = gap; i < arr.length; i++) {
                int j = i;
                int temp = arr[j];
                if (arr[j] < arr[j - gap]) {
                    while (j - gap >= 0 && temp < arr[j - gap]) {
                        // 元素进行移动
                        arr[j] = arr[j - gap];
                        j -= gap;
                    }
                    //找到插入的位置
                    arr[j] = temp;
                }
            }
        }
    }
}
```



## 五、快速排序



### 基本思想

​	通过一趟排序 将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分 的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个 排序过程可以递归进行，以此达到整个数据变成有序序列

![image-20220903102405691](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903102405691.png)

左右递归有顺序

![image-20220903103631161](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903103631161.png)

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/3
 */
public class QuickSort {
    public static void main(String[] args) {
        int[] arr = {-9, 78, 0, 23, -567, 70};
        quickSort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr));
    }

    /**
     * 快速排序
     * @param arr
     */
    public static void quickSort(int[] arr, int left, int right) {
        //左下标
        int l = left;
        //右下标
        int r = right;
        //中轴值
        int pivot = arr[(left + right) / 2];

        //作为交换
        int temp = 0;

        // 比 pivot 小的值 放到左边，大的值放到右边
        while (l < r) {
            //在pivot的左边找，比pivot大于等于的值
            while (arr[l] < pivot) {
                l += 1;
            }
            //在pivot的右边找，比pivot小于等于的值
            while (arr[r] > pivot) {
                r -= 1;
            }
            //左边是小于pivot的值， 右边大于等于pivot的值
            if (l == r) {
                break;
            }
            //进行交换
            temp = arr[l];
            arr[l] = arr[r];
            arr[r] = temp;

            //交换后，发现arr[l] == pivot 值 ,则前移
            if (arr[l] == pivot) {
                r -= 1;
            }
            //交换后，发现arr[r] == pivot 值 ,则后移
            if (arr[r] == pivot) {
                l += 1;
            }
        }
        // l==r 要 l++ r--
        if (l == r) {
            l += 1;
            r -= 1;
        }
        //左递归
        if (left < r) {
            quickSort(arr, left, r);
        }
        //右递归
        if (right > l) {
            quickSort(arr, l, right);
        }
    }
}
```

## 六、归并排序



​	采用分治策略。分治法将问题分 (divide) 成一些小的问 题然后递归求解，而治(conquer) 的阶段则将分的阶段得到的各答案"修补"在一 起，即分而治之。

![image-20220903153717766](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903153717766.png)

​	以上结构很像一棵完全二叉树，采用递归去实现（也可采用迭代的方式去实现）。分阶段可以理解为就是递归 拆分子序列的过程

### 分析

上图合并了七次，下图为最后一次的合并详解：

![image-20220903154707564](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903154707564.png)

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/3
 */
public class MergeSort {
    public static void main(String[] args) {
        int[] arr = {8, 4, 5, 7, 1, 3, 6, 2};


        System.out.println("要排序的数组:" + Arrays.toString(arr));
        //归并需要一个额外的空间
        int[] temp = new int[arr.length];

        mergeSort(arr, 0, arr.length - 1, temp);

        System.out.println("归并排序结果：" + Arrays.toString(arr));
    }

    /**
     * 分解 + 合并 过程
     */
    public static void mergeSort(int[] arr, int left, int right, int[] temp) {
        if (left < right) {
            int mid = (left + right) / 2;
            // 向左递归进行分解
            mergeSort(arr, left, mid, temp);

            //向右递归分解
            mergeSort(arr, mid + 1, right, temp);

            //合并
            merge(arr, left, mid, right, temp);
        }
    }


    /**
     * 合并起来
     * @param arr 原始数组
     * @param left 左边有序序列的初始索引
     * @param mid 中间索引
     * @param right 右边索引
     * @param temp 做中转数组
     */
    public static void merge(int[] arr, int left, int mid, int right, int[] temp) {
        // 初始化i 左边有序序列的初始索引
        int i = left;
        // 初始化 j ,右边有序序列的初始索引
        int j = mid + 1;
        // 指向temp数组的当前索引
        int t = 0;

        // 1. 左右两边的数据，按照规则进行填充到 temp 数组，直到左右两边的有序序列，有一边完成为止
        while (i <= mid && j <= right) {
            //左边的有序序列的当前元素，小于等于右边有序序列的当前元素，即将左边的当前元素，拷贝到 temp 中
            if (arr[i] < arr[j]) {
                temp[t] = arr[i];
                t += 1;
                i += 1;
            } else {
                // 右边的比左边的元素大，填充到temp数据
                temp[t] = arr[j];
                t += 1;
                j += 1;

            }
        }


        // 2. 把剩余数据的一边的数据依次全部填充到 temp 中
        while (i <= mid) {
            //左边的 有序序列还有剩余元素，全部填充到 temp 中去
            temp[t] = arr[i];
            t += 1;
            i += 1;
        }

        while (j <= right) {
            //左边的 有序序列还有剩余元素，全部填充到 temp 中去
            temp[t] = arr[j];
            t += 1;
            j += 1;
        }

        // 3. 将temp 数据的元素拷贝到 arr,并不是每次拷贝所有
        t = 0;
        int tempLeft = left;
        //最后一次 tempLeft = 0 ,right = 7
        System.out.println("tempLeft=" + tempLeft + " " + "right=" + right);
        while (tempLeft <= right) {
            arr[tempLeft] = temp[t];
            t += 1;
            tempLeft += 1;
        }
    }
}
```



## 七、基数排序（桶排序）

1.  基数排序（radix sort）属于“分配式排序”（distribution sort），又称“桶子法”（bucket sort）或bin sort
2. 它是通过键值的各个位的值， 将要排序的元素分配至某些 “桶” 中，达到排序的作用。
3. 基数排序法是属于稳定性的排序，基数排序法的是效率高的稳定性排序法（相同的数字会有先后顺序）

### 基本思想

- 将所有待比较数值统一为同样的数位长度，数位较短的数前面补零。然后，从最低位开始，依次进行一次排序。这样从最低位排序一直到最高位排序完 成以后, 数列就变成一个有序序列

### 分析

将数组 {53, 3, 542, 748, 14, 214} 使用基数排序, 进行升序排序。==有多少位数就要进行多少次桶排序==

说明： 事先准备10个数组(10个桶)， 0-9 分别对应位数的 0-9

1. 第1轮排序

   1. 将各个数，按照==个位==大小放入到对应的各个数组中 （看每个元素的个位数，把这个多位数，放置在个位数对应的桶中（一个桶一个数组））

   2. 然后从 0-9 个数组 / 桶，依次按照加入元素的先后顺序取出

      ![image-20220903170419527](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903170419527.png)

   3. 得到结果 ：542 、53、3、14、214、748

2. 第二轮排序 （后一轮是根据上一轮得到的结果进行排序）

   1.  将各个数，按照 ==十位== 大小放入到对应的各个 数组 / 桶 中

   2. 然后从 0-9 个数组 / 桶，依次按照加入元素的先后顺序取出 

      ![image-20220903171202967](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903171202967.png)

   3. 得到结果：3、14、214、542、748、53

3. 第三轮

   1. 将各个数，按照 ==百位== 大小放入到对应的各个数组 / 桶中

   2. 然后从 0-9 个数组 / 桶，依次按照加入元素的先后顺序取出

      ![image-20220903171511702](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220903171511702.png)

   3. 得到结果：3 、14、 53、 214、 542、 748

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/3
 */
public class RadixSort {
    public static void main(String[] args) {
        int[] arr = {53, 3, 542, 748, 14, 214};
        radixSort(arr);

    }

    /**
     * 基数排序  时间换空间算法
     * @param arr
     */
    public static void radixSort(int[] arr) {
        //第一轮(每个元素的个位数进行处理)

        //二维数组表示十个桶，每个桶就是一个一维数组
        //防止数据溢出，将一维数组大小为arr.length

        int[][] bucket = new int[10][arr.length];
        //记录桶放入的有效数据中，实际存放的数据。存放bucket[0~10]的对应的数据
        int[] bucketElementCounts = new int[10];

        //得到数组中最大的数的位数
        int max = arr[0];
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > max) {
                max = arr[i];
            }
        }
        //得到最大的位数
        int maxLength = (max + "").length();


        for (int i = 0, n = 1; i < maxLength; i++, n *= 10) {
            //取出各位 个 十 百 千 位
            for (int j = 0; j < arr.length; j++) {
                //取出每个元素对应位数的值
                int digitOfElment = arr[j] / n % 10;

                //放入对应的桶中,前一个找到对应的桶，后一个为该个位对应的多位数
                bucket[digitOfElment][bucketElementCounts[digitOfElment]] = arr[j];
                //下一个桶
                bucketElementCounts[digitOfElment]++;
            }
            //依次桶的顺序，依次取出数据，放入原来的数组
            int index = 0;

            //遍历每一个桶，就将桶的数据，放入到原数组中，
            for (int k = 0; k < bucketElementCounts.length; k++) {
                //桶中有数据才放入原数组
                if (bucketElementCounts[k] != 0) {
                    //循环改桶的数据，放入原数组
                    for (int l = 0; l < bucketElementCounts[k]; l++) {
                        //取出元素放入 arr
                        arr[index++] = bucket[k][l];
                    }
                }
                //对桶进行清零
                bucketElementCounts[k] = 0;
            }
            System.out.println("第" + (i + 1) + "次排序结果:" + Arrays.toString(arr));
        }


        //以下为推导过程
        /*//第二轮：取出十位
        for (int j = 0; j < arr.length; j++) {
            //得到十位的数 每一轮只要修改这个取模的 个 十 百 千 位
            int digitOfElment = arr[j] / 10 % 10;

            //放入对应的桶中,前一个找到对应的桶，后一个为该个位对应的多位数
            bucket[digitOfElment][bucketElementCounts[digitOfElment]] = arr[j];
            //下一个桶
            bucketElementCounts[digitOfElment]++;
        }
        //依次桶的顺序，依次取出数据，放入原来的数组
        index = 0;

        //遍历每一个桶，就将桶的数据，放入到原数组中，
        for (int k = 0; k < bucketElementCounts.length; k++) {
            //桶中有数据才放入原数组
            if (bucketElementCounts[k] != 0) {
                //循环改桶的数据，放入原数组
                for (int l = 0; l < bucketElementCounts[k]; l++) {
                    //取出元素放入 arr
                    arr[index++] = bucket[k][l];
                }
            }
            //对桶进行清零
            bucketElementCounts[k] = 0;
        }
        System.out.println("第二轮结果:" + Arrays.toString(arr));

        //第三轮：取出白位
        for (int j = 0; j < arr.length; j++) {
            //得到十位的数 每一轮只要修改这个取模的 个 十 百 千 位
            int digitOfElment = arr[j] / 100;

            //放入对应的桶中,前一个找到对应的桶，后一个为该个位对应的多位数
            bucket[digitOfElment][bucketElementCounts[digitOfElment]] = arr[j];
            //下一个桶
            bucketElementCounts[digitOfElment]++;
        }
        //依次桶的顺序，依次取出数据，放入原来的数组
        index = 0;

        //遍历每一个桶，就将桶的数据，放入到原数组中，
        for (int k = 0; k < bucketElementCounts.length; k++) {
            //桶中有数据才放入原数组
            if (bucketElementCounts[k] != 0) {
                //循环改桶的数据，放入原数组
                for (int l = 0; l < bucketElementCounts[k]; l++) {
                    //取出元素放入 arr
                    arr[index++] = bucket[k][l];
                }
            }
            //对桶进行清零
            bucketElementCounts[k] = 0;
        }
        System.out.println("第三轮结果:" + Arrays.toString(arr));*/
    }
}
```



## 排序算法对比

![image-20220904153537107](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220904153537107.png)

### 解释：

1. 稳定：如果 a原本在 b前面，而a=b ， 排序之后 a仍然在 b的前面；
2. 不稳定：如果 a原本在 b的前面，而 a=b，排序之后 a可能会出现在 b的后 面； 
3. 内排序：所有排序操作都在内存中完 成；
4. 外排序：由于数据太大，因此把数据 放在磁盘中，而排序通过磁盘和内存 的数据传输才能进行；
5. 时间复杂度： 一个算法执行所耗费 的时间。 
6. 空间复杂度：运行完一个程序所需内 存的大小。
7. n：数据规模
8. k：“桶”的个数 
9. In -place：不占用额外内存 
10. Out -place：占用额外内存



# 查找算法



## 顺序（线性查找）查找

- 从头到尾一个一个进行对比查找，找到则返回下标

```java
/**
 * @author Kcs 2022/9/5
 */
public class SequenceSearch {
    public static void main(String[] args) {
        //数组
        int[] arr = {1 ,-25, 45, 32, 3, 0, 12, -20};
        int index = seqSearch(arr, 0);
        if (index == -1) {
            System.out.println("查无次数据");
        } else {
            System.out.println("该数字位于:" + index);
        }
    }

    /**
     * 找到一个就返回
     * @param arr 匹配数组
     * @param value 要查找的数
     * @return index
     */
    public static int seqSearch(int[] arr, int value) {
        //逐一比对
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == value) {
                return i;
            }
        }
        return -1;
    }
}
```

## 二分查找 / 折半查找

- 必须是顺序的数组，若是无序的，则需要先排序（小到大 / 大到小）

### 思路

（以下是排序已为由小到大）

1. 首先确定该数组的中间下标
   - mid = （left + right）/ 2
2. 然后让需要查找的数 findValue 和 arr[mid] 进行比较
   1. findValue > mid[arr] ：说明要查找的数在 mid 的右边，应该向右查找（向右递归查找）
   2. findValue < mid[arr] ：说明要查找的数在 mid 的左边，应该向左查找（向左递归查找）
   3. findValue = mid[arr] ：说明已经找到，则返回
3. 退出递归
   1. 找到目标退出递归
   2. 找不到退出递归 （==left > right==）

```java
/**
 * @author Kcs 2022/9/5
 */
public class BinarySearch {
    public static void main(String[] args) {
        //有序数组
        int[] arr = {0, 11, 22, 33, 44, 45, 55, 77, 88, 88, 88, 88, 99};
        // int index = binarySearch(arr, 0, arr.length - 1, 12);
        // System.out.println("index=" + index);
        List<Integer> integers = binarySearch2(arr, 0, arr.length - 1, 99);
        System.out.println(integers);

    }

    /**
     * 二分查找算法
     * @param arr 查找数组
     * @param left 左边索引
     * @param right 右边索引
     * @param findValue 查找的值
     * @return index
     */
    public static int binarySearch(int[] arr, int left, int right, int findValue) {

        //没有找到
        if (left > right) {
            return -1;
        }

        //中间索引
        int mid = (left + right) / 2;

        //中间值
        int midValue = arr[mid];

        //判断递归的方向
        //向右
        if (findValue > midValue) {
            return binarySearch(arr, mid + 1, right, findValue);
        } else if (findValue < midValue) {
            return binarySearch(arr, left, mid - 1, findValue);
        } else {

            //查找到所有相同的值，并返回
            return mid;
        }
    }

    /**
     * 查找重复的值索引
     * @param arr
     * @param left
     * @param right
     * @param findValue
     * @return
     */
    public static ArrayList<Integer> binarySearch2(int[] arr, int left, int right, int findValue) {

        //没有找到
        if (left > right) {
            return new ArrayList<Integer>();
        }

        //中间索引
        int mid = (left + right) / 2;

        //中间值
        int midValue = arr[mid];

        //判断递归的方向
        //向右
        if (findValue > midValue) {
            return binarySearch2(arr, mid + 1, right, findValue);
        } else if (findValue < midValue) {
            return binarySearch2(arr, left, mid - 1, findValue);
        } else {
            ArrayList<Integer> resIndexlist = new ArrayList<>();
            int temp = mid - 1;
            //向mid左边开始继续搜索
            while (true) {
                //退出
                if (temp < 0 || arr[temp] != findValue) {
                    break;
                }
                resIndexlist.add(temp);
                temp -= 1;
            }
            resIndexlist.add(mid);
            //向mid右边继续搜索
            temp = mid + 1;
            while (true) {
                if (temp > (arr.length - 1) || arr[temp] != findValue) {
                    break;
                }
                resIndexlist.add(temp);
                temp += 1;
            }
            return resIndexlist;
        }
    }
}
```





## 插值查找

1. 也是得用在==有序数组==上

2. 插值查找每次从自适应mid处开始查找

3. 将折半查找中的求mid 索引的公式 , low 表示左边索引left, high表示右边索引right. key 就是 findValue

   ![image-20220906222633930](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220906222633930.png)

   int mid = low + (high - low) * (key - arr[low]) / (arr[high] - arr[low]) ;

   对应前面的代码公式： int mid = left + (right – left) * (findVal – arr[left]) / (arr[right] – arr[left])

特点

- 可以一次就能查找想要的结果
- 与二分查找相比， 想过肯定的好很多的



### 使用场景

- 对于数据量较大，关键字分布比较均匀的查找表来说，采用插值查找, 速度较快
- 关键字分布不均匀的情况下，该方法不一定比折半查找要好

```java
/**
 * @author Kcs 2022/9/6
 */
public class InsertValueSearch {
    public static void main(String[] args) {
        //1 ~ 100 数组
        int[] array = new int[100];
        for (int i = 0; i < 100; i++) {
            array[i] = i + 1;
        }
        int index = insertValueSearch(array, 0, array.length - 1, 50);
        System.out.println("index = " + index);

    }

    /**
     * 插值查找算法
     * @param array 查找的数组
     * @param left 左边 索引
     * @param right 右边索引
     * @param findValue 查找的值
     * @return index
     */
    public static int insertValueSearch(int[] array, int left, int right, int findValue) {
        System.out.println("查找了！！！！");

        //不符合，则退出 优化查找，防止mid越界。自适应的查找
        if (left > right || findValue < array[0] || findValue > array[array.length - 1]) {
            return -1;
        }
        //求出mid
        int mid = left + (right - left) * (findValue - array[left]) / (array[right] - array[left]);
        //中间的值
        int midValue = array[mid];

        if (findValue > midValue) {
            //向右递归查找
            return insertValueSearch(array, mid + 1, right, findValue);
        } else if (findValue < midValue) {
            //向左递归查找
            return insertValueSearch(array, left, mid - 1, findValue);
        } else {
            //相等
            return mid;
        }
    }
}
```



## 斐波那契查找

​	斐波那契数列 {1, 1, 2, 3, 5, 8, 13, 21, 34, 55 ···} 发现斐波那契数 列的两个相邻数 的比例，无限接近黄金分割值0.618

### 原理

mid不 再是中间或插值得到，而是位于黄金分 割点附近，即mid=low+F(k-1)-1 （F代表斐波那契数列）

![image-20220907211854950](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220907211854950.png)

- 由斐波那契数列 F[k]=F[k-1]+F[k-2] 的性质，可以得到 （F[k]-1）=（F[k-1]-1）+（F[k-2]-1）+1 。 该式说明：只要顺序表的长度为F[k]-1，则可以将该表分成长度为F[k-1]-1和F[k-2]-1的两段，即如 上图所示。从而中间位置为mid=low+F(k-1)-1

- 顺序表长度n不一定刚好等于F[k]-1，所以需要将原来的顺序表长度n增加至F[k]-1。这里的k值只 要能使得F[k]-1恰好大于或等于n即可，由以下代码得到,顺序表长度增加后，新增的位置（从n+1到 F[k]-1位置），都赋为n位置的值即可

### 分析

有序数组进行斐波那契查找 {1,8, 10, 89, 1000, 1234}

```java
import java.util.Arrays;

/**
 * @author Kcs 2022/9/7
 */
public class FibonacciSearch {

    //斐波那契额数列的显示个数
    public static int maxSize = 20;

    public static void main(String[] args) {
        int[] arr = {1, 8, 10, 89, 1000, 1234};
        System.out.println(fibSearch(arr, 8));
    }


    /**
     * 20个斐波那契数列
     * @return f[]
     */
    public static int[] fib() {
        int[] f = new int[maxSize];
        f[0] = 1;
        f[1] = 1;
        for (int i = 2; i < maxSize; i++) {
            f[i] = f[i - 1] + f[i - 2];
        }
        return f;
    }

    /**
     * 斐波那契薯类
     * @param a 要在查找的数组
     * @param key 需要查找的关键值
     * @return index
     */
    public static int fibSearch(int[] a, int key) {
        //左边下标
        int low = 0;

        //右边下标
        int high = a.length - 1;

        //斐波那契分割数值的下标
        int k = 0;

        //mid
        int mid = 0;

        //获取斐波那契数列
        int[] f = fib();

        while (high > f[k] - 1) {
            k++;
        }

        //防止f[k] 大于 数组的长度,不足的时候使用 0 填充
        int[] temp = Arrays.copyOf(a, f[k]);

        //不使用0 进行填充，使用 arr数组的最后一位进行填充
        for (int i = high + 1; i < temp.length; i++) {
            temp[i] = a[high];
        }

        //查找目标值
        while (low <= high) {
            mid = low + f[k - 1] - 1;
            if (key < temp[mid]) {
                //查找前半部分（左边）
                high = mid - 1;
                k--;
            } else if (key > temp[mid]) {
                //向右边查找
                low = mid + 1;
                //f[k-1] = f[k -3]+f[k -4]
                k -= 2;
            } else {
                //查找到
                if (mid <= high) {
                    //左边mid
                    return mid;
                } else {
                    //右边的index
                    return high;
                }
            }
        }
        //没有找到
        return -1;
    }
}
```



# 哈希表

- 哈希表属于数据结构

散列表（Hash table，也叫哈希表）， 是根据关键码值(Key value)而直接进行访问的数据结构。它通过把关键码值映射到表中一个位置来访问记录，以加快查找的速度。这个映射函数叫做散列函数，存放记录的数组叫做散列表。

## 哈希表

![image-20220909200436898](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220909200436898.png)



## 思路

有一个公司,当有新的员工来报道时,要求将该员工的信息加入 (id,,名字，···),当输入该员工的id时,要求查找到该员工的所有信息

### 要求

- 不使用数据库,,速度越快越好=>哈希表(散列) 
- 添加时，保证按照id从低到高插入



### 实现思路

1. 使用链表来实现哈希表, 该链表不带表头 [即: 链表的第一个结点就存放雇员信息]  
2. ![image-20220909202217237](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220909202217237.png)
3. 代码实现[增删改查(显示所有员工，按id查询)]

### 散列函数

**散列函数能使对一个数据序列的访问过程更加迅速有效，通过散列函数，数据元素将被更快地定位。**

实际工作中需视不同的情况采用不同的哈希函数，通常考虑的因素有：

1. 计算哈希函数所需时间
2. 关键字的长度
3. 哈希表的大小
4. 关键字的分布情况
5. 记录的查找频率

### 散列函数的几种方法

1. 直接寻址法
2. 数字分析法
3. 平方取中法
4. 折叠法
5. 随机数法
6. 除留余数法

创建三个类

1. 雇员类：雇员的信息
2. 雇员链表类：管理雇员
3. 哈希表类：存放 n个 雇员，散列函数：使 id 对应的链表

```java

import java.util.Scanner;

/**
 * @author Kcs 2022/9/9
 */
public class HashTabDemo {
    public static void main(String[] args) {
        HashTab hashTab = new HashTab(7);

        //测试菜单
        String key = "";
        Scanner scanner = new Scanner(System.in);
        while (true) {
            System.out.println("add：添加雇员");
            System.out.println("list：显示雇员");
            System.out.println("find：查找雇员");
            System.out.println("delete：删除雇员");
            System.out.println("exit：退出系统");
            System.out.println("请选择add/list/find/delete/exit");

            key = scanner.next();
            switch (key) {
                case "add":
                    System.out.println("请添加员工id");
                    int id = scanner.nextInt();
                    System.out.println("请添加员工姓名");
                    String name = scanner.next();
                    // 创建雇员
                    Emp emp = new Emp(id, name);
                    hashTab.add(emp);
                    System.out.println("添加成功！");
                    break;
                case "list":
                    hashTab.list();
                    break;
                case "find":
                    System.out.println("请输入要查找雇员的id");
                    id = scanner.nextInt();
                    hashTab.findEmpByID(id);
                    System.out.println("查找成功！");
                    break;
                case "delete":
                    System.out.println("请输入要删除雇员的id");
                    id = scanner.nextInt();
                    hashTab.delEmp(id);
                    System.out.println("删除成功！");
                    break;
                case "exit":
                    scanner.close();
                    System.exit(0);
                    System.out.println("成功退出！");
                    break;
                default:
                    break;
            }
        }
    }
}

/**
 * 雇员类
 */
class Emp {
    /**
     * id
     */
    public int id;
    /**
     * 姓名
     */
    public String name;
    /**
     * next : null
     */
    public Emp next;

    public Emp(int id, String name) {
        this.id = id;
        this.name = name;
    }
}

/**
 * 哈希表 管理雇员
 */
class HashTab {
    //数组存放雇员信息
    private EmpLinkedList[] empLinkedListsArray;
    //链表总数
    private int size;

    /**
     * 构造
     * @param size 多少链表
     */
    public HashTab(int size) {
        this.size = size;
        //初始化 empLinkedListsArray
        empLinkedListsArray = new EmpLinkedList[size];

        //初始化每个链表
        for (int i = 0; i < size; i++) {
            empLinkedListsArray[i] = new EmpLinkedList();
        }
    }

    /**
     * 添加雇员
     */
    public void add(Emp emp) {
        //根据id 获得该员工的应该添加到的那一条链表
        int empLinkedListNo = hashFun(emp.id);
        // 添加到对应的链表种
        empLinkedListsArray[empLinkedListNo].add(emp);
    }

    /**
     * 遍历所有链表
     */
    public void list() {
        for (int i = 0; i < size; i++) {
            empLinkedListsArray[i].list(i);
        }
    }

    /**
     * 根据id 查找雇员
     */
    public void findEmpByID(int id) {
        //散列函数确定查找的链表
        int empLinkedListNo = hashFun(id);
        Emp emp = empLinkedListsArray[empLinkedListNo].findEmpById(id);
        if (emp != null) {
            System.out.printf("在第%d 条链表中找到 雇员 id = %d\n", (empLinkedListNo + 1), id);
        } else {
            System.out.println("在哈希表中，没有找到该雇员！");
        }
    }

    /**
     * 删除雇员信息
     * @param id 雇员id
     */
    public void delEmp(int id) {
        int i = hashFun(id);
        empLinkedListsArray[i].delete(id);
    }

    /**
     * 散列函数 取模
     */
    public int hashFun(int id) {
        return id % size;
    }

}


/**
 * 创建EmpLinkedList，表示链表
 */
class EmpLinkedList {
    /**
     * 头指针，指向第一个雇员的Emp
     */
    private Emp head;

    /**
     * 添加雇员
     * 添加的雇员id 自增长，id 总是从小到大，所有将该雇员添加到本链表的最后
     */
    public void add(Emp emp) {
        //第一个雇员
        if (head == null) {
            head = emp;
            return;
        }
        //不是第一个雇员,添加到链表最后
        Emp curEmp = head;
        while (true) {
            //到链表最后
            if (curEmp.next == null) {
                break;
            }
            //后移
            curEmp = curEmp.next;
        }
        //退出时，加入链表
        curEmp.next = emp;
    }

    /**
     * 遍历链表
     */
    public void list(int num) {
        //链表为空
        if (head == null) {
            System.out.println("第" + (num + 1) + "个链表为空!");
            return;
        }
        System.out.print("第" + (num + 1) + "链表的信息为：");
        Emp curEmp = head;
        while (true) {
            System.out.printf("=> id = %d ,name=%s\t", curEmp.id, curEmp.name);
            //curEmp到最后结点
            if (curEmp.next == null) {
                break;
            }
            //指针后移
            curEmp = curEmp.next;
        }
        System.out.println();
    }

    /**
     * 通过id查找雇员信息
     * @param id 雇员id
     * @return 雇员信息
     */
    public Emp findEmpById(int id) {
        //链表是否为空
        if (head == null) {
            System.out.println("链表为空！");
            return null;
        }
        Emp curEmp = head;
        //id 不重复
        while (true) {
            if (curEmp.id == id) {
                //curEmp指向要查找的雇员
                break;
            }
            //退出
            if (curEmp.next == null) {
                //没有找到该雇员的信息
                curEmp = null;
            }
            //后移
            curEmp = curEmp.next;
        }
        return curEmp;
    }

    /**
     * 根据id删除雇员信息
     * @param id
     */
    public void delete(int id) {
        if (head == null) {
            System.out.println("链表为空,无须删除");
            return;
        }
        if (head.id == id) {
            //头节点为空
            if (head.next == null) {
                head = null;
            } else {
                //后移
                head = head.next;
            }
            return;
        }
        //辅助指针
        Emp curEmp = head;
        boolean flag = false;
        while (true) {
            if (head.id == id) {
                head = head.next;
                return;
            }
            if (curEmp.next.id == id) {
                flag = true;
                break;
            }
            if (flag) {
                curEmp.next = curEmp.next.next;
            } else {
                System.out.println("要删除的雇员不存在");
            }
            curEmp = curEmp.next;
        }
    }
}
```





