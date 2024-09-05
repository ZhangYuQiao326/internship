// 2024-4-8 重新学习mysql

![image-20240408120409737](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240408120409737.png)



[参考资料](E:\typora索引文件\sql\mysql数据库课件.pdf)



## 1 cmd启动/关闭服务/登录账号

```mysql
# 启动/关闭服务
net start mysql80
net stop mysql80
```

```mys
mysql -h 主机名 -P 端口号 -u 用户名 -p 密码
mysql -h localhost -P 3306 -u root -p
123456
```

注意： 

（1）-p与密码之间不能有空格，其他参数名与参数值之间可以有空格也可以没有空格。

（2）密码建议在下一行输入，保证安全

（3）客户端和服务器在同一台机器上，所以输入localhost或者IP地址127.0.0.1。同时，因   

​    为是连接本 机： -hlocalhost就可以省略，如果端口号没有修改：-P3306也可以省略

## 2 命令行导入数据库

```sql
souce D:/mysql.sql
```

## 3 创建/查看数据库/表格

```sql
show databases;
create database db;
drop database db;
use db;

show tables;
//(名称、类型、约束)
create table user(id int unsigned primary key not null auto_increment,
				  name varchar(50) not null,
				  age tinyint not null,
				  sex enum('M','W') not null)
				  engine=INNODB default charset=utf8;
drop table user;
// 查看表头结构
desc user;
// 查看创建表的sql语句,\G结尾
show create table user \G

select(distinct) [字段] as [新字段]                  -----1

from mytb1 as tb1 join mytb2 as tb2 on [条件]		  -----2
where [过滤、不聚合函数]
group by [字段]
having [过滤，有聚合函数]

order by [字段]                                     -----3
limit[条数]

```

* 执行顺序 2 -> 1-> 3
* 在select as中的别名，无法在from中使用，可以在order中使用
* 统一在from中起别名

### 增删改

```mysql
# auto_increment自动增长的键不用用户输入，自行增长
insert into user(name,age,sex) values('张三',12,'M');


delete from user where age between 20 and 22;
delete from user; // 清空表

update user set age=23 where name='zhang san';
update user set age=age+1 where id=3;

```

### 3.1 单表查询

#### 1 去重

```mysql
select distinct name from user;
```

#### 2 limit

```mysql
select name from user limit 3;   # 取前3条  （0，3）0开始，取3条
select name from user limit 1,4;  # 从1开始，取4条
```

* 在没有索引的情况下，limit可以优化查询效率
* 没有索引，使用where过滤，需要搜寻整张表
* 没有索引，使用where过滤，加上limit 1，搜索到第一条满足的记录就会停止

分页：

```mysql
# 每页20条
select * from user limit (page - 1)*20, 20;
# 问题： 偏移量的部分需要全部搜寻，导致越往后的页加载越慢
# 解决： 通过where+索引列进行过滤
select * from user where id > '前一页最后一条数据id' limit 20;
```

内联: 无法使用where提高效率，使用内联

```mysql
select * from user a
join (select id from user) b
on a.id = b.id;
```



#### 3 order by

```mysql
select name from user order by age asc; #默认升序
select name from user order by age desc;
```

* orderby的效率和 select的数据 和 排序基于的数据有关
* `select key from user order by key`, 是通过索引排序，效率高(索引树以及按照key进行排序，此时直接搜索)
* 其他情况，是通过外文件排序`using filesort`，效率低 

#### 4 group by

```mysql
select age from user group by age;
```

* group by 会默认排序，若是按照非索引键排序，会使用外排序`using filesort`效率低
* 通过索引键分组，会按照索引排序`using index`，效率高

### 3.2 多表连接查询

#### 1 内联查询

* 表重命名
* 流程：通过小表来查大表，小表全部扫描（索引没用），然后去大表搜寻

```mysql
select a.uid, a.name, b.cid, b.course from stu a 
join scores b on a.uid = b.uid
```

![image-20240409161922330](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240409161922330.png)

