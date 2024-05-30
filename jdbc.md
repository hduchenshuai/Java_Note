# JDBC概述

## 1、JDBC是什么？

Java DataBase Connectivity（Java语言连接数据库）

## 2、JDBC的本质是什么？

一套接口。

JDBC是SUN公司制定的一套接口（interface）
java.sql.*; (这个软件包下有很多接口。)

接口都有调用者和实现者。
实现者：各大数据库厂商
调用者：程序员
面向接口调用、面向接口写实现类，这都属于面向接口编程。

![f2a302c1333fb957cd4f4fd9ffd6448](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202405251721221.png)

为什么要面向接口编程？
	解耦合：降低程序的耦合度，提高程序的扩展力。
	多态机制就是非常典型的：面向抽象编程。（不要面向具体编程）
		建议：
			Animal a = new Cat();
			Animal a = new Dog();
			// 喂养的方法
			public void feed(Animal a){ // 面向父类型编程。
			}
		不建议：
			Dog d = new Dog();
			Cat c = new Cat();



思考：为什么SUN制定一套JDBC接口呢？
	因为每一个数据库的底层实现原理都不一样。
	Oracle数据库有自己的原理。
	MySQL数据库也有自己的原理。
	MS SqlServer数据库也有自己的原理。
	....
	每一个数据库产品都有自己独特的实现原理。



## 3、JDBC开发前的准备工作

先从官网下载对应的驱动jar包，然后将其配置到环境变量classpath当中。

classpath=.;D:\course\06-JDBC\resources\MySql Connector Java 5.1.23\mysql-connector-java-5.1.23-bin.jar

以上的配置是针对于文本编辑器的方式开发，使用IDEA工具的时候，不需要配置以上的环境变量。IDEA有自己的配置方式。

## 4、JDBC编程六步（需要背会）

​	

	第一步：注册驱动（作用：告诉Java程序，即将要连接的是哪个品牌的数据库）
	
	第二步：获取连接（表示JVM的进程和数据库进程之间的通道打开了，这属于进程之间的通信，重量级的，使用完之后一定要关闭通道。）
	
	第三步：获取数据库操作对象（专门执行sql语句的对象）
	
	第四步：执行SQL语句（DQL DML....）
	
	第五步：处理查询结果集（只有当第四步执行的是select语句的时候，才有这第五步处理查询结果集。）
	
	第六步：释放资源（使用完资源之后一定要关闭资源。Java和数据库属于进程间的通信，开启之后一定要关闭。）



```java
//JDBC编程六步
import java.sql.Driver;
import java.sql.DriverManager;
import java.sql.SQLException;
import java.sql.Connection;
import java.sql.Statement;

public class JDBCTest01 {
    public static void main(String[] args) {
        Connection conn = null;
        Statement stmt = null;
        try {
            //1、注册驱动
            Driver driver = new com.mysql.jdbc.Driver(); // 多态，父类型引用指向子类型对象。
            // Driver driver = new oracle.jdbc.driver.OracleDriver(); // oracle的驱动。
            DriverManager.registerDriver(driver);
            //2、获取连接
        /*
            url：统一资源定位符（网络中某个资源的绝对路径）
            https://www.baidu.com/ 这就是URL。
            URL包括哪几部分？
                协议
                IP
                PORT
                资源名

            http://182.61.200.7:80/index.html
                http:// 通信协议
                182.61.200.7 服务器IP地址
                80 服务器上软件的端口
                index.html 是服务器上某个资源名


            jdbc:mysql://127.0.0.1:3306/bjpowernode
                jdbc:mysql:// 协议
                127.0.0.1 IP地址
                3306 mysql数据库端口号
                bjpowernode 具体的数据库实例名。

            说明：localhost和127.0.0.1都是本机IP地址。

            jdbc:mysql://192.168.151.27:3306/bjpowernode

            什么是通信协议，有什么用？
                通信协议是通信之前就提前定好的数据传送格式。
                数据包具体怎么传数据，格式提前定好的。

            oracle的URL：
                jdbc:oracle:thin:@localhost:1521:orcl
        */
            String url = "jdbc:mysql://192.168.151.9:3306/bjpowernode";
            String user = "root";
            String password = "981127";
            conn = DriverManager.getConnection(url, user, password);
            // com.mysql.jdbc.JDBC4Connection@41cf53f9
            System.out.println("数据库连接对象 = " + conn);

            //3、获取数据库操作对象(Statement专门执行sql语句的)
            stmt = conn.createStatement();

            //4、执行sql(DML:delete,update,insert)
            //String sql = "delete from dept where deptno = 40";
            //String sql = "update dept set dname = '销售部', loc = '天津' where deptno = 20";
            String sql = "insert into dept(deptno,dname,loc) values(50,'人事部','北京')";
            // JDBC中的sql语句不需要提供分号结尾。
            // 专门执行DML语句的(insert delete update)
            // 返回值是“影响数据库中的记录条数”
            int count = stmt.executeUpdate(sql);
            System.out.println(count == 1 ? "保存成功" : "保存失败");

            //5、处理查询结果集

        } catch (SQLException e) {
            e.printStackTrace();
        } finally {
            //6、释放资源
            // 为了保证资源一定释放，在finally语句块中关闭资源
            // 并且要遵循从小到大依次关闭
            // 分别对其try..catch
            try {
                if (stmt != null) {
                    stmt.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
            try {
                if (conn != null) {
                    conn.close();
                }
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
}
```



