# 进程与线程

进程 ：

* 系统进行**资源分配和调度**的最小单位
* 进程就是用来加载指令、管理内存、管理 IO 的 
* 当一个程序被运行，从磁盘加载这个程序的代码至内存，这时就开启了一个进程。 
* 进程就可以视为程序的一个实例。

线程 ：

* 系统进行**运算调度**（或程序执行的）的最小单位
* 一个进程之内可以分为一到多个线程。
* 一个线程就是一个指令流，将指令流中的一条条指令以一定的顺序交给 CPU 执行 



二者对比：

* 进程基本上相互独立的，而线程存在于进程内，是进程的一个子集 
* 进程拥有共享的资源，如内存空间等，供其内部的线程共享 
* 进程间通信较为复杂 
  * 同一台计算机的进程通信称为 IPC（Inter-process communication） 
  * 不同计算机之间的进程通信，需要通过网络，并遵守共同的协议，例如 HTTP 

* 线程通信相对简单，因为它们共享进程内的内存，一个例子是多个线程可以访问同一个共享变量 
* 线程更轻量，线程上下文切换成本一般上要比进程上下文切换低



## 并发与并行

* 并发：**在同一时间段，多个指令在单个CPU上交替执行**；使用单核CPU的时候，同一时刻只能有一条指令执行，但多个指令被快速的轮换执行，使得在宏观上具有多个指令同时执行的效果，但在微观上并不是同时执行的，只是把时间分成若干端，使多个指令快速交替的执行。**（微观串行，宏观并行）**

* 并行： **在同一时刻，多个指令在多个CPU上同时进行**；使用多核CPU的时候，同一时刻，有多条指令在多个CPU上同时执行**（微观、宏观皆并行）**



不管并发还是并行，都提高了程序对CPU资源的利用率，最大限度地利用CPU资源，而我们使用多线程的目的就是为了提高CPU资源的利用率。



## 同步与异步

以调用方角度来讲，如果

* 需要等待结果返回，才能继续运行就是同步
* 不需要等待结果返回，就能继续运行就是异步



# Java线程

## 创建和运行线程

### 方法1：Thread类

```java
//创建线程对象
Thread t = new Thread("t1"){
    @Override
    public void run(){
        //执行的任务
    }
};
//开启线程
t1.start();
```

### 方法2：Runnable接口配合Thread类

把【线程】和【任务】（要执行的代码）分开

* Thread 代表线程 
* Runnable 可运行的任务（线程要执行的代码）

```java
Runnable task = new Runnable() {
    @Override
	public void run(){
     // 要执行的任务
    }  
};
// 创建线程对象
// 参数1 是任务对象; 参数2 是线程名字，推荐
Thread t = new Thread(task,"t2");
// 启动线程
t2.start(); 
```

lambda简化：

```java
new Thread(() -> {
    System.out.println(Thread.currentThread().getName() + "c");
}, "t1").start();
```

### Thread 与 Runnable 的关系

方法1 是把线程和任务合并在了一起，方法2 是把线程和任务分开了 

* 用 Runnable 更容易与线程池等高级 API 配合 
* 用 Runnable 让任务类脱离了 Thread 继承体系，更灵活



### 方法3：实现Callable接口 + FutureTask类配合Thread类

FutureTask 能够接收 Callable 类型的参数，用来处理有返回结果的情况

```java
public class CreateThread03 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //3.创建MyCallable对象
        MyCallable myCallable = new MyCallable();
        //4.创建Future接口的实现类FutureTask的对象，将MyCallable对象作为构造方法的参数
        FutureTask<String> ft = new FutureTask<>(myCallable);
        //5.创建Thread类的对象，将FutureTask对象作为构造方法的参数
        Thread thread1 = new Thread(ft);
        Thread thread2 = new Thread(ft);
        //6.启动线程
        thread1.start();
        thread2.start();
        //7.调用FutureTask对象的get()方法，可以获取线程结束之后的结果
        String result = ft.get();
        System.out.println(result);
	}
}
//1.定义一个类MyCallable实现Callable接口
class MyCallable implements Callable<String>{
    //2.重写call()方法
    @Override
    public String call() throws Exception {
        System.out.println(Thread.currentThread().getName());
        return "ok";
    }
}
```