```mysql
select a.uid, a.name, b.cid, b.course from stu a 
join scores b on a.uid = b.uid
where a.uid = 2;
```

* 流程：当有where时，先执行where，得到最终的大小表，遍历小表所有，用小表搜寻大表

![image-20240409162114370](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240409162114370.png)

* inline join可以优化limit的查询效率

#### 2 左连接、右连接查询

* 输出左侧左右的数据，若是没有在右表中出现，则右表字段设为NULL

* 左连接和右连接 和 内联的不同点： 内联的过滤条件可以放在where 和 on 后，一样

  ​															左右连接的过滤必须放在on后用and连接，where之后只判断为null的情况

  ```mysql
  select a.* from student a left join exame b on a.uid = b.uid and b.cid = 3 where b.cid is NULL;
  ```

  

### 3.3 聚合函数

* 聚合函数一般结合分组

```sql
max()  min()  avg()  sum() count()  
```

select后面跟聚合函数字段的情况：

1、聚合函数操作的字段

```sql
select count(num) from table group by name;
```

2、被分组的字段+聚合函数操作的字段

```sql
select name,count(num) from table group by name;
```



## 4 数据类型、约束、范式

### 六大约束

* 创建表的时候设置字段的属性

* 外键约束基本不用（多张表关联）

  ![image-20240408161112747](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240408161112747.png)



![image-20240408161159307](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240408161159307.png)

在 MySQL 中创建表时设置主键的作用主要有以下几点：

1. **唯一性保证**：主键的值必须是唯一的，这意味着两行不能有相同的主键值。这个特性帮助保持数据的完整性，确保每一行都可以被唯一识别。

2. **索引**：主键自动成为表的一个索引。这使得基于主键的查询非常快速，因为数据库可以利用索引直接定位到数据的存储位置，而无需扫描整个表。

3. **关系完整性**：在关系型数据库中，表之间通过主键和外键建立关系。外键在一个表中指向另一个表的主键，这种机制支持将数据的完整性约束从一个表扩展到多个表，确保了数据库中数据的一致性和准确性。

4. **自增特性**：对于自增主键（通常是整数类型），数据库管理系统会在新行添加到表中时自动为该行生成一个唯一的主键值。这简化了新数据插入操作，因为用户不需要手动创建一个唯一的主键值。

```mysql
// 设置单个主键
CREATE TABLE Students (
    StudentID INT NOT NULL,
    Name VARCHAR(100),
    Age INT,
    PRIMARY KEY (StudentID)
);
// 设置联合主键
CREATE TABLE Enrollments (
    StudentID INT NOT NULL,
    CourseID INT NOT NULL,
    EnrollmentDate DATE,
    PRIMARY KEY (StudentID, CourseID)
);

```



### 四大范式

* 设计表时所需要遵循的规则

  1. **每一列保持原子特性** （满足关系型数据库）

     | id   | addr     |
     | ---- | -------- |
     | 11   | 山西运城 |

     修改：addr可以再拆分

     | id   | 省份 | 城市 |
     | ---- | ---- | ---- |
     | 11   | 山西 | 运城 |

  2. **一张表内的所有属性要完全依赖于主键**(均与主键有关系)

     id 与 课程联合主键

     | id   | 性别 | 课程 | 学分 |
     | ---- | ---- | ---- | ---- |
     | 1    | 男   | os   | 2    |

     修改：性别 与 课程无关、学分与id无关

     | id   | 性别 |
     | ---- | ---- |
     | 1    | 男   |

     | 课程 | 学分 |
     | ---- | ---- |
     | os   | 2    |

     | id   | 课程 |
     | ---- | ---- |
     | 1    | os   |

  3. **属性之间不能相互依赖**

  4. BC范式：**每一个表只有一个候选键**：每一个表中只有一个属性的值完全不同，其余所有的属性都有重复的

  5. **消除表中的多余依赖**

     | id   | skill      |
     | ---- | ---------- |
     | 1    | c++ golang |
     | 2    | c++ java   |

     修改：

     | 1    | c++    |
     | ---- | ------ |
     | 1    | golang |
     | 2    | c++    |
     | 2    | java   |

