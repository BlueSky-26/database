## mysql安装命令

sudo apt-get install mysql-server
[centOS 安装mariadb]

### 配置mysql方法

使用命令mysql检查是否启动
systemctl status|start mysql

1、找回密码方式：
a.关闭数据库服务：systemctl stop mysql
b.在mysqld.cnf[my.cnf]文件中加的[mysqld]字段中加入skip-grant-tables(一般加在skip-external-locking的下面即可)
  参考位置：/etc/mysql/mysql.conf.d/mysqld.cnf
c.启动 systemctl start mysql  并使用mysql命令链接进入（d1和d2选一个走就ok）
  #d1.创建一个新用户并授权：grant all on *.* to 'python'@'%' identified by 'yourpassword';
  d2.找回密码（首选）
​     update mysql.user set plutin='mysql_native_password',authentication_string=password('yourpassword') where user='root';
e.刷新权限：flush privileges;需要使用exit命令退出mysql shell环境
f.进入配置文件：将bind 127.0.0.1 这一行注释掉，在行前加# 用以打开远程访问限制
  将skip-grant-tables注释掉
g.重启服务 systemctl restart mysql
h、验证：mysql -uroot -pyourpassword 或者 mysql -uroot -p

### 安装可视化mysql工具MySQL-workbench

如果你已经装好mysql的相关服务，那么直接使用如下命令即可安装：

sudo apt-get install mysql-workbench



### mysql使用

mysql数据库管理命令（mysql的命令均以分号结束）
show databases; 查看当前有哪些数据库
注意：mysql库的user表定义了用户以及权限，我们可以通过修改表的数据实现用户的新增以及授权操作
命令：use <databasename>; 将databasename指定的库作为当前工作库
命令：show tables; 查看当前库的列表
命令：select database(); 查看当前工作库
命令删除数据库：drop database <databasename>; 删除指定数据库

关于授权：上述d1 使用grant语句
​     grant 权限列举[all] on 库名.表名[*.*] to username@host[%|localhost] identified by 密码 [with grant option(给前面的用户授予授权的权力)]

### 表操作：

#### 1、创建表：

create table tablename(列名 数据类型 约束条件，列名 数据类型 约束条件)charset=utf8 指定表内容字符编码集

create table cart(
uid int(11) not null, 
id int(11) not null primary key auto_increment, 
account float(2) default 0, 
result float(2) default 0
)charset=utf8;



##### 重要约束选项：

 *primary key 主键约束 该列将作为主键使用（该列的值不能重复）。
 unique 唯一约束 允许 null重复出现。
 *auto_increment 自增约束，当该列为整形时 值自增。
 *foreign key 外键约束 主要用来实现表与表之间的关系。
 *not null 非空约束  该列内容不允许空值。

##### 数据类型：

 int(n<11)  定义一个n位的整数
 varchar(n<60000) 定义一个长度为n个字节的字符串类型
 float(n) 定义一个小数为n位的浮点数
 text()  定义一个text类型的数据
 double(m,n) 定义一个长度为m 小数位为n的双精度浮点数

#外键约束定义：
外键在从表中定义，定义时需要注意  外键列的数据类型必须和参照列的类型一致（数据长度、编码长度、数据类型）
constraint [约束名] foreign(外键列名) references<主表名>(<参照列的名字>)



#### 2、表内数据添加：

形式一：insert into <tablename> (列名1,列名2,...) values(value1,value2,...)
注意：value与列的对应关系，外键约束关系，字段约束



形二：insert into <tablename> values(value1,value2,...);
注意：不推荐该形式，value和列进行对应，和对应顺序有关



#### 3、更新数据：

update <tablename> set 列名1=value,列名2=value,...... where 列名=列值
#更新指定列的值等于列值的数据的指定列



#### 4、删除表数据

delete from <tablename> where 条件 #删除指定表中符合where子句条件的数据行



#### 5、清除表内容

形式一：delete table <tablename>

形式二：truncate table <tablename>;

两条命令的区别点：形式一不重置 自增树形



命令：show create table <tablename>; 查看表结构信息
​            desc table <tablename>; 查看表结构



### mysql增加列，修改列名、列属性，删除列语句

alter table test rename test1; --修改表名  

alter table test add  column name varchar(10); --添加表列  

alter table test drop  column name; --删除表列  

​       alter table test modify address char(10) --修改表列类型  
​       alter table test change address address  char(40)  

alter table test change  column address address1 varchar(30)--修改表列名



### mysql表创建好后添加外键

命令：alter table 需加外键的表 add constraint 外键名 foreign key(需加外键表的字段名) references 关联表名(关联字段名);

注意：外键名不能重复



### mysql 如何修改、添加、删除表主键

