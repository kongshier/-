> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

# 树结构基础部分

## 树

1. 数组存储方式

   - 优点：通过下标方式访问元素，速度快。对于有序数组，可使用二分查找提高检索速度。 

   - 缺点：如果要检索具体某个值，或者插入值(按一定顺序)会整体移动，效率较低

     ![image-20220910090154661](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910090154661.png) 

2. 链式存储方式

   - 优点：在一定程度上对数组存储方式有优化(比如：插入一个数值节点，只需要将插 入节点，链接到链表中即可， 删除效率也很好)。 

   - 缺点：在进行检索时，效率仍然较低，比如(检索某个值，==需要从头节点开始遍历==) 

     插入 6 ：

     ![image-20220910090723548](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910090723548.png)

3. 树存储方式

   - 能提高数据存储，读取的效率, 比如利用 二叉排序树(Binary Sort Tree)，既可以保证数据的检索速度，同时也可以保证数据的插入，删除，修改的速度。

   - 小于根节点的放置左边，大于的放在右边

     ![image-20220910091902475](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910091902475.png)

## 树示意图

### 树的常用术语

1. 节点
2. 根节点
3. 父节点
4. 子节点
5. 叶子节点（没有子节点的节点）
6. 节点的权（节点值）
7. 层
8. 路径（从root节点找到该节点的路线）
9. 子树
10. 树的高度（最大的层数）
11. 森林：多棵子树构成森林

![image-20220910092156545](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910092156545.png)



## 二叉树概念

- 二叉树：每个节点最多只能有两个子节点的一种形式

- 二叉树的子节点分为左节点和右节点

  ![image-20220910092540471](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910092540471.png)

- 满二叉树：该二叉树的所有叶子节点都在最后一层，并且节点总数= 2^n^ -1 , n 为层 数

  ![image-20220910092744037](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910092744037.png)

- 完全二叉树：该二叉树的所有叶子节点都在最后一层或者倒数第二层，而且最后一层 的叶子节点在左边连续，倒数第二层的叶子节点在右边连续

  ![image-20220910092946580](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910092946580.png)

## 二叉树遍历



前序遍历：==先输出父节点==，再遍历左子树和右子树

中序遍历：先遍历左子树，==再输出父节点==，再遍历右子树

后序遍历：先遍历左子树，再遍历右子树，==最后输父节点==

父节点输出位置判断是属于哪一个序遍历



### 二叉树遍历步骤（前、中、后序）

![image-20220910101429183](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910101429183.png)



1. 创建一个二叉树
2. 前序遍历
   1. 先输出当前节点（初始为根节点开始遍历）
   2. 判断==左子节点==是否为空，为空，则递归继续前序遍历
   3. 判断==右子节点==是否为空，为空，则递归继续前序遍历
3. 中序遍历
   1. 若当前节点的==左子节点==不为空，则递归中序遍历
   2. 输出当前节点
   3. 若当前节点的==右子节点==不为空，则递归中序遍历
4. 后续遍历
   1. 若当前节点的==左子节点==不为空，则递归后序遍历
   2. 若当前节点的==右子节点==不为空，则递归后序遍历
   3. 输出当前的节点

### 添加节点

![image-20220910093606628](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910093606628.png)

1. 在3号节点 "卢俊" , 增加一个左子节点 [5, 关胜]
2. 查看遍历结果
   - 前序：1 、2、3、5、4
   - 中序：2、1、5、3、4
   - 后续：2、5、4、3、1

### 二叉树的查找

要求（查找指定的节点）

1. 请编写前序查找，中序查找和后序查找的方法
2. 并分别使用三种查找方式，查找 heroNO = 5 的节点
3. 并分析各种查找方式，分别比较了多少次
   - 前序：
   - 中序：
   - 后序：

分析：

1. 前序查找
   1. 先判断当前节点的 no 是否等于要查找的
   2. 若是相等，则返回当前节点
   3. 若是不相等的，则判断当前节点的左子节点是否为空，如果不为空，则递归前序查找
   4. 若左递归前序查找，找到节点，则返回，否则继续判断，当前节点的右子节点是否为空，不为空，则继续向右递归查找。
2. 中序查找
   1. 判断当前节点的左子节点是否为空，如果不为空，则递归中序查找
   2. 若是找到，则返回，若是没有找到，则与当前节点比较，若是当前节点则返回当前节点，否则进行进行右递归的中序查找
   3. 若是有递归中序查找，查找到则返回，否则返回null
3. 后序查找
   1. 判断当前节点的左子节点是否为空，如果不为空，则递归后序查找
   2. 若是找到，则返回，若是没有找到，则判断当前节点的右子节点是否为孔，若不为空，则右递归进行后序查找，如果查找到，就返回
   3. 与当前节点进行比较，如果是则返回，否则返回null

### 二叉树-删除节点

要求

1. 如果删除的节点是叶子节点，则删除该节点
2. 如果删除的节点是非叶子节点，则删除该子树.
3. 测试，删除掉 5号叶子节点 和 3号子树.

![image-20220910153129208](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910153129208.png)

思路步骤：

1. 若树为空（root 为空 ），若只有一个root结点，则等价于二叉树置空
2. 因为当前的二叉树是单向的，判断当前节点的子结点是否需要删除节点，而不能去判断当前结点是否需要删除结点
3. 如果当前节点的左子树不为空，并且左子结点就是要删除结点，就将 this.left =null ，并且返回（递归删除）
4. 如果当前节点的右子树不为空，并且右子结点就是要删除结点，就将 this.right =null ，并且返回（递归删除）
5. 第2和第3都没有删除结点，则进行向左子树递归删除
6. 第4步左子树没有删除成功，则进行右子树递归删除





二叉树的遍历、查找、删除完整代码

```java
package com.tree;

/**
 * @author Kcs 2022/9/10
 */
public class BinaryTreeDemo {
    public static void main(String[] args) {
        //创建二叉树
        BinaryTree binaryTree = new BinaryTree();

        //创建节点
        HeroNode root = new HeroNode(1, "宋江");
        HeroNode node2 = new HeroNode(2, "吴用");
        HeroNode node3 = new HeroNode(3, "卢俊义");
        HeroNode node4 = new HeroNode(4, "林冲");
        HeroNode node5 = new HeroNode(5, "关胜");

        //手动创建二叉树
        root.setLeft(node2);
        root.setRight(node3);
        node3.setRight(node4);
        node3.setLeft(node5);

        binaryTree.setRoot(root);


        //前序遍历
        System.out.println("前序遍历：");
        binaryTree.preOrder();

        //中序遍历
        System.out.println("中序遍历：");
        binaryTree.infixOrder();

        //后续遍历
        System.out.println("后序遍历：");
        binaryTree.postOrder();

        //前序遍历查找 查找了4 次
        System.out.println("前序遍历查找~~~");
        HeroNode resNode = binaryTree.preOrderSearch(5);
        if (resNode != null) {
            System.out.printf("找到了！，HeroNode{no = %d  name = %s}", resNode.getNo(), resNode.getName());
        } else {
            System.out.printf("该编号 no = %d 的人物不存在！", 5);
        }

        System.out.println();
        //中序遍历查找 查找了 3 次
        System.out.println("中序遍历查找~~~");
        resNode = binaryTree.infixOrderSearch(5);
        if (resNode != null) {
            System.out.printf("找到了！，HeroNode{no = %d  name = %s}", resNode.getNo(), resNode.getName());
        } else {
            System.out.printf("该编号 no = %d 的人物不存在！", 5);
        }

        System.out.println();
        //后序遍历查找 查找了 5 次
        System.out.println("后序遍历查找~~~");
        resNode = binaryTree.postOrderSearch(5);
        if (resNode != null) {
            System.out.printf("找到了！，HeroNode{no = %d  name = %s}", resNode.getNo(), resNode.getName());
        } else {
            System.out.printf("该编号 no = %d 的人物不存在！", 5);
        }


        //删除结点
        System.out.println("删除前，前序遍历");
        binaryTree.preOrder();
        // binaryTree.delNode(5);
        //删除子树
        binaryTree.delNode(3);
        System.out.println("删除后，前序遍历");
        binaryTree.preOrder();

    }
}

/**
 * 二叉树
 */
class BinaryTree {
    private HeroNode root;

    public void setRoot(HeroNode root) {
        this.root = root;
    }


    /**
     * 前序遍历方法 ： 从根节点出发遍历
     */
    public void preOrder() {
        //根节点不为空
        if (this.root != null) {
            this.root.preOrder();
        } else {
            //为空
            System.out.println("二叉树为空，无法遍历！");
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        //根节点不为空
        if (this.root != null) {
            this.root.infixOrder();
        } else {
            //为空
            System.out.println("二叉树为空，无法遍历！");
        }
    }

    /**
     * 后序遍历
     */
    public void postOrder() {
        //根节点不为空
        if (this.root != null) {
            this.root.postOrder();
        } else {
            //为空
            System.out.println("二叉树为空，无法遍历！");
        }
    }

    /**
     * 前序遍历查找
     */
    public HeroNode preOrderSearch(int no) {
        if (root != null) {
            return root.preOrderSearch(no);
        } else {
            return null;
        }
    }

    /**
     * 序遍历查找
     */
    public HeroNode infixOrderSearch(int no) {
        if (root != null) {
            return root.infixOrderSearch(no);
        } else {
            return null;
        }
    }

    /**
     * 后序遍历查找
     */
    public HeroNode postOrderSearch(int no) {
        if (root != null) {
            return root.postOrderSearch(no);
        } else {
            return null;
        }
    }

    /**
     * 删除二叉树结点
     */
    public void delNode(int no) {
        if (root != null) {

            //root是否为删除的结点
            if (root.getNo() == no) {
                root = null;
            } else {
                // 递归删除
                root.deleteNode(no);
            }
        } else {
            System.out.println("该树为空，无法删除！");
        }
    }
}

/**
 * 创建 herNode节点
 */
class HeroNode {
    /**
     * 序号
     */
    private int no;
    /**
     * 姓名
     */
    private String name;
    /**
     * 左节点，默认null
     */
    private HeroNode left;
    /**
     * 右节点，默认null
     */
    private HeroNode right;

    public HeroNode(int no, String name) {
        this.no = no;
        this.name = name;
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public HeroNode getLeft() {
        return left;
    }

    public void setLeft(HeroNode left) {
        this.left = left;
    }

    public HeroNode getRight() {
        return right;
    }

    public void setRight(HeroNode right) {
        this.right = right;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }

    /**
     * 前序遍历，输出：中=>左=>右
     */
    public void preOrder() {
        System.out.println("当前父节点:" + this);

        //递归向左子树前序遍历
        if (this.left != null) {
            this.left.preOrder();
        }
        //递归向右子树前序遍历
        if (this.right != null) {
            this.right.preOrder();
        }
    }

    /**
     * 中序遍历 输出：左=>中=>右
     */
    public void infixOrder() {
        //先递归向左子树中序遍历
        if (this.left != null) {
            this.left.infixOrder();
        }
        //再中序输出父节点
        System.out.println("当前父节点" + this);

        //后递归向右子树中序遍历
        if (this.right != null) {
            this.right.infixOrder();
        }
    }

    /**
     * 后序遍历 输出：左=>右=>中
     */
    public void postOrder() {
        //先递归向左子树后序遍历
        if (this.left != null) {
            this.left.postOrder();
        }
        //再递归向右子树后序遍历
        if (this.right != null) {
            this.right.postOrder();
        }
        //最后输出后序父节点
        System.out.println("当前父节点" + this);
    }

    /**
     * 前序遍历查找 输出：中=>左=>右
     * @param no 查找no
     * @return 返回Node，为空返回null
     */
    public HeroNode preOrderSearch(int no) {
        System.out.println("进入前序查找");
        //首先判断当前节点是否为no
        if (this.no == no) {
            return this;
        }
        //结果节点
        HeroNode resNode = null;
        //判断当前节点的左子节点是否为空，如果不为空，则递归前序查找
        if (this.left != null) {
            resNode = this.left.preOrderSearch(no);
        }
        //左子树查找到节点，则返回
        if (resNode != null) {
            //查到结果
            return resNode;
        }
        //右子树递归后序查找，判断当前节点的右子节点是否为空，不为空，则继续向右递归查找。
        if (this.right != null) {
            resNode = this.right.preOrderSearch(no);
        }
        return resNode;
    }


    /**
     * 中序遍历查找 输出：左=>中=>右
     * @param no 查找no
     * @return 返回Node，为空返回null
     */
    public HeroNode infixOrderSearch(int no) {

        //结果节点
        HeroNode resNode = null;
        //判断当前节点的 左子节点 是否为空，如果不为空，则递归中序查找
        if (this.left != null) {
            resNode = this.left.infixOrderSearch(no);
        }
        //左子树查找到节点，则返回
        if (resNode != null) {
            //查到结果
            return resNode;
        }

        System.out.println("进入中序查找");
        //左子树没有找到，则判断当前节点是否为no
        if (this.no == no) {
            return this;
        }

        //右子树递归后序查找，判断当前节点的 右子节点 是否为空，不为空，则继续向右递归查找。
        if (this.right != null) {
            resNode = this.right.infixOrderSearch(no);
        }
        return resNode;
    }


    /**
     * 后序遍历查找 输出：左=>右=>中
     * @param no 查找no
     * @return 返回Node，为空返回null
     */
    public HeroNode postOrderSearch(int no) {
        //结果节点
        HeroNode resNode = null;
        //判断当前节点的 左子节点 是否为空，如果不为空，则递归 后序查找
        if (this.left != null) {
            resNode = this.left.postOrderSearch(no);
        }
        //左子树后序查找到节点，则返回
        if (resNode != null) {
            //查到结果
            return resNode;
        }

        //右子树递归后序查找，判断当前节点的 右子节点 是否为空，不为空，则继续向右递归查找。
        if (this.right != null) {
            resNode = this.right.postOrderSearch(no);
        }
        System.out.println("进入后序查找");
        //左右子树都没有找到，判断当前节点是否为no
        if (this.no == no) {
            return this;
        }
        return resNode;
    }

    /**
     * 递归删除结点
     * 1. 如果删除的节点是叶子节点，则删除该节点
     * 2. 如果删除的节点是非叶子节点，则删除该子树
     */
    public void deleteNode(int no) {
        //删除左子结点
        if (this.left != null && this.left.no == no) {
            this.left = null;
            return;
        }
        //删除右子结点
        if (this.right != null && this.right.no == no) {
            this.right = null;
            return;
        }
        //左子树递归删除
        if (this.left != null) {
            this.left.deleteNode(no);
        }
        //左子树递归删除
        if (this.right != null) {
            this.right.deleteNode(no);
        }
    }
}
```

## 顺序存储二叉树

从数据存储来看，数组存储方式和树 的存储方式可以相互转换，即数组可 以转换成树，树也可以转换成数组