```java
/*
	注册驱动的另一种方式（这种方式常用）
*/
import java.sql.*;

public class JDBCTest03{
    public static void main(String[] args){
        try{
            //1、注册驱动
            // 这是注册驱动的第一种写法。
            // DriverManager.registerDriver(new com.mysql.jdbc.Driver());
            // 注册驱动的第二种方式：常用的。
            // 为什么这种方式常用？因为参数是一个字符串，字符串可以写到xxx.properties文件中。
            // 以下方法不需要接收返回值，因为我们只想用它的类加载动作。
            Class.forName("com.mysql.jdbc.Driver");
            //2、获取连接
            Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode","root","333");
            // com.mysql.jdbc.JDBC4Connection@41cf53f9
            System.out.println(conn);

        }catch(SQLException e){
            e.printStackTrace();
        }catch(ClassNotFoundException e){
            e.printStackTrace();
        }
    }
}
```



```java
底层原理：
`com.mysql.jdbc.Driver.java源码如下：`

public class Driver extends NonRegisteringDriver implements java.sql.Driver {

    static {
        try {
            java.sql.DriverManager.registerDriver(new Driver());
        } catch (SQLException E) {
            throw new RuntimeException("Can't register driver!");
        }
    }


    public Driver() throws SQLException {
        // Required for Class.forName().newInstance()
    }
}
```

```
Class.forName("com.mysql.jdbc.Driver")语句执行会产生类加载的动作，静态代码块里的代码会执行，从而实现注册
```





* 从属性资源文件中读取连接数据库信息

`jdbc.properties文件：`

```properties
driver=com.mysql.jdbc.Driver
url=jdbc:mysql://192.168.151.9:3306/bjpowernode
user=root
password=981127
```

```java
//将连接数据库的所有信息配置到配置文件中
/*
	实际开发中不建议把连接数据库的信息写死到java程序中。
*/
import java.sql.*;
import java.util.*;

public class JDBCTest04{
	public static void main(String[] args){

		// 使用资源绑定器绑定属性配置文件
		ResourceBundle bundle = ResourceBundle.getBundle("jdbc");
		String driver = bundle.getString("driver");
		String url = bundle.getString("url");
		String user = bundle.getString("user");
		String password = bundle.getString("password");

		Connection conn = null;
		Statement stmt = null;
		try{
			//1、注册驱动
			Class.forName(driver);
			//2、获取连接
			conn = DriverManager.getConnection(url,user,password);
			//3、获取数据库操作对象
			stmt = conn.createStatement();
			//4、执行SQL语句			
			String sql = "update dept set dname = '销售部2', loc = '天津2' where deptno = 20";
			int count = stmt.executeUpdate(sql);
			System.out.println(count == 1 ? "修改成功" : "修改失败");
		}catch(Exception e){
			e.printStackTrace();
		}finally{
			//6、释放资源
			if(stmt != null){
				try{
					stmt.close();
				}catch(SQLException e){
					e.printStackTrace();
				}	
			}
			if(conn != null){
				try{
					conn.close();
				}catch(SQLException e){
					e.printStackTrace();
				}	
			}
		}
	}
}
```



