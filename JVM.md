# 类的生命周期

**1.加载(Loading)**

类加载器根据类的全限定名通过不同的渠道以二进制流的方式将字节码信息加载到内存中，存放在方法区和堆上

* 不同渠道包括：本地文件（磁盘上的字节码文件）、程序运行时使用动态代理生成、通过网络传输的类
* 类加载器在加载完类之后，Java虚拟机会将字节码中的信息保存到内存的方法区中；生成一个InstanceKlass对象，保存类的所有信息，里边还包含实现特定功能比如多态的信息
* 同时，Java虚拟机还会在堆中生成一份与方法区中数据类似的java.lang.Class对象；作用是在Java代码中去获取类的信息以及存储静态字段的数据（JDK8及之后）

**2.连接(Linking)**

* **2.1 验证**：是检测Java字节码文件是否遵守了《Java虚拟机规范》中的约束，这个阶段一般不需要程序员参与
* **2.2 准备**：为静态变量分配内存并设置初始值
  * byte 0、short 0、int 0、long 0L、double 0.0、boolean false 、char '\u0000'、引用数据类型 null
  * final修饰的基本数据类型的静态变量，准备阶段直接会将代码中的值进行赋值

* **2.3 解析**：将常量池中的符号引用替换为指向内存的直接引用
  * 符号引用就是在字节码文件中使用编号来访问常量池中的内容
  * 直接引用不再使用编号，而是使用内存中地址进行访问具体的数据

**3.初始化(Initialization)**

执行**静态代码块中**的代码，并为**静态变量**赋值。执行流程与代码流程一致。

执行字节码文件中clinit部分的字节码指令

* 以下几种方式会导致类的加载并初始化
  * 访问一个类的静态变量或者静态方法，注意变量是final修饰的并且等号右边是常量不会触发初始化
  * 调用Class.forName(String className)
  * new一个该类的对象时
  * 执行Main方法的当前类

*  clinit指令在特定情况下不会出现，比如：如下几种情况是不会进行初始化指令执行（即不存在初始化阶段）：
  * 无静态代码块且无静态变量赋值语句
  * .有静态变量的声明，但是没有赋值语句
  * 静态变量的定义使用final关键字，这类变量会在准备阶段直接进行初始化

* 存在继承关系的情况：
  * 直接访问父类的静态变量，不会触发子类的初始化
  * 子类的初始化clinit调用之前，会先调用父类的clinit初始化方法

* 其他情况
  * 数组的创建不会导致数组中元素的类进行初始化
  * final修饰的变量如果赋值的内容需要执行指令才能得出结果，会执行clinit方法进行初始化

**4.使用(Using)**

**5.卸载(Unloading)**

# 类加载器

## 什么是类加载器

类加载器（ClassLoader）是jvm提供给应用程序去实现获取类和接口字节码数据的技术

![b66ce533a4bb7fa7b937ad0b08b4d97](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231646670.png)

## 类加载器的分类

 ![4673b82cceb53f43599bb098f6cc0da](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231646229.png)

所有Java中实现的类加载器都需要继承 ClassLoader这个抽象类，具体继承结构：

![bfcf5a38bb5af5f25008a19e135ddd5](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231646901.png)

## 双亲委派机制

在类加载的过程中，每个类加载器都会先检查是否已经加载了该类，如果已经加载则直接返回，否则会将加载请求委派给父类加载器；如果所有的父类加载器都无法加载该类，则由当前类加载器自己尝试加载；当父类加载器反馈自己无法完成这个加载请求（它的搜索范围没有找到所需的类）时，会自顶向下委派子类加载器加载。

![ec3374ca3c63f289e93e49778973986](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231646896.png)

* 每个Java实现的类加载器中保存了一个成员变量叫“父”（Parent）类加载器，可以理解为它的上级， 并不是继承关系

  ```java
  private final ClassLoader parent;
  ```

* 应用程序类加载器的parent父类加载器是扩展类加载器，而扩展类加载器的parent是空
*  启动类加载器使用C++编写，没有上级类加载器



## **双亲委派机制的作用**

1. 保证类加载的安全性

   通过双亲委派机制让顶层的类加载器去加载核心类，避免恶意代码替换JDK中的核心类库，比如自定义String类，启动类加载器在加载过程中会先加载jdk自带的文件（rt.jar中java.lang.String.class），报错说没main方法，这样确保核心类库的完整性和安全性。

2. 避免重复加载

   双亲委派机制可以避免同一个类被 多次加载，上层的类加载器如果加载过类，就会直接返回该类，避免重复加载。



## 打破双亲委派机制

### **1.自定义类加载器并且重写 loadClass方法**

ClassLoader中包含了4个核心方法，双亲委派机制的核心代码就位于**loadClass**方法中

![4114dd4db8c1feafd4ddbcd529028b5](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231645575.png)

故重写loadClass方法，去除双亲委派机制核心代码，自然就打破了双亲委派机制；

正确的去实现一个自定义类加载器的方式是重写findClass方法，这样不会破坏双亲委派机制

注意：

* 自定义类加载器父类是AppClassLoader
  * ClassLoader类中提供了构造方法设置parent的内容；这个构造方法由另外一个构造方法调用，其中父类加载器由getSystemClassLoader方法设置，该方法返回的 是AppClassLoader

* 两个自定义类加载器加载相同限定名的类，会不会冲突？
  * 不会冲突，在同一个Java虚拟机中，只有**相同类加载器+相同的类限定名**才 会被认为是同一个类

### **2.线程上下文类加载器**

JDBC中使用了DriverManager来管理项目中引入的不同数据库的驱动，比如mysql驱动、oracle驱动； DriverManager类位于rt.jar包中，由启动类加载器加载；在初始化DriverManager时，通过SPI机制加载jar包中的myql驱动，SPI中利用了线程上下文类加载器（应用程序类加载器）去加载类并创建对象，这种由启动类加载器加载的类，委派应用程序类加载器去加载类的方式，打破了双亲委派机制

**SPI：**![f6acc4cc6095952d41706df6ffd2cb1](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231643659.png)

![a3cce3703b1a336b85585b9748317b2](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202408231643240.png)

注意：另一种看法，JDBC只是在DriverManager加载完之后，通过初始化阶段触发了驱动类的加载，类的加载依然遵循双亲委派机制，并没有打破。真正意义上的打破双亲委派只有重写掉loadclass方法中关于双亲委派的代码

### **3.OSGi模块化**

OSGi模块化框架，它存在同级之间的类加载器的委托加载