1. 右图的二叉树的结点，要求以数组的方式来存放 arr : [1, 2, 3, 4, 5, 6, 6]

2. 要求在遍历数组 arr[ ] 时，仍然可以以前序遍历，中序遍历和后序遍历的 方式完成结点的遍历

   ![image-20220910171315607](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220910171315607.png)

   

### 特点

1. 顺序二叉树通常只考虑完全二叉树
2. 第n个元素的左子节点为 2 * n + 1 
3. 第n个元素的右子节点为 2 * n + 2
4. 第n个元素的父节点为 (n-1) / 2
5. n : 表示二叉树中的第几个元素



### 要求

给你一个数组 {1,2,3,4,5,6,7}，要求以二叉树前序遍历的方式进行遍历。 前序遍历的结果应当为 1,2,4,5,3,6,7

- 前、中、后序遍历的输出顺序不一样

```java
package com.tree;

/**
 * @author Kcs 2022/9/10
 */
public class ArrayBinaryTreeDemo {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 4, 5, 6, 7};
        ArrayBinaryTree arrayBinaryTree = new ArrayBinaryTree(arr);
        //前序
        System.out.println("前序遍历：");
        arrayBinaryTree.preOrder();
        System.out.println();
        //中序
        System.out.println("中序遍历：");
        arrayBinaryTree.infixOrder();
        System.out.println();
        //前序
        System.out.println("后序遍历：");
        arrayBinaryTree.postOrder();
        System.out.println();
    }
}

//编写一个ArrayBinaryTree存储二叉树遍历
class ArrayBinaryTree {
    /**
     * 存储数据结点的数组
     */
    private int[] arr;

    public ArrayBinaryTree(int[] arr) {
        this.arr = arr;
    }

    public void preOrder() {
        this.preOrder(0);
    }

    public void infixOrder() {
        this.infixOrder(0);
    }

    public void postOrder() {
        this.postOrder(0);
    }

    /**
     * 完成顺序存储二叉树的  前序遍历
     * @param index 返回下标
     */
    public void preOrder(int index) {
        //若数组为空
        if (arr == null || arr.length == 0) {
            System.out.println("数组为空，无法进行二叉树的前序遍历");
        }
        //输出当前的这个元素
        System.out.print(arr[index] + " ");

        //向左递归遍历
        if ((index * 2 + 1) < arr.length) {
            preOrder(2 * index + 1);
        }

        //向右递归
        if ((index * 2 + 2) < arr.length) {
            preOrder(2 * index + 2);
        }
    }

    /**
     * 顺序存储二叉树 中序遍历
     * @param index 索引
     */
    public void infixOrder(int index) {
        //数组为空或者数组长度为0
        if (arr == null || arr.length == 0) {
            System.out.println("数组为空，无法进行二叉树的中序遍历");
        }
        //向左遍历
        if ((index * 2 + 1) < arr.length) {
            infixOrder(index * 2 + 1);
        }
        //输出当前元素
        System.out.print(arr[index] + " ");
        //向右遍历
        if ((index * 2 + 2) < arr.length) {
            infixOrder(index * 2 + 2);
        }
    }

    /**
     * 顺序存储二叉树 后序遍历
     * @param index 索引
     */
    public void postOrder(int index) {
        //数组为空或者数组长度为0
        if (arr == null || arr.length == 0) {
            System.out.println("数组为空，无法进行二叉树的后序遍历");
        }
        //向左遍历
        if ((index * 2 + 1) < arr.length) {
            postOrder(index * 2 + 1);
        }
        //向右遍历
        if ((index * 2 + 2) < arr.length) {
            postOrder(index * 2 + 2);
        }
        //输出当前元素
        System.out.print(arr[index] + " ");
    }
}
```



## 线索化二叉树

将数列 {1, 3, 6, 8, 10, 14 } 构建成一颗二叉树. n+1=7

![image-20220911100038449](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911100038449.png)

- 上面的二叉树进行中序遍历时，数列为 {8, 3, 10, 1, 14，6 }
-  6, 8, 10, 14 这几个节点的 左右指针，并没有完全的利用上



### 线索二叉树的介绍

- n个结点的二叉链表中含有n+1 【公式 2n-(n-1)=n+1】 个空指针域。利用二叉链表中的空指针域，存放指向该结点在某种遍历次序下的前驱和后继结点的指针（附加的指针则为线索）
- 线索二叉树 (Threaded BinaryTree)：加上了线索的二叉链表称为线索链表。
  - 根据线索性质的不同，线索二叉树可分为
  - 前序线索二叉树
  - 中序线索二叉树
  - 后序线索二叉树
- 一个结点的前一个结点，称为前驱结点
  - 第一个元素没有前驱结点
- 一个结点的后一个结点，称为后继结点
  - 最后一个元素没有后继结点



![image-20220911100038449](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911100038449.png)



中序遍历结果：{8, 3, 10, 1, 14, 6}

![image-20220911100858670](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911100858670.png)

当线索化二叉树后，Node节点的 属性 left 和 right

1. left 指向的是左子树，也可能是指向的前驱节点. 比如 ① 节点 left 指向的左子树, 而 ⑩ 节点的 left  指向的就是前驱节点
2. right指向的是右子树，也可能是指向后继节点，比如 ① 节点right 指向的是右子树，而⑩ 节点的 right 指向的是后继节点



### 遍历线索化二叉树

分析

​	因为线索化后，各个结点指向有变化，因此原来的遍历方式不能使用， 这时需要使用新的方式遍历线索化二叉树，各个节点可以通过线型方式遍历， 因此无需使用递归方式，这样也提高了遍历的效率。 遍历的次序应当和中序遍历保持一致

```java
package com.tree.threadbinarytree;

/**
 * @author Kcs 2022/9/11
 */
public class ThreadBinaryTreeDemo {
    public static void main(String[] args) {
        HeroNode root = new HeroNode(1, "tom");
        HeroNode node2 = new HeroNode(3, "jack");
        HeroNode node3 = new HeroNode(6, "smith");
        HeroNode node4 = new HeroNode(8, "mary");
        HeroNode node5 = new HeroNode(10, "kong");
        HeroNode node6 = new HeroNode(14, "十二");

        //手动创建二叉树
        root.setLeft(node2);
        root.setRight(node3);

        node2.setLeft(node4);
        node2.setRight(node5);

        node3.setLeft(node6);

        ThreadBinaryTree threadBinaryTree = new ThreadBinaryTree();
        threadBinaryTree.setRoot(root);
        threadBinaryTree.infixThreadedNodes();
        
        System.out.println("====================中序线索化======================");
        //中序线索化测试
        //前驱结点
        System.out.println("中序线索化~~~");
        HeroNode infixLeftNode = node5.getLeft();
        System.out.println("10号的前驱结点为：" + infixLeftNode);
        //后继结点
        HeroNode infixRightNode = node5.getRight();
        System.out.println("10号的后继结点为：" + infixRightNode);
        //线索化二叉树遍历
        System.out.println("中序线索化二叉树遍历~~~~");
        threadBinaryTree.infixThreadedList();
    }
}

/**
 * 线索化二叉树
 */
class ThreadBinaryTree {
    private HeroNode root;

    /**
     * 线索化，当前结点的指针, 保留前一个结点
     */
    private HeroNode pre = null;

    public void setRoot(HeroNode root) {
        this.root = root;
    }

    /**
     * 重载中序线索化方法
     */
    public void infixThreadedNodes() {
        this.infixThreadedNodes(root);
    }

    /**
     * 中序线索化二叉树
     * @param node 当前线索化结点
     */
    public void infixThreadedNodes(HeroNode node) {
        //空结点，则不能线索化
        if (node == null) {
            return;
        }
        //1.左子树线索化
        infixThreadedNodes(node.getLeft());

        //2.线索化当前结点
        //当前结点的前驱结点
        if (node.getLeft() == null) {
            //左指针 指向前驱结点
            node.setLeft(pre);
            //左指针类型重置
            node.setLeftType(1);
        }
        //当前结点的后继结点
        if (pre != null && pre.getRight() == null) {
            //前驱结点的右指针指向当前接结点
            pre.setRight(node);
            //重置右指针类型
            pre.setRightType(1);
        }
        //下一个结点的前驱结点
        pre = node;

        //3.线索化右子树
        infixThreadedNodes(node.getRight());

    }
    

    /**
     * 中序遍历线索化二叉树
     */
    public void infixThreadedList() {
        //当前遍历结点，root开始
        HeroNode node = root;
        while (node != null) {
            //leftType ==1 则线索化处理后的有效节点
            while (node.getLeftType() == 0) {
                node = node.getLeft();
            }
            //打印当前结点信息
            System.out.println(node);

            //当前结点的右指针指向后继结点则输出
            while (node.getRightType() == 1) {
                //获取当前结点的后继结点
                node = node.getRight();
                System.out.println(node);
            }
            //替换当前的遍历结点
            node = node.getRight();
        }
    }

}


/**
 * 创建 HeroNode节点 实体类
 */
class HeroNode {
    /**
     * 序号
     */
    private int no;
    /**
     * 姓名
     */
    private String name;
    /**
     * 左节点，默认null
     */
    private HeroNode left;
    /**
     * 右节点，默认null
     */
    private HeroNode right;

    /**
     * 为0：指向左子树；为1指向前驱结点
     */
    private int leftType;

    /**
     * 为0：指向右子树；为1指向后继结点
     */
    private int rightType;

    /**
     * 构造器
     * @param no 编号
     * @param name 姓名
     */

    public HeroNode(int no, String name) {
        this.no = no;
        this.name = name;
    }

    public int getNo() {
        return no;
    }

    public void setNo(int no) {
        this.no = no;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public HeroNode getLeft() {
        return left;
    }

    public void setLeft(HeroNode left) {
        this.left = left;
    }

    public HeroNode getRight() {
        return right;
    }

    public void setRight(HeroNode right) {
        this.right = right;
    }

    public int getLeftType() {
        return leftType;
    }

    public void setLeftType(int leftType) {
        this.leftType = leftType;
    }

    public int getRightType() {
        return rightType;
    }

    public void setRightType(int rightType) {
        this.rightType = rightType;
    }

    @Override
    public String toString() {
        return "HeroNode{" +
                "no=" + no +
                ", name='" + name + '\'' +
                '}';
    }
}
```



# 树结构实际应用

## 堆排序

### 基础介绍

1. 堆排序是利用堆这种数据结构而设计的一种排序算法，堆排序是一种选择排序，它的 最坏，最好，平均时间复杂度均为O(nlogn)，它也是不稳定排序

2. 堆是具有以下性质的完全二叉树：每个结点的值都大于或等于其左右孩子结点的值， 称为大顶堆

   - 注意 : 没有要求结点的左孩子的值和右孩子的值的大小关系

3. 每个结点的值都小于或等于其左右孩子结点的值，称为小顶堆

   ![image-20220911154058077](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911154058077.png)

   - 小顶堆：arr[i] <= arr[2 * i+1] && arr[i] <= arr[2 * i+2] // i 对应第几个节点，i从0开始编号

4. 每个结点的值都大于或等于其左右孩子结点的值，称为大顶堆

   ![image-20220911153603198](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911153603198.png)

   - 大顶堆特点：arr[i] >= arr[2 * i+1] && arr[i] >=  arr[2 * i + 2]

   - i 对应第几个节点，i从0开始编号

5. ==升序采用大顶堆，降序采用小顶堆==



### 基本思想

1. 将待排序序列构造成一个大顶堆
2. 序列的最大值就是堆顶的根节点
3. 将其与末尾元素进行交换，此时末尾就为最大值
4. 然后将剩余n-1个元素重新构造成一个堆，会得到n个元素的次小值。反复执行，便能得到一个有序序列



### 分析

1. 构造初始堆。给定无序序列构造成一个大顶堆。原始数组[4、6、8、5、9]

2. 结构：![image-20220911155140497](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911155140497.png)

3. 从最后一个==非叶子节点== 开始（叶子节点不用调整）第一个==非叶子节点位置==： arr.length / 2-1。==从上自下，从左至右== 进行调整

   ![image-20220911155607764](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911155607764.png)

4. 找到第二个叶子节点，由于【4，9，8】中9 最大，4 和 9 交换。9与8 比较后，不需交换

   ![image-20220911155808569](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911155808569.png)

5. 这时，交换导致字根【4，5，6】结构混乱，继续调整【4，5，6】，4和6交换

   ![image-20220911155952605](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911155952605.png)

    

   此时得到一个无序的大顶堆

6. 将堆顶元素与末尾元素进行交换，使末尾元素最大。然后调整，再将堆顶元素与末尾元素交换，得到第二大元素。反复进行交换，调整（重建），交换。

   1. 将堆顶元素 9 与末尾元素 4 交换

      ![image-20220911160451158](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911160451158.png)

   2. 重新调整构造，使其继续满足堆定义

      ![image-20220911160614245](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911160614245.png)

   3. 再将堆顶元素 8 与末尾元素 5 进行交换，得到第二大元素 8 

      ![image-20220911160712757](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911160712757.png)

   4. 不断重复 上面 1 2 3 步最终得到一个有序序列

      ![image-20220911160912777](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220911160912777.png)

   

   

   

   ### 堆排序的基本思路

   1. 将无序序列构建成一个堆，根据升序降序选择大堆顶或者小堆顶
   2. 将堆顶元素与末尾元素交换，将最大元素 "沉" 到数组末端
   3. 重新调整结构，使其满足堆定义，然后继续交换堆顶元素与当前末尾元素，反复执行调整 + 交换步骤，直到整个序列有序。



## 赫夫曼树

- 别名：哈夫曼树，霍夫曼树



### 基本介绍 

1. 给定n个权值作为n个叶子结点，构造一棵二叉树，若该树的带权路径长度 (wpl)达到最小，这样的二叉树为最优二叉树，也是赫夫曼树
2. 赫夫曼树是带权路径长度最短的树，权值较大的结点离根较近



### 概念

1. 路径：在一棵树中，从一个结点往下可以达到的孩子或孙子结点之间的通路
2. 路径长度：通路中分支的数目称为路径长度
3. 若规定根结点的层数为1，则从根结点到第L层结点的路径长度为L-1
4. 结点的权：若将树中结点赋给一个有着某种含义的数值， 则该数值称为该结点的权
5. 结点的带权路径长度：从根结点到该结点 之间的路径长度与该结点的权的乘积
6. 树的带权路径长度：树的带权路径长度规定为所有叶子结点的带权路径长度之和，记 为WPL(weighted path length) ,权值越大的结点离根结点越近的二叉树才是最优二叉树

WPL举例说明：

![image-20220912090337839](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912090337839.png)



### 思路分析

数列：{13, 7, 8, 3, 29, 6, 1} 把数列构造成一颗赫夫曼树



步骤

