# 数据库概述

## 数据库类型

- 关系型数据库
  - 关系型数据库是**依据关系模型来创建**的数据库。所谓关系模型就是“**一对一、一对多、多对多**”等关系模型，关系模型就是指**二维表格模型**，因而一个关系型数据库就是由**二维表及其之间的联系**组成的一个数据组织。
  - 关系型数据可以很好地存储一些关系模型的数据，比如一个老师对应多个学生的数据（“多对多”），一本书对应多个作者（“一对多”），一本书对应一个出版日期（“一对一”）。
  - 关系模型包括数据结构（数据存储的问题，二维表）、操作指令集合（SQL语句）、完整性约束(表内数据约束、表与表之间的约束)。
- 非关系型数据库（NoSQL）
  - NoSQL最常见的解释是“non-relational”， “Not Only SQL”也被很多人接受。
  - NoSQL仅仅是一个概念，**泛指非关系型的数据库**，区别于关系数据库，它们**不保证**关系数据的ACID特性。
  - NoSQL有如下优点：**易扩展**，NoSQL数据库种类繁多，但是一个共同的特点都是去掉关系数据库的关系型特性。数据之间无关系，这样就非常容易扩展。无形之间也在架构的层面上带来了可扩展的能力。大数据量，高性能，NoSQL数据库都具有非常高的**读写性能**，尤其在大数据量下，同样表现优秀。这得益于它的无关系性，数据库的**结构简单**

## 数据库三范式

什么是数据库三范式？

数据库表设计的原则。教你怎么设计数据库表有效，并且节省空间。

* 第一范式：任何一张表都应该有**主键**，且每个字段是**原子性**的不能再分
* 第二范式：建立在第一范式基础上，另外要求所有 非主键字段 **完全依赖** 主键，不能产生 部分依赖
* 第三范式：建立在第二范式基础上，非主键字段 不能 传递 依赖于 主键字段



# SQL

## SQL概述

- **结构化查询语言**（Structured Query Language）简称SQL，是一种特殊目的的编程语言，是一种数据库查询和程序设计语言，用于存取数据以及查询、更新和管理关系数据库系统。
- 结构化查询语言是高级的非过程化编程语言，允许用户在高层数据结构上工作。它不要求用户指定对数据的存放方法，也不需要用户了解具体的数据存放方式，所以具有完全不同底层结构的不同数据库系统, 可以使用相同的结构化查询语言作为数据输入与管理的接口。结构化查询语言语句可以嵌套，这使它具有极大的灵活性和强大的功能。

## SQL分类

- DQL
  - 数据**查询**语言（Data Query Language, DQL）是SQL语言中，**负责进行数据查询**而不会对数据本身进行修改的语句，这是最基本的SQL语句。保留字SELECT是DQL（也是所有SQL）用得最多的动词，其他DQL常用的保留字有FROM，WHERE，GROUP BY，HAVING和ORDER BY。这些DQL保留字常与其他类型的SQL语句一起使用。
- DDL
  - 数据**定义**语言 (Data Definition Language, DDL) 是SQL语言集中，**负责数据结构定义与数据库对象(数据库，表，字段)定义**的语言，由CREATE、ALTER与DROP三个语法所组成，最早是由 Codasyl (Conference on Data Systems Languages) 数据模型开始，现在被纳入 SQL 指令中作为其中一个子集。
- DML
  - 数据**操纵**语言（Data Manipulation Language, DML）是SQL语言中，负责对数据库对象运行数据访问工作的指令集，以INSERT、UPDATE、DELETE三种指令为核心，分别代表**插入、更新与删除**。
- DCL
  - 数据**控制**语言 (Data Control Language) 在SQL语言中，是一种可对数据访问权进行控制的指令，它可以控制特定用户账户对数据表、查看表、预存程序、用户自定义函数等数据库对象的控制权。由 GRANT 和 REVOKE 两个指令组成。DCL以**控制用户的访问权限**为主，GRANT为授权语句，对应的REVOKE是撤销授权语句。
