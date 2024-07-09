# Java 概述

## 1.Java 运行机制

![e15b7502c68b7f1d8a6fb514bea52a2](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031625623.png)

```java

//public static void main(String[]arg)是固定的书写格式 表示一个主方法，即程序的入口
//java语言严格区分大小写
//一个源文件中最多只能有一个public类。其他类的个数不限。编译后，每一个类都对应一个.class文件
//如果源文件包含一个public类，则文件名必须按该类名命名！！！

public class Hello{

	public static void main(String[]arg){
		System.out.println("hello,world~");
	}

}
```

## 2.Java 转义字符

## 3.

# 变量

![b6c6f2fbd81fc26aa033531ff97e1a2](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031625268.png)

## 1.整数类型

## 2.浮点类型

## 3.字符类型

```java
//字符常量是用单引号（'')括起来的单个字符，不能用双引号（"")
char c1 = 'a'
char c2 = '\t'	//java允许使用转义字符'\'，使其输出的是制表符而不是'\t'
char c3 = '陈'
char c4 = 97	//字符类型可以直接存放一个数字，当输出c4时，会输出97表示的字符'a' -->ASCII编码表
```

## 4.布尔类型

## 5.基本数据类型转换





# 运算符

## 1.算术运算符

# 程序控制结构

## 1.顺序控制

* 程序从上到下逐行地执行，中间没有任何判断和跳转

## 2.分支控制（if-else)

* 让程序有选择地执行

### 2.1 单分支

```java
if(条件表达式){
    
    执行代码块;
    
}
```

* 如果 {  } 中只有一条语句，可以不用 {  }

### 2.2 双分支 

```java
if(条件表达式){
    
    执行代码块1；
        
}
else{
    
    执行代码块2；
        
}
```



### 2.3 多分支

```java
if(条件表达式1){
    
    执行代码块1；
        
}
else if(条件表达式2){
    
    执行代码块2；
        
}

......
    
else{
    
    执行代码块n；
        
}
```

* 只能有一个执行入口
* 多分支可以没有else ，如果所有的条件表达式都不成立，则一个执行入口都没有

### 2.4 嵌套分支

### 2.5 switch分支

```java
switch(表达式){
        
    case 常量1:
        语句块1;
        break;
    case 常量2:
        语句块2;
        break;
    
  	    ...
        
    case 常量n:
        语句块n;
        break;
    default:
        default语句块;
        break;             
        
}
```

* 表达式返回一个值，这个值按顺序与常量匹配，匹配成功就执行相应语句，如果一个都没匹配上，则执行 default 语句块
* break 表示退出 switch

## 3.循环控制

### 3.1 for循环

```java
for(循环变量初始化;循环条件;循环变量迭代){
    
    循环操作语句;
        
}
```

* 循环条件是返回一个布尔值的表达式
* 括号内的初始化和变量迭代可以写到其他地方，但是两边的分号不能省略
* 可以有多条初始化语句，但要求类型一样，并且中间由逗号隔开；也可以有多条变量迭代语句，中间也用逗号隔开

### 3.2 while循环

```java
循环变量初始化;
while(循环条件){

    循环体;
    循环变量迭代;
    
}
```

* 先判断，再执行

### 3.2 do...while循环

```java
循环变量初始化;
do{
    
    循环体语句;
    循环变量迭代;
    
}while(循环条件);
```

* 先执行，再判断。至少执行一次

### 3.3 多重循环

### 3.4 跳转控制语句  break

```java
{
    ...
	break;
    ...
}
```

* break 语句用于终止某个语句块的执行，一般使用在 switch 或者循环[ for , while , do-while ]中

### 3.5 跳转控制语句 continue

```java
{
    ...
	continue;
    ...
}
```

* continue 语句用于结束本次循环，继续执行下一次循环

### 3.6 跳转控制语句 return

# 数组

* 数组概述

  * 在Java中，数组是一种用于存储多个相同数据类型元素的容器

  * 数组是一种引用数据类型，隐式继承Object。因此数组也可以调用Object类中的方法

  * 数组对象存储在堆内存中

    ![image-20240709170546009](C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20240709170546009.png)

* 数组分类

  * 根据维数进行分类：一维数组，二维数组，三维数组，多维数组
  * 根据数组中存储的元素类型分类：基本类型数组，引用类型数组
  * 根据数组初始化方式不同分类：静态数组，动态数组

* 数组存储元素的特点

  * 数组长度一旦确定不可变
  * 数组中元素数据类型一致，每个元素占用空间大小相同
  * 数组中每个元素在空间存储上，内存地址是连续的
  * 每个元素有索引，首元素索引0，以1递增
  * 以首元素的内存地址作为数组对象在堆内存中的地址
  * 所有数组对象都有length属性用来获取数组元素个数。末尾元素下标：length-1

  

* 数组优点

  根据下标查询某个元素的效率极高。数组中有100个元素和有100万个元素，查询效率相同。时间复杂度O(1)。也就是说在数组中根据下标查询某个元素时，不管数组的长短，耗费时间是固定不变的，

  原因：知道首元素内存地址，元素在空间存储上内存地址又是连续的，每个元素占用空间大小相同，只要知道下标，就可以通过数学表达式计算出来要查找元素的内存地址。直接通过内存地址定位元素

* 数组缺点
  * 随机增删元素的效率较低。因为随机增删元素时，为了保证数组中元素的内存地址连续，就需要涉及到后续元素的位移问题。时间复杂度O(n)。O(n)表示的是线性阶，随着问题规模n的不断增大，时间复杂度不断增大，算法的执行效率越低。（不过需要注意的是：**对数组末尾元素的增删效率是不受影响的**。）
  * 无法存储大量数据，因为很难在内存上找到非常大的一块连续的内存

## 一维数组

* 一维数组是线性结构。二维数组，三维数组，多维数组是非线性结构
* 静态初始化
  * 第一种方式：`int[] arr = new int[]{1, 2, 3};`
  * 第二种方式：`int[] arr = {1,2,3};`

* 动态初始化

  * 使用场景：当创建数组时，不知道数组中具体存储哪些元素，可以使用动态初始化

  * 语法格式：`int[] arr = new int[3];`

  * 动态初始化一维数组之后，数组长度确定，数组中存储的每个元素将采用默认值

  * 数组的默认初始化值

    ```xml
    数据类型            默认值
    ===============================
    byte                0
    short               0
    int                 0
    long                0L
    float               0.0F
    double              0.0
    boolean             false
    char                '\u0000'
    引用数据类型          null
    ```

* 遍历数组

  * 普通for循环遍历

  * 增强for循环（for-each）

    ```java
    int[] arr = {1, 2, 3};
    for(int num : arr){
        // num代表数组中的每个元素
        System.out.println(num);
    }
    ```

    for-each的优点：代码简洁，可读性强

    for-each的缺点：没有下标，某些业务可能需要下标

* 方法在调用时如何给方法传一个数组对象？

  ```java
  public class ArrayTest {
      public static void main(String[] args) {
          // 第一种方式（静态初始化）：创建好数组对象，然后传进去
          int[] nums = {1,2,3,4};
          display(nums);
  
          // 第二种方式（静态初始化）：直接传
          //display({1,2,3,4}); // 这是错误的。
          display(new int[]{1,2,3,4}); // 这是正确的。注意这个小细节。
  
          // 动态初始化方式。
          display(new int[3]);//输出0,0,0
      }
  
      public static void display(int[] arr) {
          for(int num : arr) {
              System.out.println(num);
          }
      }
  }
  ```

* 当一维数组中存储引用时的内存图

  ![image-20240709194537652](C:/Users/HP/AppData/Roaming/Typora/typora-user-images/image-20240709194537652.png)



# 面向对象编程（基础）

## 面向对象概述

* 面向过程：**关注点在实现功能的步骤上**；面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候一个一个依次调用就可以了；对于简单的流程是适合使用面向过程的方式
* 面向对象：**关注点在实现功能需要哪些对象的参与**；面向对象就是分析出解决这个问题都需要哪些对象的参加，然后让对象与对象之间协作起来形成一个系统；面向对象开发方式耦合度低，扩展能力强，采用面向对象的思想更加容易处理复杂的问题



## 1 类与对象

* 类：
  * 现实世界中，事物与事物之间具有共同特征，将这些共同的状态和行为提取出来，形成了一个模板，称为类
  * 类实际上是人类大脑思考总结的一个模板，类是一个抽象的概念
  * 状态在程序中对应属性。属性通常用变量来表示
  * 行为在程序中对应方法。用方法来描述行为动作
  * 类 = 属性 + 方法
* 对象：
  * 实际存在的个体
  * 对象又称为实例，通过类这个模板可以实例化n个对象。（通过类可以创造多个对象）
  * 创建一个对象 == 实例化一个对象 == 把类实例化

### 1.1 对象内存布局

![8c49c6140057575b569631b0391656d](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031628906.png)

![c6b4d29d52179a2e2bc122e40c37a94](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031628928.png)

![c0e70492adfb213d4242cb4728c03ed](javanote01.assets/c0e70492adfb213d4242cb4728c03ed.png)

![ac20158121ba6876820630e9c339940](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031628264.png)

多个对象在堆内存中，都有不同的内存划分，成员变量存储在各自的内存区域中，成员方法多个对象共用的一份

### 1.2 属性概念

* 叫法上 ：属性 == 成员变量 == feild(字段) ，成员变量是用来表示属性的。
* 属性是类的一个组成部分，一般是基本数据类型，也可以是引用类型。
* 属性的定义语法同变量 ，示例： 访问修饰符 属性类型  属性名；
* 属性如果不赋值，有默认值，规则和数组一致。

### 1.3成员变量和局部变量

 **成员变量和局部变量的区别：**

* 类中位置不同：成员变量（类中方法外）局部变量（方法内部或方法声明上）
* 内存中位置不同：成员变量（堆内存）局部变量（栈内存）
* 生命周期不同：成员变量（随着对象的存在而存在，随着对象的消失而消失）局部变量（随着方法的调用而存在，醉着方法的调用完毕而消失）
* 初始化值不同：成员变量（有默认初始化值）局部变量（没有默认初始化值，必须先定义，赋值才能使用）

### 1.4 类和对象的内存分配机制

![adda3e7f97927b3ae60dcef5044c2a8](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629096.png)

* 栈：一般存放基本数据类型（局部变量）
* 堆：存放对象（Cat cat ，数组等）
* 方法区：常量池（常量，比如字符串），类加载信息（每个类只会加载一次）

## 2 成员方法

#### 2.1 方法快速入门

```java
public class method {
    public static void main(String[] args) {
        Tools t1 = new Tools();			            //控制台输出：
        t1.speak();                                 //你好                                           
        t1.cal01(10);	 						    //calo1计算结果 = 55
        int result = t1.getSum(10, 20);    
        System.out.println("result = "+ result);    //result = 30
    }
}
class Tools {

    public void speak(){
        System.out.println("你好");
    }
    public void cal01 (int n){
        int res = 0;
        for (int i = 1; i <= n ; i++) {
            res += i;
        }
        System.out.println("cal01计算结果 = " + res);
    }
    public int getSum(int num1, int num2){
        int res = num1 + num2;
        return res;
    }

}
```

