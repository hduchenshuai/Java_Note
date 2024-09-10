https://www.yuque.com/dujubin/ltckqu/kipzgd?#WuqzZ 访问密码:mg9b

## Spring是如何创建对象的呢？原理是什么？

spring是通过调⽤类的⽆参数构造⽅法来创建对象的，所以要想让spring给你创建对象，必须保证⽆参数构造⽅法是存在的。

```java
 // dom4j解析beans.xml⽂件，从中获取class的全限定类名
 // 通过反射机制调⽤⽆参数构造⽅法创建对象
 Class clazz = Class.forName("com.powernode.spring6.bean.User");
 Object obj = clazz.newInstance();
```

## 在配置⽂件中配置的类必须是⾃定义的吗，可以使⽤JDK中的类吗，例如：java.util.Date？

在spring配置⽂件中配置的bean可以任意类，只要这个类不是抽象的，并且提供了⽆参 数构造⽅法

# 依赖注入

## set注入

基于set方法实现的，底层会通过反射机制调用属性对应的set方法然后给属性赋值。这种方式要求属性必须对外提供set方法。

```xml
<property name="userDao" ref="userDaoBean"/>
```



## 构造注入

核心原理：通过调用构造方法来给属性赋值

```xml
 <!--index="0"表示构造方法的第一个参数，将orderDaoBean对象传递给构造方法的第一个参数。-->
 <constructor-arg index="0" ref="orderDaoBean"/>
```

## p命名空间注入

使用p命名空间注入的前提条件包括两个：

- 第一：在XML头部信息中添加p命名空间的配置信息：xmlns:p="http://www.springframework.org/schema/p"
- 第二：p命名空间注入是基于setter方法的，所以需要对应的属性提供setter方法。

```xml
<bean id="customerBean" class="com.powernode.spring6.beans.Customer" p:name="zhangsan" p:age="20"/>
```

## c命名空间注入

c命名空间是简化构造方法注入的。

使用c命名空间的两个前提条件：

第一：需要在xml配置文件头部添加信息：xmlns:c="http://www.springframework.org/schema/c"

第二：需要提供构造方法。

```xml
<bean id="myTimeBean" class="com.powernode.spring6.beans.MyTime" c:_0="2008" c:_1="8" c:_2="8"/>
```

# Bean的作用域

作用域对应**scope属性**，**它一共包括8个选项**：

- singleton：默认的，单例。
- prototype：原型。每调用一次getBean()方法则获取一个新的Bean对象。或每次注入的时候都是新对象。
- request：一个请求对应一个Bean。**仅限于在WEB应用中使用**。
- session：一个会话对应一个Bean。**仅限于在WEB应用中使用**。
- global session：**portlet应用中专用的**。如果在Servlet的WEB应用中使用global session的话，和session一个效果。（portlet和servlet都是规范。servlet运行在servlet容器中，例如Tomcat。portlet运行在portlet容器中。）
- application：一个应用对应一个Bean。**仅限于在WEB应用中使用。**
- websocket：一个websocket生命周期对应一个Bean。**仅限于在WEB应用中使用。**
- 自定义scope：很少使用。