```
Thread-0
ok
注意：只会有一个线程实现任务
```

lambda简化：

```java
FutureTask<Integer> task = new FeatureTask<>(() ->{
    //要执行的任务
    return 100;//有返回值
});
new Thread(task,"t3").start();

// 主线程阻塞，同步等待 task 执行完毕的结果
Integer result = task3.get();
```



## 查看进程线程的方法

* linux 
  * `ps -fe` 查看所有进程 
  * `ps -fT -p <PID>`查看某个进程（PID）的所有线程 
  * `kill` 杀死进程 
  * `top` 按大写 H 切换是否显示线程 
  * `top -H -p <PID>` 查看某个进程（PID）的所有线程
* Java （在IDEA的Terminal输入指令）
  * `jps` 命令查看所有 Java 进程 
  * `jstack <PID>` 查看某个 Java 进程（PID）的所有线程状态 
  * `jconsole` 来查看某个 Java 进程中线程的运行情况（图形界面）

## 栈与栈帧

JVM中的栈内存是给谁用的呢？其实就是线程，每个线程启动后，虚拟机就会为其分配一块栈内存。 

* 每个栈由多个栈帧（Frame）组成，对应着每次方法调用时所占用的内存 

* 每个线程只能有**一个活动栈帧**，对应着当前正在执行的那个方法





## 线程上下文切换 

因为以下一些原因导致 cpu 不再执行当前的线程，转而执行另一个线程的代码 ：

* 线程的 cpu 时间片用完
* 垃圾回收 
* 有更高优先级的线程需要运行 
* 线程自己调用了 sleep、yield、wait、join、park、synchronized、lock 等方法 

当 上下文切换 发生时，需要由操作系统保存当前线程的状态，并恢复另一个线程的状态，Java 中对应的概念 就是程序计数器（Program Counter Register），它的作用是记住下一条 jvm 指令的执行地址，是线程私有的

* 状态包括程序计数器、虚拟机栈中每个栈帧的信息，如局部变量、操作数栈、返回地址等
* 上下文切换 频繁发生会影响性能



## Thread中的方法

### 常见方法概览

| 方法名           | static | 功能说明                                                     | 注意                                                         |
| ---------------- | ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| start()          |        | 启动一个新线 程，在新的线程运行 run 方法中的代码             | start 方法只是让线程进入就绪，里面代码不一定立刻 运行（CPU 的时间片还没分给它）。每个线程对象的 start方法**只能调用一次**，如果调用了多次会出现 IllegalThreadStateException |
| run()            |        | 新线程启动后会 调用的方法                                    | 如果在构造 Thread 对象时传递了 Runnable 参数，则 线程启动后会调用 Runnable 中的 run 方法，否则默认不执行任何操作。但可以创建 Thread 的子类对象， 来覆盖默认行为 |
| join()           |        | 使其他线程等待调用该方法的线程运行结束                       |                                                              |
| join(long n)     |        | 等待线程运行结 束,最多等待 n 毫秒                            |                                                              |
| getId()          |        | 获取线程长整型 的 id                                         | id 唯一                                                      |
| setName(String)  |        | 修改线程名                                                   |                                                              |
| getName()        |        | 获取线程名                                                   |                                                              |
| getPriority()    |        | 获取线程优先级                                               |                                                              |
| setPriority(int) |        | 修改线程优先级                                               | java中规定线程优先级是1~10 的整数，较大的优先级能提高该线程被 CPU 调度的机率 |
| getState()       |        | 获取线程状态                                                 | Java 中线程状态是用 6 个 enum 表示，分别为： NEW, RUNNABLE, BLOCKED, WAITING, TIMED_WAITING, TERMINATED |
| isInterrupted()  |        | 判断是否被打断                                               | 判断线程是否被打断，是则返回true，否则返回false;**不会清除 打断标记** |
| interrupt()      |        | 打断线程                                                     | 如果被打断线程正在 sleep，wait，join 会导致被打断的线程抛出 InterruptedException，并清除打断标记 （false)；如果打断的正在运行的线程，则会设置打断标记 ；park 的线程被打断，也会设置 打断标记 |
| interrupted()    | static | 判断当前线程是 否被打断                                      | 与isInterrupted()的唯一区别就是：**会清除打断标记**          |
| currentThread()  | static | 获取当前正在执 行的线程                                      |                                                              |
| sleep(long n)    | static | 让当前执行的线程休眠n毫秒，休眠时让出 cpu 的时间片给其它线程 | 1. 调用 sleep 会让当前线程从 Running 进入 Timed Waiting 状态（阻塞） 2. 其它线程可以使用 interrupt 方法打断正在睡眠的线程，这时 sleep 方法会抛出 InterruptedException 3. 睡眠结束后的线程未必会立刻得到执行 4. 建议用 TimeUnit 的 sleep 代替 Thread 的 sleep 来获得更好的可读性 |
| yield()          | static | 提示线程调度器让出当前线程对 CPU的使用                       | 1.调用 yield 会让当前线程从 Running 进入 Runnable 就绪状态，然后调度执行其它线程 2. 具体的实现依赖于操作系统的任务调度器 |