- TPL
  - 数据事务管理语言（Transaction Processing Language）它的语句能确保**被DML语句影响的表的所有行及时得以更新**。TPL语句包括BEGIN TRANSACTION，COMMIT和ROLLBACK。
- CCL
  - 指针控制语言（Cursor Control Language），它的语句，像DECLARE CURSOR，FETCH INTO和UPDATE WHERE CURRENT用于对一个或多个表单独行的操作。

## DBMS、SQL、DB之间的关系

- DBMS通过执行SQL来操作DB中的数据。





## 1.DDL

### 1.1数据库操作

* `查询所有数据库`

  ```SQL
  show databases;
  ```

* `查询当前数据库`

  ```sql
  select database();
  ```

* `创建数据库`

  ```sql
  create database [if not exists] 数据库名 [default charset 字符集] [collate 排序规则];
  ```

* `删除数据库`

  ```sql
  drop database [if exists] 数据库名;
  ```

* `切换数据库`

  ```sql
  use 数据库名;
  ```

### 1.2表操作

* `查询当前数据库所有表`

  ```sql
  show tables;
  ```

* `查看指定表结构`

  ```sql
  desc 表名;
  ```

* `查询指定表的建表语句`

  ```sql
  show create table 表名;
  ```

* `建表`

  ```sql
  create table 表名(
  	字段1 类型 [comment 注释],
  	字段2 类型 [comment 注释],
  	...
  	字段N 类型 [comment 注释]
  )[comment 注释] ;
  ```

  注意：最后一个字段后面没有逗号

* `添加字段`

  ```sql
  ALTER TABLE 表名 ADD 字段名 类型（长度）[comment 注释] [约束];
  ```

* `修改数据类型`

  ```sql
  ALTER TABLE 表名 MODIFY 字段名 新数据类型（长度）;
  ```

* `修改字段名和字段类型`

  ```sql
  ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型（长度）[comment 注释] [约束];
  ```

* `删除字段`

  ```sql
  ALTER TABLE 表名 DROP 字段名;
  ```

* `修改表名`

  ```sql
  ALTER TABLE 表名 RENAME TO 新表名;
  ```

* `删除表`

  ```sql
  DROP TABLE [ IF EXISTS ] 表名;
  ```

* `删除表中的数据，表结构还在`

  ```sql
  TRUNCATE TABLE 表名;
  ```

## 2.DML

### 2.1添加数据

* `给指定字段添加数据`

  ```sql
  INSERT INTO 表名 (字段1,字段2,字段3,...) VALUES (值1,值2,...);
  ```

* `给全部字段添加数据`

  ```sql
  INSERT INTO 表名 VALUES (值1,值2,...);
  ```

* `批量添加数据`

  ```sql
  ① INSERT INTO 表名 (字段1,字段2,字段3,...) VALUES (值1,值2,...), (值1,值2,...),(值1,值2,...);
  ② INSERT INTO 表名 VALUES (值1,值2,...), (值1,值2,...),(值1,值2,...);
  ```

  注意：1.插入数据时，指定的字段顺序需要与值的顺序是一一对应的

  ​            2.字符串和日期型数据应该包含在引号中

  ​            3.插入的数据大小，应该在字段的规定范围内

### 2.2修改数据

* `修改数据`

  ```sql
  UPDATE 表名 SET 字段1=值1 , 字段2=值2, ... [ WHERE 条件 ] ;
  ```

  注意：不带 WHERE条件的话就是给对应字段的所有行数据进行修改

### 2.3删除数据

* `删除数据`

  ```sql
  DELETE FROM 表名 [ WHERE 条件 ] ;
  ```

  * DELETE 语句的条件可以有，也可以没有，如果没有条件，则会删除整张表的所有数据。

  * DELETE 语句不能删除某一个字段的值(可以使用UPDATE，将该字段值置为NULL即可)。



## 3.DQL

### 3.1基本查询（不带任何条件）