#### 2.2 方法调用机制

![96db0d047d696589fa33f6db510a47e](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629072.png)

* 当程序执行到方法时，就会开辟一个独立的空间（栈空间）
* 当方法执行完毕，或者执行到return语句时，就会返回到调用的地方，同时开辟的栈空间释放
* 返回后继续执行后面的代码
* 当main方法（栈）执行完毕，整个程序退出，同时main栈空间也释放

#### 2.3 成员方法的定义

```java
访问修饰符  返回数据类型  方法名（形参列表）{
    语句;
    return 返回值;
}
```

* 形参列表：表示成员方法的输入
* 返回数据类型：表示成员方法的输出，void 表示没有返回值
* return 语句不是必须的

#### 2.4 方法使用细节

* 一个方法**最多有一个**返回值（返回多个结果可以采用数组）

  ```
  
  ```

  

* 返回数据类型可以是任意类型，包含基本类型或引用类型（数组，对象）

* 如果方法要求有返回数据类型，则方法中最后执行语句必须为**return  值** ，而且要求返回值类型必须和return 的值类型一致或兼容

* 如果方法是 void ，则方法体中**可以没有**return 语句，或者只写 return，**不能带值**否则报错形参列表：

* 一个方法可以有零个参数，也可以有多个参数，中间用逗号隔开

* 参数类型可以为任意类型，包含基本类型或引用类型

* 调用带参数的方法时，一定对应着参数列表传入相同或兼容类型的参数

* 方法不能嵌套定义！

* 同一个类中的方法调用：直接调用

* 跨类中的方法调用：需要通过对象名调用

#### 2.5 方法传参机制

基本数据类型，传递的是值（值拷贝），形参的任何改变不影响实参

引用类型传递的是地址（传递的也是值，但是值是地址），可以通过形参影响实参

#### 2.6 方法递归调用

#### 2.7 方法的重载

* 方法重载概念

  方法重载指同一个类中定义的多个方法之间的关系，满足下列条件的多个方法相互构成重载

  * 多个方法在同一个类中
  * 多个方法具有相同的方法名
  * 多个方法的参数不相同，类型不同或者数量不同

* 注意：

  * 重载仅对应方法的定义，与方法的调用无关，调用方式参照标准格式
  * 重载仅针对同一个类中方法的名称与参数进行识别，与返回值无关，换句话说不能通过返回值来判定两个方法是否相互构成重载

#### 2.8 可变参数

Java允许将同一个类中多个同名同功能但参数个数不同的方法封装成一个方法，由可变参数实现

## 3 变量作用域

## 4 构造器

* 基本介绍

​        构造器又叫构造方法，是类的一种特殊方法，主要作用是完成对新对象的初始化。

* 基本语法

  ```
  [访问修饰符] 方法名（形参列表）{}
  ```
  
* 基本案例

  ```java
  public class Constructor {
      public static void main(String[] args) {
          Person p1 = new Person("xiaoming",10);
          System.out.println(p1.age); 
          System.out.println(p1.name);
      }
  }
  class Person {
      String name;
      int age;
      public Person(String pname, int page){
          System.out.println("构造器被调用");
          name = pname;
          age = page;
      }
  }
  ```
  
  ```Java
  构造器被调用
  10
  xiaoming
  ```
  
* 构造器的作用

  * 构造方法的执行分为两个阶段：对象的创建和对象的初始化。这两个阶段不能颠倒，也不可分割
  * 在Java中，当我们使用关键字new时，就会在堆内存中开辟空间，然后给属性赋默认值，完成对象的创建（这个过程是在构造方法体执行前就完成了），这时虽然对象已经被创建出来了，但还没有被初始化。而初始化则是在执行构造方法体时进行的。构造方法体执行结束，表示对象初始化完毕
  
* 使用细节

  ①一个类可以定义多个不同的构造器，即构造器重载

  ②构造器名（方法名）和类名必须相同

  ③构造器不需要提供返回值，也不能写void，如果提供了返回值就是不构造方法了，而是普通方法

  ④构造方法执行结束后，会自动将创建的对象的内存地址返回，但方法体中不需要提供"return  值"这样的语句

  ⑤在创建对象时，系统会自动的调用该类的构造器完成对象的初始化
  
  ⑥如果一个类没有显示的定义任何构造方法，系统会默认提供一个无参数构造方法，也被称为缺省构造器。一旦显示      	的定义了构造方法，则缺省构造器将不存在
  
  

## 5 this

* this出现在实例方法中，代表当前对象的引用（地址值），即代表当前对象
* `this.`大部分情况下可以省略
* this可以区分局部变量和成员变量的重名问题
  * 方法的形参如果与成员变量同名，不带this修饰的变量指的是形参，而不是成员变量
  * 方法的形参没有与成员变量同名，不带this修饰的变量指的是成员变量
* this存储在**实例方法栈帧的局部变量表的0号槽位**上

![image-20240703112308614](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031123697.png)

* this不能出现在静态方法中
* `this(实参)`语法：
  * 只能出现在构造方法的第一行
  * 通过当前构造方法去调用本类中其他的构造方法
  * 作用是：代码复用

# 面向对象编程（中级）

## 1. IntelliJ IDEA

### 1.1 破解方法

### 1.2 常用快捷键

```java
Ctrl + Y  		//删除当前行
Ctrl + D 		//复制当前行
Alt + /  		//自动补全代码
Alt + Enter 	//导入该行需要的类
Alt + Ins		//生成构造器
Ctrl + H   		//查看类的层级关系
Ctrl + B		//定位方法
Ctrl + Alt + L  //格式化代码
.var 			//自动分配变量名
```

### 1.3 模板

<img src="https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629597.png" alt="fe7d7a882c47230beeb10f986f9d84b" style="zoom:150%;" />

## 2. 包



## 3. 访问修饰符

* private（私有的）无法访问：使用private关键字，就意味着被声明的成员或方法，除了本类，其他任何类都无法访问。

* public（公共的）接口访问权限：使用public关键字，就意味着被声明的成员或方法对所有类都是可以访问的。

* protected（受保护的）继承访问权限：使用protected关键字，就意味着被声明的成员或方法，在子类以及相同包内的其他类都是可以访问的。

* default（默认的）包访问权限：即不写任何关键字，就意味着只要包相同，包内所有类都可以访问，包外都不可以访问，无关子类与否。
  ![f2addb23c780eeea2c79c4cd24af044](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629456.png)

* 注意事项：
  * 类中的属性和方法访问权限共有四种：private、缺省默认、protected和public
  * 类的访问权限只有两种：public和 缺省
  * 访问修饰符不能修饰局部变量

## 4. 封装

* 面向对象三大特征之一：封装

* 什么是封装？

  封装是一种将数据和方法加以包装，使之成为一个独立的实体，并且把它与外部对象隔离开来的机制。具体来说，封装是将一个对象的所有“状态（属性）”以及“行为（方法）”统一封装到一个类中，从而隐藏了对象内部的具体实现细节，向外界提供了有限的访问接口，以实现对对象的保护和隔离。

* 封装的好处

  封装通过限制外部对对象内部的直接访问和修改，保证了数据的安全性，并提高了代码的可维护性和可复用性。

* 封装的实现步骤：
  * 将属性私有化
  * 提供一个公共的setter方法，用于对属性判断并赋值。可以放在构造器内
  * 提供一个公共的getter方法，用于获取属性的值

​	

## 5. 继承

* 面向对象三大特征之一：继承

* 继承的作用：
  * 基本作用：代码复用
  * 重要作用：有了继承，才有了方法覆盖和多态机制

* 语法：`[修饰符列表] class 类名 extends 父类名{}`
* 继承相关的术语：当B类继承A类时
  * A类称为：父类、超类、基类、superclass
  * B类称为：子类、派生类、subclass

* 细节
  * Java只支持单继承，一个类只能直接继承一个类
  * Java不支持多继承，但支持多重继承（多层继承）
  * 子类继承父类后，除私有的不支持继承、构造方法不支持继承。其它的全部会继承
  * 子类继承了所有的属性和方法，但是私有的属性和方法不能在子类直接访问，要通过父类提供公共的方法去访问
  * 一个类没有显示继承任何类时，默认继承java.lang.Object类
  * Object类是JDK类库的根类，Java中所有类都是Object类的子类
  * 子类必须调用父类的构造器，先完成父类的初始化
  * 当创建子类对象时，不管使用子类的哪个构造器，默认情况下总会去调用父类的无参构造器，如果父类无参构造器被覆盖，则必须在子类的构造器中用super去指定使用父类的哪个构造器完成对父类的初始化工作，否则编译不通过
  * `super()`必须放在子类构造器的第一行（`super()`只能在构造器中使用）
  * `super()`和`this()`都只能放在构造器的第一行，因此这两个方法不能在同一个构造器中共存
  * 父类构造器的调用不限于直接父类，将一直往上追溯直到Object类（顶级父类）

* 继承的本质分析：

![image-20240704115301317](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407041153690.png)

```java
public class ExtendsTheory {
    public static void main(String[] args) {
        Son son = new Son();

        //1.首先看子类是否有该属性
        //2.若子类有这个属性，并且可以访问，则返回信息
        //3.若子类没有这个属性，则查看父类有没有这个属性，若父类有该属性，并且可以访问，就返回信息；若父类也没有则继续向上查找直到 Object类，如果都没有，则报错
        //4.按以上规则查找到某层级有这个属性，但不能访问，则报错（即使更高级父类有公开的该属性）
        System.out.println(son.age);//40
        System.out.println(son.name);//报错

    }
}
class GrandaPa {
    String name = "爷爷";
    String hobby = "旅游";
}
class Father extends GrandaPa {
    String name = "爸爸";
    int age = 40;

}
class Son extends Father{
    private String name = "儿子";
}
```





## 6. super

super代表父类的引用，用于访问父类的属性，方法，构造器

**基本语法：**

1. 访问父类的属性，但不能访问父类的private属性

   super.属性名