### start()与run()

* run()
  * 就是普通方法，封装了要被线程执行的代码
  * 可以被调用多次; 
  * `run()`方法不结束，main方法是无法继续执行的
  * 在主线程中创建了一个线程t，调用`t.run()`其实是主线程在运行
* start()
  * 用来启动线程，底层自动调用run方法，start方法**只能被调用一次**
  * `start()`瞬间就会结束，原因这个方法的作用是：启动一个新的线程，只要新线程启动成功了，`start()`就结束了



### sleep()与yield()

**sleep**

1. 调用 sleep 会让当前线程从 *Running* 进入 *Timed Waiting* 状态（阻塞）
2. 其它线程可以使用 interrupt 方法打断正在睡眠的线程，这时 sleep 方法会抛出 InterruptedException
3. 睡眠结束后的线程未必会立刻得到执行
4. 建议用 TimeUnit 的 sleep 代替 Thread 的 sleep 来获得更好的可读性

**yield**

1. 调用 yield 会让当前线程从 *Running* 进入 *Runnable* 就绪状态，然后调度执行其它线程
2. 具体的实现依赖于操作系统的任务调度器



###  interrupt()

**打断 sleep，wait，join的线程**

这几个方法都会让线程进入阻塞状态

打断  sleep，wait，join 的线程, 它们都是以抛异常的方式来表示被打断，会清空打断状态（isInterrupted()返回false）

**打断正常运行的线程**

打断正常运行的线程, 不会清空打断状态（isInterrupted()返回true）

对于正常运行的线程，其他线程去打断他只是会告诉他被打断了，但继不继续运行，还是自己说了算

用如下代码示例可以优雅的打断线程，比如线程可以在被打断前处理一些善后工作

```java
private static void test2() throws InterruptedException {
	Thread t2 = new Thread(()->{
 		while(true) {
 			Thread current = Thread.currentThread();
 			boolean interrupted = current.isInterrupted();
 			if(interrupted) {
 				log.debug(" 打断状态: {}", interrupted);
				 break;
 			}
 		}
 	}, "t2");
 	t2.start();
 	sleep(0.5);
 	t2.interrupt();
}
```

### 过时的方法

以下是不推荐使用的方法，这些方法已过时，容易破坏同步代码块，造成线程死锁（比如强制打断时，该线程还持有锁，锁无法释放）

* stop()  停止线程运行

* suspend()  挂起（暂停）线程运行

* resume()  恢复线程运行

## 守护线程

默认情况下，Java 进程需要等待**所有**线程都运行结束，才会结束。

有一种特殊的线程叫做守护线程，只要其它非守护线程运行结束了，**即使守护线程的代码没有执行完**，也会强制结束。

```java
// 设置该线程为守护线程
t1.setDaemon(true);
t1.start();
```

注意：