* `查询多个字段`

  ```sql
  ① SELECT 字段1 [ AS 别名1 ] , 字段2 [ AS 别名2 ] ... FROM 表名;
  ② SELECT * FROM 表名;
  ```

  * \* 号代表查询所有字段，在实际开发中尽量少用（不直观、影响效率）
  * AS 代表起别名，其中 AS 可以省略

* `去除重复记录`

  ```sql
  SELECT DISTINCT 字段列表 FROM 表名;
  ```

注意：

* DISTINCT去重只是将显示的结果去重，**原表数据不会被更改**

* DISTINCT只能出现在所有字段的**最前面**

* 当DISTINCT出现后，后面多个字段一定是**联合去重**的

​		



### 3.2条件查询（WHERE）

* 基本语法

  ```sql
  SELECT 字段列表 FROM 表名 WHERE 条件列表 ;
  ```

* 常用比较运算符

  | 比较运算符          | 功能                                                         |
  | ------------------- | ------------------------------------------------------------ |
  | >                   | 大于                                                         |
  | >=                  | 大于等于                                                     |
  | <                   | 小于                                                         |
  | <=                  | 小于等于                                                     |
  | =                   | 等于                                                         |
  | <> 或 !=            | 不等于                                                       |
  | BETWEEN ... AND ... | 在某个范围之内(含最小、最大值)                               |
  | IN(...)             | 在 IN 之后的列表中的值，多选一                               |
  | NOT IN(...)         | 不在列表值范围内                                             |
  | LIKE 占位符         | 模糊匹配( _ 匹配单个字符,  % 匹配任意个字符)                 |
  | IS NULL             | 是NULL； 判断某个数据是否为null，不能使用等号，只能使用 is null； |
  | IS  NOT NULL        | 不是NULL；判断某个数据是否不为null，不能使用不等号，只能使用 is not null； |

  * 注意：

    * **在数据库中null不是一个值，不能用等号和不等号衡量，null代表什么也没有，没有数据，没有值**

    * in的执行原理实际上是采用=和or的方式；not in的执行原理实际上是采用<>和and的方式

      ```sql
      select * from emp where comm in(NULL, 300);
      以上SQL语句实际上是：
      select * from emp where comm = NULL or comm = 300;
      其中NULL不能用等号=进行判断，所以comm = NULL结果是false，然而中间使用的是or，所以comm = NULL被忽略了。所以查询结果就以上一条数据。
      通过以上的测试得知：**in是自动忽略NULL的**。
      
      select * from emp where comm not in(NULL, 300);
      以上SQL语句实际上是：
      select * from emp where comm <> NULL and comm <> 300;
      其中NULL的判断不能使用<>，所以comm <> NULL结果是false，由于后面是and，and表示并且，comm <> NULL已经是false了，所以and右边的就没必要运算了，comm <> NULL and comm <> 300的整体运算结果就是false。所以查询不到任何数据。
      通过以上测试得知，**not in是不会自动忽略NULL的**，所以在使用not in的时候一定要提前过滤掉NULL。
      ```

    * in和or的效率比拼

      ```
      如果in和or所在列有索引或者主键的话，or和in没啥差别，执行计划和执行时间都几乎一样。
      
      如果in和or所在列没有索引的话，性能差别就很大了：
      在没有索引的情况下，随着in或者or后面的数据量越多，in的效率不会有太大的下降，但是or会随着记录越多的话性能下降非常厉害，基本上是指数级增长。
      ```

      

* 常用逻辑运算符

  | 逻辑运算符 | 功能                        |
  | ---------- | --------------------------- |
  | AND 或 &&  | 并且 (多个条件同时成立)     |
  | OR 或 \|\| | 或者 (多个条件任意一个成立) |
  | NOT 或 !   | 非 , 不是                   |

  * and和or同时出现时，and优先级较高，会先执行，如果希望or先执行，这个时候需要给or条件添加小括号。另外，以后遇到不确定的优先级时，可以通过添加小括号的方式来解决。

### 3.3聚合函数（COUNT、MAX、MIN、AVG、SUM）