2. 访问父类的方法，但不能访问父类的private方法

   super.方法名(参数列表）

3. 访问父类的构造器，只能放在子类的构造器的第一句，且只能出现一句

   super.(参数列表）

**super细节：**

当子类与父类中的成员（属性和方法）有重名时，为了访问父类的成员，必须通过super 。如果没有重名，则使用super、this和直接访问是一样的效果。

```java
public class SuperDetail {
    public static void main(String[] args) {
        B b = new B();
        b.sum();
    }
}
class A{
    public int n = 1;
    public void cal(){
        System.out.println("A的cal()被调用");
    }
}
class B extends A{
    public int n = 2;
    public void cal(){
        System.out.println("B的cal()被调用");
    }

    public void sum(){
        cal();
        this.cal();
        super.cal();

        System.out.println(n);
        System.out.println(this.n);
        System.out.println(super.n);
    }
}
```

```java
B的cal()被调用
B的cal()被调用
A的cal()被调用
2
2
1
```

找cal方法规则（cal() 和 this.cal() )：

1. 先找本类，如果有，则调用
2. 如果本类没有，则找父类，如果有，并且可以调用，则调用
3. 如果父类也没有，则继续向上查找，直到Object类
4. 如果查找过程中，找到了，但是私有的不能访问，则报错
5. 如果查找过程中，没有找到，则提示方法不存在，编译不通过
6. super.cal() 的查找规则是直接查找父类，没有再向上查找，即跳过本类，其他规则一样
7. 属性同理

**super和this的比较：**

![4600fb42005ba8ccba3374fcc20be79](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629428.png)

## 7. 方法重写/覆盖(override)

* 什么情况下考虑使用方法覆盖？

  当从父类中继承过来的方法无法满足当前子类的业务需求时

* 发生方法覆盖的条件：
  * 具有继承关系的父子类之间
  * 具有相同的方法名（必须严格一样）
  * 具有相同的形参列表（必须严格一样）
  * 具有相同的返回值类型（可以是父类方法返回值类型的子类）

* 方法覆盖细节：

  * 当子类将父类方法覆盖后，将来子类对象调用方法的时候，一定会执行重写之后的方法

  * @Override注解标注的方法会在编译阶段检查该方法是否重写了父类的方法
  * 如果返回值类型是引用数据类型，那么重写方法的返回值类型可以是原类型的子类型
  * 访问权限不能变低，可以变高（public > protected > 默认 > private)
  * 抛出异常不能变多，可以变少
  * 私有方法不能继承，所以不能覆盖
  * 构造方法不能继承，所以不能覆盖
  * 方法覆盖针对实例方法，和静态方法无关
  * 方法覆盖针对实例方法，和实例变量无关



**重载与重写的比较：**

![c0028360e36cf813918eb9a2b01a82a](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031629651.png)



## 8. 多态（polymorphic）

* **什么是向上转型和向下转型？**

  * java允许具有继承关系的父子类型之间的类型转换

  * 向上转型：子类型的对象可以赋值给一个父类型的引用

    ​					`父类类型（不仅限于直接父类）	引用名	=	new	子类类型（）；`

  * 向下转型：父类型的引用可以转换为子类型的引用。但是需要加强制类型转换符

    ​                    `子类类型	引用名	=	（子类类型）父类引用；`

  * 无论是向上转型还是向下转型，前提条件是：两种类型之间必须存在继承关系。这样编译器才能编译通过

* 什么是多态？

  * 父类型引用指向子类对象，Animal a = new Cat(); a.move();
  * 程序分为编译阶段和运行阶段：
    * 编译阶段：编译器只知道a是Animal类型，因此去Animal类中找move()方法，找到之后，绑定成功，编译通过。这个过程通常被称为静态绑定。
    * 运行阶段：运行时和JVM堆内存中的真实Java对象有关，所以运行时会自动调用真实对象的move()方法。这个过程通常被称为动态绑定。

  * 多态指的是：多种形态，编译阶段一种形态，运行阶段另一种形态，因此叫做多态,面向对象三大特征之一

* 注意事项：

  * 向上转型时，不能调用子类中特有成员

    ```java
    public class Fu {}
    
    public class Zi extends Fu {
        public String s = "子类特有属性";
        
        public void fun(){
            System.out.println("子类特有方法");
        }
    }
    ```

    ```java
    Fu f = new Zi();
    f.fun();//编译报错
    System.out.println(f.s);//编译报错
    ```

    ```xml
    原因：编译器只知道f是Fu类型，去Fu类中找fun()方法和s属性，结果没有找到，无法完成静态绑定，编译报错。
    ```

    如果就要a去调用fun( )方法，怎么办？

    ——向下转型

    什么时候我们会考虑使用向下转型？

    ——当需要调用的方法是子类中特有的方法时

    ```java
    Fu f = new Zi();
    Zi z = (Zi) f;
    z.fun();
    System.out.println(z.s);
    ```

    ```
    子类特有方法
    子类特有属性
    ```

  * ```JAVA
    public class Fu {}
    public class Zi extends Fu {}
    public class Nv extends Fu{}
    ```

    ```
    Fu f = new Zi();
    Nv n = (Nv) f;
    n.fun();//
    ```

    

  

  

  

  

  

**基本介绍：**

方法或对象具有多种形态。是面向对象的第三大特征，多态建立在封装和继承基础之上的。

**多态的具体体现：**

1. 方法的多态

   重写和重载就体现方法的多态

2. 对象的多态

   (1) 一个对象的编译类型和运行类型可以不一致

   (2) 编译类型在定义对象时就确定了不能改变

   (3) 运行类型是可以变化的

   (4) 编译类型看定义时 “=”的左边，运行类型看“=”的右边

   ```java
   Animal animal = new Dog(); //animal 编译类型是Animal，运行类型是 Dog
   animal = new Cat(); //animal 编译类型仍然是Animal，运行类型变成 Cat
   ```

**多态的运行特点**

调用成员变量时：编译看左边，运行看左边

调用成员方法时：编译看左边，运行看右边

代码示例：

```java
Fu f = new Zi()；
//编译看左边的父类中有没有name这个属性，没有就报错
//在实际运行的时候，把父类name属性的值打印出来
System.out.println(f.name);
//编译看左边的父类中有没有show这个方法，没有就报错
//在实际运行的时候，运行的是子类中的show方法
f.show();
```

**注意事项和细节：**

多态的前提是：两个对象（类）存在继承关系

多态的向上转型：

​		1）本质： 父类的引用指向了子类的对象

​		2）语法：`父类类型（不仅限于直接父类）	引用名	=	new	子类类型（）；`

​		3）特点： 编译类型看左边，运行类型看右边

​							可以调用父类中的所有成员（需遵守访问权限）；不能调用子类中特有成员；最终运行效果看子类的具体实现

多态的向下转型：

​		1）语法：`子类类型	引用名	=	（子类类型）父类引用；`

​		2）只能强转父类的引用，不能强转父类的对象

​		3）要求父类的引用必须原先指向的是当前目标类型的对象

​		4）向下转型后，可以调用子类类型中所有的成员		

属性没有重写之说！属性的值看编译类型

```java
public class PolyDetail {
    public static void main(String[] args) {
        A a = new B();
        System.out.println(a.n);
        B b = new B();
        System.out.println(b.n);
    }
}
class A {
    int n = 10;
}
class B extends A {
    int n = 20;
}
```

```java
10
20
```

instanceof 比较操作符，用于判断对象的运行类型是否为某某类型或某某类型的子类型

```java
变量名 instanceof 数据类型 
如果变量属于该数据类型或者其子类类型，返回true。
如果变量不属于该数据类型或者其子类类型，返回false。
```

**Java的动态绑定机制**

1.当调用对象方法时，该方法会和该对象的内存地址/运行类型绑定

2.当调用对象属性时，没有动态绑定机制，哪里声明哪里使用

```java
public class DynamicBinding {
    public static void main(String[] args) {
        A a = new B();
        System.out.println(a.sum());//40
        System.out.println(a.sum1());//30
    }
}
class A {
    public int i = 10;
    public int sum(){
        return  geti() + 10;
    }
    public int sum1(){
        return i + 10;
    }
    public int geti(){
        return i;
    }
}
class B extends A {
    public int i = 20;
    public int sum(){
        return i + 20;
    }
    public int sum1(){
        return i + 10;
    }
    public int geti(){
        return i;
    }
}
```

```java
public class DynamicBinding {
    public static void main(String[] args) {
        A a = new B();
        //a 的编译类型 A ，运行类型 B
        System.out.println(a.sum());//30
        System.out.println(a.sum1());//30
    }
}
class A {
    public int i = 10;
    public int sum(){
        return  geti() + 10;
    }
    public int sum1(){
        return i + 10;
    }
    public int geti(){
        return i;
    }
}
class B extends A {
    public int i = 20;

    public int sum1(){
        return i + 10;
    }
    public int geti(){
        return i;
    }
}
```

**多态的应用**：

1）多态数组

```java
public class PolyArr {
    public static void main(String[] args) {
        Person[] persons = new Person[5];
        persons[0] = new Person("jack", 20);
        persons[1] = new Student("jack", 20, 100);
        persons[2] = new Student("smith", 19, 80);
        persons[3] = new Teacher("travis", 30, 20000);
        persons[4] = new Teacher("scott", 40, 25000);

        for (int i = 0; i < persons.length; i++) {
            //persons[i]编译类型是 Person， 运行类型随实际情况而改变
            System.out.println(persons[i].say());
            if (persons[i] instanceof Student) {
                Student student = (Student) persons[i];
                student.study();
                //((Student) persons[i]).study();
            }else if (persons[i] instanceof Teacher){
                Teacher teacher = (Teacher) persons[i];
                teacher.teach();
                //((Teacher) persons[i]).teach();
            }else {
                System.out.println("error");
            }

        }
    }

}
class Person{
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String say(){
        return "姓名："+ name +"\t" + "年龄："+age;
    }
}
class Student extends Person{
    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }

    @Override
    public String say() {
        return "学生"+ super.say() + "成绩：" + score;
    }
    public void study(){
        System.out.println("学生"+ getName()+ "正在上课");
    }
}
class Teacher extends Person{
    private double salary;

    public Teacher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String say() {
        return "老师"+ super.say() + "薪水：" + salary;
    }
    public void teach(){
        System.out.println("老师"+ getName()+ "正在授课");
    }
}
```

```java
姓名：jack	年龄：20
error
学生姓名：jack	年龄：20成绩：100.0
学生jack正在上课
学生姓名：smith	年龄：19成绩：80.0
学生smith正在上课
老师姓名：travis	年龄：30薪水：20000.0
老师travis正在授课
老师姓名：scott	年龄：40薪水：25000.0
老师scott正在授课
```

2）多态参数

方法定义的形参类型为父类类型，实参类型允许为子类类型

## 9. Object类详解

java.lang.Object是所有类的超类。java中所有类都实现了这个类中的方法。

### 9.1 equals()方法

* == 和 equals的对比

  * ==  是比较运算符，既可以判断基本类型，也可以判断引用类型

    但只有一个比较规则，就是比较的是变量中保存的值是否相等

    引用类型变量中保存的值是对象的地址，即比较引用类型时，就是比较对象的地址

  * equals 是Object类中的方法，只能判断引用类型

    默认判断的是地址是否相等，子类中往往重写该方法，用于判断内容是否相等

### 9.2 hashCode()方法

* 总结
  * 该方法返回的是该对象的哈希码值，可以提高具有哈希结构的容器的效率
  * 两个引用，如果指向的是同一个对象，则哈希值肯定是一样的
  * 两个引用，如果指向不同对象，则哈希值是不一样的
  * 哈希值主要根据地址号来的，但不能完全将哈希值等价于地址
  * 在集合中，hashCode如果需要的话也会重写

### 9.3 toString()方法

* 默认返回：全类名+@+哈希值的十六进制
* 通常重写toString方法，输出对象的属性（alt+insert -> toString）
* 当打印输出一个引用时，会自动调用"`引用.toString()`"

### 9.4 finalize()方法