* 处理查询结果集

![d5806f793104495288c0e0225e18ab7](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202405251721636.png)

```java
/*
	处理查询结果集（遍历结果集。）
*/
import java.sql.*;

public class JDBCTest05{
	public static void main(String[] args){
		Connection conn = null;
		Statement stmt = null;
		ResultSet rs = null;
		try{
			//1、注册驱动
			Class.forName("com.mysql.jdbc.Driver");
			//2、获取连接
			conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode","root","333");
			//3、获取数据库操作对象
			stmt = conn.createStatement();
			//4、执行sql
			String sql = "select empno as a,ename,sal from emp";
			// int executeUpdate(insert/delete/update)
			// ResultSet executeQuery(select)
			rs = stmt.executeQuery(sql); // 专门执行DQL语句的方法。
			//5、处理查询结果集
			/*
			boolean flag1 = rs.next();
			//System.out.println(flag1); // true
			if(flag1){
				// 光标指向的行有数据
				// 取数据
				// getString()方法的特点是：不管数据库中的数据类型是什么，都以String的形式取出。
				String empno = rs.getString(1); // JDBC中所有下标从1开始。不是从0开始。
				String ename = rs.getString(2);
				String sal = rs.getString(3);
				System.out.println(empno + "," + ename + "," + sal);
			}

			flag1 = rs.next();
			if(flag1){
				// 以下程序的1 2 3 说的第几列。
				String empno = rs.getString(1);
				String ename = rs.getString(2);
				String sal = rs.getString(3);
				System.out.println(empno + "," + ename + "," + sal);
			}
			*/

			while(rs.next()){
				/*
				String empno = rs.getString(1);
				String ename = rs.getString(2);
				String sal = rs.getString(3);
				System.out.println(empno + "," + ename + "," + sal);
				*/

				/*
				// 这个不是以列的下标获取，以列的名字获取
				//String empno = rs.getString("empno");
				String empno = rs.getString("a"); // 重点注意：列名称不是表中的列名称，是查询结果集的列名称。
				String ename = rs.getString("ename");
				String sal = rs.getString("sal");
				System.out.println(empno + "," + ename + "," + sal);
				*/

				// 除了可以以String类型取出之外，还可以以特定的类型取出。
				/*
				int empno = rs.getInt(1);
				String ename = rs.getString(2);
				double sal = rs.getDouble(3);
				System.out.println(empno + "," + ename + "," + (sal + 100));
				*/

				int empno = rs.getInt("a");
				String ename = rs.getString("ename");
				double sal = rs.getDouble("sal");
				System.out.println(empno + "," + ename + "," + (sal + 200));
			}

		}catch(Exception e){
			e.printStackTrace();
		}finally{
			//6、释放资源
			if(rs != null){
				try{
					rs.close();
				}catch(Exception e){
					e.printStackTrace();
				}
			}
			if(stmt != null){
				try{
					stmt.close();
				}catch(Exception e){
					e.printStackTrace();
				}
			}
			if(conn != null){
				try{
					conn.close();
				}catch(Exception e){
					e.printStackTrace();
				}
			}
		}
	}
}
```



# SQL注入问题

```
用户名：fdsa
密码：fdsa' or '1'='1
登录成功
这种现象被称为SQL注入(安全隐患)。（黑客经常使用）
```

```
导致SQL注入的根本原因是什么？
用户输入的信息中含有sql语句的关键字，并且这些关键字参与sql语句的编译过程，
导致sql语句的原意被扭曲，进而达到sql注入。
```

```
解决SQL注入问题？
只要用户提供的信息不参与SQL语句的编译过程，问题就解决了。
即使用户提供的信息中含有SQL语句的关键字，但是没有参与编译，不起作用。
要想用户信息不参与SQL语句的编译，那么必须使用java.sql.PreparedStatement
PreparedStatement接口继承了java.sql.Statement接口
PreparedStatement是属于预编译的数据库操作对象。
PreparedStatement的原理是：预先对SQL语句的框架进行编译，然后再给SQL语句传“值”。
```