在我们使用mysql的时候，有时会遇到须要更改或者删除mysql的主键，我们能够简单的使用alter table table_name drop primary key;来完成。以下我使用数据表table_test来作了样例。
1、首先创建一个数据表table_test：
create table table_test(
`id` varchar(100) NOT NULL,
`name` varchar(100) NOT NULL,
PRIMARY KEY (`name`)
)ENGINE=MyISAM DEFAULT CHARSET=gb2312;
2、如果发现主键设置错了,应该是id是主键,但如今表里已经有好多数据了,不能删除表再重建了，仅仅能在这基础上改动表结构。
先删除主键
alter table table_test drop primary key;
然后再增加主键
alter table table_test add primary key(id);
注:在增加主键之前,必须先把反复的id删除掉。



### 什么是外键

若有两个表A、B，id是A的主键，而B中也有id字段，则id就是表B的外键，外键约束主要用来维护两个表之间数据的一致性。所以外键其实就是一张表中含有的另一张表的主键字段。

A为基本表，B为信息表



## 181212-week3

select [column1,column2,......] 指定要显示的列

from 表1 链接关键字 表2 on 表1.column=表2.column 将两张表按照关键字指定的方式以on 指定的链接进行拼接形成一个新的数据表（虚表）

链接关键字：
1.cross join  叉乘（前面表的每一行和后面表的每一行构成一个新数据）
2.left join  左连（以左边的表为主表，主表每一行必须出现，若主表的行没有对应的从表数据，则从表位置空但会打出，若主表没有行对应从表则从表行丢弃）
3.right join  右连（以右边的表为主表，主表每一行必须出现，若主表的行没有对应的从表数据，则从表位置空NULL，若主表没有行对应从表则从表行丢弃）
4.inner join  内联（左右没有主从之分，没有匹配到条件则丢弃，没有on约束过滤则等价于叉乘）
5.union  联合查询，该关键字前后分别为一个完整的select语句，其结果是将所查询的结果组成一个表输出



### 通过关系表左链接

select a.Name,a.Title,c.CourseName
from Teacher a left join Tea_Cour b 
on a.idTeacher=b.idTea left join Course c 
​         on b.idCou=c.idCourse;



select * from Student where StudentName regexp '^d';
regexp  正则表达式 
‘  ’里面写正则表达式



### where条件

>   <  >=  <=  !< !> = != <> 
>   between and
>   not betewwn and
>   or 
>   and
>   like
>   regexp
>   in
>   not in
>   not

select 聚合：max（求最大） min（求最小） sum（求和） avg（求平均） count（求数目）
聚合使用以上聚合函数，聚合函数的参数为列名，意味这使用那个列进行聚合。



### 分组

group by column   分组语句在where过滤之后 直接分组不加where

```mysql
select a.Name,avg(d.score) 
from Teacher a left join Tea_Cour b  
on a.idTeacher=b.idTea left join Course c 
on b.idCou=c.idCourse  left join Stu_Cour d 
on c.idCourse=d.Cou_id 
group by a.Name;
```

对于分组结果使用having语句进行过滤
`注意`：除聚集计算语句(max、min、count、avg、sum)外，select语句中的每个列名都必须在group by子句中给出，未在这两个地方提到的列名将产生错误【因为你最后选取的字段一定是分组后有的字段才可以】
`另外`：having后面也是对组进行操作，注意条件字段名

```mysql
SELECT DEPT, EDLEVEL, MAX( SALARY ) AS MAXIMUM
FROM staff
WHERE HIREDATE > '2010-01-01'
GROUP BY DEPT, EDLEVEL
ORDER BY DEPT, EDLEVEL
```



### 排序

order by column desc(降序)   asc(升序)



### 条数限制(分页查询)

limit n       显示前n条
limit m,n  从第m+1条开始显示n条



### sql查询语句格式

```mysql
select  字段1,字段2,字段3,......
from    table 或者 table1 left join table2  .......
[WHERE…]
[GROUP BY…]
[HAVING…]
[ORDER BY…]
[WITH OWNERACCESS OPTION]
```



#### 顺序

先from-->where-->group by-->having-->order by-->limit-->select



### 事务

#### 数据库引擎(mysql)

innodb      慢     持久化(磁盘)         支持事务       分布式        行锁     死锁问题低
myIsam    快      持久化(磁盘)        不支持事务    少量数据    表锁     死锁问题高
memory   最快  非持久化(内存)     不支持事务    缓存

查询当前表的引擎：show create table <tablename>;
查询DBMS支持的数据引擎：show ENGINES;



#### 事务：保证数据完整性和insert  update  delete语句的执行有关

同一个事务中的所有语句要不全部成功，要不都不成功
具有的特征：
原子性
一致性
隔离性
持久性
事务的开启：begin
事务的回滚：rollback
事务的提交：commit



### ***补充索引：

在建库的时候创建索引列

create tabel <tablename>(
...............
name varchar(20) not null,
index iname(name),
...............
)

当创建完成之后，通过语句添加索引：create index <indexname> on <tablename>(<column[(num)]>)
给tablename指定的表使用column列的前num个字符创建一个名为indexname的索引

