* 基本介绍

  将一列数据作为一个整体，进行纵向计算

* 常见聚合函数

  | 函数  | 功能     |
  | ----- | -------- |
  | count | 统计数量 |
  | max   | 最大     |
  | min   | 最小     |
  | avg   | 平均     |
  | sum   | 求和     |

* 语法

  ```sql
  SELECT 聚合函数(字段列表) FROM 表名 ;
  ```

  注意：**NULL值是不参与所有聚合函数运算的。**

### 3.4分组查询（GROUP BY）

* 语法

  ```sql
  SELECT 字段列表 FROM 表名 [ WHERE 条件 ] GROUP BY 分组字段名 [ HAVING 分组后过滤条件 ];
  ```

* WHERE 与 HAVING 的区别
  * 执行时机不同：where是分组前进行过滤，不满足where条件，不参与分组；而having是分组之后对结果进行过滤
  * 判断条件不同：where不能对聚合函数进行判断，而having可以

* 注意事项：
  * **当select语句中有group by的话，select后面只能跟聚合（分组）函数或参加分组的字段**，查询其他字段无任何意义
  * 执行顺序: **where > 聚合函数 > having** 
  * 支持多字段分组，具体语法为 : group by  columnA，columnB
  * ```sql
    聚合函数不能直接使用在where子句当中
    select ename,job from emp where sal > avg(sal); 这个会报错的
    原因：分组的行为是在where执行之后才开始的
    ```
  
    

### 3.5排序查询（ORDER BY)

* 语法

  ```sql
  SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1 , 字段2 排序方式2 ;
  ```

* 排序方式
  * ASC：升序（默认值）
  * DESC：降序

* 注意事项
  * 如果是升序, 可以不指定排序方式ASC 
  * 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序 

### 3.6分页查询（LIMIT）

* 语法

  ```sql
  SELECT 字段列表 FROM 表名 LIMIT 起始索引, 查询记录数 ;
  ```

* 注意事项
  * 起始索引从0开始，起始索引 = （查询页码 - 1）* 每页显示记录数
  * 分页查询是数据库的方言，不同的数据库有不同的实现，MySQL中是LIMIT
  *  如果查询的是第一页数据，起始索引可以省略，直接简写为 limit 10



### 总结单表DQL的执行顺序

```txt
select ...6
from ...1
where ...2
group by ...3
聚合函数 ...4
having ...5
order by ...7
limit ...8
```



## 4.DCL

# 函数

函数是指一段可以直接被另一段程序调用的程序或代码。 也就意味着这一段程序或代码在MySQL中已经给我们提供好了，我们要做的就是在合适的业务场景调用对应的函数完成对应的业务需求即可。

MySQL中的函数主要分为以下四类： 字符串函数、数值函数、日期函数、流程函数

# 约束

## 概述

概念：约束是作用于表中**字段上的规则**，用于限制存储在表中的数据

目的：保证数据库中数据的正确、有效性和完整性