## 5 存储引擎、索引

### 5.1 引擎对比

MySQL的存储引擎是一种**数据表存储和处理机制的实现**。不同的存储引擎提供不同的数据表操作功能和性能优化，选择适合的存储引擎可以对数据库的性能和行为产生显著影响。

**MyISAM：**

不支持事务、也不支持外键，索引采用非聚集索引，其优势是访问的速度快，对事务完整性没 有要求，以 SELECT、INSERT 为主的应用基本上都可以使用这个存储引擎来创建表。MyISAM的表在磁 盘上存储成 3 个文件，其文件名都和表名相同，扩展名分别是：

| 后缀名 | 存储类型        |
| ------ | --------------- |
| .frm   | 存储表定义      |
| .MYD   | mydata 存储数据 |
| .MYI   | myindex存储索引 |

**Innodb:**存储引擎提供了具有提交、回滚和崩溃恢复能力的事务安全，支持自动增长列，外键等功能， 索引采用聚集索引，索引和数据存储在同一个文件，所以InnoDB的表在磁盘上有两个文件，其文件名 都和表名相同

| 后缀名 | 存储类型       |
| ------ | -------------- |
| .frm   | 存储表定义     |
| .ibd   | 存储数据和索引 |

**具体的引擎对比**

| 存储引擎 | 锁机制   | B树索引 | 哈希索引 | 外键     | 事务     | 索引缓存 | 数据缓存 |
| -------- | -------- | ------- | -------- | -------- | -------- | -------- | -------- |
| MyISAM   | 表锁     | 支持    | 不支持   | 不支持   | 不支持   | 支持     | 不支持   |
| InnoDB   | ==行锁== | 支持    | 不支持   | ==支持== | ==支持== | 支持     | 支持     |
| Memory   | 表锁     | 支持    | 支持     | 不支持   | 不支持   | 支持     | 支持     |

锁机制：表示数据库在并发请求访问的时候，多个事务在操作时，并发操作的粒度。

 B-树索引和哈希索引：主要是加速SQL的查询速度。

外键：子表的字段依赖父表的主键，设置两张表的依赖关系。 

事务：多个SQL语句，保证它们共同执行的原子操作，要么成功，要么失败，不能只成功一部分，失败 需要回滚事务。 

索引缓存和数据缓存：和MySQL Server的查询缓存相关，在没有对数据和索引做修改之前，重复查询 可以不用进行磁盘I/O（数据库的性能提升，目的是为了减少磁盘I/O操作来提升数据库访问效率），读 取上一次内存中查询的缓存就可以了。



### 5.2 索引

#### 1 优缺点

优： 当数据量非常大时，遍历查询耗时，使用索引加速查询，生成索引后，会按照索引将数据进行排序



缺：

* 索引也需要生成索引文件，使用索引需要访问索引文件，涉及io操作，使用不当，会造成SQL查询时，进行大量无用的磁盘I/O操作，降低了SQL的查询效率
* 当索引非常多的时候，对数据的增删改都会让索引重新排序，也会增大大量io操作，降低效率

* 索引只与where过滤的字段有关



#### 2 分类

物理：聚集索引（Innodb的数据和索引放在一个文件内）

​			非聚集索引（MyISAM的数据和索引分开存放）

逻辑：一级索引：单列索引（主键索引primary kry、唯一索引unique）、联合索引

​			二级索引：普通索引，可以给任意字段创建普通索引



==一次sql查询只能用一个索引==

| 一级索引 | 分类                                                         |
| -------- | ------------------------------------------------------------ |
| 单列索引 | 主键索引primary key、唯一性索引unique，会自动创建索引        |
| 联合索引 | primary key(id, name)， innodb默认创建主键                   |
| 全文索引 | 用于搜索字符串文本，不常用，全文搜寻使用搜索引擎（workflow） |

| 二级索引 | 分类                             |
| -------- | -------------------------------- |
| 普通索引 | 可以给任何字段创建索引，数量不限 |