* 当对象被回收时，系统自动调用该对象的finalize方法。子类可以重写该方法，做一些释放资源的操作
* 当某个对象没有任何引用时，则jvm就认为这个对象是一个垃圾对象，会使用垃圾回收机制来销毁该对象，在销毁对象前，会先调用finalize方法
* 垃圾回收机制的调用，是由系统来决定的（即有自己的GC算法），也可以通过System.gc()主动触发垃圾回收机制







## 10. 断点调试（debug）





# 面向对象编程（高级）

## 1. 类变量和类方法（static关键字）

### 1.1 类变量

* 类变量也叫静态变量/静态属性，是该类的所有对象共享的变量，任何一个该类的对象去访问它时，取到的值都相同，同样任何一个该类的对象去修改它时，修改的也是同一个变量。

* 使用场景：当所有对象的某个属性的值是相同的，建议将该属性定义为静态变量，来节省内存的开销

* 定义语法：

​		`访问修饰符  static  数据类型  变量名   ；`

​		`static  访问修饰符  数据类型  变量名   ；`

* 访问类变量：

​    	类名 **.**  类变量名

​		对象名 **.**  类变量名

​		静态变量的访问修饰符的访问权限和普通属性一致

```java
public class Static_ {
    public static void main(String[] args) {
        
        System.out.println(A.name);
        A a = new A();
        System.out.println(a.name);
    }
}

class A {
    public static String name = "travis";
}
```

* 注意事项和细节
  * 加上static称为类变量或静态变量，否则称为实例变量/普通变量/非静态变量
  * 类变量是该类的所有对象共享的，而实例变量是每个对象独享的
  * 实例变量不能通过 类名.类变量名 方式来访问
  * static修饰的成员属于类，会存储在一块固定的内存区域（jdk8以后，这个区域在堆内存中），是随着类的加载而加载的，且只加载一次，所以只有一份，节省内存。所以，即使没有创建对象实例也可以访问，可以直接被类名调用。它优先于对象存在，所以，可以被所有对象共享。
  * 类变量的生命周期是随着类的加载开始，随着类消亡而销毁
  * 使用“引用.”访问静态相关的（静态方法或者变量），即使引用为null，也不会出现空指针异常

### 1.2 类方法

* 基本介绍：

  类方法也叫静态方法

  `访问修饰符 static 数据返回类型 方法名(){}`

  `static 访问修饰符 数据返回类型 方法名(){}`

* 类方法的调用：

  类名.类方法

  对象名.类方法

  前提：满足访问修饰符的访问权限

* 使用场景：

  当我们希望不创建实例，也可以调用某个方法（即当做工具来使用），这时适合将方法设为静态方法，提高开发效率

* 注意事项和细节：

  * 类方法和普通方法都是随着类的加载而加载，将结构信息存储在方法区

  * 类方法中无this的参数

    普通方法中隐含着this参数

  * 普通方法和对象有关，需要通过对象名调用，不能通过类名调用

    类方法既可以通过类名调用，也可以通过对象名调用

  * 类方法中不允许使用和对象有关的关键字，比如this和super

  * 类方法中只能访问 静态变量 或 静态方法

  * 普通成员方法既可以访问非静态变量（方法），也可以访问静态变量（方法），同时遵循访问权限

    

## 2. main方法

```java
public static void main(String[] args){ }
```

* main方法是虚拟机调用，所以该方法的访问权限必须是public

* Java虚拟机在执行nain方法时不必创建对象，所以必须加static

* main方法接收String类型的数组参数，该数组中保存执行Java命令时传递给所运行的类的参数

* 在main方法中，可以直接调用main方法所在类的静态方法或静态属性

  但不能直接访问该类中的非静态成员，必须创建该类的一个实例对象后，才能通过这个对象去访问类中的非静态成员

  

## 3. 代码块

* 基本介绍：
* 代码块又称为初始化块，属于类中的成员（即是类的一部分），类似于方法，将逻辑语句封装在方法体中，通过{ }包围起来，但和方法不同，没有方法名，没有参数，没有返回，只有方法体，而且不用通过对象或类显示调用，而是加载类时，或创建对象时隐式调用

* 基本语法：

  `[修饰符] {`

  ​	`代码`

  `};`

  说明：①修饰符可选，但要写的话只能写 static

  ​			②代码块分为两类，使用static修饰的叫静态代码块，没有static修饰的叫普通代码块/非静态代码块

  ​			③逻辑语句可以为任何逻辑语句（输入输出、方法调用、循环、判断...)

  ​			④ ；号可以写也可以不写

* 代码块的理解：
  * 相当于另外一种形式的构造器（对构造器的补充机制），可以做初始化的操作
  * 如果多个构造器中在最开始的时候都有重复的语句，可以抽取到初始化块中，提高代码的复用性（代码块执行早于构造方法）

* 注意事项和使用细节：

  *  static代码块也叫静态代码块，作用是对类进行初始化，而且它随着类的加载而执行，并且**只会执行一次**（类只加载一次）。如果是普通代码块，每创建一个对象就会执行
  *  静态代码块在类加载时执行，一个类中可以编写多个静态代码块，遵循自上而下的顺序依次执行
  *  静态代码块代表了类加载时刻，如果你有代码需要在此时刻执行，可以将该代码放到静态代码块中
  * 类什么时候被加载？
    * 创建对象实例时（new）
    * 创建子类对象实例，父类也会被加载，而且父类先被加载
    * 使用类的静态成员时（静态属性，静态方法）

  * 类加载早于main方法

  * 普通代码块在创建对象实例时会被隐式的调用，被创建一次就会调用一次；

    如果只是使用类的静态成员时，普通代码块并不会执行

  * 创建一个对象时，执行顺序：

    * 1.调用静态代码块和静态属性初始化

      注：静态代码块和静态属性初始化调用的优先级一样，如果有多个静态代码块和多个静态变量初始化，则按定义顺序调用

    * 2.调用普通代码块和普通属性初始化

      注：普通代码块和普通属性初始化调用的优先级一样，如果有多个普通代码块和多个普通变量初始化，则按定义顺序调用
  
    * 3.调用构造器

  * 构造器的最前面其实隐含了 super() 和调用普通代码块。静态相关的代码块，属性初始化，在类加载时就执行完毕
  
  * l
  
  * 静态代码块只能直接调用静态成员，普通代码块可以调用任意成员
  
  

​	 	

## 4. 单例设计模式

## 5. final 关键字

* 基本介绍：

  final 可以修饰 类、属性、方法和局部变量

  如下情况会使用到final：

  * 当不希望类被继承时
  * 当不希望父类的某个方法被子类重写时
  * 当不希望类的某个属性的值被修改时
  * 当不希望某个局部变量被修改时

* 注意事项和细节：

  * final修饰的属性又叫常量，一般用XX_XX_XX来命名（如TAX_RATE)
  * final 修饰的属性在定义时，必须赋初值，并且以后不能再修改，赋值可以在如下位置之一：
    * 定义时，如 public final double TAX_RATE = 0.08 ;
    * 在构造器中
    * 在代码块中

  * 如果final 修饰的属性是静态的，则初始化的位置只能是
    * 定义时
    * 静态代码块中

  * final类不能被继承，但是可以实例化对象

  * 如果类不是final类，但是含有final方法，则该方法虽然不能重写，但是可以被继承

  * 一般来说，如果一个类已经是final类了，就没有必要再将方法修饰成final方法了

  * final不能修饰构造器

  * final 和 static 往往搭配使用效率更高，不会导致类的加载，因为底层编译器做了优化处理

    ```java
    
    ```

  * 包装类（Integer,Double,Float,Boolean等）和String都是final类

​		 







##  6. 抽象类

当一个类中存在抽象方法时，需要将该类声明为abstract类

所谓抽象方法就是没有实现的方法，即没有方法体包括“{ }”

```java
abstract class Animal{
    String name;
    public abstract void eat();
}
```

* 基本介绍：
  * 用abstract关键字来修饰一个类时，这个类就叫抽象类
  * 用abstract关键字来修饰一个方法时，这个方法就叫抽象方法

* 使用情况：

  如果类中有些方法无法实现或者没有意义，可以将方法定义为抽象方法。类定义为抽象类。这样在抽象类中只提供公共代码，具体的实现强行交给子类去做。比如一个Person类有一个问候的方法greet()，但是不同国家的人问候的方式不同，因此greet()方法具体实现应该交给子类。

* 注意事项和细节：
  * 抽象类有构造方法，但无法实例化。抽象类的构造方法是给子类使用的
  * 抽象类不一定要包含abstract方法
  * 一旦类包含了abstract方法，则这个类必须声明为abstract
  * abstract 只能修饰类和方法，不能修饰属性和其他的
  * 抽象类也是类，可以有任意成员
  * 如果一个类继承了抽象类，则它必须实现/重写抽象类的**所有**抽象方法，**除非它自己也声明为abstract类**
  * 抽象方法不能使用private、final和static来修饰，因为这些关键字都是和重写相违背

## 7. 接口

* 快速入门：

  ```java
  public interface UsbInterface {
      public void start();
      public void stop();
  }
  
  ```

  ```java
  public class Phone implements UsbInterface {
      @Override
      public void start() {
          System.out.println("手机开始工作");
      }
  
      @Override
      public void stop() {
          System.out.println("手机停止工作");
      }
  }
  ```

  ```java
  public class Camera implements UsbInterface {
      @Override
      public void start() {
          System.out.println("相机开始工作");
      }
  
      @Override
      public void stop() {
          System.out.println("相机停止工作");
      }
  }
  ```

  ```java
  public class Computer {
      public void work(UsbInterface usbInterface){
          usbInterface.start();
          usbInterface.stop();
      }
  }
  ```

  ```java
  public class interface_ {
      public static void main(String[] args) {
          Camera camera = new Camera();
          Phone phone = new Phone();
          Computer computer = new Computer();
          computer.work(phone);
          System.out.println("================");
          computer.work(camera);
      }
  }
  ```

  ```java
  手机开始工作
  手机停止工作
  ================
  相机开始工作
  相机停止工作
  ```

* 基本介绍：

  接口就是给出一些没有实现的方法，封装到一起，到某个类要使用的时候，再根据具体情况把这些方法写出来

  语法：

  `interface 接口名{`

  `属性;`

  `方法;`

  `}`

  ——————————————————————

  `class 类名 implements 接口{`

  `自己属性;`

  `自己方法;`

  `必须实现的接口的抽象方法；`

  `}`

  ——————————————————————

  注：在JDK7.0前，接口里所有的方法都没有方法体，即都是抽象方法；

   JDK8.0及以后的版本接口可以有静态方法和默认方法，且必须有方法的具体实现。

  ```java
  default public void func(){
  }
  public static void func(){
  }
  ```

  