* 只有在启动守护线程**之前**将其设置为守护线程才有效
* 垃圾回收器线程就是一种守护线程



## 线程生命周期以及状态转换

* 线程生命周期指的是：从线程对象新建，到最终线程死亡的整个过程。
* 线程生命周期包括七个重要阶段：
  * 新建状态（NEW）
  * **就绪状态（RUNNABLE）**
  * **运行状态（RUNNABLE）**
  * 超时等待状态（TIMED_WAITING）
  * 等待状态（WAITING）
  * 阻塞状态（BLOCKED）
  * 死亡状态（TERMINATED）

![7aeea772041a235159f91d1bf7dd4ec](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202409160053697.png)

注意：

* 在运行状态时，执行到**wait()无参方法**，则会进入无期限的等待，进入等待状态，放弃占有的时间片，当被唤醒时，因为把锁也丢了要重新竞争锁，故由等待状态进入阻塞状态，获得锁后，再进入就绪状态：

  **运行状态—>等待状态—>阻塞状态—>就绪状态**

* 在运行状态时，执行到**wait(时间)有参方法**，则会进入计时等待，进入超时等待状态，放弃占有的时间片，当被唤醒或者计时结束时，由等待状态进入阻塞状态，获得锁后，再进入就绪状态：

  **运行状态—>超时等待状态—>阻塞状态—>就绪状态**

  



# 共享模型之管程

## 临界区 

* 一个程序运行多个线程本身是没有问题的 
* 问题出在多个线程访问共享资源 
  * 多个线程读共享资源其实也没有问题
  * 在多个线程对共享资源**读写操作时发生指令交错**，就会出现问题 
* 一段代码块内如果存在**对共享资源的多线程读写操作**，称这段代码块为**临界区** 



## 竞态条件 

多个线程在临界区内执行，由于**代码的执行序列**不同而导致结果无法预测，称之为发生了竞态条件



## synchronized 解决方案

为了避免临界区的竞态条件发生，有多种手段可以达到目的。

* 阻塞式的解决方案：synchronized，Lock 
* 非阻塞式的解决方案：原子变量 

synchronized 俗称【对象锁】，它采用**互斥**的方式让同一 时刻至多只有一个线程能持有【对象锁】，其它线程再想获取这个【对象锁】时就会阻塞住。这样就能保证拥有锁的线程可以安全的执行临界区内的代码，不用担心线程上下文切换 

## 互斥与同步

注意 ：

* 虽然 java 中互斥和同步都可以采用 synchronized 关键字来完成，但它们还是有区别的： 
  * 互斥是保证临界区的竞态条件发生，同一时刻只能有一个线程执行临界区代码 
  * 同步是由于线程执行的先后、顺序不同、需要一个线程等待其它线程运行到某个点





## synchronized

```java
static int counter = 0;
static final Object room = new Object();

public static void main(String[] args) throws InterruptedException {
    
     Thread t1 = new Thread(() -> {
         for (int i = 0; i < 5000; i++) {
             synchronized (room) {
             	counter++;
         	 }
     	 }
     }, "t1");
    
     Thread t2 = new Thread(() -> {
         for (int i = 0; i < 5000; i++) {
             synchronized (room) {
             	counter--;
             }
         }
     }, "t2");
    
     t1.start();
     t2.start();
     t1.join();
     t2.join();
     log.debug("{}",counter);
}
```

synchronized 实际是用**对象锁**保证了**临界区内代码的原子性**，临界区内的代码对外是不可分割的，不会被线程切换所打断。

* 如果把 synchronized(obj) 放在 for 循环的外面，如何理解？
  * -- 原子性 ：那么5000次for循环被视为不可分割的原子操作集
* 如果 t1 synchronized(obj1) 而 t2 synchronized(obj2) 会怎样运作？
  * -- 锁对象的唯一性
  * 锁对象需要被多个线程共享，且仅此一份



**面向对象改进**

