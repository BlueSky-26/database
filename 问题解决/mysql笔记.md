### mysql安装命令

sudo apt-get install mysql-server
[centOS 安装mariadb]


--------------------配置mysql方法--------------------

使用命令mysql检查是否启动
systemctl status|start mysql

1、找回密码方式：
a.关闭数据库服务：systemctl stop mysql
b.在mysqld.cnf[my.cnf]文件中加的[mysqld]字段中加入skip-grant-tables(一般加在skip-external-locking的下面即可)
  参考位置：/etc/mysql/mysql.conf.d/mysqld.cnf
c.启动 systemctl start mysql  并使用mysql命令链接进入（d1和d2选一个走就ok）
  #d1.创建一个新用户并授权：grant all on *.* to 'python'@'%' identified by 'yourpassword';
  d2.找回密码（首选）
     update mysql.user set plutin='mysql_native_password',authentication_string=password('yourpassword') where user='root';
e.刷新权限：flush privileges;需要使用exit命令退出mysql shell环境
f.进入配置文件：将bind 127.0.0.1 这一行注释掉，在行前加# 用以打开远程访问限制
  将skip-grant-tables注释掉
g.重启服务 systemctl restart mysql
h、验证：mysql -uroot -pyourpassword 或者 mysql -uroot -p