* 注意事项和细节：
  * 接口不能被实例化
  
  * 接口中所有的方法都是public方法，但不用写public，接口中的抽象方法可以不用abstract修饰
  
  * 一个普通类实现接口，就必须将该接口的**所有方法**都实现（alt+enter）
  
  * 抽象类实现接口，可以不用实现接口的方法
  
  * 一个类可以同时实现多个接口
  
  * 接口中的属性，只能是final的，而且都是默认 public static final 修饰符
  
    ```java
    int n = 10; //等价  public static final int n = 10;
    ```
  
  * 接口中属性的访问形式：接口名.属性名
  
  * 接口不能继承其他的类，但是可以继承多个别的接口
  
  * 接口的修饰符只能是 public和默认，这点和类的修饰符是一样的 
  
  * 类与接口是实现关系，接口与接口是继承关系



## 8. 内部类

* 基本介绍

  一个类的内部又完整的嵌套了另一个类结构，被嵌套的类称为内部类（inner class），嵌套其他类的类称为外部类（outer class）。是类的第五大成员（属性、方法、构造器、代码块、内部类），内部类的最大特点就是可以直接访问外部类的私有成员，并且可以体现类与类之间的包含关系

  

* 内部类的分类

  1. **实例内部类**，类定义在了成员位置 (类中方法外称为成员位置，无static修饰的内部类)
  
  2. **静态内部类**，类定义在了成员位置 (类中方法外称为成员位置，有static修饰的内部类)
  
  3. **局部内部类**，类定义在方法内
  4. **匿名内部类**，没有名字的内部类，可以在方法中，也可以在类中方法外



### **局部内部类**

* 定义在外部类的局部位置，和局部变量一个级别

* 局部内部类是定义在外部类的局部位置，通常在方法或代码块中
* 局部内部类不能添加访问修饰符，但是可以使用 final
* 作用域：仅仅在定义它的方法或代码块中
* 局部内部类能否访问外部类成员，取决于局部内部类所在的方法：
  * 若方法是静态的，则只能访问外部类的静态成员（包括私有）
  * 若方法是实例的，则可以访问所有成员（包括私有）

* 局部内部类在访问外部的局部变量时，这个局部变量必须是final修饰的，从JDK8开始，不需要手动添加final了，但JVM会自动添加

```java
public class LocalInnerClass {
    public static void main(String[] args) {
        Outer outer01 = new Outer();
        outer01.function();
        //Inner inner = new Inner();错误，外部其他类不能访问局部内部类，因为局部内部类地位是一个局部变量
    }
}

class Outer {
    private int n = 100;
    private void fun01() {
        System.out.println("fun01()执行中");
    }
    public void function() {
        //局部变量
        int i = 100;
        //局部内部类
        final class Inner {
            //本质仍然还是个类
            private int n = 200;
            public void fun02() {
              //如果外部类和局部内部类的成员重名时，默认遵守就近原则，如果想访问外部类的成员，则可以使用（外部类名.this.成员）去访问,这里Outer.this指的是调用function()的对象outer01，如果只用（this.同名成员），则this这里指的是调用fun02()的对象inner
                System.out.println("内部类的n = " + n + "  外部类的n = " + Outer.this.n);
                System.out.println("this.n = " + this.n);
                System.out.println("i = " + i);
                fun01();
            }
        }
        //class Inner01 extends Inner {}
        //5.外部类在方法中，创建Inner对象，然后调用方法即可
        Inner inner = new Inner();
        inner.fun02();
    }
}
```

```java
内部类的n = 200  外部类的n = 100
this.n = 200
i = 100
fun01()执行中
```



### **匿名内部类**

* 隐藏了名字的内部类，可以写在成员位置，也可以写在局部位置

* 语法格式

  ```java
  new 类名或接口名(){
  	重写方法;
  };
  ```

* 格式细节：包含了继承或实现，方法重写，创建对象。整体就是一个类的子类对象或者接口的实现类对象

* 使用场景：当方法的参数是接口或者类时，以接口为例，可以传递这个接口的实现类对象，如果实现类只需要使用一次，就可以用匿名内部类简化代码

  ```java
  public class Test {
      public static void main(String[] args) {
  
          Computer computer = new Computer();
  
          computer.conn(new Usb(){
              @Override
              public void read() {
                  System.out.println("read.....");
              }
  
              @Override
              public void write() {
                  System.out.println("write.....");
              }
          });
      }
  }
  
  class Computer {
      public void conn(Usb usb){
          usb.read();
          usb.write();
      }
  }
  
  interface Usb {
      void read();
      void write();
  }
  ```

  



### 实例内部类

定义在外部类的成员位置，并且没有static修饰

**内部类的使用格式**：

```java
 外部类.内部类。 // 访问内部类的类型都是用 外部类.内部类
```

**获取成员内部类对象的两种方式**：

方式一：外部直接创建成员内部类的对象

```java
外部类.内部类 变量 = new 外部类（）.new 内部类（）;
```

方式二：在外部类中定义一个方法提供内部类的对象



实例内部类的细节

1. 实例内部类可以被四个访问权限修饰符所修饰，比如： private，默认，protected，public
2. 在实例内部类里面，JDK16之前不能定义静态变量，JDK16开始才可以定义静态变量。
3. 创建内部类对象时，对象中有一个隐含的Outer.this记录外部类对象的地址值。（请参见3.6节的内存图）

详解：

​	内部类被private修饰，外界无法直接获取内部类的对象，只能通过3.3节中的方式二获取内部类的对象

​	被其他权限修饰符修饰的内部类一般用3.3节中的方式一直接获取内部类的对象

​	

​	内部类如果想要访问外部类的成员变量，外部类的变量必须用final修饰，JDK8以前必须手动写final，JDK8之后不需要手动写，JDK默认加上。

注意：内部类访问外部类对象的格式是：**外部类名.this**

```java
public class Test {
    public static void main(String[] args) {
        Outer.inner oi = new Outer().new inner();
        oi.method();
    }
}

class Outer {	// 外部类
    private int a = 30;

    // 在成员位置定义一个类
    class inner {
        private int a = 20;

        public void method() {
            int a = 10;
            System.out.println(???);	// 10   答案：a
            System.out.println(???);	// 20	答案：this.a
            System.out.println(???);	// 30	答案：Outer.this.a
        }
    }
}
```



### **静态内部类**

**静态内部类特点**：

* 静态内部类是一种特殊的成员内部类

- 有static修饰，属于外部类本身的
- 总结：静态内部类与其他类的用法完全一样。只是访问的时候需要加上外部类.内部类
- **拓展1**:静态内部类可以直接访问外部类的静态成员
- **拓展2**:静态内部类不可以直接访问外部类的非静态成员，如果要访问需要创建外部类的对象
- **拓展3**:对于静态内部类，四个访问修饰符都可以用
- **拓展4**:静态内部类中没有隐含的Outer.this

**内部类的使用格式**：

```
外部类.内部类。
```

**静态内部类对象的创建格式**：

```java
外部类.内部类  变量 = new  外部类.内部类构造器;
```

**调用方法的格式：**

* 调用非静态方法的格式：先创建对象，用对象调用
* 调用静态方法的格式：外部类名.内部类名.方法名();

**案例演示**：

```java
// 外部类：Outer01
class Outer01{
    private static  String sc_name = "黑马程序";
    // 内部类: Inner01
    public static class Inner01{
        // 这里面的东西与类是完全一样的。
        private String name;
        public Inner01(String name) {
            this.name = name;
        }
        public void showName(){
            System.out.println(this.name);
            // 静态内部类可以直接访问外部类的静态成员。
            System.out.println(sc_name);
        }
    }
}

public class InnerClassDemo01 {
    public static void main(String[] args) {
        // 创建静态内部类对象。
        // 外部类.内部类  变量 = new  外部类.内部类构造器;
        Outer01.Inner01 in  = new Outer01.Inner01("张三");
        in.showName();
    }
}
```





# 枚举和注解

## 1. 枚举的两种实现方式

**（1）自定义类实现枚举**

* 构造器私有化
* 类内部创建一组对象
* 对外暴露对象（通过为对象添加public final static修饰）
* 可以提供 get 方法，但是不要提供 set 方法

```java
public class Enum_ {
    public static void main(String[] args) {
        System.out.println(Season.AUTUMN);

    }
}

class Season {

    private String name;
    private String desc;
    public final static Season SPRING = new Season("春天", "温暖");
    public final static Season SUMMER = new Season("夏天", "炎热");
    public final static Season AUTUMN = new Season("秋天", "凉爽");
    public final static Season WINTER = new Season("冬天", "寒冷");
    private Season(String name, String desc) {
        this.name = name;
        this.desc = desc;

    }

    public String getName() {
        return name;
    }

//    public void setName(String name) {
//        this.name = name;
//    }

    public String getDesc() {
        return desc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }
//    public void setDesc(String desc) {
//        this.desc = desc;
//    }
}
```



**（2）使用enum关键字实现枚举**

```java
enum Season {
    SPRING("春天", "温暖"),SUMMER("夏天", "炎热"),AUTUMN("秋天", "凉爽"),WINTER("冬天", "寒冷");
    private String name;
    private String desc;
    ...
}
```

注意事项：

* 当使用enum关键字开发一个枚举类时，默认会继承Enum类，而且是一个final类

![0fd41338e8cc454965103cbb4be765d](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031630026.png)

* 传统的 `public final static Season SPRING = new Season("春天", "温暖");` 简化为`SPRING("春天", "温暖")` 
* 如果使用无参构造器创建枚举对象，则实参列表和小括号都可以省略
* 当有多个枚举对象时，使用逗号分隔，最后用一个分号结尾
* 枚举对象必须放在枚举类的行首

## 2. enum常用方法

<img src="https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031630639.png" alt="4df721006371caf9c178e0b5b827fb5" style="zoom:150%;" />



## 3. 注解

注解（Annotation）也被称为元数据（Metadata），用于修饰解释包、类、方法、属性、构造器、局部变量等数据信息

修饰注解的注解，称为元注解

和注释一样，注解不影响程序逻辑，但注解可以被编译或运行，相当于嵌入在代码中的补充信息

使用Annotation时要在其前面增加@符号，并把Annotation当成一个修饰符使用，用于修饰它支持的程序元素

三个基本的Annotation：

* @Override：限定某个方法，是重写父类方法，该注解只能修饰方法
* @Deprecated：用于表示某个程序元素已过时
* @SupperessWarnings：抑制编译器警告

# 异常（Exception）

## 1. 异常概述

* 基本概念

  Java语言中，将程序执行中发生的不正常情况称为“异常”（开发过程中的语法错误和逻辑错误不是异常）

* 执行过程中所发生的异常事件可分为两大类
  * Error（错误）：Java虚拟机无法解决的严重问题。如：JVM系统内部错误、资源耗尽等严重情况，如栈溢出和内存不足。程序出现错误，只有一个结果，就是终止JVM的执行，所有的错误都是无法处理的，但是是可抛出的
  
  * Exception：其他因编程错误或偶然的外在因素导致的一般性问题，可以使用针对性的代码进行处理。如空指针访问，试图读取不存在的文件，网络连接中断等。所有的异常都是可抛出的，同时也都是可处理的。
  
    Exception 分为两大类：运行时异常 和 编译时异常(除了运行时异常之外的)

* 在java中，异常是以类和对象的形式存在的，定义异常本质就是定义一个类，异常如果发生的话，也需要通过这个类new对象。如在某行代码发生空指针异常的时候，底层一定new了一个NullPointerException对象