```java
class Room {
    //共享变量
    private int counter = 0;
    
    public synchronized void increment() {
        counter++;
    }

    public synchronized void decrement() {
        counter--;
    }
    
	//注意：get方法也要加锁
    public synchronized int getCounter() {
        return counter;
    }
}

public class Test {
    public static void main(String[] args) throws InterruptedException {
        //这里room实例就一个，synchronized加在实例方法上，锁的就是实例对象，这里锁有效；如果是两个实例被两个线程分别使用，则锁失效
        Room room = new Room();
        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 5000; i++) {
                room.increment();
            }
        }, "t1");

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 5000; i++) {
                room.decrement();
            }
        }, "t2");

        t1.start();
        t2.start();
        t1.join();
        t2.join();
        log.debug("{}", room.getCounter());
    }
}
```



## 方法上的 synchronized

* **实例方法**

```java
class Test{
	public synchronized void test() {}
}

等价于

class Test{
	public void test() {
		synchronized(this) {}
    }
}
```

注意：

1. 同步实例方法是在实例上进行锁定，而不是在整个类上进行锁定，因此不同的实例可以并发执行同步实例方法，即锁失效，无互斥效果

2. 在使用同步实例方法时，同一对象上的其它同步方法会被阻塞，但非同步方法不会。

3. 同步实例方法中锁定的是当前对象，如果有多个对象则不会阻塞对其它对象的访问。

   

* **静态方法**

```java
class Test{
	public synchronized static void test() {}
}

等价于
    
class Test{
	public static void test() {
 		synchronized(Test.class) {}
	}
}
```



注意：

1. 凡是在静态方法上添加synchronized，线程执行时会找类锁，记住：一个类不管创建了多少个对象，类只有一个，类锁也只有一把锁，通常静态方法上添加synchronized是为了保护静态变量的安全。
2. 如果一个是同步实例方法，一个是同步静态方法，不论是同个实例对象去执行两个方法还是两个不同实例对象分别去执行两个方法，两个线程都不会互斥，因为实例方法锁的是实例对象，静态方法锁的是类对象，两个对象不一样
3. 如果两个都是同步静态方法，两个同类的不同实例对象分别去执行两个方法，两个线程是互斥的，因为类对象就一个，不论是不是相同实例，只要是同一个类，都是共用一个类对象，即一把锁





## **变量的线程安全分析** 

**实例变量**和**静态变量**是否线程安全？ 

* 如果它们没有共享，则线程安全 

* 如果它们被共享了，根据它们的状态是否能够改变，又分两种情况 
  * 如果只有**读**操作，则线程安全 
  * 如果有**读写**操作，则这段代码是临界区，需要考虑线程安全 

**临界区：对共享变量有读写操作的代码段**



**局部变量**是否线程安全？ 

* 局部变量是线程安全的 
* 但局部变量**引用的对象**则未必 
  * 如果该对象没有逃离方法的作用访问，它是线程安全的 
  * 如果该对象逃离方法的作用范围，需要考虑线程安全



## 常见线程安全类

* String 
* Integer
*  StringBuﬀer
*  Random 
* Vector
*  Hashtable 
* java.util.concurrent 包下的类 

这里说它们是线程安全的是指，多个线程调用它们**同一个实例**的某个方法时，是线程安全的。也可以理解为

* 它们的每个方法是原子的 

* 但注意它们多个方法的组合不是原子的





## ReentrantLock

相对于 synchronized 它具备如下特点 ：

* 可中断 (指其他线程破坏当前线程的blocking状态，即在阻塞队列等锁的状态)
* 可以设置超时时间 
* 可以设置为公平锁 
* 支持多个条件变量

与 synchronized 一样，都支持可重入



基本语法：

```java
//获取锁
ReentrantLock lock = new ReentrantLock();
//该处的lock就相当于是synchronized中的monitor，即lock就是锁本身
lock.lock();//该行代码放在try外面和里面作用一样，无区别
try{
    //临界区
}finally{
    //释放锁
    lock.unlock();
}
```



### 可重入

可重入是指**同一个线程**如果首次获得了这把锁，那么因为它是这把锁的拥有者，因此有权利再次获取这把锁 

如果是不可重入锁，那么第二次获得锁时，自己也会被锁挡住