```
解决SQL注入的关键是什么？
用户提供的信息中即使含有sql语句的关键字，但是这些关键字并没有参与编译。不起作用。
```



# Statement与PreparedStatement对比

* Statement用法示例

```java
// 1、注册驱动
Class.forName("com.mysql.jdbc.Driver");
// 2、获取连接
conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode", "root", "333");

// 3、获取数据库操作对象
Statement stmt = conn.createStatement();

// 4、执行sql
String sql = "select * from t_user where loginName = '"+loginName+"' and loginPwd = '"+loginPwd+"'";
// 以上正好完成了sql语句的拼接，以下代码的含义是，发送sql语句给DBMS，DBMS进行sql编译。
// 正好将用户提供的“非法信息”编译进去。导致了原sql语句的含义被扭曲了。
rs = stmt.executeQuery(sql); 

// 5、处理结果集
if(rs.next()){
    loginSuccess = true;
}
..//6、释放资源   
```

* PreparedStatement用法示例

```java
// 1、注册驱动
Class.forName("com.mysql.jdbc.Driver");
// 2、获取连接
conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode", "root", "333");

// 3、获取预编译的数据库操作对象
// SQL语句的框子。其中一个?，表示一个占位符，一个?将来接收一个“值”，注意：占位符不能使用单引号括起来。
String sql = "select * from t_user where loginName = ? and loginPwd = ?";
// 程序执行到此处，会发送sql语句框子给DBMS，然后DBMS进行sql语句的预先编译。
PreparedStatement ps = conn.prepareStatement(sql);
// 给占位符?传值（第1个问号下标是1，第2个问号下标是2，JDBC中所有下标从1开始。）
ps.setString(1, loginName);
ps.setString(2, loginPwd);

// 4、执行sql
rs = ps.executeQuery();

// 5、处理结果集
if(rs.next()){
    // 登录成功
    loginSuccess = true;
}
..//6、释放资源
```

* 对比一下Statement和PreparedStatement?

```
* Statement存在sql注入问题，PreparedStatement解决了SQL注入问题。
* Statement是编译一次执行一次。PreparedStatement是编译一次，可执行N次。PreparedStatement效率较高一些
* PreparedStatement会在编译阶段做类型的安全检查
```

综上所述：PreparedStatement使用较多。只有极少数的情况下需要使用Statement

什么情况下必须使用Statement呢？
业务方面要求必须支持SQL注入的时候。
Statement支持SQL注入，凡是业务方面要求是需要进行sql语句拼接的，必须使用Statement。

```java
// 用户在控制台输入desc就是降序，输入asc就是升序
        Scanner s = new Scanner(System.in);
        System.out.println("输入desc或asc，desc表示降序，asc表示升序");
        System.out.print("请输入：");
        String keyWords = s.nextLine();
        ...
-----------------------------------------------------------------
错误            
        String sql = "select ename from emp order by ename ?";
        ps = conn.prepareStatement(sql);
        ps.setString(1, keyWords);
		rs = ps.executeQuery();
-----------------------------------------------------------------
正确
    	stmt = conn.createStatement();
    	String sql = "select ename from emp order by ename " + keyWords;
        rs = stmt.executeQuery(sql);
```



# PreparedStatement完成增删改

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;

/**
 * 作者：杜聚宾
 * PreparedStatement完成INSERT DELETE UPDATE
 */