#### 3 使用

* 创建\销毁二级索引

  ```mysql
  CREATE TABLE index1(id INT,
  name VARCHAR(20),
  sex ENUM('male', 'female'),
  INDEX(id,name)); // 创建普通索引
  
  # 在已经存在的表上创建索引
  create index 'nameidx' on student('name');
  
  # 删除索引
  drop index 'nameindx' on student;
  ```
  
  
  
### 5.3 explain检查sql的信息

  ```
  > explain select * from student where uid == 2;
  ```

  ![image-20240711230106997](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240711230106997.png)

| select_type                     | table                    | type                               | ref  | Extra |
| ------------------------------- | ------------------------ | ---------------------------------- | ---- | ----- |
| simple: 简单查询不需要union     | 查询表名                 | const:唯一索引/主键索引            |      |       |
| primary: 1个需要union或者子查询 | null: 不涉及对数据库操作 | ref: 辅助索引、普通索引            |      |       |
| union： 连接的两个select        | <>: 临时表               | range：范围索引，between、in、like |      |       |

* possible_keys: 可用的索引
* key ： 最后使用的索引
* rows： 扫描的行数 

![image-20240711231132396](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240711231132396.png)

* name没有索引，进行整表扫描

#### 4 总结

1. 为经常作为where条件过滤的字段添加索引
2. 字符串列创建索引时，尽量规定索引的长度，而不能让索引的长度key_len过长
3. 当索引字段涉及类型强转，mysql的函数调用、表达式计算等，索引就失效



### 5.3 B树（Blance）



![image-20240411010616414](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411010616414.png)

本质：m阶平衡树（300-500），一次磁盘IO读取的磁盘块内容，刚好存储在B树的一个节点，尽量保证在3层

1. 节点的大小通常等于一个磁盘块的大小，可存放300-500个索引

2. 通常最多有三层，进行三次IO操作

3. ==data区域==的存储内容

   MYISam: 索引数据分离，data存储数据在磁盘上的地址

   INNOdb：data存储的是数据本身

4. `select * from tbale where uid == 1;`查询步骤

>* 当where过滤的字段并非索引字段：
>  * MyISAM: 此时只有.myd文件存储数据，对所有数据==进行遍历==
>  * Innodb：有.ibd文件，自动生成索引且存放数据，但是过滤字段并非索引，对==整张表==进行过滤
>* 当where过滤字段是索引字段：
>  * MyISAM：mysql_server识别到为索引字段 -> 从磁盘（.MYI文件）取出一个磁盘块（一个节点大小）放入内存 ->内存中构建B树（节点中的data存放的是数据的地址，通过地址在.MYD中寻找）-> 通过二分查找加速过滤寻找
>  * Innodb： 识别索引 -> 从Ibd文件中取出索引和数据放入内存 ->  内存中构建B树（data存放具体的数据）->==二分查找==
>
>* 当重新设置字段为辅助索引
>  * 重新按照辅助索引，构建索引树

| 存在问题(Inodb为例)                                          | q    |
| ------------------------------------------------------------ | ---- |
| 索引数据分散在不同的节点上，离根近，则搜索快，导致磁盘IO次数不平均 |      |
| 每一个非叶子节点除了存储索引，还需要存储data，占用过多的空间，从而导致B树较高 |      |
| 不方便进行整表遍历和范围遍历，遍历树没有遍历链表或者数组方便 |      |

### 5.4 B+树

![image-20240411012040271](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411012040271.png)

| 改善                                                         | p                |
| ------------------------------------------------------------ | ---------------- |
| 非叶子节点只存放索引，不存放data，一个节点内存放的索引增加，B+树层数变低，IO次数变少 |                  |
| data全部存放在叶子节点上，保证每行的搜索时间平均             | `where uid == 1` |
| 将叶子节点串在链表中，形成有序链表，需要对data进行范围或整表遍历时，只需要遍历链表 | `where uid < 4`  |

