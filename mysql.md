###### 1、关键字

- DQL ：查询语句
- DML ：对表中数据进行增删改
- DDL：对表结构的增删改
- TCL：事务控制语言（提交：commit；回滚：rollback）
- DCL：数据控制



- between  ...  and ...

  闭区间

- and  优先级高于   or

  先执行or的话要加括号

- in  括号后面跟具体的值

- 排序：默认升序

  desc降序

  asc升序

- group  by  

  按照某一个字段或某一些字段进行分组

  如果一个语句有group  by

- having :   必须和group  by 一起使用

  分完组之后的数据进行再次过滤
  
- distinct   关键字去除重复记录

![image-20210710004902764](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210710004902764.png)

**where后面不能用分组函数**

分组函数一般是和group  by  连用的

where执行实在group  by 之前执行

自动忽略NULL

select  ename, max(sal),job from emp group by job;

![image-20210710103330055](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210710103330055.png)

select  deptno, avg(sal)  from  emp  group  by  deptno  having  avg(sal)  >  2000;

###### 2、总结一个完整的DQL语句怎么写？

![image-20210710180240228](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210710180240228.png)

![image-20210711005720388](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210711005720388.png)

distinct  只能出现在所有字段的最前面

###### 3、分组

![image-20210711160057352](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210711160057352.png)

###### 4、内连接与外连接

![image-20210711180103474](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210711180103474.png)



![image-20210711222117099](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210711222117099.png)

###### 5、from后面嵌套子查询

（1）找出每个部门平均薪水的等级

![image-20210712235033447](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210712235033447.png)

![image-20210712235055665](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210712235055665.png)

（2）找出每个部门平均的薪水等级

![image-20210713000116802](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210713000116802.png)

![image-20210713000133844](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210713000133844.png)

###### 6、在select后面嵌套子查询

![image-20210713001349916](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210713001349916.png)

###### 7、limit（重点中的重点，分页查询全靠它）

1. limit是MySQL特有的，其他数据库中没有，不通用。（Oracle中有一个相同的机制，叫做rownum）。

2. limit取结果集中的部分数据，这是它的作用

3. 语法机制：

   limit  startIndex,  length

   ​	startIndex表示起始位置，从0开始，0表示第一条数据

   ​	length表示取几个

4. limit是sql语句最后执行的一个环节：

   select				  5

   ​		...

   from					1

   ​		...

   where				 2

   ​		...				

   group  by			3

   ​		...

   having				 4

   ​		...

   order  by			  6

   ​		...

   limit					  7

   ​		...;

5. ![image-20210713003440309](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210713003440309.png)

6. 

###### 8、创建表

建表语句的语法格式：

​				create  table  表名(

​						字段名1   数据类型，

​						字段名2   数据类型，

​						字段名3   数据类型，

​						.....

​					);

数据类型：

1. int             整数型  
2. bigint        长整型
3. float           浮点型
4. char            定长字符串
5. varchar       可变长字符串
6. date             日期类型
7. BLOB            二进制大对象（存储图片、视频等流媒体信息）
8. CLOB            字符大对象（存储较大文本，比如：可以存储4G的字符串）

###### 9、CRUD操作（增删改查）

###### 10、约束

1. 什么是约束？常见的约束有哪些？

   在创建表的时候，可以给表的字段添加相应的约束，添加约束的目的是为了保证表中数据的合法性、有效性、完整性。

   常见的约束有哪些呢？

   非空约束（not  null） ：约束的字段不能为NULL

   唯一约束（unique） ：约束的字段不能重复

   主键约束（primary  key）：约束的字段既不能为NULL，也不能重复

   外键约束（foreign  key）

   检查约束（check）：注意Oracle数据库有check约束，但是MySQL没有，目前MySQL不支持该约束。
   
2. 唯一性约束：唯一约束修饰的字段具有唯一性，不能重复。但可以为NULL。