## 2. 异常继承体系结构

![dc7ace23033dcafbd64c6ae2de5425b](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031630261.png)

* 异常体系中最上层父类：Exception

* 运行时异常 和 编译时异常的区别

  * 运行时异常：

    *  RuntimeException本身及其所有子类，都是运行时异常
    *  在编译阶段可以选择处理，也可以不处理，没有硬性要求
    * 运行时异常一般是由程序员的错误引起的，并且不需要强制进行异常处理

  * 编译时异常：

    * Exception所有的子类（除RuntimeException之外），都是编译时异常
    
    * 在编译阶段必须提前处理，如果不处理编译器报错
    
    * 编译时异常一般是由外部环境或外在条件引起的，如网络故障、磁盘空间不足、文件找不到等
    
      
  
  注意：编译时异常并不是在编译阶段发生的异常，所有的异常发生都是在运行阶段的，因为每个异常发生都是会new异常对象的，new异常对象只能在运行阶段完成。那为什么叫做编译时异常呢？这是因为这种异常必须在编译阶段提前预处理，如果不处理编译器报错，因此而得名编译时异常

* 异常的发生

  ```Java
  public static void main(String[] args) {
      //异常的发生需要经过两个阶段
      //1.创建异常对象
      NullPointerException e = new NullPointerException();
      //2.让异常发生（手动抛出异常）
      throw e;
  }
  ```

  不过通常简写为：

  ```Java 
  throw new NullPointerException();
  ```

## 3. 自定义异常

①第一步：编写异常类继承 Exception（编译时异常） 或 RuntimeException（运行时异常）

②第二步：提供一个无参数构造方法，再提供一个带`String msg`参数的构造方法，在构造方法中调用父类的构造方法

```java
/**
 * 定义一个编译时异常
 */
public class IllegalAgeException extends Exception {
    public IllegalAgeException() {
    }

    public IllegalAgeException(String message) {
        super(message);
    }
}
```

```java 
/**
 * 定义一个运行时异常
 */
public class IllegalNameException extends RuntimeException {
    public IllegalAgeException() {
    }

    public IllegalAgeException(String message) {
        super(message);
    }
}
```



## 4. 异常处理

### 4.1 异常处理的两种方式

第一种方式：声明异常（throws关键字）

* 在方法定义时使用throws关键字声明异常，告知调用者，调用这个方法可能会出现异常。如果出现了异常则会抛给调用者（方法）来处理：

  `public void m() throws AException, BException... {}`

* 如果AException和BException都继承了XException，那么也可以这样写：

  `public void m() throws XException{}`

* 调用者在调用m()方法时，编译器会检测到该方法上用throws声明了异常，表示可能会抛出异常，编译器会继续检测该异常是否为编译时异常，如果为编译时异常则必须在编译阶段进行处理，如果不处理编译器就会报错
* 如果所有位置都采用throws，包括main方法的处理态度也是throws，如果运行时出现了异常，最终异常是抛给了main方法的调用者（JVM），JVM则会终止程序的执行。因此为了保证程序在出现异常后不被中断，至少main方法不要再使用throws进行声明了
* 发生异常后，在发生异常的位置上，往下的代码是不会执行的，除非进行了异常的捕捉

第二种方式：捕捉异常 (try...catch...关键字)

* 在可能出现异常的代码上使用 try..catch 进行捕捉处理。其它方法如果调用这个方法，对于调用者来说是不知道这个异常发生的。因为这个异常被抓住并处理掉了

* 语法格式：

  ```java
  try{
  // 尝试执行可能会出现异常的代码
  // try块中的代码如果执行出现异常，出现异常的位置往下的代码是不会执行的，直接进入catch块执行
  }catch(AException e){
  // 如果捕捉到AException类型的异常，在这里处理
  }catch(BException e){
  // 如果捕捉到BException类型的异常，在这里处理
  }catch(XException e){
  // 如果捕捉到XException类型的异常，在这里处理
  }
  // 当try..catch..将所有发生的异常捕捉后，这里的代码是会继续往下执行的。
  ```

* 注意事项：

  * catch可以写多个。并且遵循自上而下，从小到大（这里的大小代表子父类的关系，父类大，子类小），如果是同级别，则不论先后

  * catch语句块可以看作是分支，try catch语句中，最多只有一个catch分支执行

  * Java7新特性：catch后面小括号中可以编写多个异常，使用运算符 “ | ” 隔开：

    `catch(AException | BException e){}`

  

### 4.2 异常处理方式的选用

* 异常在处理的整个过程中应该是：声明和捕捉联合使用

* 什么时候捕捉？什么时候声明？

  如果异常发生后需要调用者来处理的，需要调用者知道的，则采用声明方式。否则采用捕捉

  

## 5. 异常的常用方法

* `getMessage()`：这个方法可以获取当时创建异常对象时给异常构造方法传递的 `String message`参数的值

* `printStackTrace()`：打印异常堆栈信息
  * 异常信息的打印是符合栈数据结构的，也就是说主要看最上面的异常信息（栈顶），才能定位到根源
  * 采用多线程打印，输出顺序不一

## 6. 异常在开发中的应用

学习异常之前处理异常情况都如下处理：

```java 
if(xxx){
    System.out.println(xxx);
    reurn;
}
```

异常和return都能终止方法运行：

```java
public class ExceptionTest {
    public static void main(String[] args) {
        User user = new User();
        try {
            user.setAge(101);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}

class User{
    private int age;
    public User(){
    }
    public User(int age) {
        this.age = age;
    }
    public int getAge() {
        return age;
    }
    public void setAge(int age) throws Exception {
        
        if(age < 0 || age > 100){
            throw new Exception("年龄不合法");
        }
        this.age = age;
    }
}
```



## 7. finally语句块

* finally语句块中的代码是一定会执行的
* finally语句块不能单独使用，至少需要配合try语句块一起使用（可以不要catch）
* 通常在finally语句块中完成资源的释放
  * 资源释放的工作比较重要，如果资源没有释放会一直占用内存
  * 为了保证资源的关闭，也就是说：不管程序是否出现异常，关闭资源的代码一定要保证执行
  * 因此在finally语句块中通常进行资源的释放
* final、finally、finalize分别是什么？
  * final是一个关键字，修饰的类无法继承，修饰的方法无法覆盖，修饰的变量不能修改
  * finally是一个关键字，和try一起使用，finally语句块中的代码一定会执行
  * finalize是一个标识符，它是Object类中的一个方法名

## 8. 方法覆盖与异常

子类继承父类，方法重写之后，不能比父类方法抛出更多的异常，可以更少



























# 常用API

## 1.包装类（Wrapper）

* **包装类的分类**
  * 针对八种基本数据类型相应的引用类型—包装类
  * 有了类的特点，就可以调用类中的方法

![8da2eee40cb3d09ed5eecad3dd9bc39](javanote01.assets/8da2eee40cb3d09ed5eecad3dd9bc39.png)

<img src="javanote.assets/0860e33f124b537a2bab1f6c4a79a16.png" alt="0860e33f124b537a2bab1f6c4a79a16" style="zoom:150%;" />

<img src="javanote.assets/479a366eb6d05d91cf87515ccdcb98a.png" alt="479a366eb6d05d91cf87515ccdcb98a" style="zoom:150%;" />

<img src="javanote.assets/7a2186ddec50e9e207eaa75b3dfc6a3.png" alt="7a2186ddec50e9e207eaa75b3dfc6a3" style="zoom:150%;" />

* **包装类和基本数据类型的转换**

  * jdk5前是手动装箱和拆箱方式，装箱：基本类型一>包装类型，反之就是拆箱
  * jdk5及以后都是自动装箱和拆箱方式
  * 自动装箱底层调用的是valueOf方法，比如Integer.valueOf()

  ```java
  public class wrapper02 {
      public static void main(String[] args) {
          //手动装箱 int->Integer
          int n1 = 10;
          Integer integer = new Integer(n1);//方式一
          Integer integer01 = Integer.valueOf(n1);//方式二
  
          //手动拆箱 Integer->int
          int i = integer.intValue();
  
          //自动装箱 int->Integer
          int n2 =20;
          Integer integer02 = n2;//底层使用的是Integer.valueOf(n2)
          //自动拆箱 Integer->int
          int n3 = integer02;//底层使用的是intValue()方法
      }
  }
  ```

  

* **包装类型与String类型的相互转化**

```java
//以Integer和 String转换为例，其他类似
public class Wrapper01 {
    public static void main(String[] args) {
        //包装类(Integer)->String
        Integer i = 100;

        //方式1
        String str1 = i + "";
        //方式2
        String str2 = i.toString();
        //方式3
        String str3 = String.valueOf(i);

        //String->包装类(Integer)
        String str4 = "12345";
        
        //方式1
        Integer i1 = Integer.parseInt(str4);//使用到自动装箱
        //方式2
        Integer i2 = new Integer(str4);//使用到Integer构造器
    }
}
```

## 2. String 类

### 2.1 String类概述

String 类代表字符串，Java 程序中的所有字符串文字（例如“abc”）都被实现为此类的实例。也就是说，Java 程序中所有的双引号字符串，都是 String 类的对象。String 类在 java.lang 包下，所以使用的时候不需要导包！

### 2.2 String类的特点

- 字符串不可变，它们的值在创建后不能被更改
- 虽然 String 的值是不可变的，但是它们可以被共享
- 字符串效果上相当于字符数组( char[] )，但是底层原理是字节数组( byte[] )

### 2.3 String类的构造方法

- 常用的构造方法

  | 方法名                      | 说明                                      |
  | --------------------------- | ----------------------------------------- |
  | public   String()           | 创建一个空白字符串对象，不含有任何内容    |
  | public   String(char[] chs) | 根据字符数组的内容，来创建字符串对象      |
  | public   String(byte[] bys) | 根据字节数组的内容，来创建字符串对象      |
  | String s =   “abc”;         | 直接赋值的方式创建字符串对象，内容就是abc |

- 示例代码

  ```java
  public class StringDemo01 {
      public static void main(String[] args) {
          //public String()：创建一个空白字符串对象，不含有任何内容
          String s1 = new String();
          System.out.println("s1:" + s1);
  
          //public String(char[] chs)：根据字符数组的内容，来创建字符串对象
          char[] chs = {'a', 'b', 'c'};
          String s2 = new String(chs);
          System.out.println("s2:" + s2);
  
          //public String(byte[] bys)：根据字节数组的内容，来创建字符串对象
          byte[] bys = {97, 98, 99};
          String s3 = new String(bys);
          System.out.println("s3:" + s3);
  
          //String s = “abc”;	直接赋值的方式创建字符串对象，内容就是abc
          String s4 = "abc";
          System.out.println("s4:" + s4);
      }
  }
  ```

### 2.4 创建字符串对象两种方式的区别

- 通过构造方法创建

  ​	通过 new 创建的字符串对象，每一次 new 都会申请一个内存空间，虽然内容相同，但是地址值不同