* MyISAM: 主键索引树和辅助索引树的data内均==存放数据==的地址

### 5.5 辅助索引

#### 1 InnoDB

![image-20240411112707624](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411112707624.png)

* 主键索引 primary key

​	存在主键索引时，则mysql server让内核在内存中构建主键索引树

​	where过滤字段为主键索引，则二分查找快速定位，若非索引，则遍历搜索树的叶子节点链表

| 索引类型          | 存储                                             |
| ----------------- | ------------------------------------------------ |
| 主键索引          | 叶子节点存储：主键uid索引    ； data存放完成数据 |
| 辅助索引/二级索引 | 叶子节点：辅助索引age   ；data存放主键uid        |

1. 辅助索引树内只有字段：主键 和 索引字段（uid，age）
2. 若`select uid sex from user where age = 12;`需要==回表==，根据age 查到uid，从主键索引树查找data内的sex
3. 为了减少回表带来的损耗，则select选择具体的字段值，不要使用*

#### 2 myIsam

![image-20240714153838689](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240714153838689.png)

1. 主键索引和辅助索引树基本一样
2. 都是从磁盘根据地址获取data

### 5.5 联合索引

`select * from user where age = 20 order by name;`

1. 若只添加age为辅助索引，虽然可以查找到对应的数据

2. 通过name排序时，会`using filesort`外部排序，开销大

3. 使用联合索引，将age和name均设为索引，索引树先按age排序，再按name排序

4. 此时可以直接搜找data，无需using filesort

### 5.6 自适应哈希索引

![image-20240411133457805](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411133457805.png) 

1. 哈希索引只能==等值查询==效率很高，但无法使用排序、范围搜索等操作，因为在不同的哈希桶中
2. 只适合搜索在==内存==中的数据，无法减少IO操作
3. 优化为Innodb的自适应哈希索引

-----

![image-20240411134225846](https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411134225846.png)

* 当大量使用==辅助索引树==的时候，辅助索引->回表->关键索引->获取data数据
* 当innodb引擎检测到，同样的二级索引不断被使用，那么会根据二级索引在==内存==上创建哈希索引，拉加速搜索
* 在内存中优化，根据==辅助索引树==创建==哈希表索引==，直接通过哈希索引值得到data数据
* 自适应哈希本身数据维护也是==耗费性能==，不是任何时候打开哈希索引，都会加速查询效率。根据需求是否打开自适应哈希

```mysql
show engine innodb status\G
1. 自适应哈希默认8个分区，可以查看等待线程的树木
2 走自适应哈希索引搜索的频率 和 走二级索引树的搜索频率，觉得是否关闭
```

<img src="https://cdn.jsdelivr.net/gh/ZhangYuQiao326/study_nodes_pictures@main/img/image-20240411135757840.png" alt="image-20240411135757840" style="zoom:67%;" />

   ## 6 日志

### 6.1 慢查询日志

* 用来记录SQL执行时间超过指定值
* 通过在慢查询日志中explain分析语句，判断为什么效率低下

```mysql
#打开慢查询日志开关
mysql> show variables like '%slow_query%';
+---------------------+--------------------------+
| Variable_name       | Value                    |
+---------------------+--------------------------+
| slow_query_log      | ON                       |
| slow_query_log_file | LAPTOP-M2JC4G2K-slow.log |
+---------------------+--------------------------+

# 若是关闭的则打开
# 以全局的方式打开，所有session均打开
set global slow_query_log = on;

# 查看最长时间
mysql> show variables like 'long_query%';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
# 设置最长sql语句执行时间，单位s
set slow_query_time = 0.01;  # 10ms
```

* 通过profiles显示更加精确的sql执行时间

```mysql
show variables likt 'profiling';
+---------------+-------+
| Variable_name | Value |
+---------------+-------+
| profiling     | OFF   |
+---------------+-------+
# 打开
set profiling=on;

执行sql

# 查看精细的时间
show profiles;
```

## 7 事务