```java
static ReentrantLock lock = new ReentrantLock();

public static void main(String[] args) {
 	method1();
}

public static void method1() {
     lock.lock();
     try {  
         log.debug("execute method1");
         method2();
     } finally {
     	 lock.unlock();
     }
}

public static void method2() {
 	lock.lock();
 	try {
 		log.debug("execute method2");
		method3();
 	} finally {
		lock.unlock();
	}
}

public static void method3() {
 	lock.lock();
 	try {
 		log.debug("execute method3");
 	} finally {
 		lock.unlock();
 	}
}
```

输出：

```java
execute method1
execute method2
execute method3 
```



### 可打断（lockInterruptibly()实现）

注意如果是不可中断模式（lock.lock())，那么即使使用了 interrupt 也不会让等待中断

```java
ReentrantLock lock = new ReentrantLock();

Thread t1 = new Thread(() -> {
	log.debug("启动...");
 	try {
        //如果没有竞争那么此方法就会获取lock对象锁
        //如果有竞争就进入阻塞队列，可以被其他线程用interruput方法打断
 		lock.lockInterruptibly();
 	} catch (InterruptedException e) {
 		e.printStackTrace();
 		log.debug("等锁的过程中被打断");
 		return;
 	}
 	try {
 		log.debug("获得了锁");
 	} finally {
 		lock.unlock();
 	}
}, "t1");

lock.lock();//主线程在t1.start()前先上锁了
log.debug("获得了锁");
t1.start();

try {
 sleep(1);
 t1.interrupt();//在主线程去打断t1的blocking状态
 log.debug("执行打断");
} finally {
 	lock.unlock();
}
```

```
18:02:40.520 [main] 获得了锁
18:02:40.524 [t1] 启动...
18:02:41.530 [main] 执行打断
18:02:41.532 [t1] 等锁的过程中被打断
```



### 锁超时(tryLock()实现)

```java
public class Test {
    private static ReentrantLock lock = new ReentrantLock();
    public static void main(String[] args) {
        Thread t1 = new Thread(() -> {
            log.debug("尝试获得锁");
            try {
                //lock.tryLock()无参表示获取不到锁立即返回false
                if (! lock.tryLock(2, TimeUnit.SECONDS)) {
                    log.debug("获取不到锁");
                    return;
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
                log.debug("获取不到锁");
                return;
            }
            try {
                log.debug("获得到锁");
            } finally {
                lock.unlock();
            }
        }, "t1");

        lock.lock();
        log.debug("获得到锁");
        t1.start();
        sleep(1);
        log.debug("释放了锁");
        lock.unlock();
    }
}
```

```
18:19:40.537 [main] c.TestTimeout - 获得了锁
18:19:40.544 [t1] c.TestTimeout - 启动...
18:19:41.547 [t1] c.TestTimeout - 获取等待 1s 后失败，返回
```

### 公平锁

ReentrantLock 默认是不公平的

```java
ReentrantLock lock = new ReentrantLock(ture);//传入true即可设置成公平锁
```

公平锁可以解决解饿问题，但一般没有必要（tryLock即可解决），会降低并发度，后面分析原理时会讲解

### 条件变量

synchronized 中也有条件变量，当条件不满足时进入 waitSet 等待 

ReentrantLock 的条件变量比 synchronized 强大之处在于，它是支持多个条件变量的，这就好比

* synchronized 是那些不满足条件的线程都在一间休息室等消息 
* 而 ReentrantLock 支持多间休息室，有专门等烟的休息室、专门等早餐的休息室、唤醒时也是按休息室来唤醒



使用要点： 

* await 前需要获得锁 
* await 执行后，会释放锁，进入 conditionObject 等待 
* await 的线程被唤醒（或打断、或超时）取重新竞争 lock 锁 
* 竞争 lock 锁成功后，从 await 后继续执行