- 直接赋值方式创建

  ​	以“ ”方式给出的字符串，只要字符序列相同(顺序和大小写)，无论在程序代码中出现几次，JVM 都只会建立一个 String 对象，并在字符串池中维护。字符串池在jdk7以前放在方法区，jdk7开始放在堆内存里

### 2.5 字符串的比较

#### 2.5.1==号的作用

- 比较基本数据类型：比较的是具体的值
- 比较引用数据类型：比较的是对象地址值

#### 2.5.2equals方法的作用

- 方法介绍

  ```java
  public boolean equals(String s)     比较两个字符串内容是否相同、区分大小写
  ```

- 示例代码

  ```java
  public class StringDemo02 {
      public static void main(String[] args) {
          //构造方法的方式得到对象
          char[] chs = {'a', 'b', 'c'};
          String s1 = new String(chs);
          String s2 = new String(chs);
  
          //直接赋值的方式得到对象
          String s3 = "abc";
          String s4 = "abc";
  
          //比较字符串对象地址是否相同
          System.out.println(s1 == s2);//false
          System.out.println(s1 == s3);//false
          System.out.println(s3 == s4);//ture
          System.out.println("--------");
  
          //比较字符串内容是否相同
          System.out.println(s1.equals(s2));//ture
          System.out.println(s1.equals(s3));//ture
          System.out.println(s3.equals(s4));//ture
      }
  }
  ```

### 2.6 StringBuilder

当我们在拼接字符串和反转字符串的时候会使用到

![322501839a59faafbef0347662a1c70](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631988.png)

![f4e3f6184dbca97283b2ded6fa080b9](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631485.png)

![864e6606ca5b6acfdcc04d5283b5133](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631406.png)

* 基本使用

```java
public class StringBuilderDemo3 {
    public static void main(String[] args) {
        //1.创建对象
        StringBuilder sb = new StringBuilder("abc");

        //2.添加元素
        sb.append(1);
        sb.append(2.3);
        sb.append(true);//打印输出：abc12.3true

        //反转
        sb.reverse();//打印输出：cba

        //获取长度
        int len = sb.length();
        System.out.println(len);//输出：3


        //打印
        //普及：
        //因为StringBuilder是Java已经写好的类
        //java在底层对他做了一些特殊处理。
        //打印对象不是地址值而是属性值。
        System.out.println(sb);
    }
}
```

### 链式编程

```java
public class StringBuilderDemo4 {
    public static void main(String[] args) {
        //1.创建对象
        StringBuilder sb = new StringBuilder();

        //2.添加字符串
        sb.append("aaa").append("bbb").append("ccc").append("ddd");
        //sb.append()返回的数据类型还是 StringBuilder，故可用链式编程

        System.out.println(sb);//aaabbbcccddd

        //3.再把StringBuilder变回字符串
        String str = sb.toString();
        System.out.println(str);//aaabbbcccddd

    }
}
```

![903ba64f5e61056d77bc219e46f2af2](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631570.png)

## 3. Math

* 基本介绍

  Math 类包含用于执行基本数学运算的方法，如初等指数、对数、平方根和三角函数等

## 4. Date

## 5. System 类

## 6. Arrays

![439727698c05726ee8eab1c420ef70d](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631014.png)

<img src="javanote01.assets/d6388b4d685e572a869c61f250266f7.png" alt="d6388b4d685e572a869c61f250266f7" style="zoom:150%;" /><img src="https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631593.png" alt="21878afbe1e9bf88e9745c449f38920" style="zoom:150%;" /><img src="javanote01.assets/2f0757ee950ac52e32bac5d7e23b6cf.png" alt="2f0757ee950ac52e32bac5d7e23b6cf" style="zoom:150%;" /><img src="javanote01.assets/97ac9e6e22bec5f3d6a98bc992d4efd-1705305963579-9.png" style="zoom:150%;" /><img src="https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631814.png" alt="27fa611e922929b061687e6f9b3575e" style="zoom:150%;" /><img src="https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031631504.png" alt="c3c24146d752000c9801bf50c8dca23" style="zoom:150%;" />

## 9. BigInterger 和 BigDecimal 类

应用场景

BigInterger 适合保存比较大的整数

BigDecimal 适合保存精读更高的浮点数（小数）

## 10. Lambda表达式

![ec6533fbfcc663b195b7c886fc40f44](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031632131.png)

![e6816f5825de4fb89ab96ba5943d618](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202407031632009.png)

![2ddceebae68b753392d3e3a8e866baa](javanote01.assets/2ddceebae68b753392d3e3a8e866baa.png)

![fd21ab09065d703e58af09324d15996](javanote01.assets/fd21ab09065d703e58af09324d15996.png)

# 集合

## 集合体系结构

* 集合主要分两组：**单列集合**（Collection）和双列集合（Map）

* **集合与数组的对比：**
  * 数组长度固定；集合长度可变
  * 数组可以存储基本类型和引用类型；集合只能存储引用类型，基本类型要转成包装类



## 单列集合

List系列集合：添加的元素是有序、可重复、有索引

Set系列集合：添加的元素是无序、不重复、无索引

有序指的是存取顺序

### Collection

#### 常用方法

![2b97ce0b9cb35dade82f513dd5b5402](javanote01.assets/2b97ce0b9cb35dade82f513dd5b5402.png)

ps:

* Collection方法集成了Set和List，故操作对象都是元素，无索引操作

* add( )方法中，如果往List系列集合添加元素，方法永远返回true

  ​						如果往Set系列集合添加元素，若要添加元素不存在，方法返回true

  ​																		  若要添加元素已经存在，方法返回false

* remove( )方法中，删除成功，则返回true；删除失败，则返回false，元素不存在就会删除失败
* contains( )方法中，底层是依赖equals方法进行判断是否存在的，所以，如果集合中存储的是自定义对象，也想通过contains方法来判断是否包含，那么在自定义类中一定要重写equals方法，重写后的方法是根据对象属性来判断；如果没有重写equals方法，则默认使用Object类中的equals方法进行判断，默认equals方法是依赖地址值进行判断，无意义

#### Collection集合的遍历

1. 迭代器遍历

![96387c6f4af696726cb7761785fefe5](javanote01.assets/96387c6f4af696726cb7761785fefe5.png)

![c9dd179a2f9a657b748c0232c15358e](javanote01.assets/c9dd179a2f9a657b748c0232c15358e.png)

注：集合对象调用iterator()方法

![a225a605abdf2457979f9528dc025fe](javanote01.assets/a225a605abdf2457979f9528dc025fe.png)

2. 增强 for 遍历

   循环内不会改变集合内元素

![6fd92926d43245655f056a81539530b](javanote01.assets/6fd92926d43245655f056a81539530b.png)

3. Lambda 表达式遍历

![622c6339a0f91f4dd88ef25353cd895](javanote01.assets/622c6339a0f91f4dd88ef25353cd895.png)

```java
public class A07_CollectionDemo7 {
    public static void main(String[] args) {
       /* 
        lambda表达式遍历：
                default void forEach(Consumer<? super T> action):
        */

        //1.创建集合并添加元素
        Collection<String> coll = new ArrayList<>();
        coll.add("zhangsan");
        coll.add("lisi");
        coll.add("wangwu");
        //2.利用匿名内部类的形式
        //底层原理：
        //其实也会自己遍历集合，依次得到每一个元素
        //把得到的每一个元素，传递给下面的accept方法
        //s依次表示集合中的每一个数据
       /* coll.forEach(new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);
            }
        });*/

        //lambda表达式
        coll.forEach(s -> System.out.println(s));
    }
}
```



总结

![b0ba9611dbce62649d84f26fd1415e1](javanote01.assets/b0ba9611dbce62649d84f26fd1415e1.png)



### List

特有方法

- 方法介绍

  | 方法名                          | 描述                                                         |
  | ------------------------------- | ------------------------------------------------------------ |
  | void add(int index,E   element) | 在此集合中的指定位置插入指定的元素，原来索引及以后的元素依次往后移 |
  | E remove(int   index)           | 删除指定索引处的元素，返回被删除的元素                       |
  | E set(int index,E   element)    | 修改指定索引处的元素，返回被修改的元素                       |
  | E get(int   index)              | 返回指定索引处的元素                                         |

  


List集合的五种遍历方式

1. 迭代器
2. 列表迭代器
3. 增强for
4. Lambda表达式
5. 普通for循环

代码示例：

```java
//创建集合并添加元素
List<String> list = new ArrayList<>();
list.add("aaa");
list.add("bbb");
list.add("ccc");

//1.迭代器
/*Iterator<String> it = list.iterator();
     while(it.hasNext()){
        String str = it.next();
        System.out.println(str);
}*/


//2.增强for
//下面的变量s，其实就是一个第三方的变量而已。
//在循环的过程中，依次表示集合中的每一个元素
/* for (String s : list) {
       System.out.println(s);
   }*/

//3.Lambda表达式
//forEach方法的底层其实就是一个循环遍历，依次得到集合中的每一个元素
//并把每一个元素传递给下面的accept方法
//accept方法的形参s，依次表示集合中的每一个元素
//list.forEach(s->System.out.println(s) );


//4.普通for循环
//size方法跟get方法还有循环结合的方式，利用索引获取到集合中的每一个元素
/*for (int i = 0; i < list.size(); i++) {
            //i:依次表示集合中的每一个索引
            String s = list.get(i);
            System.out.println(s);
        }*/

// 5.列表迭代器
//获取一个列表迭代器的对象，里面的指针默认也是指向0索引的

//额外添加了一个方法：在遍历的过程中，可以添加元素
ListIterator<String> it = list.listIterator();
while(it.hasNext()){
    String str = it.next();
    if("bbb".equals(str)){
        //qqq
        it.add("qqq");
    }
}
System.out.println(list);
```

细节点注意：

List系列集合中的两个删除的方法

```java
1.直接删除元素
2.通过索引进行删除
```

代码示例:

```java
//List系列集合中的两个删除的方法
//1.直接删除元素
//2.通过索引进行删除

//1.创建集合并添加元素
List<Integer> list = new ArrayList<>();

list.add(1);
list.add(2);
list.add(3);


//2.删除元素
//请问：此时删除的是1这个元素，还是1索引上的元素？
//为什么？
//因为在调用方法的时候，如果方法出现了重载现象
//优先调用，实参跟形参类型一致的那个方法。

//list.remove(1);


//手动装箱，手动把基本数据类型的1，变成Integer类型
Integer i = Integer.valueOf(1);

list.remove(i);

System.out.println(list);

```

#### ArrayList

* ArrayList 可以加null，并且多个
* 线程不安全

ArrayList 集合底层原理（动态数组）

![a9583a9f71576ef68c51bab01547815](javanote01.assets/a9583a9f71576ef68c51bab01547815.png)

![2819393c1614fa80637220c8c4e3138](javanote01.assets/2819393c1614fa80637220c8c4e3138.png)

#### LinkedList

* 底层双向链表
* 可以加null
* 线程不安全



LinkedList 集合底层原理（双向链表）

LinkedList 特有API：

![36d216b942f9db1e030c73e37a5ddac](javanote01.assets/36d216b942f9db1e030c73e37a5ddac.png)