1. 从小到大进行排序, 将每一个数据，每个数据都是一个节点 ， 每个节点可以看成是一颗最简单的二叉树
2. 取出根节点权值最小的两颗二叉树
3. 组成一颗新的二叉树, 该新的二叉树的根节点的权值是前面两颗二叉树根节点权值的和
4. 再将这颗新的二叉树，以根节点的权值大小 再次排序， 不断重复 1-2-3-4 的步骤， 直到数列中，所有的数据都被处理，就得到一颗赫夫曼树

最终得到的赫夫曼树：

![image-20220912094052604](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912094052604.png)



```java
package com.huffmantree;

import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

/**
 * @author Kcs 2022/9/12
 */
public class HuffmanTree {
    public static void main(String[] args) {
        int[] array = {13, 7, 8, 3, 29, 6, 1};
        Node root = createHuffmanTree(array);

        System.out.println("=====================前序遍历=====================");
        preOrder(root);
        System.out.println("=====================中序遍历=====================");
        infixOrder(root);
        System.out.println("=====================后序遍历=====================");
        postOrder(root);
    }

    /**
     * 创建赫夫曼树
     * @param array 创建好之后的root结点
     */
    public static Node createHuffmanTree(int[] array) {
        //将Node 放入ArrayList<>
        List<Node> nodes = new ArrayList<Node>();
        //遍历数组
        for (int value : array) {
            //数组元素构成一个Node
            nodes.add(new Node(value));
        }

        while (nodes.size() > 1) {
            //排序
            Collections.sort(nodes);

            //取出跟结点全职最小的两颗二叉树
            //最小的结点
            Node leftNode = nodes.get(0);

            //第二小的结点
            Node rightNode = nodes.get(1);

            //大到小排序
            // Node leftNode = nodes.get(nodes.size() - 1);
            // Node rightNode = nodes.get(nodes.size()-2);

            //构建一颗父节点的二叉树
            Node parent = new Node(leftNode.value + rightNode.value);
            parent.left = leftNode;
            parent.right = rightNode;

            //删除处理郭的二叉树
            nodes.remove(leftNode);
            nodes.remove(rightNode);

            //将parent加入到nodes
            nodes.add(parent);
        }
        //返回赫夫曼树的根节点
        return nodes.get(0);
    }

    /**
     * 前序遍历方法 输出顺序：中 =》左=》右
     */
    public static void preOrder(Node root) {
        if (root != null) {
            root.preOrder();
        } else {
            System.out.println("该赫夫曼树为空！！！");
        }
    }

    /**
     * 中序遍历方法  输出顺序：左=》中 =》右
     */
    public static void infixOrder(Node root) {
        if (root != null) {
            root.infixOrder();
        } else {
            System.out.println("该赫夫曼树为空！！！");
        }
    }

    /**
     * 后序遍历方法  输出顺序：左=》右 =》中
     */
    public static void postOrder(Node root) {
        if (root != null) {
            root.postOrder();
        } else {
            System.out.println("该赫夫曼树为空！！！");
        }
    }

}

/**
 * 结点类
 * 实现Comparable接口 进排序
 */
class Node implements Comparable<Node> {
    /**
     * 节点值
     */
    int value;
    /**
     * 结点的左子节点
     */
    Node left;
    /**
     * 结点的右子节点
     */
    Node right;

    public Node(int value) {
        this.value = value;
    }

    /**
     * 前序遍历
     */
    public void preOrder() {
        System.out.println(this);
        if (this.left != null) {
            this.left.preOrder();
        }
        if (this.right != null) {
            this.right.preOrder();
        }
    }


    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (this.left != null) {
            this.left.infixOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.infixOrder();
        }
    }

    /**
     * 后序遍历
     */
    public void postOrder() {
        if (this.left != null) {
            this.left.postOrder();
        }
        if (this.right != null) {
            this.right.postOrder();
        }
        System.out.println(this);
    }

    @Override
    public String toString() {
        return "Node{" +
                "value=" + value +
                '}';
    }

    @Override
    public int compareTo(Node o) {
        //从小到大排序
        return this.value - o.value;
        //大到小
        // return o.value - this.value;
    }

}
```



## 赫夫曼编码

- 算法
- 赫夫曼编码广泛地用于数据文件压缩。其压缩率通常在20%～90%之间
- 赫夫曼码是可变字长编码(VLC)。

### 定长编码

![image-20220912104912865](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912104912865.png)

![image-20220912105542227](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912105542227.png)

### 赫夫曼编码

原理：

1. i like like like java do you like a java  // 共40个字符(包括空格)
2. d:1 y:1 u:1 j:2 v:2 o:2 l:4 k:4 e:4 i:5 a:5 :9 // 各个字符对应的个数
3. 按照上面字符出现的次数构建一颗赫夫曼树, 次数作为权值

最终形成的赫夫曼树

![image-20220912111627899](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912111627899.png)



根据赫夫曼树，给各个字符规定编码 ， 向左的路径为0 向右的路径为1 ， 编码如下

> o: 1000 u: 10010 d: 100110 y: 100111 i: 101 a : 110 k: 1110 e: 1111 j: 0000 v: 0001 l: 001  [空格] : 01

"i like like like java  do you like a java" 字符串对应的编码为

> 1010100110111101111010011011110111101001101111011110100001100001110011001111000011001111000100100100110111101111011100100001100001110

长度为 ： 133

原来长度是 359 , 压缩了 (359-133) / 359 = 62.9% 2) 此编码满足前缀编码, 即字符的编码都不能是其他字符编码的前缀。不会造成匹配的多义性



赫夫曼树根据排序方法不同，也可能不太一样，这样对应的赫夫曼编码也不完全一样，但是wpl 是一样的，都是最小的, 比如: 让每次生成新的二叉树总是排在权值相同的二叉树的最后一个，则生成的二叉树为

![image-20220912113420940](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220912113420940.png)



### 数据压缩

根据赫夫曼编码压缩数据的原理，需要创建 "i like like like java do you  like a java" 对应的赫夫曼树

1. Node{date(存放数据)，weight(权重)，left，right }
2. 得到字符串对应的数组
3. 将构建赫夫曼树的Node 节点放到List 
4. 通过List创建对应的赫夫曼树

```java
package com.huffmancode;

import java.util.*;

/**
 * @author Kcs 2022/9/12
 */
public class HuffmanCode {
    public static void main(String[] args) {
        String content = "i like you and must love you and only love you";
        byte contentBytes[] = content.getBytes();
        //字符串长度
        System.out.println("字符串长度：" + contentBytes.length);

        //测试
        List<HuffmanNode> nodes = getHuffmanNodes(contentBytes);
        System.out.println("nodes=" + nodes);

        //测试创建二叉树
        System.out.println("前序遍历当前的赫夫曼树~~~");
        HuffmanNode huffmanTreeRoot = creatHuffmanTree(nodes);
        huffmanTreeRoot.preOrder();

        //测试一把是否赫夫曼编码
        //getCodes(HuffmanTreeRoot,"",stringBuilder);
        Map<Byte, String> huffmanCodes = getCodes(huffmanTreeRoot);
        System.out.println("~生成的赫夫曼编码表~\n" + huffmanCodes);

    }

    /**
     * 生成赫夫曼树对应的赫夫曼编码
     * 将赫夫曼编码表放在Map<Byte,String>
     * {[key:value] [key:value]}
     */
    static Map<Byte, String> huffmanCodes = new HashMap<Byte, String>();
    /**
     * 在生成赫夫曼编码表时，拼接路径，用StringBuilder 存储某个叶子节点的路径
     */
    static StringBuilder stringBuilder = new StringBuilder();

    /**
     * 重载getCodes
     * @param root 跟结点
     * @return map
     */
    private static Map<Byte, String> getCodes(HuffmanNode root) {
        if (root == null) {
            return null;
        }
        //处理root的左子树
        getCodes(root.left, "0", stringBuilder);
        //处理root的右子树
        getCodes(root.right, "1", stringBuilder);
        return huffmanCodes;
    }

    /**
     * 功能：得到传入的node节点的所有赫夫曼编码，并存放到huffmanCodes集合中
     * @param node 传入的节点（默认从root）
     * @param code 该节点的路径（左子节点0和右子节点1）
     * @param stringBuilder 拼接路径
     */
    private static void getCodes(HuffmanNode node, String code, StringBuilder stringBuilder) {
        StringBuilder stringBuilder2 = new StringBuilder(stringBuilder);
        //将传入的code加入到stringBuilder2中
        stringBuilder2.append(code);
        if (node != null) {
            //node==null不处理
            //判断当前node时叶子节点还是非叶子节点
            if (node.data == null) {
                //非叶子节点
                //向左递归
                getCodes(node.left, "0", stringBuilder2);
                //向右递归
                getCodes(node.right, "1", stringBuilder2);
            } else {
                //叶子节点
                huffmanCodes.put(node.data, stringBuilder2.toString());
            }
        }
    }

    /**
     * @param bytes 接受的数组
     * @return 返回List形式：[Node[date=97,weight =5],Node[date=32,weight=9]]
     */
    private static List<HuffmanNode> getHuffmanNodes(byte bytes[]) {
        //创建ArrayList
        ArrayList<HuffmanNode> nodes = new ArrayList<HuffmanNode>();
        //遍历bytes，统计每个byte出现的次数->map
        Map<Byte, Integer> counts = new HashMap<>();
        for (byte b : bytes) {
            Integer count = counts.get(b);
            if (count == null) {
                //首次，Map没有字符数据
                counts.put(b, 1);
            } else {
                counts.put(b, count + 1);
            }
        }
        //遍历Map。把每个键值对转成HuffmanNode对象，并加入nodes中
        for (Map.Entry<Byte, Integer> entry : counts.entrySet()) {
            nodes.add(new HuffmanNode(entry.getKey(), entry.getValue()));
        }
        return nodes;
    }

    /**
     * 通过List，创建赫夫曼树
     * @param nodes list列表
     * @return 根节点
     */
    private static HuffmanNode creatHuffmanTree(List<HuffmanNode> nodes) {
        while (nodes.size() > 1) {
            Collections.sort(nodes);
            //排序小到大
            HuffmanNode leftNode = nodes.get(0);
            HuffmanNode rightNode = nodes.get(1);
            //创建新的二叉树，没有data只有权值weight
            HuffmanNode parent = new HuffmanNode(null, leftNode.weight + rightNode.weight);
            parent.left = leftNode;
            parent.right = rightNode;
            //移除旧的结点
            nodes.remove(leftNode);
            nodes.remove(rightNode);
            //添加新的二叉树
            nodes.add(parent);
        }
        return nodes.get(0);
    }

    /**
     * 前序遍历
     * @param root
     */
    private static void preOrder(HuffmanNode root) {
        if (root != null) {
            root.preOrder();
        } else {
            System.out.println("空树");
        }
    }
}


/**
 * 创建Node
 */
class HuffmanNode implements Comparable<HuffmanNode> {
    /**
     * 存放数据本身'a'->97 ' '->32
     */
    Byte data;
    /**
     * 权值,字符出现的次数
     */
    int weight;
    HuffmanNode left;
    HuffmanNode right;

    public HuffmanNode(Byte data, int weight) {
        this.data = data;
        this.weight = weight;
    }

    @Override
    public int compareTo(HuffmanNode huffmanNode) {
        //表示从小到达排序
        return this.weight - huffmanNode.weight;
    }

    @Override
    public String toString() {
        return "HuffmanNode{" + "data=" + data + ", weight=" + weight + '}';
    }

    /**
     * 前序遍历
     */
    public void preOrder() {
        System.out.println(this);
        if (this.left != null) {
            this.left.preOrder();
        }
        if (this.right != null) {
            this.right.preOrder();
        }
    }
}
```



## 二叉排序树

对数列 (7, 3, 10, 12, 5, 1, 9)操作，高效的完成对数据的查询和添加

### 分析：

**使用数组**：

1. 数组未排序
   - 优点：直接在数组尾添加，速度快
   -  缺点：查找速度慢
2. 数组排序
   - 优点：可以使用二分查找，查找速度快
   - 缺点：为了保证数组有序， 在添加新数据时，找到插入位置后，后面的数据需整体移动，速度慢

**使用链表**：

- 不管链表是否有序，查找速度都慢，添加数据速度比数组快，不需要数据整体 移动

**使用二叉排序树**：



### 基本介绍

- 二叉排序树：BST: (Binary Sort(Search) Tree), 对于二叉排序树的任何一个非叶子节点，要求==左子节点的值比当前节点的值小，右子节点的值比当前节点的值大==。

- 如果有相同的值，可以将该节点放在左子节点或右子节点

- 对数据(7, 3, 10, 12, 5, 1, 9)进行二叉排序树

  ![image-20220914222821047](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220914222821047.png)

### 二叉排序树创建与遍历

数组创建成一个二叉排序树，使用中序遍历二叉排序树。Array(7, 3, 10, 12, 5, 1, 9) 对此数组进行中序遍历二叉排序树





### 二叉排序树的删除



分析

1. 删除叶子节点 (比如：2, 5, 9, 12)
   - 即该节点下==没有==左右子节点
   
   1. 找到要删除的结点，targetNode
   2. 找到 targetNode 的父节点 parent 
   3. 确定 targetNode 是parent 的左子结点，还是右子结点
   4. 更情况来对应删除
      - 左子结点：parent . left = null
      - 右子结点：parent . right = null
   