事务：一个事务是由一条或多条sql组成的原子单元，执行时要么全部完成，要么全部失败。所有sql执行完毕后，才提交（commit）事务，写入磁盘，若是有错误，则需要回滚（rollback）到最初状态

**创建事务**

```mysql
# 1 设置手动提交任务
mysql> select @@autocommit;
+--------------+
| @@autocommit |
+--------------+
| 1 |
+--------------+
mysql> set autocommit=0;   # 1 自动提交，0 手动提交

```

```mysql
# 查看事务隔离界别
select @@tx_isolation;

# 设置事务隔离界别
set tx_isolation = 'REPEATABLE-READ'
```

```mysql
begin; # 开启事务
try:
    select * from user where id = 1;
    select * from user wherer id = 2;

    commit;  # 执行完毕，提交任务，数据写入cache
catch:
 rollback; # 任务执行失败，回滚到开始位置
 
 // 设置事务隔离级别
 set
```

**ACID特性**：

| 特性   | 介绍                                                         |
| ------ | ------------------------------------------------------------ |
| 原子性 | 事务是一个整体，要么全部执行，要么全部不执行   undo log 回滚日志 |
| 一致性 | 事务执行前后，数据库必须保持一致性，及不允许事务在执行过程中，数据库数据更改 |
| 隔离性 | 当多个事务并发执行时，保证数据的安全，各个事务之间不能影响   |
| 持久性 | 事务执行完成之后，数据==》cache ==》磁盘，必须保证这个过程中数据仍然存在（停电 ）redo log重做日志 |

**若没有隔离性，并行造成的危害**

| 危害       | 介绍                                                         |
| ---------- | ------------------------------------------------------------ |
| 脏读       | 事务B读取了事务A执行过程中的中间数据（未提交数据）（==脏数据==，之后会被A修改）---必须解决 |
| 不可重复读 | 事务B读取了事务A提交后的数据，事务A再次修改，导致B==两次读入的单个数据值不同==---A的90分变98分 |
| 幻读       | 事务B读取了数据后，A对数据插入或删除，导致B两次读取的==数据个数==不一样--20条数据变10条数据 |

* 不可重复读和幻读根据情况可接受
* 脏读不能接受

**由此设置隔离级别，保证并发时的数据安全**

* orcle默认在已提交读,不允许脏读，允许不可重复读、幻读
* mysql默认在可重复读，只允许幻读

| 隔离级别                       |          | 介绍                         |
| ------------------------------ | -------- | ---------------------------- |
| `TRANSACTION_READ_UNCOMMITTED` | 未提交读 | 允许B在A未提交时候读数据     |
| `TRANSACTION_READ_COMMITTED`   | 已提交读 | 只允许B在A提交后读数据       |
| `TRANSACTION_REPEATABLE_READ`  | 可重复读 | 保证B多次读取数据保持一致    |
| `TRANSACTION_SERIALIZABLE`     | 串行化   | 让所有事务串行执行，不会并发 |

| 隔离级别 | 脏读   | 不可重复读 | 幻读               |
| -------- | ------ | ---------- | ------------------ |
| 未提交读 | 可以   | 可以       | 可以               |
| 已提交读 | 不可以 | 可以       | 可以               |
| 可重复读 | 不可以 | 不可以     | 可以，部分解决幻读 |
| 串行化   | 不可以 | 不可以     | 不可以             |

* 事务等级越高，性能花费越高

* 可重复读，可以==部分解决==幻读问题（事务A插入 删除数据，事务B查找的数据量不变），

  但是不能防止==（update）更新==产生的虚读，update更新查询后，A插入删除的数据会被B查到，造成幻读



## 8 锁机制




# n 面试题

> **1 mysql的服务器模型采用select + 线程池模型，为什么不适用epoll+线程池？**
>
> 考虑到mysql不仅向内存存储数据，还要向磁盘存储，考虑到磁盘IO