#### vector

* 底层是对象数组
* 线程同步，即线程安全，操作方法带有synchronized
* 除线程安全外，与ArrayList无异





### Set

![8d87ec95d28f4b13af04b363c4c6353](javanote01.assets/8d87ec95d28f4b13af04b363c4c6353.png)

![52dccee3359bc6fdd356ae99c01950f](javanote01.assets/52dccee3359bc6fdd356ae99c01950f.png)

![b3c4d6f450842888d8f33aee77e9822](javanote01.assets/b3c4d6f450842888d8f33aee77e9822.png)



#### HashSet

![9b75f78e664daa6ad056dc205d302f2](javanote01.assets/9b75f78e664daa6ad056dc205d302f2.png)

![4946f9514a7efd92a861745d917f332](javanote01.assets/4946f9514a7efd92a861745d917f332.png)

![dd120c53d339055ff2f324740a8ca1c](javanote01.assets/dd120c53d339055ff2f324740a8ca1c.png)

![65d30cf14e0b14ce08a757ec99bbd56](javanote01.assets/65d30cf14e0b14ce08a757ec99bbd56.png)

![0495ec6bcfa6c5ee569156891c7b9bc](javanote01.assets/0495ec6bcfa6c5ee569156891c7b9bc.png)

自定义对象，不重写两个方法，则hashCode方法根据地址值计算hash值，equals方法比较的也是地址，没有什么意义

HashSet集合存储自定义类型元素,要想实现元素的唯一,要求必须重写hashCode方法和equals方法

#### LinkedHashSet

![5bbd29424d468956a2affb9316fa2be](javanote01.assets/5bbd29424d468956a2affb9316fa2be.png)

![edf479e005c9fa5df36cfd39525684f](javanote01.assets/edf479e005c9fa5df36cfd39525684f.png)

#### TreeSet

![2de7316925cd8c84d96646fb1a04561](javanote01.assets/2de7316925cd8c84d96646fb1a04561.png)

![e734fc6a59d7e2368ba2a4d0a00aabd](javanote01.assets/e734fc6a59d7e2368ba2a4d0a00aabd.png)

​	![b90e5c73edc200530eb1e851c2574aa](javanote01.assets/b90e5c73edc200530eb1e851c2574aa.png)																																																																																										

## 双列集合

![774ac77e6c8ed75ca7cc481a2586040](javanote01.assets/774ac77e6c8ed75ca7cc481a2586040.png)

* 双列集合的特点

![26ee7a6cc0b54133354d07fa313499a](javanote01.assets/26ee7a6cc0b54133354d07fa313499a.png)

### Map

* Map的key可以为null，只能有一个，value也可以为NULL，可以有多个

* Map常见API

![991f60783055b32814b341c3e4724cc](javanote01.assets/991f60783055b32814b341c3e4724cc.png)

* 代码示例

<img src="javanote01.assets/406c62cafe4783167c41bf1f0bc0cfa.png" alt="406c62cafe4783167c41bf1f0bc0cfa" style="zoom:150%;" />

![1f6a446c01ae37df797360f9f8ba701](javanote01.assets/1f6a446c01ae37df797360f9f8ba701.png)

* Map的遍历方式

  1. 键找值

     <img src="javanote01.assets/923c131cd80145a89ba2481992627e4-1705476639806-6.png" alt="923c131cd80145a89ba2481992627e4" style="zoom:150%;" />

     

  2. 键值对

     ![4d8c8c074507d0a1e09e7345b5f69ad](javanote01.assets/4d8c8c074507d0a1e09e7345b5f69ad.png)

     

  3. Lambda表达式

     <img src="javanote01.assets/8c9ebb1aa8218f382ff97ea4114b4df.png" alt="8c9ebb1aa8218f382ff97ea4114b4df" style="zoom:150%;" />

### HashMap

* 线程不安全

* 特点

![02099a799b1a83e349029ead9fd8bc5](javanote01.assets/02099a799b1a83e349029ead9fd8bc5.png)

* 底层原理

![968725aab490f9502328a523697375e](javanote01.assets/968725aab490f9502328a523697375e.png)

![7aab4c42832b37e334d3be39cf0f938](javanote01.assets/7aab4c42832b37e334d3be39cf0f938.png)



### LinkedHashMap

![a5ac3ac636a33953ae4221c7fae2358](javanote01.assets/a5ac3ac636a33953ae4221c7fae2358.png)



### HashTable

* 存放键值对
* 键和值都不能为NULL
* 使用方法基本和HashMap一样
* HashTable是线程安全的，hashmap不是
* ![a6cca15aeba287879b68f6af839c404](javanote01.assets/a6cca15aeba287879b68f6af839c404.png)





### TreeMap

![41b353df636453fee9a7609293357a2](javanote01.assets/41b353df636453fee9a7609293357a2.png)

### Properties

![2fe206b610f62df62499991ff81da78](javanote01.assets/2fe206b610f62df62499991ff81da78.png)



## Collections

![a41867926592db2ce3adf738dec38e2](javanote01.assets/a41867926592db2ce3adf738dec38e2.png)

![45479487cca34d122769753c5ac19c7](javanote01.assets/45479487cca34d122769753c5ac19c7.png)





















# 泛型

![bbc2e41e922b137e4c4ed846b2edd35](javanote01.assets/bbc2e41e922b137e4c4ed846b2edd35.png)

![6c034fa04edf68ddf73f05013ae8c8d](javanote01.assets/6c034fa04edf68ddf73f05013ae8c8d.png)

底层上存入集合的还是Object类，不过取出的时候自动强转

![c948695e99113196f6efd58d66e1d40](javanote01.assets/c948695e99113196f6efd58d66e1d40.png)



# 多线程

进程：程序的基本执行实体

线程：操作系统能够进行运算调度的最小单位，包含在进程之中，是进程的实际运作单位



并行： 在同一时刻，多个指令在多个CPU上同时进行

并发：在同一时间段，多个指令在单个CPU上交替执行



## 实现多线程的三种方式

1.继承Thread类

```java
//步骤
//1.自定义一个类MyThread继承Thread类
//2.在MyThread类中重写run()方法
//3.创建MyThread类的对象
//4.调用start()方法开启线程
public class MyThread extends Thread {
    @Override
    public void run() {
        for(int i=0; i<100; i++) {
            System.out.println(i);
        }
    }
}
public class MyThreadDemo {
    public static void main(String[] args) {
        MyThread my1 = new MyThread();
        MyThread my2 = new MyThread();

        my1.start();
        my2.start();
    }
}
```

2.实现Runnable接口

```java
//步骤
//1.自定义一个类MyRunnable实现Runnable接口
//2.在MyRunnable类中重写run()方法
//3.创建MyRunnable类的对象
//4.创建Thread类的对象，把MyRunnable对象作为构造方法的参数
//5.调用start()方法开启线程
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        for(int i=0; i<100; i++) {
            System.out.println(Thread.currentThread().getName()+":"+i);
        }
    }
}
public class MyRunnableDemo {
    public static void main(String[] args) {
        MyRunnable my = new MyRunnable();
        Thread t1 = new Thread(my);
        Thread t2 = new Thread(my);
        t1.start();
        t2.start();
    }
}
```

3.利用Callable接口和Future接口

```java
//步骤
//1.定义一个类MyCallable实现Callable接口
//2.在MyCallable类中重写call()方法
//3.创建MyCallable类的对象
//4.创建Future的实现类FutureTask对象，把MyCallable对象作为构造方法的参数
//5.创建Thread类的对象，把FutureTask对象作为构造方法的参数
//6.启动线程
//7.再调用get方法，就可以获取线程结束之后的结果。
public class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        for (int i = 0; i < 100; i++) {
            System.out.println("跟女孩表白" + i);
        }
        //返回值就表示线程运行完毕之后的结果
        return "答应";
    }
}
public class Demo {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        //线程开启之后需要执行里面的call方法
        MyCallable mc = new MyCallable();
        
        FutureTask<String> ft = new FutureTask<>(mc);
        
        Thread t1 = new Thread(ft);
        t1.start();
        
        String s = ft.get();
        System.out.println(s);
    }
}
```

![d76010950d17812177d4235321a64b5](javanote01.assets/d76010950d17812177d4235321a64b5.png)



## 线程优先级

线程调度

- 两种调度方式
  - 分时调度模型：所有线程轮流使用 CPU 的使用权，平均分配每个线程占用 CPU 的时间片
  - 抢占式调度模型：优先让优先级高的线程使用 CPU，如果线程的优先级相同，那么会随机选择一个，优先级高的线程获取的 CPU 时间片相对多一些

- Java使用的是抢占式调度模型

优先级线程默认优先级是5；线程优先级的范围是：1-10（10代表优先级最高，表示抢到cpu概率是大的，但也仅仅是概率）

## 线程的生命周期

![fdda97278806a32dd54af7f5a53a5f5](javanote01.assets/fdda97278806a32dd54af7f5a53a5f5.png)

## 生产者和消费者（等待唤醒机制）

## 线程池

![f32b507767e036a82106eb3fc22bf27](javanote01.assets/f32b507767e036a82106eb3fc22bf27.png)

# IO流

## 文件

* 创建文件

  ```java
  
  import org.junit.jupiter.api.Test;
  
  import java.io.File;
  import java.io.IOException;
  
  public class CreatFile {
      public static void main(String[] args) {
      }
      @Test
      //方式1 new File(String pathname)
      public void create01(){
          String filepath = "D:\\news1.txt";
          File file = new File(filepath);
          try {
              file.createNewFile();
              System.out.println("文件创建成功");
          } catch (IOException e) {
              throw new RuntimeException(e);
          }
  
      }
      @Test
      //方式2 new File(File parent, String child) 父目录文件＋子路径
      public void create02(){
          File parentfile = new File("D:\\");
          String fileName = "news2.txt";
          File file = new File(parentfile, fileName);
          try {
              file.createNewFile();
              System.out.println("创建成功");
          } catch (IOException e) {
              throw new RuntimeException(e);
          }
      }
      @Test
      //方式3 new File(String parent, String child) 父目录＋子路径
      public void create03(){
          String parentPath = "d:/";
          String fileName = "news3.txt";
          File file = new File(parentPath, fileName);
          try {
              file.createNewFile();
              System.out.println("创建成功");
          } catch (IOException e) {
              throw new RuntimeException(e);
          }
  
      }
  }
  ```

  * 文件的常用方法

  

  ## IO流原理及流的分类

  * 流的分类
    * 按操作数据

  

  

  

  ## 节点流和处理流

  ## 输入流

  ## 输出流

  ## Properties类





# 反射

反射机制允许程序在执行期借助子Reflection API取得任何类的内部信息(比如成员变量，构造器，成员方法等等)，并能操作对象的属性及方法

加载完类之后,在堆中就产生了一个Class类型的对象(一个类只有一个Class对象)，这个对象包含了类的完整结构信息。通过这个对象得到类的结构。这个对象就像一面镜子,透过这个镜子看到类的结构 所以,形象的称之为：反射

# 动态代理