2. 删除只有一颗子树的节点 (比如：1）
   - 即该节点有左子节点==或==者右子节点
   
   1. 找到要删除的结点，targetNode
   2. 找到 targetNode 的父节点 parent
   3. 确定 targetNode 的子节点是左子结点还是右子结点
   4. targetNode 是 parent 的左子结点还是右子结点
   5. 若targetNode 有左子结点
      - targetNode 是 parent 的左子结点
      - parent.left = targetNode.left
      - targetNode 是 parent 的右子结点
      - parent.right= targetNode.left
   6. 若targetNode 有右子结点
      - targetNode 是 parent 的左子结点
      - parent.left = targetNode.right
      - targetNode 是 parent 的右子结点
      - parent.right= targetNode.right
   
3. 删除有两颗子树的节点. (比如：删除10 )
   - 即该节点有左子节点==和==者右子节点
   
   1. 找到要删除的结点，targetNode
   2. 找到 targetNode 的父节点 parent
   3. 从 targetNode 的右子树找到最小的结点，保存在一个变量中 temp
   4. 删除最小结点
   5. targetNode.value = temp
   
   

![image-20220914223559216](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220914223559216.png)

```java
package com.binarysorttree;

/**
 * @author Kcs 2022/9/15
 */
public class BinarySortTreeDemo {
    public static void main(String[] args) {
        int[] arr = {7, 3, 10, 12, 5, 1, 9, 2};
        BinarySortTree binarySortTree = new BinarySortTree();

        //添加结点进二叉排序树
        for (int i = 0; i < arr.length; i++) {
            binarySortTree.add(new Node(arr[i]));
        }

        //遍历二叉排序树
        System.out.println("================前序遍历=================");
        binarySortTree.preOrder();
        System.out.println("================中序遍历=================");
        binarySortTree.infixOrder();
        System.out.println("================后序遍历=================");
        binarySortTree.postOrder();

        //删除叶子结点
        binarySortTree.deleteNode(2);
        System.out.println("================删除叶子结点后：中序遍历二叉排序树=================");
        binarySortTree.infixOrder();


        //删除一棵子树结点
        binarySortTree.deleteNode(1);
        System.out.println("================删除存在一棵子树的结点后：中序遍历二叉排序树=================");
        binarySortTree.infixOrder();

        //删除两棵子树结点
        binarySortTree.deleteNode(10);
        System.out.println("================删除右两颗子树的结点后：中序遍历二叉排序树=================");
        binarySortTree.infixOrder();

        binarySortTree.deleteNode(3);
        binarySortTree.deleteNode(5);
        binarySortTree.deleteNode(7);
        binarySortTree.deleteNode(9);
        binarySortTree.deleteNode(12);

        System.out.println("删除完之后");
        binarySortTree.infixOrder();

    }
}

/**
 * 二叉排序树
 */
class BinarySortTree {
    private Node root;

    /**
     * 添加结点
     * @param node 结点
     */
    public void add(Node node) {
        if (root == null) {
            root = node;
        } else {
            root.add(node);
        }
    }

    /**
     * 前序遍历
     */
    public void preOrder() {
        if (root != null) {
            root.preOrder();
        } else {
            System.out.println("二叉排序树为空！！");
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (root != null) {
            root.infixOrder();
        } else {
            System.out.println("二叉排序树为空！！");
        }
    }

    /**
     * 后序遍历
     */
    public void postOrder() {
        if (root != null) {
            root.postOrder();
        } else {
            System.out.println("二叉排序树为空！！");
        }
    }

    /**
     * 查找要删除的结点
     * @param value
     * @return
     */
    public Node search(int value) {
        if (root == null) {
            return null;
        } else {
            return root.search(value);
        }
    }

    /**
     * 查找父结点
     * @param value 删除的结点
     * @return 结点信息
     */
    public Node searchParent(int value) {
        if (root == null) {
            return null;
        } else {
            return root.searchParent(value);
        }
    }

    /**
     * @param node 传入的结点 二叉排序树的根节点
     * @return 返回node为跟结点的二叉排序树的最小结点值
     */
    public int deleteRightTreeMin(Node node) {
        Node target = node;
        //查找左节点,找到最小节点
        while (target.left != null) {
            target = target.left;
        }
        //删除最小结点
        deleteNode(target.value);
        return target.value;
    }

    /**
     * 删除叶子结点
     * @param value 删除的结点的值
     */
    public void deleteNode(int value) {
        if (root == null) {
            return;
        } else {
            //找到要删除的结点 targetNode
            Node targetNode = search(value);
            //没有找到删除的结点
            if (targetNode == null) {
                return;
            }
            //当前的二叉排序树只有一个结点
            if (root.left == null && root.right == null) {
                root = null;
                return;
            }
            //targetNode的父节点
            Node parent = searchParent(value);

            //删除的结点为叶子结点
            if (targetNode.left == null && targetNode.right == null) {
                // 判断 targetNode是父节点的左子结点
                if (parent.left != null && parent.left.value == value) {
                    parent.left = null;
                } else if (parent.right != null && parent.right.value == value) {
                    // targetNode是父节点的左子结点
                    parent.right = null;
                }
            } else if (targetNode.left != null && targetNode.right != null) {
                //删除两颗子树的结点
                int minValue = deleteRightTreeMin(targetNode.right);
                targetNode.value = minValue;
            } else {
                //删除一个子树的结点

                //删除的结点存在左子结点
                if (targetNode.left != null) {
                    if (parent != null) {
                        // targetNode 为 parent 的左子结点
                        if (parent.left.value == value) {
                            parent.left = targetNode.left;
                        } else {
                            //targetNode 为父parent的右子结点
                            parent.right = targetNode.left;
                        }
                    } else {
                        root = targetNode.left;
                    }
                } else {
                    if (parent != null) {
                        //删除的结点存在右子结点
                        // targetNode 为 parent 的左子结点
                        if (parent.left.value == value) {
                            parent.left = targetNode.right;
                        } else {
                            //targetNode 为父parent的右子结点
                            parent.right = targetNode.right;
                        }
                    } else {
                        root = targetNode.right;
                    }
                }
            }

        }

    }


}

/**
 * 结点
 */
class Node {
    /**
     * 值
     */
    int value;
    /**
     * 左右结点
     */
    Node left;
    Node right;

    public Node(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "Node{" + "value=" + value + '}';
    }

    /**
     * 查找要删除的结点
     * @param value 删除的结点的值
     * @return 返回改结点
     */
    public Node search(int value) {
        if (value == this.value) {
            //找到改结点
            return this;
        } else if (value < this.value) {
            //查找的值小于当前结点的值，向左递归找
            if (this.left == null) {
                return null;
            }
            return this.left.search(value);
        } else {
            //大于或等于改结点
            if (this.right == null) {
                return null;
            }
            return this.right.search(value);
        }
    }

    /**
     * 查找删除结点的父节点
     * @param value 目标查找的结点
     * @return 父节点
     */
    public Node searchParent(int value) {
        //找到目标删除的结点的父节点
        if ((this.left != null && this.left.value == value) || (this.right != null && this.right.value == value)) {
            return this;
        } else {
            //查找的值小于当前的值。当前结点的左子结点不为空
            if (value < this.value && this.left != null) {
                return this.left.searchParent(value);
            } else if (value >= this.value && this.right != null) {
                //查找的值小于当前的值。当前结点的左子结点不为空
                //向右递归
                return this.right.searchParent(value);
            } else {
                //找到不到父节点
                return null;
            }
        }

    }

    /**
     * 添加结点
     * 递归添加结点，满足二叉排序树
     * @param node 结点信息
     */
    public void add(Node node) {
        //结点为空
        if (node == null) {
            return;
        }

        if (node.value < this.value) {
            //当前结点左子结点为空
            if (this.left == null) {
                this.left = node;
            } else {
                //递归左子结点添加
                this.left.add(node);
            }
        } else {
            //添加的结点大于大于当前结点的值
            if (this.right == null) {
                //右子树为空，则添加在右结点
                this.right = node;
            } else {
                //递归向右添加
                this.right.add(node);
            }
        }
    }


    /**
     * 前序遍历
     */
    public void preOrder() {
        System.out.println(this);
        if (this.left != null) {
            this.left.preOrder();
        }
        if (this.right != null) {
            this.right.preOrder();
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (this.left != null) {
            this.left.infixOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.infixOrder();
        }
    }

    /**
     * 后序遍历
     */
    public void postOrder() {
        if (this.left != null) {
            this.left.postOrder();
        }
        if (this.right != null) {
            this.right.postOrder();
        }
        System.out.println(this);
    }

}
```





## 平衡二叉树



根据数列  {1,2,3,4,5,6}，创建一个二叉排序树（BSL）

![image-20220918151718383](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918151718383.png)

左边（BSL）==存在问题==分析

1. 左子树全部为空，从形式上看，更像一个单链表
2. 插入速度没有影响
3. 查询速度明显降低(因为需要依次比较), 不能发挥BST 的优势，因为每次还需要比较左子树，其查询速度比 单链表还慢
4. 平衡二叉树（AVL）



### 基本介绍

别名：平衡二叉搜索树（Self-balancing binary search tree），AVL树

==保证查询效率较高==

**满足二叉排序树**





### 特点

- AVL是一 棵空树或左右两个子树的==高度差的====绝对值不超过1==，且左右两个子树都是一棵平衡二叉树
- 常用实现方法
  1. 红黑树
  2. AVL
  3. 替罪羊树
  4. Treap （横二叉树）
  5. 伸展树



### 平衡二叉树 - 单旋转（左旋转）

根据数列 {4,3,6,5,7,8}，创建出对应的平衡二叉树

结点的左旋转

1. 将 A 节点的 右节点 的 左节点 ，指向 A节点
2. 将 A 节点的右节点，指向 A 节点的右节点的左节点

**左旋转原因**

- 右子树高度比左子树高度 高 并且高度差绝对值大于1

**左旋转目的**

- 降低右子树高度



**AVL树高度求解**

- 总的高度
- 右子树高度
- 左子树高度

**代码分析**

1. 创建一个新结点newNode，值为当前根节点值

2. 将新节点的左子树设置为当前节点的左子树

   newNode.left = left

3. 将新节点的右子树设置为当前节点的右子树的左子树

   newNode.right= right.left

4. 将当前节点的值为右子节点的值

   value = right.value

5. 将当前节点的右子树设置为右子树的右子树

   right = right .right

6. 将当前节点的左子树设置为新节点

   left = newNode



### 平衡二叉树 - 单旋转（右旋转）

根据数列 {10,12, 8, 9, 7, 6}，创建出对应的平衡二叉树

结点的右旋转

1. 将 A 节点的 左节点 的左节点 ，指向 A节点
2. 将 A节点的 左节点，指向 A 节点的右节点的左节点

**左旋转原因**

- 左子树高度 比 右子树高度 高 ，并且高度差绝对值大于1

**左旋转目的**

- 降低左子树高度

**AVL树高度求解**

- 总的高度
- 右子树高度
- 左子树高度



**代码分析**

1. 创建一个新结点newNode，值为当前根节点值

2. 将新节点的右子树设置为当前节点的右子树

   newNode.right= right

3. 将新节点的左子树设置为当前节点的左子树的右子树

   newNode.left= left.right

4. 将当前节点的值为右子节点的值

   value = left.value

5. 将当前节点的左子树设置为左子树的左子树

   left= left.left

6. 将当前节点的右子树设置为新节点

   right= newNode



### 平衡二叉树 - 双旋转（左右旋转）

进行单旋转(即一次旋转)就可以将非平衡二叉树转成平衡二叉树, 但是在某些情况下，单旋转不能完成平衡二

叉树的转换

![image-20220918162829954](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918162829954.png)

**双旋转原因分析**

1. 符合右旋转的条件
2. 它的左子树的右子树的高度大于它的左子树的高度
3. 对当前这个结点的左节点进行左旋转
4. 再对当前结点进行右旋转

![image-20220918214116829](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918214116829.png)

```java
package com.avl;

/**
 * @author Kcs 2022/9/18
 */
public class AvlTreeDemo {
    public static void main(String[] args) {
        //左旋转数组
        int[] arrLeft = {4, 3, 6, 5, 7, 8};
        //右旋转数组
        int[] arrRight = {10,12, 8, 9, 7, 6};
        //双旋转数组
        int[] arrDouble = {10,11, 7, 6, 8, 9};


        AvlTree avlTree = new AvlTree();

        for (int i = 0; i < arrDouble.length; i++) {
            avlTree.add(new Node(arrDouble[i]));
        }
        avlTree.infixOrder();

        System.out.println("平衡处理后~~~");
        System.out.println("当前根节点树的高度=" + avlTree.getRoot().height());
        System.out.println("树的左子树的高度=" + avlTree.getRoot().leftHeight());
        System.out.println("树的右子树的高度=" + avlTree.getRoot().rightHeight());
        System.out.println("当前根节点= "+avlTree.getRoot());
        System.out.println("当前根节点的左子节点= "+avlTree.getRoot().left);
        System.out.println("当前根节点的右子节点= "+avlTree.getRoot().right);
    }
}

/**
 * AVL树
 */
class AvlTree {
    private Node root;

    public Node getRoot() {
        return root;
    }

    /**
     * 添加结点
     * @param node 结点
     */
    public void add(Node node) {
        if (root == null) {
            root = node;
        } else {
            root.add(node);
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (root != null) {
            root.infixOrder();
        } else {
            System.out.println("二叉排序树为空！！");
        }
    }

}

/**
 * 结点
 */
class Node {
    /**
     * 值
     */
    int value;
    /**
     * 左右结点
     */
    Node left;
    Node right;

    public Node(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "Node{" + "value=" + value + '}';
    }

    /**
     * 返回当前节点的高度，以该节点为根节点的树的高度
     * @return 节点的高度
     */
    public int height() {
        return Math.max(left == null ? 0 : left.height(), right == null ? 0 : right.height()) + 1;
    }

    /**
     * 返回左子树的高度
     * @return 左子树高度
     */
    public int leftHeight() {
        if (left == null) {
            return 0;
        }
        return left.height();
    }

    /**
     * 返回右子树的高度
     * @return 右子树高度
     */
    public int rightHeight() {
        if (right == null) {
            return 0;
        }
        return right.height();
    }

    /**
     * 左旋转
     */
    private void leftRotate() {
        //1.创建一个新结点newNode，值为当前根节点值
        Node newNode = new Node(value);
        //2.将新节点的左子树设置为当前节点的左子树
        newNode.left = left;
        //3.将新节点的右子树设置为当前节点的右子树的左子树
        newNode.right = right.left;
        //4.将当前节点的值换为右子节点的值
        value = right.value;
        //5.将当前节点的右子树设置为右子树的右子树
        right = right.right;
        //6.将当前节点的左子树设置为新节点
        left = newNode;
    }

    /**
     * 右旋转
     */
    private void rightRotate() {
        // 1. 创建一个新结点newNode，值为当前根节点值
        Node newNode = new Node(value);
        // 2. 将新节点的右子树设置为当前节点的右子树
        newNode.right = right;
        // 3. 将新节点的左子树设置为当前节点的左子树的右子树
        newNode.left = left.right;
        // 4. 将当前节点的值为右子节点的值
        value = left.value;
        // 5. 将当前节点的左子树设置为左子树的左子树
        left = left.left;
        // 6. 将当前节点的右子树设置为新节点
        right = newNode;
    }

    /**
     * 添加结点
     * 递归添加结点，满足二叉排序树
     * @param node 结点信息
     */
    public void add(Node node) {
        //结点为空
        if (node == null) {
            return;
        }

        if (node.value < this.value) {
            //当前结点左子结点为空
            if (this.left == null) {
                this.left = node;
            } else {
                //递归左子结点添加
                this.left.add(node);
            }
        } else {
            //添加的结点大于大于当前结点的值
            if (this.right == null) {
                //右子树为空，则添加在右结点
                this.right = node;
            } else {
                //递归向右添加
                this.right.add(node);
            }
        }

        //右子树的高度 - 左子树的高度 > 1，则进行左旋转
        if (rightHeight() - leftHeight() > 1) {
            //它的右子树的 左子树的高度 大于 它的右子树的 右子树的高度
            if (right != null && right.leftHeight() > right.rightHeight()) {
                //先右子树右旋转
                right.rightRotate();
                //再对当前结点进行左旋转
                leftRotate();
            }else {
                //不满足，直接进行左旋转
                leftRotate();
            }
            return;
        }

        //左子树的高度 - 右子树的高度 > 1，则进行右旋转
        if (leftHeight() - rightHeight() > 1) {
            //它的左子树的右子树的高度大于它的左子树的高度
            if (left != null && left.rightHeight() > left.leftHeight()) {
                //当前结点的左子树，进行左旋转
                left.leftRotate();
                //当前结点进行右旋转
                rightRotate();
            }else {
                //直接进行右旋转
                rightRotate();
            }
        }
    }

    /**
     * 中序遍历
     */
    public void infixOrder() {
        if (this.left != null) {
            this.left.infixOrder();
        }
        System.out.println(this);
        if (this.right != null) {
            this.right.infixOrder();
        }
    }

}
```

# 多路查找树

![image-20220918215002972](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918215002972.png)



## 多叉树

![image-20220918215105024](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918215105024.png)

## B树

 ![image-20220918215806241](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918215806241.png)



结点的度：链接有多少个子结点

树的度：所有结点的度中最大的度



### B树

B-tree树 ：b树



![image-20220918222031151](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918222031151.png)



1. B树的阶：节点的最多子节点个数。比如2- 3树的阶是3，2-3-4树的阶是4 
2. B-树的搜索，从根结点开始，对结点内的 关键字（有序）序列进行二分查找，如果 命中则结束，否则进入查询关键字所属范 围的儿子结点；重复，直到所对应的儿子 指针为空，或已经是叶子结点 
3. 关键字集合分布在整颗树中, 即叶子节点 和非叶子节点都存放数据. 
4. 搜索有可能在非叶子结点结束 
5. 其搜索性能等价于在关键字全集内做一次 二分查找



### B+树

B树的变体，也是一种多路搜索树

![image-20220918222243157](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918222243157.png)

1. B+树的搜索与B树也基本相同，区别是B+树只有达到叶 子结点才命中（B树可以在非叶子结点命中），其性能 也等价于在关键字全集做一次二分查找 
2. 所有关键字都出现在叶子结点的链表中（即数据只 能在叶子节点【也叫稠密索引】），且链表中的关 键字(数据)恰好是有序的。 
3. 不可能在非叶子结点命中 
4. 非叶子结点相当于是叶子结点的索引（稀疏索引）， 叶子结点相当于是存储（关键字）数据的数据层 
5. 更适合文件索引系统 
6. B树和B+树各有自己的应用场景，不能说B+树完全 比B树好，反之亦然.

### B*树

B*树是B+树的变体，在B+树的非根和非叶子结点再增加指向兄弟的指针

![image-20220918222506625](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220918222506625.png)

1. B*树定义了非叶子结点关键字个数至少为 (2/3)*M，即块的最低使用率为2/3，而B+树 的块的最低使用率为B+树的1/2。 
2. 从第1个特点我们可以看出，B*树分配新结点 的概率比B+树要低，空间使用率更高



## 2-3 树 

最简单的B树结构



### 特点

1. 2-3树的所有叶子节点都在同一层.(只要是B树都满足这个条件)
2. 有两个子节点的节点叫二节点，二节点要么没有子节点，要么有两个子节点.
3. 有三个子节点的节点叫三节点，三节点要么没有子节点，要么有三个子节点.
4. 2-3树是由二节点和三节点构成的树。



### 分析

将数列{16, 24, 12, 32, 14, 26, 34, 10, 8, 28, 38, 20} 构建成2-3树，并保证数据插入的 大小顺序



1. 2-3树的所有叶子节点都在同一层.(只要 是B树都满足这个条件)
2. 有两个子节点的节点叫二节点，二节点 要么没有子节点，要么有两个子节点.
3. 有三个子节点的节点叫三节点，三节点 要么没有子节点，要么有三个子节点
4. 当按照规则插入一个数到某个节点时， 不能满足上面三个要求，就需要拆，先 向上拆，如果上层满，则拆本层，拆后 仍然需要满足上面3个条件。
5. 对于三节点的子树的值大小仍然遵守 (BST 二叉排序树)的规则

# 图

表示多对多的关系

图是一种数据结构，其中结点可以具有零个或多个相邻元素。

- 边（edge）：两个结点之间的连接
- 顶点（vertex）：结点
- 路径：
- 无向图：

![image-20220919200615388](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919200615388.png)

- 有向图

- 带权图

  ![image-20220919200731543](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919200731543.png)

## 图的表示方式



### 一、邻接矩阵（二维数组）

- 表示图形中顶点之间相邻关系的矩阵，对于n个顶点的图而言，矩阵是 的row和col表示的是1....n个点

  ![image-20220919201027586](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919201027586.png)



- 0：没有直接链接
- 1：有直接链接



### 二、邻接表（链表）

1. **邻接矩阵**需要为每个顶点都分配n个边的空间，其实有很多边都是不存在,会造 成空间的一定损失
2. 邻接表的实现只关心存在的边，不关心不存在的边。因此没有空间浪费，邻接 表由数组+链表组成

![image-20220919201256912](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919201256912.png)



## 图的创建



### 分析

1. 存储顶点String 使用ArraList
2. 保存矩阵 int [ ] [ ] edges



## 图的遍历



### 深度优先遍历（DFS）

1. 深度优先遍历，从初始访问结点出发，初始访问结点可能有多个邻接结点，深度优先遍历的策略就是首先访问第一个邻接结点，然后再以这个被访问的邻接 结点作为初始结点，访问它的第一个邻接结点，（每次都在访问完当前结点后首先访问当前结点的第一个邻接结点）
2. 优先往纵向挖掘深入，而不是对一个结点的 所有邻接结点进行横向访问
3. 深度优先搜索是一个递归过程



**DFS算法遍历步骤**

1. 访问初始结点v，并标记结点v为已访问
2. 查找结点v的第一个邻接结点w
3. 若w存在，则继续执行4，如果w不存在，则回到第1步，将从v的下一个结点继续
4. 若w未被访问，对w进行深度优先遍历递归（即把w当做另一个v，然后进行步骤123）
5. 查找结点v的w邻接结点的下一个邻接结点，转到步骤3

![image-20220919213943423](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919213943423.png)



### 广度优先遍历（BFS）

分层搜索的过程，广度优先遍历需要使用一个队列以保持访问过的结点的顺序， 以便按这个顺序来访问这些结点的邻接结点。



**BFS算法遍历步骤**

1. 访问初始结点v并标记结点v为已访问
2. 结点v入队列
3. 当队列非空时，继续执行，否则算法结束
4. 出队列，取得队头结点u
5. 查找结点u的第一个邻接结点w
6. 若结点u的邻接结点w不存在，则转到步骤3；否则循环执行以下三个步骤查找结点u的第一个邻接结点w
   1. 若结点w尚未被访问，则访问结点w并标记为已访问
   2. 结点w入队列
   3. 查找结点u的继w邻接结点后的下一个邻接结点w，转到步骤6

![image-20220919213930379](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919213930379.png)



### DFS与BFS比较

![image-20220919221339514](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919221339514.png)



图的实现代码：

```java
package com.graph;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.LinkedList;

/**
 * @author Kcs 2022/9/19
 */
public class Graph {

    /**
     * 存储顶点
     */
    private ArrayList<String> vertexList;

    /**
     * 存储图对应的邻接矩阵
     */
    private int[][] edges;

    /**
     * 边数目
     */
    private int numOfEdges;

    /**
     * 记录结点是否被访问到
     */
    private boolean[] isVisited;

    public static void main(String[] args) {

        //结点个数
        int n = 9;
        //顶点
        String[] vertexs = {"A", "B", "C", "D", "E"};
        //dfs与bfs比较
        // String[] vertexs = {"1", "2", "3", "4", "5","6", "7", "8"};
        //图对象
        Graph graph = new Graph(n);

        //添加顶点
        for (String value : vertexs) {
            graph.insertVertex(value);
        }
        //添加边
        graph.insertEdge(0, 1, 1);
        graph.insertEdge(0, 2, 1);
        graph.insertEdge(1, 2, 1);
        graph.insertEdge(1, 3, 1);
        graph.insertEdge(1, 4, 1);

        //dfs与bfs比较
        // graph.insertEdge(0, 1, 1);
        // graph.insertEdge(0, 2, 1);
        // graph.insertEdge(1, 3, 1);
        // graph.insertEdge(1, 4, 1);
        // graph.insertEdge(3, 7, 1);
        // graph.insertEdge(4, 7, 1);
        // graph.insertEdge(2, 5, 1);
        // graph.insertEdge(2, 6, 1);
        // graph.insertEdge(5, 6, 1);
        
        //显示图
        graph.showGraph();

        //dfs遍历
        System.out.println("================深度优先遍历================");
        graph.dfs();
        System.out.println();

        //bfs遍历
        System.out.println("================广度优先遍历================");
        graph.bfs();
    }

    /**
     * 构造器
     * @param n
     */
    public Graph(int n) {
        //初始化矩阵
        edges = new int[n][n];
        //初始化存储顶点
        vertexList = new ArrayList<String>(n);

        numOfEdges = 0;


    }

    /**
     * 第一个邻接结点的下标 w
     * @param index
     * @return 返回对应的下标
     */
    public int getFirstNeighbor(int index) {
        for (int j = 0; j < vertexList.size(); j++) {
            if (edges[index][j] > 0) {
                return j;
            }
        }
        return -1;
    }

    /**
     * 根据前一邻接结点的下标获取下一个邻接结点
     * @param v1
     * @param v2
     * @return 下一个结点的下标
     */
    public int getNextNeighbor(int v1, int v2) {
        for (int j = v2 + 1; j < vertexList.size(); j++) {
            if (edges[v1][j] > 0) {
                return j;
            }
        }
        return -1;
    }

    /**
     * 深度优先遍历算法
     * @param isVisited 访问的结点
     * @param i 首次为0
     */
    private void dfs(boolean[] isVisited, int i) {
        //访问结点
        System.out.print(getValueByIndex(i) + "—>");

        //设置结点为已经访问的结点
        isVisited[i] = true;
        //查找结点 i 的第一个邻接结点
        int w = getFirstNeighbor(i);
        while (w != -1) {
            //存在但还没有访问
            if (!isVisited[w]) {
                dfs(isVisited, w);
            }
            //w结点被访问过
            w = getNextNeighbor(i, w);
        }
    }

    /**
     * 重载dfs,遍历所有的结点，进行dfs
     */
    public void dfs() {
        //访问的结点
        isVisited = new boolean[vertexList.size()];
        //遍历所有的结点，回溯
        for (int i = 0; i < getNumOfVertex(); i++) {
            if (!isVisited[i]) {
                dfs(isVisited, i);
            }
        }
    }

    /**
     * 对结点进行广度优先遍历
     */
    private void bfs(boolean[] isVisited, int i) {
        //队列头节点对应的下标
        int u;
        //邻接结点的下标
        int w;
        //队列，结点访问的顺序
        LinkedList queue = new LinkedList();
        //访问结点
        System.out.print(getValueByIndex(i) + "=>");
        //标记isVisited
        isVisited[i] = true;

        //结点入队列
        queue.addLast(i);

        //队列不为空
        while (!queue.isEmpty()) {
            //取出头结点
            u = (Integer) queue.removeFirst();
            //得到第一邻接结点的下标 w
            w = getFirstNeighbor(u);
            //w 存在
            while (w != -1) {
                //存在但还没有访问
                if (!isVisited[w]) {
                    System.out.print(getValueByIndex(w) + "=>");
                    isVisited[w] = true;
                    //入队
                    queue.addLast(w);
                }
                //以u为前驱（或者非直接前驱）结点，找w后面的下一个结点
                w = getNextNeighbor(u, w);
            }
        }
    }

    /**
     * 重载bfs，遍历所有结点，进行广度优先搜索
     */
    public void bfs() {
        //访问的结点
        isVisited = new boolean[vertexList.size()];
        for (int i = 0; i < getNumOfVertex(); i++) {
            if (!isVisited[i]) {
                bfs(isVisited, i);
            }
        }
    }

    /**
     * 插入顶点
     * @param vertex 顶点值
     */
    public void insertVertex(String vertex) {
        vertexList.add(vertex);
    }

    /**
     * 添加边
     * @param v1 第一个顶点的下标：0开始
     * @param v2 第二个顶点的下标：0开始
     * @param weight 权值
     */
    public void insertEdge(int v1, int v2, int weight) {
        edges[v1][v2] = weight;
        edges[v2][v1] = weight;
    }

    /**
     * 返回结点的个数
     */
    public int getNumOfVertex() {
        return vertexList.size();
    }

    /**
     * 返回边的数目
     */
    public int getNumOfEdges() {
        return numOfEdges;
    }

    /**
     * 返回结点的下标
     */
    public String getValueByIndex(int i) {
        return vertexList.get(i);
    }

    /**
     * 返回v1 、v2的权值
     */
    public int getWeight(int v1, int v2) {
        return edges[v1][v2];
    }

    /**
     * 显示图
     */
    public void showGraph() {
        for (int[] link : edges) {
            System.err.println(Arrays.toString(link));
        }
    }

}
```





# 十大算法

1. 二分查找算法
2. 分治算法
3. 动态规划算法
4. KMP算法
5. 贪心算法
6. 普利姆算法
7. 克鲁斯卡尔算法
8. 迪杰斯特拉算法
9. 弗洛伊德算法
10. 马踏棋盘算法



# 二分查找算法

非递归方式

- 二分查找法只适用于从有序的数列中进行查找(比如数字和字母等)，将数列排 序后再进行查找
- 二分查找法的运行时间为对数时间O(㏒₂^n^) ，即查找到需要的目标位置最多只需 要㏒₂^n^步，假设从[0,99]的队列(100个数，即n=100)中寻到目标数30，则需要查 找步数为㏒₂^100^ , 即最多需要查找7次( 2^6^ < 100 < 2^7^)



## 非递归实现二分查找算法

数组{1，3，8，10，11，67，100}

```java
package com.kcs.binarysearchnoresursion;

/**
 * @author Kcs 2022/9/21
 */
public class BinarySearchNoRecur {
    public static void main(String[] args) {
        int[] arr = {1, 3, 8, 10, 11, 67, 100};
        int index = binarySearch(arr, 20);
        System.out.println("index = " + index);
    }


    /**
     * 二分查找算法非递归
     * @param arr 查找的数组
     * @param target 查找的目标
     * @return index
     */
    public static int binarySearch(int[] arr, int target) {
        int left = 0;
        int right = arr.length - 1;
        while (left <= right) {
            //中间值
            int mid = (left + right) / 2;
            //中间就是查找的值
            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] > target) {
                //向左查找
                right = mid - 1;
            } else {
                //向右查找
                left = mid + 1;
            }
        }
        return -1;
    }
}
```

# 分治算法（DAC）



## 介绍

- 分而治之
- 把一个复杂的问题分 成两个或更多的相同或相似的子问题，再把子问题分成更小的子问题……直到最后子问题 可以简单的直接求解，原问题的解即子问题的解的合并

### 求解经典问题

1. 二分搜索
2. 大整数乘法
3. 棋盘覆盖
4. 合并排序
5. 快速排序
6. 线性时间选择
7. 最接近点问题
8. 循环赛日程表
9. 汉诺塔



## 步骤

分治法每一层递归都有三个步骤

1. 分解：将原问题分解为若干个规模较小，相互独立，与原问题形式相同的子问题
2. 解决：若子问题规模较小而容易被解决则直接解，否则递归地解各个子问题
3. 合并：将各个子问题的解合并为原问题的解

![image-20220919224538606](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919224538606.png)



![image-20220919225902477](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919225902477.png)



## 汉诺塔分析

![image-20220919230241177](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919230241177.png)

1. 如果是有一个盘， A->C
   - 如果我们有 n >= 2 情况，我们总是可以看做是两个盘 1.最下边的盘 2. 上面的盘
2. 先把 最上面的盘 A->B
3. 把最下边的盘 A->C
4. 把B塔的所有盘从 B->C

```java
package com.kcs.dac;

/**
 * @author Kcs 2022/9/21
 */
public class HanoiTower {

    private static int count = 0;

    public static void main(String[] args) {
        hanoiTower(5, 'A', 'B', 'C');
        System.out.println("移动步数："+count);
    }
    
    /**
     * 分治算法
     * 移动汉诺塔
     * @param num 总共几个盘
     * @param a a 、b、c柱子
     * @param b
     * @param c
     */
    public static void hanoiTower(int num, char a, char b, char c) {
        count++;
        //只有一个盘
        if (num == 1) {
            System.out.println("第1个盘从 " + a + "->" + c);
        } else {
            //num >2时
            //A->B,最上面的盘
            hanoiTower(num - 1, a, c, b);
            //A->C 最下面的盘
            System.out.println("第" + num + "个盘从 " + a + "->" + c);
            //B->C B塔的盘
            hanoiTower(num - 1, b, a, c);
        }
    }
}
```

# 动态规划算法（DP）

（Dynamic Programming）

## 介绍

1. 将大问题划分为小问题进 行解决，从而一步步获取最优解的处理算法
2. 将待求解问题分解成若干个子 问题，先求解子问题，然后从这些子问题的解得到原问题的解
3. 与分治法不同的是，适合于用动态规划求解的问题，经分解得到子问题往往不 是互相独立的。 ( 即下一个子阶段的求解是建立在上一个子阶段的解的基础上， 进行进一步的求解 )
4. 动态规划可以通过填表的方式来逐步推进，得到最优解】

## 动态规划--背包问题

![image-20220919230600384](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220919230600384.png)

### 分析

1. 背包问题主要是指一个给定容量的背包、若干具有一定价值和重量的物品，如何选 择物品放入背包使物品的价值最大。其中又分01背包和完全背包(完全背包指的是： 每种物品都有无限件可用)
2. ==这里的问题属于01背包，即每个物品最多放一个。而无限背包可以转化为01背包==。
3. 算法的主要思想，利用动态规划来解决。每次遍历到的第i个物品，根据 w[i] 和 v[i] 来确定是否需要将该物品放入背包中。即对于给定的n个物品，设v[i]、w[i]分别为第 i 个物品的价值和重量，C为背包的容量。
   1. v[ i ] [ 0 ]=v[ 0 ] [ j ]=0; //表示填入表第一行和第一列是0
   2. 当w[i]> j 时：v[ i ] [ j ]=v[i-1] [ j ] // 当准备加入新增的商品的容量大于 当前背包的容量时，就直接使用上一个单元格的装入策略
   3. 当j>=w[i]时： v[ i ] [ j ]=max{v[ i-1] [ j ], v [ i ]+ v[ i-1] [ j - w[ i ] ]} 
4. 当准备加入的新增的商品的容量小于等于当前背包的容量
   - 装入的方式: v[i-1] [ j ]： 就是上一个单元格的装入的最大值 
   - v[ i ]：表示当前商品的价值
   - w[ j ]：表示当前商品的重量
   - v[i-1] [ j-w [ i ] ] ： 装入i-1商品，到剩余空间 j - w[ i ] 的最大值 
   - 当 j >=w[ i ]时： v[ i ] [ j ]=max{v[i-1] [ j ], v[i]+v[i-1] [j-w[ i ] ] } 


```java
package com.kcs.dynamic;

/**
 * @author Kcs 2022/9/21
 */
public class KnapsackProblem {
    public static void main(String[] args) {
        //物品重量
        int[] weight = {1, 4, 3, 2};
        //物品价值
        int[] value = {1500, 3000, 2000, 2100};
        //背包容量
        int m = 10;
        //物品个数
        int n = value.length;

        //记录放入的商品
        int[][] path = new int[n + 1][m + 1];

        //二维数组存放第i个物品中能够装入容量为j的背包中的最大价值
        int[][] v = new int[n + 1][m + 1];

        //初始化第一行、第一列，默认为0
        for (int i = 0; i < v.length; i++) {
            for (int j = 0; j < v[0].length; j++) {
                v[0][j] = 0;
                v[i][0] = 0;
            }
        }

        //动态规划处理
        //不处理第一行，i从1开始
        for (int i = 1; i < v.length; i++) {
            //不处理第一列 ，j从1开始
            for (int j = 1; j < v[0].length; j++) {
                // 此处为 i - 1
                if (weight[i - 1] > j) {
                    //当准备加入新增的商品的容量大于当前背包的容量时，就直接使用上一个单元格的装入策略
                    v[i][j] = v[i - 1][j];
                } else {
                    //i从1开始 修改成value[i-1] + v[i - 1][j - weight[i-1]]
                    // v[i][j] = Math.max(v[i - 1][j], value[i - 1] + v[i - 1][j - weight[i - 1]]);

                    //替代上面的公式
                    if (v[i - 1][j] < value[i - 1] + v[i - 1][j - weight[i - 1]]) {
                        v[i][j] = value[i - 1] + v[i - 1][j - weight[i - 1]];
                        //获得当前的路径
                        path[i][j] = 1;
                    } else {
                        v[i][j] = v[i - 1][j];
                    }

                }
            }
        }


        //遍历二维数组
        for (int i = 0; i < v.length; i++) {
            for (int j = 0; j < v[i].length; j++) {
                System.out.print(v[i][j] + "\t");
            }
            System.out.println();
        }

        System.out.println("================放入背包方案=====================");
        //输出最合理的商品放入背包方案

        //行的最大下标
        int i = path.length - 1;
        //列的最大下标
        int j = path[0].length - 1;
        //逆向遍历
        while (i > 0 && j > 0) {
            if (path[i][j] == 1) {
                System.out.printf("第%d商品放入背包。\n", i);
                j -= weight[i - 1];
            }
            i--;
        }
    }
}
```

# KMP算法

## 应用场景-字符串匹配问题

字符串匹配问题：

1. 有一个字符：str1 = "hello world Java 欢迎来到我的世界 我的世界 的世界"
2. 子字符串：str2 = "我的世界"
3. 现在要判断 str1 是否含有 str2, 如果存在，就返回第一次出现的位置, 如果没有， 则返回-1

## 解决方案

### 1.暴力破解

![image-20220921213721777](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921213721777.png)

```java
package com.kcs.kmp;

import sun.security.timestamp.TSRequest;

/**
 * @author Kcs 2022/9/21
 */
public class ViolenceMatch {
    public static void main(String[] args) {
        String str1 = "hello world Java 欢迎来到我的世界 我的世界 的世界";
        String str2 = "欢迎来到我的世界";
        int index = violenceMatch(str1, str2);
        System.out.println(index);
    }

    public static int violenceMatch(String str1, String st2) {
        char[] s1 = str1.toCharArray();
        char[] s2 = st2.toCharArray();

        int s1len = s1.length;
        int s2len = s2.length;

        // s1索引
        int i = 0;
        // s2索引
        int j = 0;
        while (i < s1len && j < s2len) {
            if (s1[i] == s2[j]) {
                i++;
                j++;
            } else {
                i = i - (j - 1);
                j = 0;
            }
        }
        if (j == s2len) {
            return i - j;
        }
        return -1;
    }
}
```

### 2.KMP算法



## KMP介绍

- KMP是一个解决模式串在文本串是否出现过，如果出现过，找出最早出现的位置的经典算法
- KMP方法算法就利用之前判断过信息，通过一个next数组，保存模式串中前后 最长公共子序列的长度，每次回溯时，通过next数组找到，前面匹配过的位置， 省去了大量的计算时间
- [KMP介绍](https://www.cnblogs.com/zzuuoo666/p/9028287.html)
- 不要把 搜索位置移回已经比较过的位置，继续把它向后移
- 后移位数公式：==移动位数 = 已匹配的字符数 - 对应的部分匹配值==



## 最佳应用-匹配字符串

1. 有一个字符串 str1= "BBC ABCDAB ABCDABCDABDE"，和一个子串 str2="ABCDABD"
2. 现在要判断 str1 是否含有 str2, 如果存在，就返回第一次出现的位置, 如果没有， 则返回-1
   1.  先得到字串的部分匹配表
   2. 使用部分匹配表完成KMP匹配

```java
package com.kcs.kmp;

import java.util.Arrays;

/**
 * @author Kcs 2022/9/21
 */
public class KmpAlgorithmDemo {
    /**
     * 搜索思路分析：
     * 遇到不匹配的字符,主串的指针不必移动,模式串的指针移动到 对应模式串不匹配字符下标next数组中对应的数值
     * 相当于后缀与前缀中间的字串已经匹配过了,不必再匹配
     * 且next数组中记录的是前后缀最长公共长度。
     * 所以字符串的第一个字符(即前缀的第一个字符)跳转到后缀的第一个字符位置
     * 但是模式串并不重新再扫描前缀,因为前后缀字符串一样,而是从前缀的下一个字符开始进行匹配
     */
    public static void main(String[] args) {

        String str1 = "BBC ABCDAB ABCDABCDABDE";
        String str2 = "ABCDABD";

        int[] next = kmpNext(str2);
        System.out.println("next = " + Arrays.toString(next));

        int index = kmpSearch(str1, str2, next);
        System.out.println("index=" + index);

    }

    /**
     * kmp搜索算法
     * @param str1 源字符串
     * @param str2 子串
     * @param next 部分匹配表, 是子串对应的部分匹配表
     * @return -1没有匹配到，否则返回第一个匹配的位置
     */
    public static int kmpSearch(String str1, String str2, int[] next) {

        for (int i = 0, j = 0; i < str1.length(); i++) {
            //不相等
            while (j > 0 && str1.charAt(i) != str2.charAt(j)) {
                j = next[j - 1];
            }
            if (str1.charAt(i) == str2.charAt(j)) {
                j++;
            }
            if (j == str2.length()) {
                return i - j + 1;
            }
        }
        return -1;
    }

    //dest是子串
    public static int[] kmpNext(String dest) {

        int[] next = new int[dest.length()];
        // 如果字符串是长度为1 部分匹配值就是0
        next[0] = 0;
        for (int i = 1, j = 0; i < dest.length(); i++) {
            while (j > 0 && dest.charAt(i) != dest.charAt(j)) {
                //不匹配的前一位
                j = next[j - 1];
            }
            if (dest.charAt(i) == dest.charAt(j)) {
                j++;
            }
            next[i] = j;
        }
        return next;
    }
}
```



# 贪心算法

## 介绍

1. 贪婪算法(贪心算法)是指在对问题进行求解时，在每一步选择中都采取最好或 者最优(即最有利)的选择，从而希望能够导致结果是最好或者最优的算法
2. ==贪婪算法所得到的结果不一定是最优的结果(有时候会是最优解)，但是都是相 对近似(接近)最优解的结果==



## 最佳应用-集合覆盖

1. 假设存在如下表的需要付费的广播台，以及广播台信号可以覆盖的地区。 如何 选择最少的广播台，让所有的地区都可以接收到信号

   ![image-20220921223603439](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921223603439.png)

2. 使用穷举法实现,列出每个可能的广 播台的集合，这被称为幂集。假设总的有n个广播台，则广播台的组合总共有 2ⁿ -1 个,假设每秒可以计算10个子集

   ![image-20220921223650172](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921223650172.png)

3. 因为需要覆盖全部地区的最小集合

   1. 遍历所有的广播电台, 找到一个覆盖了最多未覆盖的地区的电台(此电台可能包 含一些已覆盖的地区，但没有关系）
   2. 将这个电台加入到一个集合中(比如ArrayList), 想办法把该电台覆盖的地区在下 次比较时去掉
   3. 重复第1步直到覆盖了全部的地区



# 普利姆算法

## 应用场景

![image-20220921224056588](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224056588.png)

## 最小生成树（MST）

1. 最小生成树：给定一个带权的无向连通图,如何选取一棵生成树,使树上所有边上权的总和为最小
2. N个顶点，一定有N-1条边
3. 包含全部顶点
4. N-1条边都在图中

![image-20220921224222530](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224222530.png)

## 普利姆算法介绍

![image-20220921224253451](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224253451.png)



## 应用实例

![image-20220921224347266](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224347266.png)



### 图解

1. 假如从A顶点开始处理，将A放入集合中，并可连接到其他顶点有C、G、B

   ![image-20220922220814966](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220922220814966.png)

2. 此时这三条边的最小权重值是A-G 为2，于是我们G放入集合中，《A，G》

   ![image-20220922220849361](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220922220849361.png)

3. 此时这五条边的最小权重值是B-B 为3，于是我们B放入集合中，《A，G，B》

   ![image-20220922220907688](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220922220907688.png)

4. 此时这四条边的最小权重值是G-E 为4，于是我们E放入集合中，《A，G，B，E》

   ![image-20220922220929034](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220922220929034.png)

5. 此时这五条边的最小权重值是E-F 为5，以此类推加入到集合中

   最后的集合结果应该是<A，G，B，E，F，D，C>

   ![image-20220922220952663](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220922220952663.png)

#### 普里姆代码思路分析

1. 需要一个存放顶点的char数组，以及顶点的边数
2. 需要使用邻接矩阵来表示顶点之间的连接情况与权重值
3. 需要生成minTree树
4. 需要创建图

```java
package com.kcs.prim;

import java.util.Arrays;

/**
 * @author Kcs 2022/9/22
 */
public class PrimAlgorithm {
    public static void main(String[] args) {

        char[] data = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        //顶点的个数就是data的长度
        int verxs = data.length;
        //邻接矩阵的关系使用二维数组表示,10000：表示两个点不联通
        int[][] weight = {
                {10000, 5, 7, 10000, 10000, 10000, 2},
                {5, 10000, 10000, 9, 10000, 10000, 3},
                {7, 10000, 10000, 10000, 8, 10000, 10000},
                {10000, 9, 10000, 10000, 10000, 4, 10000},
                {10000, 10000, 8, 10000, 10000, 5, 4},
                {10000, 10000, 10000, 4, 5, 10000, 6},
                {2, 3, 10000, 10000, 4, 6, 10000},};
        Graph graph = new Graph(verxs);
        Tree tree = new Tree();
        tree.createGraph(graph, verxs, data, weight);
        Tree.prim(graph, 0);

    }
}

/**
 * 创建树
 */
class Tree {
    /**
     * 创建图的邻接矩阵
     * @param graph 图
     * @param vertexes 顶点
     * @param data 图各个顶点的值
     * @param weight 图的邻接矩阵
     */
    public void createGraph(Graph graph, int vertexes, char[] data, int[][] weight) {

        //顶点
        for (int i = 0; i < vertexes; i++) {
            //顶点的值赋值给图
            graph.data[i] = data[i];
            for (int j = 0; j < vertexes; j++) {
                //邻接矩阵赋给图
                graph.weight[i][j] = weight[i][j];
            }
        }
    }

    /**
     * 显示图的邻接矩阵
     * @param graph 图
     */
    public void showGraph(Graph graph) {
        //把二维数组（邻接矩阵）的每一行输出来
        for (int[] link : graph.weight) {
            System.out.println(Arrays.toString(link));
        }

    }

    /**
     * 普利姆算法
     * 把图 转成 最小生成树
     * @param graph 图
     * @param v 图从结点生成的最小生成树
     */
    public static void prim(Graph graph, int v) {

        //最小生成树的总最小权值
        int totalWeight = 0;
        //isVisited：表示顶点是否被访问过，1：已访问过  0：没有被访问过
        int[] isVisited = new int[graph.vertexes];
        //第一个顶点设置为已访问
        isVisited[v] = 1;
        //循环中的两个顶点的下标
        int h1 = -1;
        int h2 = -1;
        //最小值10000：两个顶点之间没有边
        int minWeight = 10000;
        //n个顶点的图会生成n-1 条边的最小生成树 ，所以遍历图的顶点的时候要从1开始
        for (int k = 1; k < graph.vertexes; k++) {
            //对已访问的顶点和未被访问的顶点开始for循环遍历
            for (int i = 0; i < graph.vertexes; i++) {
                //设i为已访问过的顶点
                for (int j = 0; j < graph.vertexes; j++) {
                    //设j为未被访问过的顶点
                    //graph.weight[i][j] < minWeight 两个顶点之间的边
                    //两个顶点只要有边，其值graph.weight[i][j]肯定小于minWeight，初始化的minWeight为10000
                    if (isVisited[i] == 1 && isVisited[j] == 0
                            && graph.weight[i][j] < minWeight) {
                        //for循环刚开始二者有边
                        minWeight = graph.weight[i][j];
                        //保存二者的下标
                        h1 = i;
                        h2 = j;
                    }
                }
            }
            //每退出前面两个for循环就把minWeight保存
            totalWeight += minWeight;
            System.out.println("边< " + graph.data[h1] + "," + graph.data[h2] + " > 权值为： " + minWeight);
            //退出前面两个for循环之后，找到已被访问顶点和其周边未被访问的顶点的 最小权值的边
            //把未被访问的顶点设置为已被访问
            isVisited[h2] = 1;
            //将最小值设重新置为10000，方便第一个for循环重新构成最小生成树
            minWeight = 10000;
        }
        System.out.println("该最小生成树的路径为 " + totalWeight);
    }

}

class Graph {
    /**
     * 存放边
     */
    int vertexes;
    /**
     * 存放结点数据
     */
    char[] data;
    /**
     * 存放边，就是邻接矩阵
     */
    int[][] weight;

    public Graph(int vertexes) {
        this.vertexes = vertexes;
        data = new char[vertexes];
        weight = new int[vertexes][vertexes];
    }
}
```





# 克鲁斯卡尔算法

## 介绍

1. 克鲁斯卡尔(Kruskal)算法，是用来求加权连通图的最小生成树的算法
2. 基本思想：按照权值从小到大的顺序选择n-1条边，并保证这n-1条边不构成回路
3. 具体做法：首先构造一个只含n个顶点的森林，然后依权值从小到大从连通网中选择边加入到森林中，并使森林中不产生回路，直至森林变成一棵树为止



## 应用实例

![image-20220921224559954](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224559954.png)

## 分析

1. 先构造一个含有N个顶点的森林，然后依照权值从小到大从连通网中选择边加入到森林中，并使森林中不产生回路，直至森林变成一棵树为止。
2. 从排序好的边的初始顶点开始遍历，通过getPosition获取开始顶点和该边另一条结点的位置，分别获取它们的终点（getEnd），再比较二者的值，如果不相等则说明没有构成回路，就将其起点的终点标记为边的另一个顶点，并将该边加入到rets集合中

### 图解（用数组 R 保存最小生成树）

![image-20220923191433380](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923191433380.png)

![image-20220923191517015](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923191517015.png)

![image-20220923191528801](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923191528801.png)

![image-20220923191540188](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923191540188.png)

第1步：将边<E,F>加入 R 中。

边<E,F>的权值最小，因此将它加入到最小生成树结果 R 中。

第2步：将边<C,D>加入 R 中。

上一步操作之后，边<C,D>的权值最小，因此将它加入到最小生成树结果 R 中。

第3步：将边<D,E>加入 R 中。

上一步操作之后，边<D,E>的权值最小，因此将它加入到最小生成树结果 R 中。

第4步：将边<B,F>加入 R 中。

上一步操作之后，边<C,E>的权值最小，但<C,E>会和已有的边构成回路；因此，跳过边<C,E>。同理，跳过边<C,F>。将边<B,F>加入到最小生成树结果 R 中。

第5步：将边<E,G>加入 R 中。

上一步操作之后，边<E,G>的权值最小，因此将它加入到最小生成树结果 R 中。

第6步：将边<A,B>加入 R 中。
上一步操作之后，边<F,G>的权值最小，但<F,G>会和已有的边构成回路；因此，跳过边<F,G>。同理，跳过边<B,C>。将边<A,B>加入到最小生成树结果 R 中。

此时，最小生成树构造完成！它包括的边依次是：***<E,F> <C,D> <D,E> <B,F> <E,G> <A,B>***



```java
package com.kcs.kruskal;

import java.util.Arrays;

/**
 * @author Kcs 2022/9/23
 */

public class KruskalCase {

    /**
     * 边的个数
     */
    private int edgeNum;
    /**
     * 顶点数组
     */
    private char[] vertexs;
    /**
     * 邻接矩阵
     */
    private int[][] matrix;
    //使用 INF 表示两个顶点不能连通
    private static final int INF = Integer.MAX_VALUE;

    public static void main(String[] args) {
        char[] vertexs = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        //克鲁斯卡尔算法的邻接矩阵
        int matrix[][] = {
                /*A*//*B*//*C*//*D*//*E*//*F*//*G*/
                /*A*/ {   0,  12, INF, INF, INF,  16,  14},
                /*B*/ {  12,   0,  10, INF, INF,   7, INF},
                /*C*/ { INF,  10,   0,   3,   5,   6, INF},
                /*D*/ { INF, INF,   3,   0,   4, INF, INF},
                /*E*/ { INF, INF,   5,   4,   0,   2,   8},
                /*F*/ {  16,   7,   6, INF,   2,   0,   9},
                /*G*/ {  14, INF, INF, INF,   8,   9,   0}};
        //创建KruskalCase 对象实例
        KruskalCase kruskalCase = new KruskalCase(vertexs, matrix);
        //输出构建的
        kruskalCase.print();
        kruskalCase.kruskal();

    }

    //构造器
    public KruskalCase(char[] vertexs, int[][] matrix) {
        //初始化顶点数和边的个数
        int vlen = vertexs.length;

        //初始化顶点, 复制拷贝的方式
        this.vertexs = new char[vlen];
        for(int i = 0; i < vertexs.length; i++) {
            this.vertexs[i] = vertexs[i];
        }

        //初始化边, 使用的是复制拷贝的方式
        this.matrix = new int[vlen][vlen];
        for(int i = 0; i < vlen; i++) {
            for(int j= 0; j < vlen; j++) {
                this.matrix[i][j] = matrix[i][j];
            }
        }
        //统计边的条数
        for(int i =0; i < vlen; i++) {
            for(int j = i+1; j < vlen; j++) {
                if(this.matrix[i][j] != INF) {
                    edgeNum++;
                }
            }
        }

    }
    public void kruskal() {
        int index = 0; //表示最后结果数组的索引
        int[] ends = new int[edgeNum]; //用于保存"已有最小生成树" 中的每个顶点在最小生成树中的终点
        //创建结果数组, 保存最后的最小生成树
        EData[] rets = new EData[edgeNum];

        //获取图中 所有的边的集合 ， 一共有12边
        EData[] edges = getEdges();
        System.out.println("图的边的集合=" + Arrays.toString(edges) + " 共"+ edges.length); //12

        //按照边的权值大小进行排序(从小到大)
        sortEdges(edges);

        //遍历edges 数组，将边添加到最小生成树中时，判断是准备加入的边否形成了回路，如果没有，就加入 rets, 否则不能加入
        for(int i=0; i < edgeNum; i++) {
            //获取到第i条边的第一个顶点(起点)
            int p1 = getPosition(edges[i].start); //p1=4
            //获取到第i条边的第2个顶点
            int p2 = getPosition(edges[i].end); //p2 = 5

            //获取p1这个顶点在已有最小生成树中的终点
            int m = getEnd(ends, p1); //m = 4
            //获取p2这个顶点在已有最小生成树中的终点
            int n = getEnd(ends, p2); // n = 5
            //是否构成回路
            if(m != n) { //没有构成回路
                ends[m] = n; // 设置m 在"已有最小生成树"中的终点 <E,F> [0,0,0,0,5,0,0,0,0,0,0,0]
                rets[index++] = edges[i]; //有一条边加入到rets数组
            }
        }
        //<E,F> <C,D> <D,E> <B,F> <E,G> <A,B>。
        //统计并打印 "最小生成树", 输出  rets
        System.out.println("最小生成树为");
        for(int i = 0; i < index; i++) {
            System.out.println(rets[i]);
        }


    }

    //打印邻接矩阵
    public void print() {
        System.out.println("邻接矩阵为: \n");
        for(int i = 0; i < vertexs.length; i++) {
            for(int j=0; j < vertexs.length; j++) {
                System.out.printf("%12d", matrix[i][j]);
            }
            System.out.println();//换行
        }
    }

    /**
     * 功能：对边进行排序处理, 冒泡排序
     * @param edges 边的集合
     */
    private void sortEdges(EData[] edges) {
        for(int i = 0; i < edges.length - 1; i++) {
            for(int j = 0; j < edges.length - 1 - i; j++) {
                if(edges[j].weight > edges[j+1].weight) {
                    //交换
                    EData tmp = edges[j];
                    edges[j] = edges[j+1];
                    edges[j+1] = tmp;
                }
            }
        }
    }
    /**
     *
     * @param ch 顶点的值，比如'A','B'
     * @return 返回ch顶点对应的下标，如果找不到，返回-1
     */
    private int getPosition(char ch) {
        for(int i = 0; i < vertexs.length; i++) {
            if(vertexs[i] == ch) {
                //找到
                return i;
            }
        }
        //找不到,返回-1
        return -1;
    }
    /**
     * 功能: 获取图中边，放到EData[] 数组中，后面我们需要遍历该数组
     * 是通过matrix 邻接矩阵来获取
     * EData[] 形式 [['A','B', 12], ['B','F',7], .....]
     * @return
     */
    private EData[] getEdges() {
        int index = 0;
        EData[] edges = new EData[edgeNum];
        for(int i = 0; i < vertexs.length; i++) {
            for(int j=i+1; j <vertexs.length; j++) {
                if(matrix[i][j] != INF) {
                    edges[index++] = new EData(vertexs[i], vertexs[j], matrix[i][j]);
                }
            }
        }
        return edges;
    }
    /**
     * 功能: 获取下标为i的顶点的终点(), 用于后面判断两个顶点的终点是否相同
     * @param ends ： 数组就是记录了各个顶点对应的终点是哪个,ends 数组是在遍历过程中，逐步形成
     * @param i : 表示传入的顶点对应的下标
     * @return 返回的就是 下标为i的这个顶点对应的终点的下标, 一会回头还有来理解
     */
    private int getEnd(int[] ends, int i) { // i = 4 [0,0,0,0,5,0,0,0,0,0,0,0]
        while(ends[i] != 0) {
            i = ends[i];
        }
        return i;
    }

}

/**
 * 创建一个类EData ，它的对象实例就表示一条边
 */
class EData {
    /**
     * 边的一个点
     */
    char start;
    /**
     * 边的另外一个点
     */
    char end;
    /**
     * 边的权值
     */
    int weight;
    public EData(char start, char end, int weight) {
        this.start = start;
        this.end = end;
        this.weight = weight;
    }
    @Override
    public String toString() {
        return "EData [<" + start + ", " + end + ">= " + weight + "]";
    }
}
```

# 迪杰斯特拉算法

## 介绍

- 迪杰斯特拉(Dijkstra)算法是典型最短路径算法，用于计算一个结点到其他结点的最 短路径。 
- 主要特点是以起始点为中心向外层层扩展(广度优先搜索思想)，直到扩展到终点为止

![image-20220921224654261](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224654261.png)

![image-20220923192312587](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923192312587.png)



## 应用实例

![image-20220921224744201](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224744201.png)



```java
package com.kcs.dijkstra;

import java.util.Arrays;

/**
 * @author Kcs 2022/9/23
 */
public class DijkstraAlgorithm {
    // 不连通
    public static final int INF = 65535;
    public static void main(String[] args) {
        char[] vertexs = {'A','B','C','D','E','F','G'};
        int[][] matrix = new int[vertexs.length][vertexs.length];
        matrix[0]= new int[]{INF, 5, 7, INF, INF, INF, 2};
        matrix[1]= new int[]{5, INF, INF, 9, INF, INF, 3};
        matrix[2]= new int[]{7, INF, INF, INF, 8, INF, INF};
        matrix[3]= new int[]{INF, 9, INF, INF, INF, 4, INF};
        matrix[4]= new int[]{INF, INF, 8, INF, INF, 5, 4};
        matrix[5]= new int[]{INF, INF, INF, 4, 5, INF, 6};
        matrix[6]= new int[]{2, 3, INF, INF, 4, 6, INF};

        // 创建Graph对象
        Graph graph = new Graph(vertexs, matrix);
        graph.showGraph();
        //要开始寻找的顶点下标
        int index = 6;
        graph.dijkstra(index);
        graph.showDijkstra(index);
    }
}

class Graph {
    /**
     * 顶点数组
     */
    private final char[] vertex;
    /**
     * 邻接矩阵
     */
    private final int[][] matrix;
    /**
     * 已访问顶点集合
     */
    private VistedVertex vv; 

    // 构造器
    public Graph(char[] vertex, int[][] matrix) {
        this.vertex = vertex;
        this.matrix = matrix;
    }

    // 显示结果
    public void showDijkstra(int index) {
        vv.print(index);
    }

    // 显示图
    public void showGraph() {
        for (int[] link : this.matrix) {
            System.out.println(Arrays.toString(link));
        }
    }

    /**
     * dijkstra 算法
     * @param index index
     */
    public void dijkstra(int index) {
        vv = new VistedVertex(vertex.length, index);
        // 更新 index 下标顶点到周围顶点的距离和周围顶点的前驱顶点
        update(index);
        for (int j = 1; j < vertex.length; j++) {
            // 选择并返回新的访问顶点
            index = vv.updateArr();
            // 更新 index 下标顶点到周围顶点的距离和周围顶点的前驱顶点
            update(index);
        }
    }

    /**
     * 更新 index 下标顶点到周围顶点的距离和周围顶点的前驱顶点
     * @param index
     */
    public void update(int index) {
        int len;
        for (int i = 0; i < matrix[index].length; i++) {
            // len 含义是 : 出发顶点到 index 顶点的距离 + 从 index 顶点到 i 顶点的距离的和
            len = vv.getDis(index) + matrix[index][i];
            // 如果 i 顶点没有被访问过，并且 len 小于出发顶点到 i 顶点的距离，就需要更新
            if (!vv.in(i) && len < vv.getDis(i)) {
                //更新 i 顶点的前驱为 index 顶点
                vv.updatePre(i, index);
                //更新出发顶点到 i 顶点的距离
                vv.updateDis(i, len);
            }
        }
    }
}

// 已访问顶点集合
class VistedVertex {
    // 记录各个顶点是否被访问过 (1 表示访问过,0 未访问)会动态更新
    public int[] already_arr;
    // 每个下标对应的值为前一个顶点下标, 会动态更新
    public int[] pre_visited;
    // 记录出发顶点到其他所有顶点的距离,比如 G 为出发顶点，就会记录 G 到其它顶点的距离
    // 会动态更新，求的最短距离就会存放到 dis
    public int[] dis;

    /**
     * 构造器
     * @param length 顶点的个数
     * @param index 出发顶点对应的下标 eg: G -> 6
     */
    public VistedVertex(int length, int index) {
        this.already_arr = new int[length];
        this.pre_visited = new int[length];
        this.dis = new int[length];
        // 初始化 dis 数组
        Arrays.fill(dis, DijkstraAlgorithm.INF);
        // 设置出发顶点已被访问过
        this.already_arr[index] = 1;
        // 设置出发顶点的访问距离为 0
        this.dis[index] = 0;
    }

    /**
     *  判断 index 顶点是否被访问过
     * @param index 顶点对应的下标
     * @return 若访问过就返回true，否则返回false
     */
    public boolean in(int index) {
        return already_arr[index] == 1;
    }

    /**
     * 更新出发顶点到 index 顶点之间的距离
     * @param index 顶点对应的下标
     * @param len 距离
     */
    public void updateDis(int index, int len) {
        this.dis[index] = len;
    }

    /**
     * 更新 pre 顶点的前驱为 index 顶点
     * @param pre 当前前驱顶点对应的下标
     * @param index 要更新的前驱顶点对应的下标
     */
    public void updatePre(int pre, int index) {
        this.pre_visited[pre] = index;
    }

    // 返回出发顶点到 index 顶点之间的距离
    public int getDis(int index) {
        return this.dis[index];
    }

    // 继续选择并返回新的访问顶点
    // 比如这里的 G 完后，就是 A 点作为新的访问顶点(注意不是出发顶点)
    public int updateArr() {
        int min = DijkstraAlgorithm.INF;
        int index = 0;
        for (int i = 0; i < already_arr.length; i++) {
            if (already_arr[i] == 0 && dis[i] < min) {
                min = dis[i];
                index = i;
            }
        }
        // 更新 index 顶点已被访问过
        already_arr[index] = 1;
        return index;
    }

    // 打印最后的结果
    public void print(int index) {
        System.out.println("\nalready_arr==========================");
        for (int i : already_arr) {
            System.out.print(i + " ");
        }
        System.out.println("\npre_visited==========================");
        for (int i : pre_visited) {
            System.out.print(i + " ");
        }
        System.out.println("\ndis==================================");
        for (int i : dis) {
            System.out.print(i + " ");
        }
        System.out.println();
        char[] vertexs = {'A','B','C','D','E','F','G'};
        int count = 0;
        for (int i : dis) {
            if (i != DijkstraAlgorithm.INF) {
                System.out.print(vertexs[index] + "->" + vertexs[count] + "的距离：" + i + "\t");
            } else {
                System.out.println("INF");
            }
            count++;
        }
    }
}
```



# 弗洛伊德算法

## 介绍

- 弗洛伊德算法中每一个顶点都是 出发访问点，所以需要将每一个顶点看做被访问顶点， 求出从每一个顶点到其他顶点的最短路径



## 分析

![image-20220921224903523](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224903523.png)



## 应用实例

![image-20220921224937299](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921224937299.png)

## 图解

![image-20220923192415291](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923192415291.png)

![image-20220923192443380](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923192443380.png)

![image-20220923192459657](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220923192459657.png)

5. 更换中间顶点，循环执行操作，直到所有顶点都作为中间顶点更新后，计算结束

规律：

- 若以D为中间顶点，则循环会从dis矩阵中找 (A,B,C,E,F,G)-D的距离 + D-(B,C,E,F,G)的距离来更新(A,B,C,E,F,G)-(A,B,C,E,F,G)的距离



```java
package com.kcs.floyd;

import java.util.Arrays;

/**
 * @author Kcs 2022/9/23
 */
public class FloydAlgorithm {
    // 不连通
    public static final int INF = 65535;

    public static void main(String[] args) {
        char[] vertexs = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
        int[][] matrix = new int[vertexs.length][vertexs.length];
        matrix[0] = new int[]{0, 5, 7, INF, INF, INF, 2};
        matrix[1] = new int[]{5, 0, INF, 9, INF, INF, 3};
        matrix[2] = new int[]{7, INF, 0, INF, 8, INF, INF};
        matrix[3] = new int[]{INF, 9, INF, 0, INF, 4, INF};
        matrix[4] = new int[]{INF, INF, 8, INF, 0, 5, 4};
        matrix[5] = new int[]{INF, INF, INF, 4, 5, 0, 6};
        matrix[6] = new int[]{2, 3, INF, INF, 4, 6, 0};

        FGraph graph = new FGraph(matrix, vertexs);
        graph.floyd();
        graph.show();
    }
}

/**
 * 创建图
 */
class FGraph {
    /**
     * 顶点数组
     */
    private char[] vertex;
    /**
     * 保存各个顶点到其他顶点之间的距离（最后的结果也会保存在该数组中）
     */
    private int[][] dis;
    /**
     * 保存到达目标顶点的前驱顶点
     */
    private int[][] pre;

    /**
     * 构造器
     * @param matrix 邻近矩阵
     * @param vertex 顶点数组
     */
    public FGraph(int[][] matrix, char[] vertex) {
        this.vertex = vertex;
        this.dis = matrix;
        this.pre = new int[vertex.length][vertex.length];
        // 对pre数组初始化，存放的是前驱顶点下标
        for (int i = 0; i < vertex.length; i++) {
            // 刚开始的前驱顶点是它自己
            Arrays.fill(pre[i], i);
        }
    }

    /**
     * 弗洛伊德算法
     */
    public void floyd() {
        // 保存顶点之间的距离
        int len = 0;
        // 从中间顶点遍历，k表示中间顶点的下标 [A, B, C, D, E, F, G]
        for (int k = 0; k < dis.length; k++) {
            // 从顶点i开始出发，i表示起点 [A, B, C, D, E, F, G]
            for (int i = 0; i < dis.length; i++) {
                // j表示终点 [A, B, C, D, E, F, G]
                for (int j = 0; j < dis.length; j++) {
                    // len表示从 i 顶点出发，经过 k 中间顶点，到达 j 终点
                    // 即 i--k--j 的距离
                    len = dis[i][k] + dis[k][j];
                    // i--k--j 的距离 < i--j 的距离
                    if (len < dis[i][j]) {
                        // 更新最短路径
                        dis[i][j] = len;
                        // 更新前驱顶点
                        pre[i][j] = pre[k][j];
                    }
                }
            }
        }
    }

    /**
     * 显示pre数组和dis数组
     */
    public void show() {
        System.out.println("pre================================");
        for (int[] link : this.pre) {
            for (int v : link) {
                System.out.print(this.vertex[v] + "\t");
            }
            System.out.println();
        }
        System.out.println("dis================================");
        for (int i = 0; i < this.vertex.length; i++) {
            for (int j = 0; j < this.vertex.length; j++) {
                System.out.print(this.vertex[i] + "->" + this.vertex[j] + " = " + dis[i][j] + "\t");
            }
            System.out.println();
        }
    }
}
```



# 马踏棋盘算法

- 将马随机放在国际象棋的8×8棋盘 Board[0～7][0～7]的某个方格中，马按走棋 规则(马走日字)进行移动。要求每个方格只 进入一次，走遍棋盘上全部64个方格

![image-20220921225030399](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20220921225030399.png)





```java
package com.kcs.horsestepboard;

import java.awt.*;
import java.util.ArrayList;
import java.util.Comparator;

/**
 * @author Kcs 2022/9/23
 */
class HorseChessBoard {

    /**
     * 列
     */
    private static int X;
    /**
     * 行
     */
    private static int Y;

    /**
     * 数组来表示棋盘的位置是否被访问过
     */
    private static boolean visited[];
    /**
     * 使用一个属性来表示棋盘是否所有的位置都被访问,默认false
     */
    private static boolean finished;
    /**用来统计次数的
     * 
     */
    static int count = 0;

    public static void main(String[] args) {

        X = 6;
        Y = 6;
        //马从1开始
        int row = 1;
        //马从1开始编号
        int column = 1;
        //初始值都为false
        visited = new boolean[X * Y];
        int[][] chessborad = new int[X][Y];
        //      测试一下耗时
        long start = System.currentTimeMillis();
        travelChessBorad(chessborad, 1, 2, 1);
        //打印出来毫秒
        long end = System.currentTimeMillis();
        System.out.println((end - start));

        //输出棋盘
        for (int[] rows : chessborad) {
            System.out.println();
            for (int step : rows) {
                System.out.print(step + "\t");
            }
        }
        System.out.println("循环次数" + count);
    }

    /**
     * 遍历棋盘用来找符合的情况
     * @param chessborad 当前在棋盘的位置
     * @param row 行
     * @param column 列
     * @param step 步数
     */
    public static void travelChessBorad(int[][] chessborad, int row, int column, int step) {
        //1.走完棋盘
        //把每一个方格当成下一个数字
        chessborad[row][column] = step;
        //row=4 X=8,column=4
        //visited标记该位置已经被访问
        //表示马儿从该点开始出发
        visited[row * X + column] = true;

        // 获取当前位置可以走的下一个集合    把棋盘传入我们需要的函数，用来判断是否符合条件
        ArrayList<Point> ps = next(new Point(column, row));
        
        // 对他的下一步的次数进行非递减排序
        sort(ps);

        //遍历ps
        while (!ps.isEmpty()) {
            //可以走的位置的值全部为0，走了之后visited[row][column]=true;
            Point p = ps.remove(0);


            //说明还没有被访问
            if (!visited[p.y * X + p.x]) {
                //访问下一个点
                travelChessBorad(chessborad, p.y, p.x, step + 1);
                count++;
            }
        }

        //2.没有走完棋盘
        //判断马儿是否完成了任务，使用step和应该步数比较
        // step<X*Y是否走完有两种情况：1：棋盘没有走完 ，2： 正处在一个回溯的过程
        if (step < X * Y && !finished) {

            chessborad[row][column] = 0;
            visited[row * X + column] = false;
        } else {
            finished = true;
        }
    }


    /**
     * 当前的这个点由自己来决定，只要符合要求即可。
     * @param currentPoint 当前点
     * @return point
     */
    public static ArrayList<Point> next(Point currentPoint) {
        //        创建一个ArrayList
        ArrayList<Point> ps = new ArrayList<>();
        //创建一个Point
        Point p1 = new Point();
        //表示马儿可以走,图中的数表示最多的马可以走的个数，0，1，2，3，4，5，6，7

        //表示马儿可以走5这个位置
        //（总共八个数可以走只要符合稍作就可以加入到这个数组中）
        if ((p1.x = currentPoint.x - 2) >= 0 && (p1.y = currentPoint.y - 1) >= 0) {
            //符合要求把这个点加入到数组中
            ps.add(new Point(p1));
        }
        //0
        if ((p1.x = currentPoint.x + 2) < X && (p1.y = currentPoint.y - 1) >= 0) {
            ps.add(new Point(p1));
        }

        //表示走6这个位置，如果x,y不出边界就可以
        if ((p1.x = currentPoint.x - 1) >= 0 && (p1.y = currentPoint.y - 2) >= 0) {

            ps.add(new Point(p1));
        }
        //表示走7这个位置
        if ((p1.x = currentPoint.x + 1) < X && (p1.y = currentPoint.y - 2) >= 0) {
            ps.add(new Point(p1));
        }

        //1这个位置
        if ((p1.x = currentPoint.x + 2) < X && (p1.y = currentPoint.y + 1) < Y) {
            ps.add(new Point(p1));
        }
        //4

        if ((p1.x = currentPoint.x - 2) >= 0 && (p1.y = currentPoint.y + 1) < Y) {
            //符合要求把这个点加入到数组中
            ps.add(new Point(p1));
        }

        //3
        if ((p1.x = currentPoint.x - 1) >= 0 && (p1.y = currentPoint.y + 2) < Y) {
            ps.add(new Point(p1));
        }
        //2
        if ((p1.x = currentPoint.x + 1) < X && (p1.y = currentPoint.y + 2) < Y) {
            ps.add(new Point(p1));
        }
        //返回点
        return ps;
    }

    /**
     * 减少回溯的次数
     * 对这个算法的回溯的时候进行 非递减排序（1，2，2，3，3，4，5，5）可以有重复的数字
     */
    public static void sort(ArrayList<Point> ps) {
        ps.sort(new Comparator<Point>() {
            @Override
            public int compare(Point o1, Point o2) {
                //获取o1的下一步的所有的位置个数
                int count1 = next(o1).size();
                int count2 = next(o2).size();
                if (count1 < count2) {
                    return -1;
                } else if (count1 == count2) {
                    return 0;
                } else {
                    return -1;
                }
            }
        });
    }
}
```