3. 外键约束 ：**外键可以为NULL。** 

   ![image-20210716221500908](file://C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210716221500908.png?lastModify=1626528422)

###### 11、MySQL主键自增：（非常重要）

**这张表必须有主键**

create  table  t_user(

​		id  int  primary  key  **auto_increment**,   //  id字段自动维护一个自增的数字，从1开始，以1递增

​		username  varchar(255)

);



###### 12、存储引擎

1. MyISAM存储引擎：

   不支持事务，

   是mysql最常用的存储引擎，但是这种引擎不是默认的

   采用三个文件：

   - 存储格式的文件  xxx.frm
   - 存储表中数据的文件   xxx.MYD
   - 存储表中索引的文件   xxx.MYI

   优点：可被压缩，节省存储空间。并且可以转换为只读表，提高检索效率。

   缺点：不支持事务。

2. InnoDB存储引擎

   优点：支持事务、行级锁、外键等。这种存储引擎数据的安全得到保障。

   ![image-20210717205118219](file://C:/Users/17143/AppData/Roaming/Typora/typora-user-images/image-20210717205118219.png?lastModify=1626526418)

3. MEMORY存储引擎

   优点：查询速度最快

   缺点：不支持事务。数据容易丢失。因为所有数据和索引都是在内存当中。

###### 13、事务

1. 什么是事务？

   - 一个事物是一个完整的业务逻辑单元，不可再分。

   - 两条DML语句必须同时执行，或者同时失败，不允许出现一条成功，一条失败。

   - 要想保证两条DML语句同时成功或者同时失败，那么就需要使用数据库的“事务机制”。

2. 和事务相关的语句只有：DML语句。（insert   delete   update）

   为什么？因为他们这三个语句都是和数据库表中的“数据”相关的

   事务的存在是为了保证数据的完整性，安全性。

3. 假设所有的业务都能使用1条DML语句搞定，还需要事务机制吗？不需要事务。

4. 事务的特性？

   事务包括四大特性：ACID

   - A：原子性：事务是最小的工作单元，不可再分。
   - C：一致性：事务必须是保证多条DML语句同时成功或同时失败。
   - I：隔离性：事务A与事务B之间具有隔离。
   - D：持久性：说的是最终数据必须持久化到硬盘文件中，事务才算成功的结束。

5. 关于事务之间的隔离性

   事务隔离性存在隔离级别，理论上隔离级别包括4个：

   ​		第一级别：读未提交（read  uncommitted）

   ​				对方事务还没有提交，我们当前事务可以读取到对方未提交的数据。

   ​				**读未提交存在脏读现象：表示读到了脏的数据。**

   ​		第二级别：读已提交
   
   ​				对方事务提交之后的数据我方可以读取到
   
   ​				**这种隔离级别解决了：脏读现象**
   
   ​				**读已提交存在的问题是：不可重复读**
   
   ​		第三级别：可重复读
   
   ​				解决了：不可重复读问题
   
   ​				**存在的问题是：读取到的数据是幻象。**
   
   ​		第四级别：串行化读/序列化读
   
   ​				**解决了所有问题**
   
   ​				**效率低。需要事务排队。**
   
   oracle数据库默认的隔离级别是：读已提交。
   
   MySQL数据库默认的隔离级别是：可重复读
   
   

###### 14、索引

1. 什么是索引？有什么用？

   索引就相当于一本书的目录，通过目录可以快速的找到对应的资源。

   在数据库方面，查询一张表的时候有两种检索方式：

   - 第一种方式：全表扫描
   - 第二种方式：根据索引检索（效率很高）

   索引为什么可以提高检索效率呢？

   ​		其实最根本的原理是缩小了扫描的范围。

   索引虽然可以提高检索效率，但是不能随意的添加索引，因为索引也是数据库当中的对象，也需要数据库不断地维护。是有维护成本的。比如，表中的数据经常被修改就不适合添加索引，因为数据一旦修改，索引需要重新排序，进行维护。

   添加索引是给某一个字段，或者说某些字段添加索引。

   ![image-20210718151115120](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210718151115120.png)

   

2. 怎么创建索引对象？怎么删除索引对象？

   创建索引对象：

   create   index   索引名称  on  表名（字段名）;

   删除索引对象：

   drop  index  索引名称  on  表名;

3. 什么时候考虑给字段添加索引？（满足什么条件）

   - 数据量庞大。
   - 该字段很少的DML操作。
   - 该字段经常出现在where子句中。

4. 注意：主键和具有unique约束的字段会自动添加索引。

   根据主键查询效率较高。尽量根据主键检索。

5. 索引底层采用的数据结构是：B+Tree

6. 索引的实现原理？

   ![image-20210718154101008](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210718154101008.png)

   通过 B Tree 缩小扫描范围，底层索引进行了排序，分区，索引会携带数据在表中的“物理地址”，最终通过索引检索到数据之后，获取到数据之后，获取到关联的物理地址，通过物理地址定位表中的数据，效率是最高的。

   select  ename  from  emp  where  ename = 'SMITH';

   通过索引转换为：

   select  ename  from  emp  where  物理地址 = 0x3;

7. 索引的分类？

   单一索引：给单个字段添加索引

   复合索引：给多个字段联合起来添加一个索引

   主键索引：主键上会自动添加索引

   唯一索引：有unique约束的字段上会自动添加索引

8. 索引什么时候失效？

   select  ename  from  emp  where  ename  like '%A%';

   模糊查询的时候，第一个通配符使用的是%，这个时候索引是失效的。

###### 15、视图

1. 什么是视图？

   站在不同的角度去看数据。（同一张表的数据，通过不同的角度去看待）

2. 怎么创建视图？怎么删除视图？

   create  view  myview  as  select  empno, ename  from  emp;

   drop  view  myview;

   注意：只有DQL语句才能以视图对象的方式创建出来。

3. 对视图进行增删改查，会影响到原表数据。（通过视图影响原表数据的，不是直接操作的原表）

   可以对视图进行CRUD操作

4. 面向视图操作？

5. 视图的作用？

   视图可以隐藏表的实现细节。保密级别较高的系统，数据库只对外提供相关的视图，程序员只对视图对象进行CRUD。

6. DBA命令

   1. 将数据库当中的数据导出

      ![image-20210719014850016](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210719014850016.png)

   2. 导入数据

      ![image-20210719014909674](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210719014909674.png)

       

###### 16、数据库设计三范式（重点内容）

1. 什么是设计范式？

   设计表的依据，按照这个三范式设计的表**不会出现数据冗余。**

2. **三范式是什么**？

   1. 第一范式：任何一张表都应该有主键，并且每个字段原子性不可再分。

   2. 第二范式：建立在第一范式的基础上，所有非主键字段完全依赖主键，不能产生部分依赖。

      **多对多？三张表，关系表两个外键**。

   3. 第三范式：建立在第二范式的基础之上，所有非主键字段不能传递依赖于主键字段。（不要产生传递依赖）

      **一对多？两张表，多的表加外键**

3. **提醒：在实际的开发中，以满足客户的需求为主，有的时候会拿冗余换执行速度。**

4. 一对一怎么设计？

   1. 一对一设计有两种方案：主键共享![image-20210719021747444](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210719021747444.png)

   2. 外键唯一。

      ![image-20210719021829850](C:\Users\17143\AppData\Roaming\Typora\typora-user-images\image-20210719021829850.png)

   



