```java
//此代码非正式代码，仅供讲解
public class Test {
    static ReentrantLock lock = new ReentrantLock();

    public static void main(String[] args) {
        Condition condition1 = lock.newCondition(); //创建"休息室"(条件变量),可创建多个
        Condition condition2 = lock.newCondition();
        lock.lock();   // await 前需要获得锁 
        condition1.await(); //进入condition1休息等待
        
        //其他线程调用
        condition1.signal(); //唤醒condition1中的一个线程
        condition1.signalAll();
    }
}
```



### *交替打印

Q：用三个线程分别交替打印打印abc，循环5次

A：

* synchronized + wait + notify 实现

```java
public class Main {
    static boolean mark1 = true;
    static boolean mark2 = false;
    static boolean mark3 = false;
    static  Object lock = new Object();

    public static void main(String[] args) {
        Thread t1 = new Thread(()->{
            synchronized (lock){
                for (int i = 0; i < 5; i++) {
                    while(!mark1){
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            throw new RuntimeException(e);
                        }
                    }
                    System.out.print("a");
                    mark1 = false;
                    mark2 = true;
                    mark3 = false;
                    lock.notifyAll();
                }
            }

        });
        Thread t2 = new Thread(()->{
            synchronized (lock){
                for (int i = 0; i < 5; i++) {
                    while(!mark2){
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            throw new RuntimeException(e);
                        }
                    }
                    System.out.print("b");
                    mark2 = false;
                    mark3 = true;
                    mark1 = false;
                    lock.notifyAll();
                }
            }

        });
        Thread t3 = new Thread(()->{
            synchronized (lock){
                for (int i = 0; i < 5; i++) {
                    while(!mark3){
                        try {
                            lock.wait();
                        } catch (InterruptedException e) {
                            throw new RuntimeException(e);
                        }
                    }
                    System.out.print("c");
                    mark3 = false;
                    mark1 = true;
                    mark2 = false;
                    lock.notifyAll();
                }
            }

        });
        
        t1.start();
        t2.start();
        t3.start();
    }

}
```



* ReentrantLock + await + signal 实现

  * 单condition

    ```java
    public class Main {
        static boolean mark1 = true;
        static boolean mark2 = false;
        static boolean mark3 = false;
        static ReentrantLock lock = new ReentrantLock();
    
        public static void main(String[] args) {
    
            Condition condition = lock.newCondition();
    
            new Thread(()->{
                lock.lock();
                try {
                    for (int i = 0; i < 5; i++) {
                        while (!mark1){
                            condition.await();
                        }
                        System.out.print("a");
                        mark1 = false;
                        mark2 = true;
                        mark3 = false;
                        condition.signalAll();
                    }
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                } finally {
                    lock.unlock();
                }
            },"t1").start();
    
            new Thread(()->{
                lock.lock();
                try {
                    for (int i = 0; i < 5; i++) {
                        while (!mark2){
                            condition.await();
                        }
                        System.out.print("b");
                        mark1 = false;
                        mark2 = false;
                        mark3 = true;
                        condition.signalAll();
                    }
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                } finally {
                    lock.unlock();
                }
            },"t2").start();
    
            new Thread(()->{
                lock.lock();
                try {
                    for (int i = 0; i < 5; i++) {
                        while (!mark3){
                            condition.await();
                        }
                        System.out.print("c");
                        mark1 = true;
                        mark2 = false;
                        mark3 = false;
                        condition.signalAll();
                    }
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                } finally {
                    lock.unlock();
                }
            },"t3").start();
        }
    }
    ```

    

  * 多个condition + 面向对象

    ```java
    public class Main {
        public static void main(String[] args) throws InterruptedException {
            myReentrantLock lock = new myReentrantLock(5);
            Condition a = lock.newCondition();
            Condition b = lock.newCondition();
            Condition c = lock.newCondition();
            new Thread(() -> {
                lock.print("a", a, b);
            }, "t1").start();
            new Thread(() -> {
                lock.print("b", b, c);
            }, "t2").start();
            new Thread(() -> {
                lock.print("c", c, a);
            }, "t3").start();
    
            /**
             * 这里让主线程睡眠一会是保证三个线程都启动后分别进入到了各自的“休息室”，
             * 然后都各自释放了锁（await释放的），确保主线程能获得到锁
             * 假使让主线程与三个线程同时竞争锁，一旦主线程没竞争到锁，
             * 则无法执行a.signal(),导致所有线程均在各自“休息室”死等，造成死锁
             */
            Thread.sleep(1000);
            lock.lock();
            try {
                a.signal();
            } finally {
                lock.unlock();
            }
        }
    }
    class myReentrantLock extends ReentrantLock {
        private int loopNumber;
    
        public myReentrantLock(int loopNumber) {
            this.loopNumber = loopNumber;
        }
        public void print(String str, Condition current, Condition next) {
            for (int i = 0; i < loopNumber; i++) {
                lock();
                try {
                    current.await();
                    System.out.println(Thread.currentThread().getName() + ": " + str);
                    next.signal();
                } catch (InterruptedException e) {
                    throw new RuntimeException(e);
                } finally {
                    unlock();
                }
            }
        }
    }
    ```
    
    
    
    