public class JDBCTest09 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement ps = null;
        try {
            // 1、注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            // 2、获取连接
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode", "root","333");
            // 3、获取预编译的数据库操作对象
            /*String sql = "insert into dept(deptno,dname,loc) values(?,?,?)";
            ps = conn.prepareStatement(sql);
            ps.setInt(1, 60);
            ps.setString(2, "销售部");
            ps.setString(3, "上海");*/

            /*String sql = "update dept set dname = ?, loc = ? where deptno = ?";
            ps = conn.prepareStatement(sql);
            ps.setString(1, "研发一部");
            ps.setString(2, "北京");
            ps.setInt(3, 60);*/

            String sql = "delete from dept where deptno = ?";
            ps = conn.prepareStatement(sql);
            ps.setInt(1, 60);

            // 4、执行SQL
            int count = ps.executeUpdate();
            System.out.println(count);
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            // 6、释放资源
            if (ps != null) {
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```







# JDBC事务

```java
/* JDBC事务机制：
 *     JDBC中的事务是自动提交的，什么是自动提交？
 *     只要执行任意一条DML语句，则自动提交一次。这是JDBC默认的事务行为。
 *     但是在实际的业务当中，通常都是N条DML语句共同联合才能完成的，必须
 *     保证他们这些DML语句在同一个事务中同时成功或者同时失败。
 *
 *
 *  重点三行代码：
 *      conn.setAutoCommit(false);
 *      conn.commit();
 *      conn.rollback();
 */
public class JDBCTest11 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement ps = null;
        try {
            // 1、注册驱动
            Class.forName("com.mysql.jdbc.Driver");
            // 2、获取连接
            conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode", "root","333");
            // 将自动提交机制修改为手动提交
            conn.setAutoCommit(false); // 开启事务

            // 3、获取预编译的数据库操作对象
            String sql = "update t_act set balance = ? where actno = ?";
            ps = conn.prepareStatement(sql);

            // 给?传值
            ps.setDouble(1, 10000);
            ps.setInt(2, 111);
            int count = ps.executeUpdate();

            //String s = null;
            //s.toString();

            // 给?传值
            ps.setDouble(1, 10000);
            ps.setInt(2, 222);
            count += ps.executeUpdate();

            System.out.println(count == 2 ? "转账成功" : "转账失败");

            // 程序能够走到这里说明以上程序没有异常，事务结束，手动提交数据
            conn.commit(); // 提交事务

        } catch (Exception e) {
            // 回滚事务
            if(conn != null){
                try {
                    conn.rollback();
                } catch (SQLException e1) {
                    e1.printStackTrace();
                }
            }
            e.printStackTrace();
        } finally {
            // 6、释放资源
            if (ps != null) {
                try {
                    ps.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
            if (conn != null) {
                try {
                    conn.close();
                } catch (SQLException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```



# JDBC工具类的封装

```java
package com.bjpowernode.jdbc.utils;

import java.sql.*;

/**
 * JDBC工具类，简化JDBC编程。
 */
public class DBUtil {

    /**
     * 工具类中的构造方法都是私有的。
     * 因为工具类当中的方法都是静态的，不需要new对象，直接采用类名调用。
     */
    private DBUtil() {
    }

    // 静态代码块在类加载时执行，并且只执行一次。
    static {
        try {
            Class.forName("com.mysql.jdbc.Driver");
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }
    }


    /**
     * 获取数据库连接对象
     *
     * @return 连接对象
     * @throws SQLException
     */
    public static Connection getConnection() throws SQLException {
        return DriverManager.getConnection("jdbc:mysql://localhost:3306/bjpowernode", "root", "333");
    }

    /**
     * 关闭资源
     * @param conn 连接对象
     * @param ps 数据库操作对象
     * @param rs 结果集
     */
    public static void close(Connection conn, Statement ps, ResultSet rs){
        if(rs != null){
            try {
                rs.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(ps != null){
            try {
                ps.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
        if(conn != null){
            try {
                conn.close();
            } catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }

}
```

* 使用工具类实现模糊查询

```java
/**
 * 这个程序两个任务：
 *      第一：测试DBUtil是否好用
 *      第二：模糊查询怎么写？
 */
public class JDBCTest12 {
    public static void main(String[] args) {
        Connection conn = null;
        PreparedStatement ps = null;
        ResultSet rs = null;
        try {
            // 获取连接
            conn = DBUtil.getConnection();
            // 获取预编译的数据库操作对象
            
			//查找第二个字符是A的部门名称
            // 错误的写法，识别不到？
            /*
            String sql = "select ename from emp where ename like '_?%'";
            ps = conn.prepareStatement(sql);
            ps.setString(1, "A");
            */

            String sql = "select ename from emp where ename like ?";
            ps = conn.prepareStatement(sql);
            ps.setString(1, "_A%");
            rs = ps.executeQuery();
            while(rs.next()){
                System.out.println(rs.getString("ename"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally{
            // 释放资源
            DBUtil.close(conn, ps, rs);
        }

    }
}
```

u回回回u