> **2** **说一下范式数据库**
>
> 作用是规范数据库字段的设计
>
> 最主要的优点就是**减少数据冗余**，其次：2 消除异常（插入、更新、删除异常）3 使数据组织更和谐
>
> 范式1 每一列保持原子属性，这是保持关系型数据库的基本要求
>
> 范式2 所有的属性都要依赖于主键
>
> 范式3 属性之间不能相互依赖
>
> 范式4 消除表中的多余依赖
>
> BC范式：每一个表只有一个候选键



> **3 limit分页如何提高效率？**
>
> 优化where效率：在where过滤非索引列时候，会遍历整张表，加上limit n后，找到满足的n条数据后，不在搜寻后面的数据
>
> * limit的效率与 select 的数据量  和 偏移量有关
>
>   ```mysql
>   select * from user limit 1,10;   # select量影响效率
>   select id from user limit 100000,10; # 偏移量影响效率
>   ```
>
> 优化limit效率：使用limit分页时候，为了保证不造成“越往后的页，加载越慢”，通长用where过滤索引列，来避免偏移部分的全部遍历
>
> ```mysql
> select * from user where id > 1000000 limit 10;
> ```
>
> inlint join优化查询了过大的效率
>
> ```mysql
> select * from user a 
> join (select id from user limit 10000, 10) b  # 查找索引效率常数级
> on a.id = b.id; # 小表查大表，通过索引联合，效率高
> ```
>



> **4 设置主键的作用是什么？**
>
> 1. **唯一性保证**：主键的值必须是唯一的，这意味着两行不能有相同的主键值。这个特性帮助保持数据的完整性，确保每一行都可以被唯一识别。
>
> 2. **索引**：主键自动成为表的一个索引。这使得基于主键的查询非常快速，因为数据库可以利用索引直接定位到数据的存储位置，而无需扫描整个表。
>
> 3. **关系完整性**：在关系型数据库中，表之间通过主键和外键建立关系。外键在一个表中指向另一个表的主键，这种机制支持将数据的完整性约束从一个表扩展到多个表，确保了数据库中数据的一致性和准确性。
>
> 4. **自增特性**：对于自增主键（通常是整数类型），数据库管理系统会在新行添加到表中时自动为该行生成一个唯一的主键值。这简化了新数据插入操作，因为用户不需要手动创建一个唯一的主键值。
>
> 总之，主键是确保数据完整性和优化数据检索性能的重要机制。通过强制每行数据的唯一性，以及作为快速检索数据的索引



> **5 sql的索引优化，怎么切入？**
>
> 》怎么找到运行时间长、耗性能的sql，然后用explain分析
>
> * 首先打开慢查询日志，设置合适的慢查询时间，之后开始压测各种业务
>
> * 完毕之后查看慢查询日志，找到耗时的sql
>
> * 通过explain分析执行流程
>
> 》造成耗时的原因有：
>
> 1 where过滤没有索引的字段 
>
> 2 where过滤了索引字段，但是索引失效了（like通配符（%在后不失效）、not in、!=、使用函数、隐式类型转换、or语句）
>
> 优化：
>
> ​	1. 考虑给业务上经常where过滤的字段加索引
>
> 2. 对字符串字段建立索引， 规定索引长度，整的字符串作为索引，导致索引树文件过大 
> 3. where后的字段涉及到类型转换，则不能使用索引（比如字段为string，where password = 1000,为int，则无法使用索引）
> 4. order by排序时候，会出现using fileSort外部排序，影响性能，使用联合索引，将过滤字段+排序字段联合添加索引
> 5. 辅助索引时候，可能会回表，引擎根据辅助索引树在内存上创建哈希索引
> 6. 





> **6 为什么myisam存储引擎不会默认创建主键？innodb会默认创建主键？**
>
> myisam的表定义、数据、主键分三个文件存储
>
> innodb的表定义、数据和主键 分两个文件存储 



> **7 索引的底层结构,优势是什么？为什么不是，AVL,  红黑树， B树 ?**
>
> 
>
> 2000w的数据，使用AVL 需要25层，最坏情况下， 读取一个索引，需要花费25次磁盘IO。使用m=500的B+树，最多只需要3层
