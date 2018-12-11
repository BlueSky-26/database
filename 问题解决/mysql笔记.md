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



#### 5、

形式一：delete table <tablename>

形式二：truncate table <tablename>;

两条命令的区别点：形式一不重置 自增树形



命令：show create table <tablename>; 查看表结构信息
​            desc table <tablename>; 查看表结构



修改表的语句
1、给表新增或者修改指定列
alter table 



### mysql增加列，修改列名、列属性，删除列语句

alter table test rename test1; --修改表名  

alter table test add  column name varchar(10); --添加表列  

alter table test drop  column name; --删除表列  

alter table test modify address char(10) --修改表列类型  

||alter table test change address address  char(40)  

alter table test change  column address address1 varchar(30)--修改表列名



### mysql表创建好后添加外键

命令：alter table 需加外键的表 add constraint 外键名 foreign key(需加外键表的字段名) references 关联表名(关联字段名);

注意：外键名不能重复



### 什么是外键

若有两个表A、B，id是A的主键，而B中也有id字段，则id就是表B的外键，外键约束主要用来维护两个表之间数据的一致性。所以外键其实就是一张表中含有的另一张表的主键字段。

A为基本表，B为信息表

