# 共享模型之内存

## JMM

JMM 即 Java Memory Model，它定义了主存、工作内存抽象概念，底层对应着 CPU 寄存器、缓存、硬件内存、CPU 指令优化等。

JMM 体现在以下几个方面：

* 原子性 - 保证指令不会受到线程上下文切换的影响

* 可见性 - 保证指令不会受 cpu 缓存的影响 （volatile, synchronized)

* 有序性 - 保证指令不会受 cpu 指令并行优化的影响



## volatile（易变关键字）

volatile 可以保证共享变量的**可见性**和**有序性**

它可以用来修饰成员变量和静态成员变量，他可以避免线程从自己的工作缓存中查找变量的值，必须到主存中获取它的值，线程操作 volatile 变量都是直接操作主存

volatile 体现的实际就是可见性，它保证的是在多个线程之间，一个线程对 volatile 变量的修改对另一个（其他）线程可见， 不能保证原子性，**仅用在一个写线程，多个读线程的情况**



# 共享模型之工具

## 线程池

## JUC

### AQS

全称是 AbstractQueuedSynchronizer，是**阻塞式锁**和**相关的同步器工具**的框架，是一个抽象类

特点： 

* 用 state 属性来表示资源的状态（分独占模式和共享模式），子类需要定义如何维护这个状态，控制如何获取锁和释放锁 
  * getState - 获取 state 状态 
  * setState - 设置 state 状态 
  * compareAndSetState - cas 机制设置 state 状态 
  * 独占模式是只有一个线程能够访问资源，而共享模式可以允许多个线程访问资源 
* 提供了基于 FIFO 的等待队列，类似于 Monitor 的 EntryList 
* 条件变量来实现等待、唤醒机制，支持多个条件变量，其中单个条件变量类似于 Monitor 的 WaitSet



子类主要实现这样一些方法（默认抛出 UnsupportedOperationException） 

* tryAcquire 
* tryRelease 
* tryAcquireShared 
* tryReleaseShared 
* isHeldExclusively





### CopyOnWriteArrayList

CopyOnWriteArraySet 是它的马甲 

底层实现采用了 **写入时拷贝** 的思想，**增删改**操作会将底层数组拷贝一份，更改操作在新数组上执行，这时不影响其它线程的并发读，读写分离（支持**读-读**并发、**读-写**并发，但**不**支持 写-写并发）。 以新增为例：

```java
public boolean add(E e) {
	synchronized (lock) {
         // 获取旧的数组
         Object[] elements = getArray();//getArray()：return array；
         int len = elements.length;
         // 拷贝新的数组（这里是比较耗时的操作，但不影响其它读线程）
         Object[] newElements = Arrays.copyOf(elements, len + 1);
         // 添加新元素
         newElements[len] = e;
         // 替换旧的数组
         setArray(newElements);//setArray(newElements)： array = newElements;
         return true;
	}
}
```

其它读操作并未加锁，适合『读多写少』的应用场景

但是在get和遍历时会有弱一致性问题

但不要觉得弱一致性就不好 

* 数据库的 MVCC 都是弱一致性的表现 
* **并发高和一致性是矛盾的**，需要权衡
