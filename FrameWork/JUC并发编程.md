> ✨作者：猫十二懿
>
> ❤️‍🔥账号：[CSDN](https://blog.csdn.net/qq_56098191) 、[掘金](https://juejin.cn/user/3320978695270526) 、[个人博客](https://kongshier.github.io/) 、[Github](https://github.com/kongshier) 
>
> 🎉公众号：猫十二懿

[学习地址](https://www.bilibili.com/video/BV1Kw411Z7dF)

# 写在最前

JUC（`Java Util Concurrent`）学习内容框架：

~~~mermaid
graph TB
A(JUC高并发编程内容)-->a1(JUC概念)
A(JUC高并发编程内容)-->a12(Lock接口)
A(JUC高并发编程内容)-->a13(线程间通信)
A(JUC高并发编程内容)-->a14(集合的线程安全)
A(JUC高并发编程内容)-->a15(多线程锁)
A(JUC高并发编程内容)-->a16(Callable接口)
A(JUC高并发编程内容)-->a17(JUC三大辅助类)
a17(JUC三大辅助类)-->a171(CountDowLatch)
a17(JUC三大辅助类)-->a172(CyclicBarrier)
a17(JUC三大辅助类)-->a173(Semaphore)
A(JUC高并发编程内容)-->a18(读写锁:ReentrantReadWriteLock)
A(JUC高并发编程内容)-->a19(阻塞队列)
A(JUC高并发编程内容)-->a20(ThreadPool线程池)
A(JUC高并发编程内容)-->a21(Fork/Join 框架)
A(JUC高并发编程内容)-->a22(CompletableFuture)
~~~



# 1、JUC概述

## 1.1 JUC概念

JUC是Java Util Concurrent的简称，是Java 5及以后版本中新增的用于支持高并发编程的包。JUC提供了一些线程安全的集合类、原子类、锁、信号量、倒计数器、栅栏等用于并发编程的类和接口，以帮助Java开发者编写高效、安全、稳定的多线程程序。

在传统的Java多线程编程中，开发者使用synchronized关键字来保证线程的同步和协作，但是synchronized存在一些问题，比如只能使用在方法或代码块中、一旦持有锁就无法被其他线程获取等。JUC提供了更加灵活、功能更加强大的同步机制，如Lock接口、Condition接口、Semaphore类、CountDownLatch类、CyclicBarrier类等，可以更好地帮助开发者解决线程同步和协作的问题。

除此之外，JUC还提供了一些并发集合类和原子类，这些类可以在多线程环境下安全地进行操作，从而避免了多线程同时修改数据时的竞争问题，提高了并发编程的效率和稳定性。

总的来说，JUC提供了一组强大的并发编程工具，可以帮助Java开发者更好地利用多核CPU的优势，提高应用程序的并发性能，从而更好地满足现代应用对高并发处理的需求。

## 1.2 JUC 内容

JUC（Java Util Concurrent）是Java 5及以后版本中新增的用于支持高并发编程的包，其中包含了很多用于并发编程的类和接口，主要包括以下内容：

1. 并发集合类：JUC中提供了一些线程安全的集合类，如ConcurrentHashMap、CopyOnWriteArrayList、ConcurrentLinkedQueue等，这些类可以在多线程环境下安全地进行操作，从而避免了多线程同时修改数据时的竞争问题。
2. 原子类：JUC中提供了一些原子类，如AtomicInteger、AtomicLong、AtomicBoolean等，这些类可以保证在多线程环境下的原子性操作，避免了多线程同时修改数据时的竞争问题。
3. Lock接口：JUC中提供了一组Lock接口及其实现类，如ReentrantLock、ReentrantReadWriteLock等，Lock接口提供了比synchronized更加灵活的锁操作，可以更精确地控制线程的并发访问。
4. Condition接口：JUC中提供了Condition接口，可以与Lock接口配合使用，实现更加灵活的线程等待和唤醒操作。
5. Semaphore类：Semaphore是一种计数信号量，可以用来限制同时访问某个资源的线程数。
6. CountDownLatch类：CountDownLatch是一种倒计数器，可以用来实现等待多个线程完成后再执行某个操作。
7. CyclicBarrier类：CyclicBarrier是一种栅栏，可以用来等待多个线程都到达某个状态后再一起执行。

JUC提供的这些类和接口，可以帮助Java开发者更好地编写高效、安全、稳定的多线程程序，从而充分利用多核CPU的优势，提高应用程序的并发性能。



## 1.3 进程和线程

### 进程

进程是指在系统中正在运行的一个程序，一个进程可以包含多个线程。每个进程都有自己独立的内存空间和系统资源，不同的进程之间相互独立，互相之间不能访问彼此的内存空间。进程通过操作系统提供的进程调度器来实现进程的调度和管理。

### 线程

线程是进程中的一个执行单元，是操作系统进行运算调度的最小单位。在一个进程中，多个线程可以共享相同的内存空间和系统资源，可以方便地进行通信和数据共享。线程之间的切换开销较小，可以更加高效地实现并发任务。

由于进程之间的切换开销较大，所以多线程的应用比多进程的应用更加高效，可以更好地利用计算机的资源，提高应用程序的性能。同时，线程之间的共享内存和数据的操作需要进行同步和互斥，否则会出现数据竞争和死锁等问题，因此在多线程编程中需要注意线程的同步和互斥问题。

## 1.4 线程状态

### 1.4.1 线程状态枚举类

1. NEW：(新建)
2. RUNNABLE：（准备就绪）
3. BLOCKED：（阻塞）
4. WAITING：（不见不散）
5. TIMED_WAITING：（过时不候）
6. TERMINATED：(终结)

通过一个小案例说明上面的枚举值

> 你和你朋友越好一起出去玩`（NEW新建状态）`，一切准备就绪`（RUNNABLE：准备就绪状态）`，出发之后，出现了意外你在开车的路上堵车了（`BLOCKED阻塞）`，你们越好的是晚上的八点见面，由于阻塞了，你的朋友有还在等你`（WAITING不见不散）`，也有可能你的朋友已经走了你那么久还没有来`（TIMED_WAITING过时不候）`，最后可能是愉快结束见面，也有可能是不愉快的结束这次出行。`（TERMINATED终结）`

### 1.4.2 wait、sleep 的区别  

1. sleep 是 Thread 的静态方法，wait 是 Object 的方法，任何对象实例都能调用。 
2. sleep 不会释放锁，它也不需要占用锁。wait 会释放锁，但调用它的前提是当前线程占有锁(即代码要在 synchronized 中)。 （在哪里睡就在那里醒来）
3. 它们都可以被 interrupted 方法中断。



## 1.5 并发与并行  

### 1.5.1 串行模式  

串行表示所有任务都一一按先后顺序进行。

串行意味着必须先装完一车柴才能 运送这车柴，只有运送到了，才能卸下这车柴，并且只有完成了这整个三个步骤，才能进行下一个步骤。 串行是一次只能取得一个任务，并执行这个任务。 

### 1.5.2 并行模式  

并行意味着可以同时取得多个任务，并同时去执行所取得的这些任务。

并行模式相当于将长长的一条队列，划分成了多条短队列，所以并行缩短了任务队列的长度。并行的效率从代码层次上强依赖于多进程/多线程代码，从硬件角度上则依赖于多核 CPU。

### 1.5.3 并发

 并发(concurrent)指的是多个程序可以同时运行的现象，更细化的是多进程可以同时运行或者多指令可以同时运行。但这不是重点，在描述并发的时候也不会去扣这种字眼是否精确，==并发的重点在于它是一种现象==, ==并发描述 的是多进程同时运行的现象==。但实际上，对于单核心 CPU 来说，同一时刻只能运行一个线程。所以，这里的 "同时运行" 表示的不是真的同一时刻有多个线程运行的现象，这是并行的概念，而是提供一种功能让用户看来多个程序同时运行起来了，但实际上这些程序中的进程不是一直霸占 CPU 的，而是执行一 会停一会。 要解决大并发问题，通常是将大任务分解成多个小任务, 由于操作系统对进程的调度是随机的，所以切分成多个小任务后，可能会从任一小任务处执行。这可能会出现一些现象：

1. 可能出现一个小任务执行了多次，还没开始下个任务的情况。这时一般会采用队列或类似的数据结构来存放各个小任务的成果
2. 可能出现还没准备好第一步就执行第二步的可能。这时，一般采用多路复用或 异步的方式，比如只有准备好产生了事件通知才执行某个任务。 
3. 可以多进程/多线程的方式并行执行这些小任务。也可以单进程/单线程执行这 些小任务，这时很可能要配合多路复用才能达到较高的效率



### 1.5.4 小结(重点)  

#### 并发：

同一时刻多个线程在访问同一个资源，多个线程对一个点 

例子：春运抢票、电商秒杀... 

#### 并行：

多项工作一起执行，之后再汇总 

例子：泡方便面，一边电水壶烧水，一边撕调料倒入桶中



## 1.6 管程

管程(monitor)是保证了同一时刻只有一个进程在管程内活动，即管程内定义的操作在同一时刻只被一个进程调用(由编译器实现)。但是这样并不能保证进程以设计的顺序执行。

JVM 中同步是基于进入和退出管程(monitor)对象实现的，每个对象都会有一个管程 (monitor)对象，管程(monitor)会随着 java 对象一同创建和销毁 执行线程首先要持有管程对象，然后才能执行方法，当方法完成之后会释放管程，方 法在执行时候会持有管程，其他线程无法再获取同一个管程



## 1.7 用户线程和守护线程

### 1.7.1 用户线程

平时用到的普通线程，自定义线程 

### 1.7.2 守护线程

运行在后台，是一种特殊的线程，比如垃圾回收 当主线程结束后，用户线程还在运行，JVM 存活 如果没有用户线程，都是守护线程，JVM 结束

```java
/**
 * @author Shier 2023/2/21 12:38
 * 用户线程
 */
public class UserThread {
    public static void main(String[] args) {
        Thread thread = new Thread(() -> {
            //isDaemon 怕判断是否为用户线程
            System.out.println(Thread.currentThread().getName() + "::" + Thread.currentThread().isDaemon());
            // 来一个死循环
            while (true) {
            }
        }, "test");
        // 设置为守护线程
        thread.setDaemon(true);// JVM将会结束进程，进行后台运行
        
        thread.start();
        System.out.println(Thread.currentThread().getName() + "::" + Thread.currentThread().isDaemon());
    }
}
```



# 2、Lock 接口

## 2.1 Synchroniezd 锁

synchronized 是 Java 中的关键字，是一种同步锁。它修饰的对象有以下几种： 

1. 修饰一个代码块，被修饰的代码块称为同步语句块，其作用的范围是大括号{} 括起来的代码，作用的对象是调用这个代码块的对象；
2. 修饰一个方法，被修饰的方法称为同步方法，其作用的范围是整个方法，作用 的对象是调用这个方法的对象；
3. 修改一个静态的方法，其作用的范围是整个静态方法，作用的对象是这个类的 所有对象；
4. 修改一个类，其作用的范围是 synchronized 后面括号括起来的部分，作用主 的对象是这个类的所有对象。

如果一个代码块被 synchronized 修饰了，当一个线程获取了对应的锁，并执行该代码块时，其他线程便只能一直等待，等待获取锁的线程释放锁，而这里获取锁的线程释放锁只会有两种情况： 

1. 获取锁的线程执行完了该代码块，然后线程释放对锁的占有
2. 线程执行发生异常，此时 JVM 会让线程自动释放锁。

那么如果这个获取锁的线程由于要等待 IO 或者其他原因（比如调用 sleep 方法）被阻塞了，但是又没有释放锁，其他线程便只能干巴巴地等待，试想一 下，这多么影响程序执行效率。 因此就需要有一种机制可以不让等待的线程一直无期限地等待下去（比如只等 待一定的时间或者能够响应中断），通过 Lock 就可以办到。

### 2.1.1 多线程编程步骤

1. 创建资源类，在资源类中创建属性和操作方法（上部）
2. 在资源列中操作方法



例子售票员买票

```java
package com.shier.sync;

/**
 * @author Shier 2023/2/21 13:07
 */

// 1 创建资源类
class Ticket {
    // 创建属性
    private int number = 30;

    // 同步方法
    public synchronized void sale() {
        if (number > 0) {
            System.out.println(Thread.currentThread().getName() + "卖第" + (number--) + "张票，剩余：" + number);
        }
    }
}


public class SaleTicket {
    public static void main(String[] args) {
        // 调用资源类
        Ticket ticket = new Ticket();
        // 创建三个线程
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 40; i++) {
                    ticket.sale();
                }
            }
        }, "1号").start();
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 40; i++) {
                    ticket.sale();
                }
            }
        }, "2号").start();
        new Thread(new Runnable() {
            @Override
            public void run() {
                for (int i = 0; i < 40; i++) {
                    ticket.sale();
                }
            }
        }, "3号").start();
    }
}
```



## 2.2 什么是Lock 

Lock 锁实现提供了比使用同步方法和语句可以获得的更广泛的锁操作。它们允 许更灵活的结构，可能具有非常不同的属性，并且可能支持多个关联的条件对 象。Lock 提供了比 synchronized 更多的功能。



### Lock 与的 Synchronized 区别

Lock 不是 Java 语言内置的，synchronized 是 Java 语言的关键字，因此是内置特性。

Lock 是一个类，通过这个类可以实现同步访问； 

Lock 和 synchronized 有一点非常大的不同，==采用 synchronized 不需要用户去手动释放锁==，当 synchronized 方法或者 synchronized 代码块执行完之后， 系统会自动让线程释放对锁的占用；==而 Lock 则必须要用户去手动释放锁==，如果没有主动释放锁，就有可能导致出现死锁现象。

> 就好比如上厕所，如果你要去上厕所，就得先判断厕所是否有人，如果有人就得申请（叫他），别人出来了就会把门打开就是释放锁，你进去了就会把门关上（上锁），等你完事之后，就会开门（主动释放锁）。



### 2.2.1  lock 方法

lock()方法是平常使用得最多的一个方法，就是用来获取锁。如果锁已被其他 线程获取，则进行等待。 采用 Lock，必须主动去释放锁，并且在发生异常时，不会自动释放锁。因此一 般来说，使用 Lock 必须在 try{}catch{}块中进行，并且将释放锁的操作放在 finally 块中进行，以保证锁一定被被释放，防止死锁的发生。

~~~java
Lock lock = ....;    
// 上锁
lock.lock();
try {
    if (number > 0) {
        System.out.println(Thread.currentThread().getName() + "卖第" + (number--) + "张票，剩余：" + number);
    }
} finally {
    // 解锁
    lock.lock();
}
~~~



### 2.2.2 ReentrantLock

ReentrantLock，意思是“可重入锁”，关于可重入锁的概念将在后面讲述。 ReentrantLock 是唯一实现了 Lock 接口的类，并且 ReentrantLock 提供了更 多的方法。下面通过一些实例看具体看一下如何使用。

```java
/**
 * @author Shier 2023/2/21 13:07
 */
// 1 创建资源类
class Ticket {
    // 创建属性,票的数量
    private int number = 30;
    // 创建可重入锁
    private final ReentrantLock lock = new ReentrantLock();

    // 同步方法
    public void sale() {
        // 上锁
        lock.lock();
        try {
            if (number > 0) {
                System.out.println(Thread.currentThread().getName() + "卖第" + (number--) + "张票，剩余：" + number);
            }
        } finally {
            // 解锁
            lock.lock();
        }
    }
}

public class LockSaleTicket {
    public static void main(String[] args) {
        // 调用资源类,
        Ticket ticket = new Ticket();
        // 创建三个线程
        new Thread(()->{
            for (int i = 0; i < 30; i++) {
                ticket.sale();
            }
        },"1号").start();

        new Thread(()->{
            for (int i = 0; i < 30; i++) {
                ticket.sale();
            }
        },"2号").start();
        
        new Thread(()->{
            for (int i = 0; i < 30; i++) {
                ticket.sale();
            }
        },"3号").start();
    }
}
```

### 2.2.3 newCondition (条件唤醒线程)

关键字 synchronized 与 wait() / notify()这两个方法一起使用可以实现等待/通知模式， Lock 锁的 newContition()方法返回 Condition 对象，Condition 类也可以实现等待/通知模式。 用 notify()通知时，JVM 会随机唤醒某个等待的线程， 使用 Condition 类可以进行选择性通知， Condition 比较常用的两个方法：

1. await()会使当前线程等待,同时会释放锁,当其他线程调用`signal()`时，线程会重 新获得锁并继续执行。 
2. signal()用于唤醒一个等待的线程。



### 2.2.4 ReadWriteLock

ReadWriteLock 也是一个接口，在它里面只定义了两个方法

~~~
Lock readLock(); // 只读锁
Lock writeLock(); // 写锁
~~~

一个用来获取读锁，一个用来获取写锁。也就是说将文件的读写操作分开，分成2个锁来分配给线程，从而使得多个线程可以同时进行读操作。下面的 ReentrantReadWriteLock 实现了 ReadWriteLock 接口。 ReentrantReadWriteLock 里面提供了很多丰富的方法，不过最主要的有两个方法：readLock()和 writeLock()用来获取读锁和写锁。

==PS==

- 如果有一个线程已经占用了读锁，则此时其他线程如果要申请写锁，则申请写锁的线程会一直等待释放读锁。 
- 如果有一个线程已经占用了写锁，则此时其他线程如果申请写锁或者读锁，则申请的线程会一直等待释放写锁。



## 2.3 Lock 总结

Lock 和 synchronized 有以下几点不同： 

1. Lock 是一个接口，而 synchronized 是 Java 中的关键字，synchronized 是内 置的语言实现； 
2. synchronized 在发生异常时，会自动释放线程占有的锁，因此不会导致死锁现 象发生；而 Lock 在发生异常时，如果没有主动通过 unLock()去释放锁，则很 可能造成死锁现象，因此使用 Lock 时需要在 finally 块中释放锁； 
3. Lock 可以让等待锁的线程响应中断，而 synchronized 却不行，使用 synchronized 时，等待的线程会一直等待下去，不能够响应中断；
4. 通过 Lock 可以知道有没有成功获取锁，而 synchronized 却无法办到。 
5. Lock 可以提高多个线程进行读操作的效率。 在性能上来说，如果竞争资源不激烈，两者的性能是差不多的，而当竞争资源 非常激烈时（即有大量线程同时竞争），此时 Lock 的性能要远远优于 synchronized。



# 3、 线程间通信

线程间通信的模型有两种：==共享内存和消息传递==，以下方式都是基本这两种模型来实现的。我们来基本一道面试常见的题目来分析

## 3.1 多线程编程步骤

1. 创建资源类，在资源类中创建属性和操作方法（上部）
2. 在资源列中操作方法（中部）
   1. 判断（是否符合当前的状态）
   2. 干活 （具体内容）
   3. 通知（告诉另外的一个线程，值已经改变）
3. 创建多个线程，调用资源类的操作方法（下部）
4. 防止虚假唤醒问题

例子：有两个线程，实现对一个初始值是0的变量的操作，一个线程对值 + 1 ，另一个线程对值 -1 

### 使用synchronization实现：

```java
package com.shier.sync;

/**
 * @author Shier 2023/2/21 13:07
 */

// 第一步创建资源类
class Share {
    // 创建一个属性 默认值为 0
    private int num = 0;

    // 对属性加一的方法
    public synchronized void increase() throws InterruptedException {
        // 判断
        if (num == 1) {
            // 等待
            this.wait();
        }
        // 干活
        num++;
        System.out.println(Thread.currentThread().getName() + "当前值：" + num);
        // 通知
        this.notifyAll();
    }

    // 对属性减一的方法
    public synchronized void decrease() throws InterruptedException {
        // 判断
        if (num == 0) {
            // 等待
            this.wait();
        }
        // 干活
        num--;
        System.out.println(Thread.currentThread().getName() + "当前值：" + num);
        // 通知
        this.notifyAll();
    }
}

public class ThreadSingleCommunication {
    public static void main(String[] args) {
        // 创建多个线程， 调用资源类的线程
        Share share = new Share();
        new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                try {
                    share.decrease();// 减一
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "减一线程").start();

        new Thread(() -> {
            for (int i = 0; i < 10; i++) {
                try {
                    share.increase();// 加一
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "加一线程").start();
    }
}
```

以上的代码存在着一定的问题：如果是多个线程，比如四个线程就不能出现 1010的效果了，也就是出现了虚假唤醒，所以说得去指定线程执行

```java
  // 对属性加一的方法
    public synchronized void increase() throws InterruptedException {
        // 使用while循环中避免虚假唤醒
        while (num == 1) {
            // 等待
            this.wait();
        }
        // 干活
        num++;
        System.out.println(Thread.currentThread().getName() + "当前值：" + num);
        // 通知
        this.notifyAll();
    }
```

### 使用Lock 实现

```java
/**
 * @author Shier 2023/2/21 16:10
 */
// 定义一个资源类
class Share {
    // 属性
    private int number = 0;

    // 创建锁
    private Lock lock = new ReentrantLock();

    // 创建钥匙
    private Condition condition = lock.newCondition();

    // 加一方法
    public void increase() throws InterruptedException {
        //上锁
        lock.lock();
        try {
            // 避免虚假唤醒
            while (number != 0) {
                condition.await();
            }
            number++;
            System.out.println(Thread.currentThread().getName() + "当前值：" + number);
            condition.signalAll();
        } finally {
            lock.unlock();
        }
    }

    // 减一方法
    public void decrease() throws InterruptedException {
        //上锁
        lock.lock();
        try {
            // 避免虚假唤醒
            while (number != 1) {
                condition.await();
            }
            // 减一操作
            number--;
            System.out.println(Thread.currentThread().getName() + "当前值：" + number);
            // 唤醒其他线程
            condition.signalAll();
        } finally {
            lock.unlock();
        }
    }
}
```



## 3.2 线程间定制化通信

问题引入：启动三个线程A、B、C，A 线程打印 5 次，B 线程打印 10 次，C 线程打印 15 次，按照此顺序循环 10 轮

![04-线程定制化通信](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/04-%E7%BA%BF%E7%A8%8B%E5%AE%9A%E5%88%B6%E5%8C%96%E9%80%9A%E4%BF%A1.png)



```java
/**
 * @author Shier 2023/2/21 17:10
 */
// 资源类
class ShareResource {
    // 标志位
    private int flag = 1;
    // 创建lock锁
    private Lock lock = new ReentrantLock();=
    // 创建condition
    private Condition c1 = lock.newCondition();
    private Condition c2 = lock.newCondition();
    private Condition c3 = lock.newCondition();
    // 创建打印五次的方法
    public void printFive(int loop) throws InterruptedException {
        // 上锁
        lock.lock();
        try {
            // 避免虚假唤醒
            while (flag != 1) {
                c1.await();
            }
            for (int i = 1; i <= 5; i++) {
                System.out.println(Thread.currentThread().getName() + "当前值：" + i + "" + "第" + loop + "次");
            }
            flag = 2;
            // 唤醒c2
            c2.signal();
        } finally {
            lock.unlock();
        }
    }

    // 创建打印10次的方法
    public void printTen(int loop) throws InterruptedException {
        // 上锁
        lock.lock();
        try {
            // 避免虚假唤醒
            while (flag != 2) {
                c2.await();
            }
            for (int i = 1; i <= 10; i++) {
                System.out.println(Thread.currentThread().getName() + "当前值：" + i + "" + "第" + loop + "次");
            }
            flag = 3;
            // 唤醒c3
            c3.signal();
        } finally {
            lock.unlock();
        }
    }

    // 创建打印15次的方法
    public void printFifth(int loop) throws InterruptedException {
        // 上锁
        lock.lock();
        try {
            // 避免虚假唤醒
            while (flag != 3) {
                c3.await();
            }
            for (int i = 1; i <= 15; i++) {
                System.out.println(Thread.currentThread().getName() + "当前值：" + i + "" + "，第" + loop + "次");
            }
            flag = 1;
            // 唤醒 c1
            c1.signal();
        } finally {
            lock.unlock();
        }
    }
}

public class ThreadDemo {
    public static void main(String[] args) {
        ShareResource shareResource = new ShareResource();
        // 调用几次
        int loop = 5;
        new Thread(() -> {
            for (int i = 1; i <= loop; i++) {
                try {
                    shareResource.printFive(i);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "1号线程").start();
        new Thread(() -> {
            for (int i = 1; i <= loop; i++) {
                try {
                    shareResource.printTen(i);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "2号线程").start();
        new Thread(() -> {
            for (int i = 1; i <= loop; i++) {
                try {
                    shareResource.printFifth(i);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }, "3号线程").start();
    }
}
```



# 4、集合的线程安全



ArrayList 线程不安全问题引出

```java
/**
 * @author Shier 2023/2/21 17:59
 */

public class ThreadSecurity {
    public static void main(String[] args) {
        // 多个线程对集合进行修改会出现异常
        ArrayList<String> arrayList = new ArrayList<>();
        for (int i = 0; i < 30; i++) {
            new Thread(() -> {
                arrayList.add(UUID.randomUUID().toString().substring(0, 3));
                System.out.println(arrayList);
            }, String.valueOf(i)).start();
        }
    }
}
```

运行会出现一下的报错异常：==并发修改异常==

![image-20230221180446802](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230221180446802.png)

解决线程的并发修改异常有基本的三种

1. Vertor
2. Collections
3. CopyOnWriteArrayList

首先看第一种

## 4.1 Vertor 和 Collections

Vector 是矢量队列，它是 JDK1.0 版本添加的类。继承于 AbstractList，实现了 List, RandomAccess, Cloneable 这些接口。 Vector 继承了 AbstractList， 实现了List；所以，它是一个队列，支持相关的添加、删除、修改、遍历等功 能。 Vector 实现了 RandmoAccess 接口，即提供了随机访问功能。 RandmoAccess 是 java 中用来被 List 实现，为 List 提供快速访问功能的。在 Vector 中，我们即可以通过元素的序号快速获取元素对象；这就是快速随机访问。 Vector 实现了 Cloneable 接口，即实现 clone()函数。它能被克隆

==和 ArrayList 不同，Vector 中的操作是线程安全的。== 

1、将上面的代码的ArrayList 改成 Vertor

~~~java
List<String> list = new Vertor<>();
~~~

就不会出现并发修改异常

因为Vertor中的add 是使用 synchronization 同步锁关键字修饰，所以说不会出现异常

2、同样也还可以使用Collections 工具类来进行避免异常，返回的是一个同步的集合

~~~java
List<String> arrayList = Collections.synchronizedList(new ArrayList<>());
~~~

但是以上两种在实际开发过程中并不常用。

## 4.2 CopyOnWriteArrayList

它相当于线程安全的 ArrayList。和 ArrayList 一样，它是个可变数组；但是和 ArrayList 不同的时，它具有以下特性：

1. 它最适合于具有以下特征的应用程序：List 大小通常保持很小，只读操作远多 于可变操作，需要在遍历期间防止线程间的冲突。 
2. 它是线程安全的。 
3. 因为通常需要复制整个基础数组，所以可变操作（add()、set() 和 remove()  等等）的开销很大。 
4. 迭代器支持 hasNext(), next()等不可变操作，但不支持可变 remove()等操作。
5. 使用迭代器进行遍历的速度很快，并且不会与其他线程发生冲突。在构造迭代器时，迭代器依赖于不变的数组快照。

最主要的特点：

- 独占锁效率低：采用读写分离思想解决
- 写线程获取到锁，其他写线程阻塞 

CopyOnWriteArrayList 的 复制思想：

当我们往一个容器添加元素的时候，不直接往当前容器添加，而是先将当前容 器进行 Copy，复制出一个新的容器，然后新的容器里添加元素，添加完元素 之后，再将原容器的引用指向新的容器。 

这时候会抛出来一个新的问题，也就是数据不一致的问题。如果写线程还没来 得及写会内存，其他的线程就会读到了脏数据。 ==这就是 CopyOnWriteArrayList 的思想和原理。就是拷贝一份。==

```java
List<String> arrayList = new CopyOnWriteArrayList()
```

这样创建也不会出现线程安装问题。

原因分析(重点)：==动态数组与线程安全== 下面从“动态数组”和“线程安全”两个方面进一步对 CopyOnWriteArrayList 的原理进行说明。

**动态数组机制** 

- 它内部有个“volatile 数组”(array)来保持数据。在“添加/修改/删除”数据 时，都会新建一个数组，并将更新后的数据拷贝到新建的数组中，最后再将该 数组赋值给“volatile 数组”, 这就是它叫做 CopyOnWriteArrayList 的原因 
- 由于它在“添加/修改/删除”数据时，都会新建数组，所以涉及到修改数据的 操作，CopyOnWriteArrayList 效率很低；但是单单只是进行遍历查找的话， 效率比较高。 

**线程安全机制** 

- 通过 volatile 和互斥锁来实现的。 
- 通过“volatile 数组”来保存数据的。一个线程读取 volatile 数组时，总能看 到其它线程对该 volatile 变量最后的写入；就这样，通过 volatile 提供了“读 取到的数据总是最新的”这个机制的保证。 
- 通过互斥锁来保护数据。在“添加/修改/删除”数据时，会先“获取互斥锁”， 再修改完毕之后，先将数据更新到“volatile 数组”中，然后再“释放互斥 锁”，就达到了保护数据的目的。

## 4.3 HashSet、HashMap集合解决并发异常(线程不安全)

### Set集合

```java
Set<String> arrayList = new CopyOnWriteArraySet<String>();
```

### Map集合

```java
Map<String, String> hashMap = new ConcurrentHashMap<>();
```



## 4.4 小结

1. 线程安全与线程不安全集合 集合类型中存在线程安全与线程不安全的两种,

   常见例如: ArrayList ----- Vector HashMap -----HashTable 但是以上都是通过 synchronized 关键字实现,效率较低 

2. 2.Collections 构建的线程安全集合 

3. java.util.concurrent 并发包下 CopyOnWriteArrayList CopyOnWriteArraySet 类型,通过动态数组与线程安 全个方面保证线程安全



# 5、多线程锁

一个对象里面如果有多个 synchronized 方法，某一个时刻内，只要一个线程去调用其中的 一个 synchronized 方法， 其它的线程都只能等待，换句话说，某一个时刻内，只能有唯一一个线程去访问这些 synchronized 方法。

锁的是当前对象 this，被锁定后，其它的线程都不能进入到当前对象的其它的 synchronized 方法 

加个普通方法后发现和同步锁无关，换成两个对象后，不是同一把锁了，情况立刻变化。 

synchronized 实现同步的基础：Java 中的每一个对象都可以作为锁。 具体表现为以下 3 种形式。

1. 对于普通同步方法，锁是当前实例对象。 
2. 对于静态同步方法，锁是当前类的 Class 对象。 
3. 对于同步方法块，锁是 Synchonized 括号里配置的对象 

> 当一个线程试图访问同步代码块时，它首先必须得到锁，退出或抛出异常时必须释放锁。 也就是说如果一个实例对象的非静态同步方法获取锁后，该实例对象的其他非静态同步方 法必须等待获取锁的方法释放锁后才能获取锁， 可是别的实例对象的非静态同步方法因为跟该实例对象的非静态同步方法用的是不同的锁， 所以不需要等待该实例对象已获取到锁的非静态同步方法释放锁就可以获取他们自己的锁。 

所有的静态同步方法用的也是同一把锁——类对象本身，这两把锁是两个不同的对象，所以静态同步方法与非静态同步方法之间是不会有竞态条件的。 

但是一旦一个静态同步方法获取锁后，其他的静态同步方法都必须等待该方法释放锁后才 能获取锁，而不管是同一个实例对象的静态同步方法之间，还是不同的实例对象的静态同 步方法之间，只要它们同一个类的实例对象！

## 5.1 公平锁和非公平锁

源码：

```java
/**
 * Creates an instance of {@code ReentrantLock}.
 * This is equivalent to using {@code ReentrantLock(false)}.
 */
public ReentrantLock() {
    sync = new NonfairSync();
}

/**
 * Creates an instance of {@code ReentrantLock} with the
 * given fairness policy.
 *
 * @param fair {@code true} if this lock should use a fair ordering policy
 */
public ReentrantLock(boolean fair) {
    sync = fair ? new FairSync() : new NonfairSync();
}
```

### 5.1.1 非公平锁

非公平锁是指一个线程将任务都执行完毕，导致其他的线程处于一个饿死的状态。

缺点：

- 导致线程饿死

优点：

- 效率高

### 5.1.2 非公平锁

公平锁是指每一个线程都能得到任务执行，不会导致其他的线程处于一个饿死的状态。

缺点：

- 效率较低

优点：

- 线程不会出现饿死

## 5.2 可重入锁（递归锁）

synchronization（隐式锁）、lock（显示锁）

> 相当于回家开门，也就是你只要打开了大门的锁，就可以自由的（无障碍）进入里面的任何一个门（锁）

```
public class EnableInLock {
    public static void main(String[] args) {
        // synchronization 可重入锁
        Object o = new Object();
        new Thread(()->{
            synchronized (o) {
                System.out.println("外层");
                synchronized (o) {
                    System.out.println("中层");
                    synchronized (o) {
                        System.out.println("内层");
                    }
                }
            }
        }).start();
    }
}
```

### Lock 可重入锁

> 上锁和释放锁都必须主动完成，不能缺少释放锁

```java
// lock 可重入锁
ReentrantLock lock = new ReentrantLock();
new Thread(() -> {
    lock.lock();
    try {
        System.out.println("lock可重入锁外层");
        lock.lock();
        try {
            System.out.println("lock可重入锁内层");
        }finally {
            lock.unlock();
        }
    }finally {
        lock.unlock();
    }
}).start();
```

## 5.3 死锁

死锁：两个或者两个以上的进程在执行过程中，因为争夺资源而造成一种互相等待的现象，如果没有外力干涉，他们将一致处于死锁状态。

![image-20230221202424508](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230221202424508.png)



产生死锁的原因：

1. 系统资源不足
2. 进程运行顺序不合适
3. 资源分配不当

```java
/**
 * @author Shier 2023/2/21 20:27
 */
public class DeadLock {
    public static void main(String[] args) {
        Object a = new Object();
        Object b = new Object();
        new Thread(() -> {
            synchronized (a) {
                System.out.println(Thread.currentThread().getName() + "试图获取锁b");
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                synchronized (b) {
                    System.out.println(Thread.currentThread().getName() + "a获取到锁b");
                }
            }
        }).start();
        new Thread(() -> {
            synchronized (b) {
                System.out.println(Thread.currentThread().getName() + "试图获取锁a");
                System.out.println(Thread.currentThread().getName() + "试图获取锁b");
                try {
                    TimeUnit.SECONDS.sleep(1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                synchronized (a) {
                    System.out.println(Thread.currentThread().getName() + "b获取到锁a");
                }
            }
        }).start();
    }
}
```

验证死锁

1. jps -l ：查看当前进程

   ![image-20230221203910392](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230221203910392.png)

2. jstack 进程号 

![image-20230221203927604](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230221203927604.png)











# 6、callable 接口

目前我们学习了有两种创建线程的方法-一种是通过创建 Thread 类，另一种是 通过使用 Runnable 创建线程。但是，Runnable 缺少的一项功能是，当线程终止时（即 run（）方法完成时），我们无法使线程返回结果。为了支持此功能， Java 中提供了 Callable 接口。



## 6.1 创建线程的第三种方案---Callable 接口

Callable 接口特点：

- 为了实现 Runnable，需要实现不返回任何内容的 run())方法，而对于 Callable，需要实现在完成时返回结果的 cal()方法。 •
- call() 方法可以引发异常，而 run() 则不能。 
- 为实现 Callable 而必须重写 call()方法 
- 不能直接替换 runnable，因为 Thread 类的构造方法根本没有 Callable



## 6.2 Future 接口

当 call() 方法完成时，结果必须存储在主线程已知的对象中，以便主线程可 以知道该线程返回的结果。为此，可以使用 Future 对象。

将 Future 视为保存结果的对象，它可能暂时不保存结果，一旦Callable 返回将会进行保存。Future 基本上是==主线程可以跟踪进度以及得到其他线程的结果的==一种方式。要实现此接口，必须重写 5 种方法，这里列出了重要的方法，如下:

1. public boolean cancel（boolean mayInterrupt）：用于停止任务。如果尚未启动，它将停止任务。如果已启动，则仅在 mayInterrupt 为 true 时才会中断任务。
2. public Object get() 抛出 InterruptedException，ExecutionException： 用于获取任务的结果。如果任务完成，它将立即返回结果，否则将等待任务完成，然后返回结果。
3. public boolean isDone() ：如果任务完成，则返回 true，否则返回 false

可以看到 Callable 和 Future 做两件事，Callable 与 Runnable 类似，因为它封装了要在另一个线程上运行的任务，而 Future 用于存储从另一个线程获得的结果。实际上，future 也可以与 Runnable 一起使用。

## 6.3 FutureTask  

Java 库具有具体的 FutureTask 类型，该类型实现 Runnable 和 Future，并方便地将两种功能组合在一起。 可以通过为其构造函数提供 Callable 来创建 FutureTask。然后，将 FutureTask 对象提供给 Thread 的构造函数以创建 Thread 对象。因此，间接地使用 Callable 创建线程。

### 核心原理:(重点)

1. 在主线程中需要执行比较耗时的操作时，但又不想阻塞主线程时，可以把这些任务交给 Future 对象在后台完成，
2. 当主线程将来需要时，就可以通过 Future 对象获得后台任务的计算结果或者执行状态，
3. 一般 FutureTask 多用于耗时的计算，主线程可以在完成自己的任务后，再去获取结果， 
4. 仅在计算完成时才能检索结果；如果计算尚未完成，则阻塞 get 方法，一旦计算完成，就不能再重新开始或取消计算 ，
5. get 方法获取结果只有在计算完成时获取，否则会一直阻塞直到任务转入完成状态，然后会返回结果或者抛出异常 ，
6. get 只计算一次，因此 get 方法放到最后。

例子说明：

1. 我在敲代码，突然口渴了，出去买水不太合适（打断思路），我要继续敲代码，只能单独的叫一个人去帮我买水回来，然后放到我的桌子上，我就可以直接喝。（不影响主线程的情况下，单独开启一个单线程完成任务）
2. 我口渴了，叫人去买水，但是他第一次买的水不是我想喝的，后面他又在去一趟买水，买了几趟才买到想喝的水，如果我下次还叫他去帮忙买水，那么他就可以直接买我喜欢喝的就可以了，不用再折腾那么多次。（也就是汇总一次，计算一次）

```java
// Runnable 创建线程
class RunnableThread implements Runnable {
    @Override
    public void run() {
    }
}
// Callable 接口 , 有返回值
class CallableThread implements Callable {
    @Override
    public Integer call() throws Exception {
        System.out.println(Thread.currentThread().getName() + "进入callable");
        return 2222;
    }
}
public class CallableDemo {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        // Runnable 创建线程
        new Thread(new RunnableThread(), "Runnable创建线程").start();
        // Callable 接口创建线程, FutureTask未来任务
        FutureTask<Integer> futureTask = new FutureTask<>(new CallableThread());
        // 简化写法，FutureTask是一个函数式接口的类
        FutureTask<Integer> ft = new FutureTask<>(() -> {
            System.out.println(Thread.currentThread().getName() + "进入callable");
            return 1024;
        });
        // 创建线程
        new Thread(ft, "ft").start();
        new Thread(futureTask, "futureTask").start();
        // 没有计算完成就一直等待
        while (!ft.isDone()) {
            System.out.println("还在计算.....");
        }
        // 计算完成则会进行汇总 get到结果
        System.out.println(ft.get()); // 1024
        System.out.println(futureTask.get()); // 2222
        System.out.println(Thread.currentThread().getName() + "结束"); // main线程结束
    }
}
```



# 7、JUC三大辅助类

JUC 中提供了三种常用的辅助类，通过这些辅助类可以很好的解决线程数量过 多时 Lock 锁的频繁操作。这三种辅助类为：

1. `CountDownLatch`: 减少计数
2. `CyclicBarrier`: 循环栅栏
3. `Semaphore`: 信号灯



## 7.1 减少计数 CountDownLatch

CountDownLatch 类可以设置一个计数器，然后通过 countDown 方法来进行减 1 的操作，使用 await 方法等待计数器不大于 0，然后继续执行 await 方法之后的语句。

- CountDownLatch 主要有两个方法，当一个或多个线程调用 await 方法时，这些线程会阻塞
- 其它线程调用 countDown 方法会将计数器减 1(调用 countDown 方法的线程不会阻塞)
- 当计数器的值变为 0 时，因 await 方法阻塞的线程会被唤醒，继续执行

实际例子说明：

-  6 个同学陆续离开教室后值班同学才可以关门。

```java
/**
 * @author Shier 2023/2/21 22:11
 * 模拟教室人走完关灯效果
 */
public class CountDownLatchDemo {
    public static void main(String[] args) {
        // 总共10个人，走完了才可以关灯
        // 使用CountDownLatch 进行初始化数据
        CountDownLatch countDownLatch = new CountDownLatch(10);
        for (int i = 10; i > 0; i--) {
            // 创建线程
            new Thread(() -> {
                System.out.println(Thread.currentThread().getName() + "学号学生离开教室");
                // 计数减一
                countDownLatch.countDown();
            }, String.valueOf(i)).start();
        }
        // 如果还没有为0 则会一直等待
        try {
            countDownLatch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + "关门走人了...");
    }
}
```



## 7.2 循环栅栏 CyclicBarrier

使用中 CyclicBarrier 的构造方法第一个参数是目标障碍数，每次执行 CyclicBarrier 一次障碍数会加一，如果达到了目标障碍数，才会执行 cyclicBarrier.await()之后 的语句。可以将 CyclicBarrier 理解为加 1 操作

例子：

- 收集七颗龙珠召唤神龙许愿

```java
/**
 * @author Shier 2023/2/21 22:30
 */
public class CyclicBarrierDemo {
    // 创建目标到达的值
    private static final int NUMBER = 7;

    public static void main(String[] args) {
        // 创建CyclicBarrier对象
        CyclicBarrier cyclicBarrier = new CyclicBarrier(NUMBER, (() -> {
            System.out.println("集齐完毕，开始许愿，祝你愿望成真！");
        }));
        // 创建线程
        for (int i = 1; i <= 7; i++) {
            new Thread(() -> {
                try {
                    System.out.println(Thread.currentThread().getName() + "星珠到手！");
                    // 否则等待
                    cyclicBarrier.await();
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }, String.valueOf(i)).start();
        }
    }
}
```

## 7.3 信号灯 Semaphore

Semaphore 的构造方法中传入的第一个参数是最大信号量（可以看成最大线 程池），每个信号量初始化为一个最多只能分发一个许可证。使用 acquire 方法获得许可证，获得许可之后其他的线程都处于阻塞状态，release 方法释放许可，其他线程方可获得许可证。

场景: 抢车位, 6 部汽车 3 个停车位

```java
package com.shier.jucauxiliary;

import javax.swing.plaf.TableHeaderUI;
import java.util.concurrent.Semaphore;
import java.util.concurrent.TimeUnit;

/**
 * @author Shier 2023/2/21 22:45
 * 6 部汽车 3 个停车位
 */
public class SemaphoreDemo {
    public static void main(String[] args) {
        // 创建Semaphore 设置许可的数量
        Semaphore semaphore = new Semaphore(3);

        // 循环六次，创建六个线程
        for (int i = 1; i <= 6; i++) {
            new Thread(() -> {
                // 获得许可
                try {
                    semaphore.acquire();
                    System.out.println("-------" + Thread.currentThread().getName() + "号车寻找车位ing。");
                    // 设置一个随机时间来占用车位
                    Thread.sleep(2000);
                    System.out.println(Thread.currentThread().getName() + "号车获得车位。");
                } catch (Exception e) {
                    e.printStackTrace();
                } finally {
                    // 释放许可
                    System.out.println("*******" + Thread.currentThread().getName() + "号车离开车位。");
                    semaphore.release();
                }
            }, String.valueOf(i)).start();
        }
    }
}
```





# 8、读写锁  

## 8.1 读写锁介绍  

> 现实中有这样一种场景：对共享资源有读和写的操作，且写操作没有读操作那么频繁。在没有写操作的时候，多个线程同时读一个资源没有任何问题，所以应该允许多个线程同时读取共享资源；但是如果一个线程想去写这些共享资源， 就不应该允许其他线程对该资源进行读和写的操作了。

针对这种场景，JAVA 的并发包提供了读写锁 ReentrantReadWriteLock， 它表示两个锁，一个是读操作相关的锁，称为共享锁；一个是写相关的锁，称为排他锁

线程进入写锁的前提条件：

1. 没有其他线程的读锁 
2. 没有其他线程的写锁 

而读写锁有以下三个重要的特性： 

（1）公平选择性：支持非公平（默认）和公平的锁获取方式，吞吐量还是非公 平优于公平。 

（2）重进入：读锁和写锁都支持线程重进入。 

（3）锁降级：遵循获取写锁、获取读锁再释放写锁的次序，写锁能够降级成为 读锁。

### 8.1.1 读锁发生死锁

![image-20230222101944989](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222101944989.png)



### 8.1.2 写锁发生死锁

当线程1 在对第一个进行写操作，线程2对第二个进行写操作，由于是可以并发操作的，所以当线程1或者线程2对另外的一个线程正在写操作的数据进行修改时需要等待对方写操作完成才可以进行，此时就有可能会出现互相操作对方的写操作进而出现死锁。

![image-20230222102149497](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222102149497.png)

#### 锁的比较

![image-20230222110348300](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222110348300.png)

读写锁的案例实现：

```java
/**
 * @author Shier 2023/2/22 10:27
 */
class CacheDemo {

    // 创建一个map集合 volatile表示不断变化
    private volatile Map<String, Object> map = new HashMap<>();
    // 创建一个读写锁
    private ReadWriteLock readWriteLock = new ReentrantReadWriteLock();

    // 写入过程
    public void writeMethod(String key, Object value) {
        // 写锁上锁
        readWriteLock.writeLock().lock();
        try {
            System.out.println(Thread.currentThread().getName() + "正在写入内容" + key);
            TimeUnit.MICROSECONDS.sleep(300);
            // 写入内容
            map.put(key, value);
            System.out.println(Thread.currentThread().getName() + "写入完成" + key);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 释放锁
            readWriteLock.writeLock().unlock();
        }
    }

    // 读取过程
    public Object readMethod(String key) {

        // 读锁上锁
        readWriteLock.readLock().lock();
        Object result = null;
        try {
            System.out.println(Thread.currentThread().getName() + "正在读取内容" + key);
            TimeUnit.MICROSECONDS.sleep(300);
            // 读取内容
            result = map.get(key);
            System.out.println(Thread.currentThread().getName() + "读取到了" + key);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 释放锁
            readWriteLock.readLock().unlock();
        }
        return result;
    }
}

public class ReadWriteLockDemo {
    public static void main(String[] args) {
        CacheDemo cacheDemo = new CacheDemo();
        // 写
        for (int i = 1; i <= 10; i++) {
            final int number = i;
            new Thread(() -> {
                cacheDemo.writeMethod(String.valueOf(number), number);
            },String.valueOf(i)).start();
        }
        // 读
        for (int i = 1; i <= 10; i++) {
            final int number = i;
            new Thread(() -> {
                cacheDemo.readMethod(String.valueOf(number));
            },String.valueOf(i)).start();
        }
    }
}
```



### 8.1.3 读写锁降级

锁降级是指将当前持有的锁从高级别锁降为低级别锁的过程。在多线程并发执行的场景中，通常情况下我们会在业务处理的过程中加锁，为了避免死锁、性能问题等问题，有时候需要在代码执行的过程中进行锁降级。

锁降级的主要目的是==为了在持有高级别锁的情况下，可以继续执行需要持有低级别锁才能进行的操作，而不需要释放高级别锁再重新获取低级别锁的操作==。例如，在一段代码中持有了数据库的行级锁，为了执行某些操作需要进行表级锁的操作，可以通过锁降级将行级锁降为表级锁。

锁降级的操作一般有以下几个步骤：

1. 获取高级别锁；
2. 执行需要高级别锁才能执行的操作；
3. 获取低级别锁；
4. 释放高级别锁。
5. 使用低级别锁

在执行锁降级的过程中，需要保证高级别锁和低级别锁的顺序，先获取高级别锁再获取低级别锁，同时在释放锁的过程中也需要按照相反的顺序进行释放。如果顺序不正确，可能会导致死锁等问题。

总的来说，锁降级可以避免在执行代码的过程中频繁地获取和释放锁，提高并发性能和降低死锁等问题的发生。但是，在实际应用中需要根据具体情况进行评估和选择，避免过度使用锁降级导致代码难以维护。

大致的流程：



~~~mermaid
graph LR
a(获取写锁)-->b(获取读锁)-->c(释放写锁)-->d(释放读锁)
~~~

写锁的权限大于读锁的权限。

```java
public class LowerLockDemo {
    public static void main(String[] args) {
        // 创建可重入锁对象
        ReentrantReadWriteLock readWriteLock = new ReentrantReadWriteLock();
        // 写锁
        ReentrantReadWriteLock.WriteLock writeLock = readWriteLock.writeLock();
        // 读锁
        ReentrantReadWriteLock.ReadLock readLock = readWriteLock.readLock();
        // 一般来说写锁大于读锁
        // 1.获取高级锁-写锁
        writeLock.lock();
        System.out.println("高级锁-写锁");
        // 2.获取低级锁-读锁
        readLock.lock();
        System.out.println("低级锁-读锁");
        // 3. 释放高级锁
        writeLock.unlock();
        // 4. 释放低级锁
        readLock.unlock();
    }
}
```

- 读锁不能升级为写锁
- 也就是低级锁不能升级为高级所

原因: 当线程获取读锁的时候，可能有其他线程同时也在持有读锁，因此不能把 获取读锁的线程“升级”为写锁；而对于获得写锁的线程，它一定独占了读写 锁，因此可以继续让它获取读锁，当它同时获取了写锁和读锁后，还可以先释 放写锁继续持有读锁，这样一个写锁就“降级”为了读锁。



## 8.2 悲观锁

悲观锁是一种保守的锁策略，其核心思想是在访问共享资源时，假定其他线程会对该资源进行修改，因此采取加锁的方式防止其他线程的干扰。悲观锁常见的实现方式是使用 synchronized 关键字或者 ReentrantLock 等锁对象。

> 当一个人进行操作时会上锁，阻塞别人，其他人就不能进行操作，只有当这个人把锁释放掉，其他人才可以进行操作，当其他人操作时也会重复以上的步骤。

悲观锁的优点：

1. 可以保证并发访问的安全性，避免数据的脏读、幻读等问题；
2. 悲观锁适用于写操作多、读操作少的场景，可以减少写冲突的发生，提高并发性能。

悲观锁的缺点：

1. 悲观锁会在访问共享资源时，阻塞其他线程的访问，降低并发性能；
2. 不支持并发操作，只能一个人一个人的进行操作，导致效率性能降低。
3. 悲观锁对性能的影响和加锁的范围有关，加锁范围过大，会导致并发性能下降；
4. 如果悲观锁的加锁粒度太小，会导致线程频繁加锁和释放锁，从而造成性能瓶颈。

总的来说，悲观锁虽然能够==保证并发访问的安全性==，但是在==高并发场景下可能会导致性能问题==，需要开发者在应用程序设计时进行权衡，选择适合的锁策略来提高并发性能



## 8.3 乐观锁

乐观锁是一种乐观的锁策略，其核心思想是假设在并发访问时，共享资源不会发生冲突，因此不会阻塞其他线程的访问，而是在更新共享资源时检查是否有其他线程对该资源进行修改。乐观锁常见的实现方式有版本号机制和CAS（Compare And Swap）算法等。

乐观锁的优点：

1. 在并发读操作多、写操作少的场景下，乐观锁可以提高并发性能；
2. 乐观锁不会阻塞其他线程的访问，避免了加锁的开销；
3. 乐观锁的实现方式比较简单，实现成本低。

乐观锁的缺点：

1. 乐观锁不能保证并发访问的安全性，存在数据的冲突、丢失等问题；
2. 乐观锁的实现方式==需要在更新共享资源时检查是否有其他线程的干扰==，如果存在干扰需要进行重试，这会增加一定的开销；
3. 乐观锁的适用场景有限，不适用于写操作比较频繁的场景。

总的来说，乐观锁在一些==读操作多、写操作少的场景下可以提高并发性能==，但是在一些==高并发写操作的场景下可能会导致数据冲突==，需要开发者在实际应用中进行评估和选择。



## 8.4 表锁、行锁

表锁是指对整个表进行加锁，当一个事务访问某个表时，会对整个表进行加锁，其他事务无法对该表进行更新、删除等操作。

优点：实现简单，对于一些只读的操作可以提高并发性能，

缺点：并发性能较低，会对整个表进行加锁，影响其他事务的操作。



行锁是指对表中的一行或多行进行加锁，当一个事务访问某个表时，只对需要访问的行进行加锁，其他行不受影响。

优点：并发性能较高，只对需要访问的行进行加锁，不会影响其他事务的操作

缺点：实现复杂，需要保证行级锁的粒度不会过细，否则会降低并发性能，可能会出现死锁状态。

> 在实际应用中，如果只有读操作，可以采用表锁提高并发性能；如果有较多的写操作，应该采用行锁避免数据冲突。在实现行锁时，需要注意锁粒度的问题，避免锁定过细或过粗。同时，为了提高并发性能，可以采用一些辅助手段，如缓存、索引等。
>



# 9、JUC阻塞队列

## 9.1 BlockingQueue 简介

Concurrent 包中，BlockingQueue 很好的解决了多线程中，如何高效安全 “传输”数据的问题。通过这些高效并且线程安全的队列类，为我们快速搭建 高质量的多线程程序带来极大的便利。

阻塞队列，顾名思义，首先它是一个队列（先进先出）， 通过一个共享的队列，可以使得数据由队列的一端输入，从另外一端输出；

![image-20230222112840222](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222112840222.png)



- 当队列是空的，从队列中获取元素的操作将会被阻塞 
- 当队列是满的，从队列中添加元素的操作将会被阻塞 
- 试图从空的队列中获取元素的线程将会被阻塞，直到其他线程往空的队列插入新的元素 
- 试图向已满的队列中添加新元素的线程将会被阻塞，直到其他线程从队列中移除一个或多个元素或者完全清空，使队列变得空闲起来并后续新增

常用的队列主要有以下两种：

- 先进先出（FIFO）：先插入的队列的元素也最先出队列，类似于排队的功能。 从某种程度上来说这种队列也体现了一种公平性
- 后进先出（LIFO）：后插入队列的元素最先出队列，这种队列优先处理最近发 生的事件(栈)



### 9.1.1 多线程的阻塞

在多线程领域：所谓阻塞，在某些情况下会挂起线程（即阻塞），一旦条件满足，被挂起 的线程又会自动被唤起。

使用 BlockingQueue 好处是我们不需要关心什么时候需要阻塞线程，什么时候需要唤醒线程，因为这一切 BlockingQueue 都给你一手包办了

在 concurrent 包发布以前，在多线程环境下，我们每个程序员都必须去自己控制这些细节，尤其还要兼顾效率和线程安全，而这会给我们的程序带来不小的复杂度。

> 多线程环境中，通过队列可以很容易实现数据共享，比如经典的“生产者”和 “消费者”模型中，通过队列可以很便利地实现两者之间的数据共享。假设我们有若干生产者线程，另外又有若干个消费者线程。如果生产者线程需要把准 备好的数据共享给消费者线程，利用队列的方式来传递数据，就可以很方便地 解决他们之间的数据共享问题。但如果生产者和消费者在某个时间段内，万一 发生数据处理速度不匹配的情况呢？理想情况下，如果生产者产出数据的速度 大于消费者消费的速度，并且当生产出来的数据累积到一定程度的时候，那么 生产者必须暂停等待一下（阻塞生产者线程），以便等待消费者线程把累积的 数据处理完毕，反之亦然。

- 当队列中没有数据的情况下，消费者端的所有线程都会被自动阻塞（挂起）， 直到有数据放入队列 
- 当队列中填满数据的情况下，生产者端的所有线程都会被自动阻塞（挂起）， 直到队列中有空的位置，线程被自动唤醒



## 9.2 BlockingQueue 核心方法

![image-20230222121403239](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222121403239.png)

### 9.2.1 放入数据

- `offer(anObject)`：表示如果可能的话，将 anObject 加到 BlockingQueue 里，即 如果 BlockingQueue 可以容纳,则返回 true,否则返回 false.（本方法不阻塞当 前执行方法的线程） 
- `offer(E o, long timeout, TimeUnit unit)`：可以设定等待的时间，如果在指定 的时间内，还不能往队列中加入 BlockingQueue，则返回失败 
- `put(anObject)`：把 anObject 加到 BlockingQueue 里，如果 BlockQueue 没有空间,则调用此方法的线程被阻断直到 BlockingQueue 里面有空间再继续

### 9.2.2 获取数据

- `poll(time)`：取走 BlockingQueue 里排在首位的对象,若不能立即取出,则可以等 time 参数规定的时间,取不到时返回 null
- `poll(long timeout, TimeUnit unit)`：从 BlockingQueue 取出一个队首的对象， 如果在指定时间内，队列一旦有数据可取，则立即返回队列中的数据。否则知 道时间超时还没有数据可取，返回失败。  
- `take()`：取走 BlockingQueue 里排在首位的对象,若 BlockingQueue 为空,阻断 进入等待状态直到 BlockingQueue 有新的数据被加入; 
- `drainTo()`：一次性从 BlockingQueue 获取所有可用的数据对象（还可以指定 获取数据的个数），通过该方法，可以提升获取数据效率；不需要多次分批加 锁或释放锁。

```java
// 创建一个BlockingQueue对象
ArrayBlockingQueue<String> blockingQueue = new ArrayBlockingQueue<>(2);

// 第一组
System.out.println(blockingQueue.add("a"));
System.out.println(blockingQueue.add("cc"));
System.out.println(blockingQueue.element());  // 查看第一个元素添加是否成功
// System.out.println(blockingQueue.add("b")); // 超出容量，报错
System.out.println(blockingQueue.remove());
System.out.println(blockingQueue.remove());
System.out.println(blockingQueue.remove());// 报错
// 第二组
System.out.println(blockingQueue.offer("c"));
System.out.println(blockingQueue.offer("2"));
System.out.println(blockingQueue.offer("3")); // 报错
System.out.println(blockingQueue.poll());
System.out.println(blockingQueue.poll());
System.out.println(blockingQueue.poll());// 报错

// 第三组
blockingQueue.put("dd1");
blockingQueue.put("dd2");
blockingQueue.put("dd3");// 报错
System.out.println(blockingQueue.take());
System.out.println(blockingQueue.take());
System.out.println(blockingQueue.take());// 报错

//第四组
System.out.println(blockingQueue.offer("a"));
System.out.println(blockingQueue.offer("cc"));
blockingQueue.offer("asdc", 3L, TimeUnit.SECONDS);// 报错
```

## 9.3 BlockingQueue  实现类

### 9.3.1 ArrayBlockingQueue(常用) 

- 由数组结构组成的==有界阻塞队列==

### 9.3.2  LinkedBlockingQueue(常用)

-  由==链表结构组成的有界==（但大小默认值为 integer.MAX_VALUE）阻塞队列

ArrayBlockingQueue 和 LinkedBlockingQueue 是两个最普通也是最常用 的阻塞队列，一般情况下，在处理多线程间的生产者消费者问题，使用这两个 类足以。

### 9.3.3 DelayQueue

-  ==使用优先级队列实现的延迟无界阻塞队列==

### 9.3.4 PriorityBlockingQueue

基于优先级的阻塞队列（优先级的判断通过构造函数传入的 Compator 对象来 决定），但需要注意的是 PriorityBlockingQueue 并不会阻塞数据生产者，而只会在没有可消费的数据时，阻塞数据的消费者。 因此使用的时候要特别注意，生产者生产数据的速度绝对不能快于消费者消费 数据的速度，否则时间一长，会最终耗尽所有的可用堆内存空间。

在实现 PriorityBlockingQueue 时，内部控制线程同步的锁采用的是公平锁

- ==支持优先级排序的无界阻塞队列==

### 9.3.5 SynchronousQueue

- 不存储元素的阻塞队列，也即==单个元素的队列==

### 9.3.6 LinkedTransferQueue

-  由链表组成的==无界阻塞队列==

### 9.3.7 LinkedBlockingDeque

- 由链表组成的==双向阻塞队列==

## 9.4 总结

在多线程领域：所谓阻塞，在某些情况下会挂起线程（即阻塞），一旦条件满足，被挂起的线程又会自动被唤起



# 10、线程池

## 10.1 线程池简介

线程池（英语：thread pool）：一种线程使用模式。

线程池是一个维护线程的池子，可以在需要时动态地创建和回收线程，从而避免了线程创建和销毁的开销，提高了线程的复用性和并发性能。

线程池通常包括以下几个组件：

1. 任务队列：用于存放等待执行的任务。
2. 线程池管理器：用于管理线程池，包括线程的创建、销毁、监控等。
3. 线程工厂：用于创建线程。
4. 线程池执行器：用于提交任务到线程池中执行。

线程池的优点包括：

1. 降低线程创建和销毁的开销，提高了线程的复用性和并发性能。
2. 可以控制并发线程的数量，避免因过多线程导致系统负载过高或资源耗尽的问题。
3. 可以提供线程的可管理性，包括线程的监控、统计和异常处理等。

线程池的缺点主要在于对于任务处理时间较短的场景中，线程池的开销可能会比线程创建和销毁的开销更大。此外，线程池的并发度需要根据实际情况进行调整，如果并发度过高会导致系统负载过高，反之则会影响系统的性能。

在使用线程池时，需要根据实际情况进行配置，包括线程池的大小、任务队列的大小、拒绝策略等。同时，还需要注意线程池的并发度和资源使用情况，避免因过度使用线程池导致系统崩溃或性能下降。





## 10.2 线程池的使用方式

> 线程池可以通过调整线程池的大小、任务队列的大小、拒绝策略等参数来优化线程池的性能。同时，在使用线程池的过程中需要注意线程池的并发度和资源使用情况，避免因过度使用线程池导致系统崩溃或性能下降。

### 10.2.1 一池N线程 newFixedThreadPool(常用)

1. 创建线程池对象：通过线程池工厂类的静态方法创建一个线程池对象，例如通过Executors类的静态方法创建。

   ~~~java
   ExecutorService executor = Executors.newFixedThreadPool(10);
   ~~~

2. 提交任务到线程池：通过线程池的execute()方法或submit()方法提交任务到线程池中执行。

   ~~~java
   executor.execute(new Runnable() {
       @Override
       public void run() {
           // 执行具体的任务
       }
   });
   
   Future<String> future = executor.submit(new Callable<String>() {
       @Override
       public String call() throws Exception {
           // 执行具体的任务，返回结果
           return "result";
       }
   });
   ~~~

3. 关闭线程池：在任务执行完毕后，通过线程池的shutdown()方法关闭线程池，防止新的任务提交到线程池中。

   ~~~java
   executor.shutdown();
   ~~~

#### 特点

1. 线程池中的线程处于一定的量，可以很好的控制线程的并发量 
2. 线程可以重复被使用，在显示关闭之前，都将一直存在 
3. 超出一定量的线程被提交时候需在队列中等待

场景: 适用于可以预测线程数量的业务中，或者服务器负载较重，对线程数有严 格限制的场景



### 10.2.2 newCachedThreadPool(常用)

- 创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空 闲线程，若无可回收，则新建线程
- 可扩容线程池大小。

#### 特点

- 线程池中数量没有固定，可达到最大值（Interger. MAX_VALUE） 
- 线程池中的线程可进行缓存重复利用和回收（回收默认时间为 1 分钟） 
- 当线程池中，没有可用线程，会重新创建一个线程

场景: 适用于创建一个可无限扩大的线程池，服务器负载压力较轻，执行时间较短，任务多的场景。



### 10.2.3 newSingleThreadExecutor(常用)

- 创建一个使用单个 worker 线程的 Executor，以无界队列方式来运行该线程。
- 一池一线程

#### 特点

- 线程池中最多执行 1 个线程，之后提交的线程活动将会排在队列中以此执行

场景: 适用于需要保证顺序执行各个任务，并且在任意时间点，不会同时有多个 线程的场景



### 三个线程的使用方式：

~~~java
/**
 * @author Shier 2023/2/22 13:11
 */
public class ThreadPollDemo1 {
    public static void main(String[] args) {
        // 一池N线程
        // 创建线程池
        ExecutorService executorService1 = Executors.newFixedThreadPool(3);
        // 一池一线程
        ExecutorService executorService2 = Executors.newSingleThreadExecutor();
        // 一池可扩容线程
        ExecutorService executorService3 = Executors.newCachedThreadPool();
        
        try {
            for (int i = 1; i <= 5; i++) {
                // 执行线程
                executorService1.execute(() -> {
                    System.out.println(Thread.currentThread().getName() + "号线程正在执行...");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 关闭线程池
            executorService1.shutdown();
        }

    }
}
~~~



## 10.3  线程池的七个参数

1. corePoolSize：线程池的核心线程数 
2. maximumPoolSize：能容纳的最大线程数
3. keepAliveTime：空闲线程存活时间  
4. unit：存活的时间单位
5. workQueue：存放提交但未执行任务的队列
6. threadFactory：创建线程的工厂类 
7. handler：等待队列满后的拒绝策略

线程池中，有三个重要的参数，决定影响了拒绝策略：

1. corePoolSize - 核心线程数，也即最小的线程数
2. workQueue - 阻塞队列
3. maximumPoolSize - 最大线程数 当提交任务数大于 corePoolSize 的时候，会优先将任务放到 workQueue 阻塞队列中。

当阻塞队列饱和后，会扩充线程池中线程数，直到达到maximumPoolSize 最大线程数配置。此时，再多余的任务，则会触发线程池的拒绝策略了。 总结起来，也就是一句话，当提交的任务数大于（workQueue.size() +  maximumPoolSize ），就会触发线程池的拒绝策略。

### 10.3.1 拒绝策略(重点) 

1. CallerRunsPolicy：当触发拒绝策略，只要线程池没有关闭的话，则使用调用 线程直接运行任务。一般并发比较小，性能要求不高，不允许失败。但是，由 于调用者自己运行任务，如果任务提交速度过快，可能导致程序阻塞，性能效 率上必然的损失较大 。
2. AbortPolicy：丢弃任务，并抛出拒绝执行 RejectedExecutionException 异常 信息。线程池默认的拒绝策略。必须处理好抛出的异常，否则会打断当前的执 行流程，影响后续的任务执行。 
3. DiscardPolicy： 直接丢弃，其他啥都没有 
4. DiscardOldestPolicy: 当触发拒绝策略，只要线程池没有关闭的话，丢弃阻塞队列 workQueue 中最老的一个任务，并将新任务加入

![image-20230222134009491](https://xingqiu-tuchuang-1256524210.cos.ap-shanghai.myqcloud.com/2767/image-20230222134009491.png)

1. 在创建了线程池后，线程池中的线程数为零
2. 当调用 execute()方法添加一个请求任务时，线程池会做出如下判断： 
   1.  如 果正在运行的线程数量小于 corePoolSize，那么马上创建线程运行这个任务； 
   2. 如果正在运行的线程数量大于或等于 corePoolSize，那么将这个任务放入 队列； 
   3. 如果这个时候队列满了且正在运行的线程数量还小于 maximumPoolSize，那么还是要创建非核心线程立刻运行这个任务； 
   4. 如果队列满了且正在运行的线程数量大于或等于 maximumPoolSize，那么线程 池会启动饱和拒绝策略来执行。 
3. 当一个线程完成任务时，它会从队列中取下一个任务来执行 
4. 当一个线程无事可做超过一定的时间（keepAliveTime）时，线程会判断： 
   1. 如果当前运行的线程数大于 corePoolSize，那么这个线程就被停掉。 
   2. 所以线程池的所有任务完成后，它最终会收缩到 corePoolSize 的大小。

自定义线程示例：

```java
public class ThreadPollDemo2 {
    public static void main(String[] args) {
        // 自定义线程池
        ThreadPoolExecutor executor = new ThreadPoolExecutor(2,
                5,
                2L,
                TimeUnit.SECONDS,
                new ArrayBlockingQueue<>(2),
                Executors.defaultThreadFactory(),
                new ThreadPoolExecutor.AbortPolicy());
        try {
            for (int i = 1; i <= 5; i++) {
                // 执行线程
                executor.execute(() -> {
                    System.out.println(Thread.currentThread().getName() + "号线程正在执行...");
                });
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 关闭线程池
            executor.shutdown();
        }
    }
}
```



# 11、Fork/Join 框架

Fork/Join 它可以将一个大的任务拆分成多个子任务进行并行处理，最后将子 任务结果合并成最后的计算结果，并进行输出。Fork/Join 框架要完成两件事情：

- Fork：把一个复杂任务进行分拆，大事化小 
- Join：把分拆任务的结果进行合并

## 11.1 任务处理

1. 任务分割：首先 Fork/Join 框架需要把大的任务分割成足够小的子任务，如果子任务比较大的话还要对子任务进行继续分割 
2. 执行任务并合并结果：分割的子任务分别放到双端队列里，然后几个启动线程 分别从双端队列里获取任务执行。
3. 子任务执行完的结果都放在另外一个队列里， 启动一个线程从队列里取数据，然后合并这些数据。



## 11.2 Fork 方法

### 原理：

> 当我们调用 ForkJoinTask 的 fork 方法时，程序会把 任务放在 ForkJoinWorkerThread 的 pushTask 的 workQueue 中，异步地 执行这个任务，然后立即返回结果



## 11.3 join 方法

> Join 方法的主要作用是阻塞当前线程并等待获取结果。

已完成（NORMAL）、被取消（CANCELLED）、信号（SIGNAL）和出 现异常（EXCEPTIONAL）

- 如果任务状态是已完成，则直接返回任务结果
- 如果任务状态是被取消，则直接抛出 CancellationException 
- 如果任务状态是抛出异常，则直接抛出对应的异常

```java
class MyTask extends RecursiveTask<Integer> {

    // 拆分的插值不能超过10
    private static final Integer VALUE = 10;
    private int left;
    private int right;
    private int result;

    public MyTask(int left, int right) {
        this.left = left;
        this.right = right;
    }

    @Override
    protected Integer compute() {
        // 判断差值
        if ((right - left) <= 10) {
            for (int i = left; i <= right; i++) {
                result += i;
            }
        } else {
            // 进一步拆分
            int middle = (left + right) / 2;
            // 左拆分
            MyTask leftTask = new MyTask(left, middle);
            // 右拆分
            MyTask rightTask = new MyTask(middle + 1, right);

            leftTask.fork();
            rightTask.fork();
            // 合并
            result = leftTask.join() + rightTask.join();
        }
        return result;
    }
}

public class AddSum {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        MyTask myTask = new MyTask(0, 100);
        ForkJoinPool forkJoinPool = new ForkJoinPool();
        ForkJoinTask<Integer> submit = forkJoinPool.submit(myTask);
        Integer integer = submit.get();
        System.out.println(integer);
        // 关闭
        forkJoinPool.shutdown();
    }
}
```



# 12、CompletableFuture异步回调

使用CompletableFuture可以将耗时的操作异步执行，不会阻塞主线程，从而提高程序的性能和响应速度。同时，它还可以通过回调函数来处理计算结果，以及处理可能出现的异常情况。



## 12.1 有无返回值的异步调用

```java
public class CompletableFutureDemo {
    public static void main(String[] args) throws ExecutionException, InterruptedException {

        // 没有返回值的异步调用
        CompletableFuture<Void> runAsync = CompletableFuture.runAsync(() -> {
            System.out.println(Thread.currentThread().getName() + "*****没有返回值的异步调用测试");
        });
        runAsync.get();

        // 有返回值的异步调用
        CompletableFuture<Integer> supplyAsync = CompletableFuture.supplyAsync(() -> {
            System.out.println(Thread.currentThread().getName() + "======有返回值的异步调用测试");
            // int i = 1 / 0;
            return 200;
        });
        supplyAsync.whenComplete((t, u) -> {
            System.out.println("t:" + t); // 返回值
            System.out.println("u:" + u);// 异常值
        }).get();
    }
}
```



~~~java
CompletableFuture<Integer> future = CompletableFuture.supplyAsync(() -> {
    // 执行耗时的计算，返回结果
    return 1 + 2;
});

future.thenAccept(result -> {
    // 处理计算结果
    System.out.println("计算结果为：" + result);
});

future.exceptionally(ex -> {
    // 处理可能出现的异常情况
    System.out.println("计算出错：" + ex.getMessage());
    return null;
});
~~~

在这个例子中，我们使用`CompletableFuture.supplyAsync`方法来创建一个异步计算任务。该方法接受一个`Supplier`函数，用于执行耗时的计算并返回结果。然后，我们使用`thenAccept`方法来注册一个回调函数，该函数会在计算完成后被执行，并且会接收计算结果作为参数。最后，我们使用`exceptionally`方法来注册一个异常处理函数，该函数会在计算出错时被执行，并且会接收异常信息作为参数。

需要注意的是，`thenAccept`方法是一个消费者函数，它不会返回任何值，因此不能在回调函数中修改计算结果。如果需要在回调函数中修改计算结果，可以使用`thenApply`方法，该方法接受一个函数，用于将计算结果转换为另一个值，并返回转换后的结果。





