![image-20240604230125635](https://cdn.jsdelivr.net/gh/hduchenshuai/PicGo_Save/picgo/202406181743507.png)

注意：约束是作用于表中字段上的，可以在创建表/修改表的时候添加约束。

## 外键约束

* 创建表时语法：

  ```sql
  CREATE TABLE 表名(
      字段名 数据类型,
      ...
      [CONSTRAINT] [外键名称] FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名)
  );
  ```

* 修改表时语法：

  ```sql
  ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名) ;
  ```



# 连接查询

## 连接查询的分类

1. 根据语法出现的年代进行分类：
   1. SQL92（这种语法很少用，可以不用学。）
   2. SQL99（我们主要学习这种语法。）
2. 根据连接方式的不同进行分类：
   1. 内连接
      1. 等值连接
      2. 非等值连接
      3. 自连接
   2. 外连接
      1. 左外连接（左连接）
      2. 右外连接（右连接）
   3. 全连接

## 笛卡尔积

1. 当两张表进行连接查询时，如果没有任何条件进行过滤，最终的查询结果条数是两张表条数的乘积。为了避免笛卡尔积现象的发生，需要添加条件进行筛选过滤。
2. 需要注意：添加条件之后，虽然避免了笛卡尔积现象，但是匹配的次数没有减少。
3. 为了SQL语句的可读性，为了执行效率，建议给表起别名。

## 内连接

满足条件的记录才会出现在结果集中

语法：

```sql
SELECT 字段列表 FROM 表1 [ INNER ] JOIN 表2 ON 连接条件 ... ;
```



* 等值连接

  连接时，条件为等量关系

  ```sql
  select
  	e.ename,d.dname
  from
  	emp e
  inner join
  	dept d
  on
  	e.deptno = d.deptno;
  ```

* 非等值连接

  连接时，条件是非等量关系
  
  ```sql
  select
  	e.ename,e.sal,s.grade
  from
  	emp e
  join
  	salgrade s
  on
  	e.sal between s.losal and s.hisal;
  ```
  
  
  
* 自连接

  连接时，一张表看做两张表，自己和自己进行连接。
  
  ```sql
  select
  	e.ename 员工名, l.ename 领导名
  from
  	emp e
  join
  	emp l
  on
  	e.mgr = l.empno;
  ```
  
  

## 外连接

内连接是满足条件的记录查询出来。也就是两张表的交集。
外连接是除了满足条件的记录查询出来，再将其中一张表的记录全部查询出来，另一张表如果没有与之匹配的记录，自动模拟出NULL与其匹配。

外连接分为两种，分别是：左外连接 和 右外连接。具体的语法结构为：

* 左外连接

  ```sql
  SELECT 字段列表 FROM 表1 LEFT [ OUTER ] JOIN 表2 ON 条件 ... ;
  ```

* 右外连接

  ```sql
  SELECT 字段列表 FROM 表1 RIGHT [ OUTER ] JOIN 表2 ON 条件 ... ;
  ```

注：任何一个左连接都可以写作右连接，右连接也可转换成左连接



## 全连接

MySQL不支持full join。oracle数据库支持。

两张表数据全部查询出来，没有匹配的记录，各自为对方模拟出NULL进行匹配。



## 子查询

* select语句中嵌套select语句就叫做子查询

* select语句可以嵌套在哪里？

  ```SQL
  select后面 -- select ..(select)..  
  from后面 --  from ..(select)..
  where后面 -- where ..(select)..  
  ```

* where后面使用子查询

  ```sql
  案例：找出高于平均薪资的员工姓名和薪资：
  select ename,sal from emp where sal > (select avg(sal) from emp);
  ```

* from后面使用子查询

  ```sql
  from后面的子查询可以看做一张临时表
  案例：找出每个部门的平均工资的等级：
  第一步：先找出每个部门平均工资
  select deptno, avg(sal) avgsal from emp group by deptno;
  第二步：将以上查询结果当做临时表t，t表和salgrade表进行连接查询
  select t.*,s.grade from (select deptno, avg(sal) avgsal from emp group by deptno) t join salgrade s on t.avgsal between s.losal and s.hisal;
  ```

* select后面使用子查询



## exists、not exists

* **exists**

  EXISTS用于检查**子查询**的查询结果行数是否大于0。如果子查询的查询结果行数大于0，则 EXISTS 条件为真。（即存在查询结果则是true。）

  ```sql
  select * from t_customer c where exists(select * from t_order o where o.customer_id=c.customer_id);
  ```

  在这个查询语句中，子查询用于检查是否有订单与每个客户相关联。如果子查询返回**至少一行**，则表示该顾客已经下过订单，并返回此客户的所有信息，否则      该顾客将不被包含在结果中

  

* **not exists**

  NOT EXISTS 用于检查一个子查询是否返回任何行，如果没有行返回，那么 NOT EXISTS 将返回 true。

  ```sql
  select * from t_customer c where not exists(select * from t_order o where o.customer_id=c.customer_id);
  ```

  在这个查询语句中，如果没有任何与顾客相关联的订单，则 NOT EXISTS 子查询将返回一个空结果集，这时候 WHERE 条件为 true，并将返回所有顾客信息。如果顾客有订单，则 NOT EXISTS 子查询的结果集将不为空，WHERE 条件为 false，则不会返回该顾客的信息。

  

## union&union all

不管是union还是union all都可以将两个查询结果集进行合并

union会对合并之后的查询结果集进行**去重**操作

union all是直接将查询结果集合并，不进行去重操作



案例：查询工作岗位是MANAGER和SALESMAN的员工：

```sql
select ename,sal from emp where job='MANAGER'
union all
select ename,sal from emp where job='SALESMAN';
```

注意：两个结果集合并时，**列数量要相同**



# 视图

1. 只能将select语句创建为视图。
2. 创建视图

```sql
create or replace view v_emp as select e.ename,d.dname from emp e join dept d on e.deptno = d.deptno;
```

3. 视图作用
   1. 如果开发中有一条非常复杂的SQL，而这个SQL在多处使用，会给开发和维护带来成本。使用视图可以降低开发和维护的成本。
   2. 视图可以隐藏表的字段名。
4. 修改视图

```sql
alter view v_emp as select e.ename,d.dname,d.deptno from emp e join dept d on e.deptno = d.deptno;
```

5. 删除视图
   1. drop view if exists v_emp;
6. 对视图增删改（DML：insert delete update）可以影响到原表数据。

# 索引

## 什么是索引？

索引是一种能够提高检索（查询）效率的提前排好序的数据结构。例如：书的目录就是一种索引机制。索引是解决SQL慢查询的一种方式。

## 索引的创建和删除

* 主键会自动添加索引

  主键字段会自动添加索引，不需要程序员干涉，主键字段上的索引被称为`主键索引`

* unique约束的字段自动添加索引

  unique约束的字段也会自动添加索引，不需要程序员干涉，这种字段上添加的索引称为`唯一索引`

* 给指定的字段添加索引

  * 建表时添加索引：

  ```sql
  CREATE TABLE emp (
      ...
      name varchar(255),
      ...
      INDEX idx_name (name)
  );
  
  ```

  * 如果表已经创建好了，后期给字段添加索引

  ```sql
  ALTER TABLE emp ADD INDEX idx_name (name);
  ```

  * 也可以这样添加索引：

  ```sql
  create index idx_name on emp(name);
  ```


## 索引的分类

不同的`存储引擎`有不同的索引类型和实现：

- 按照数据结构分类：
  - B+树 索引（mysql的InnoDB存储引擎采用的就是这种索引）采用 B+树  的数据结构
  - Hash 索引（仅 `memory` 存储引擎支持）：采用  哈希表  的数据结构
- 按照物理存储分类：
  - 聚集索引：索引和表中数据在一起，数据存储的时候就是按照索引顺序存储的。一张表只能有一个聚集索引。
  - 非聚集索引：索引和表中数据是分开的，索引是独立于表空间的，一张表可以有多个非聚集索引。
- 按照字段特性分类：
  - 主键索引（primary key）
  - 唯一索引（unique）
  - 普通索引（index）
  - 全文索引（fulltext：仅 `InnoDB和MyISAM` 存储引擎支持）
- 按照字段个数分类：
  - 单列索引、联合索引（也叫复合索引、组合索引）

# 数据库优化

MySQL数据库的优化手段通常包括但不限于：

- SQL查询优化：这是最低成本的优化手段，通过优化查询语句、适当添加索引等方式进行。并且效果显著。
- 库表结构优化：通过规范化设计、优化索引和数据类型等方式进行库表结构优化，需要对数据库结构进行调整和改进
- 系统配置优化：根据硬件和操作系统的特点，调整最大连接数、内存管理、IO调度等参数
- 硬件优化：升级硬盘、增加内存容量、升级处理器等硬件方面的投入，需要购买和替换硬件设备，成本较高

我们主要掌握：SQL查询优化
