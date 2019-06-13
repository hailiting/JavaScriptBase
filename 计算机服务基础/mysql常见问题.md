# Server version: 5.7.26 MySQL Community Server (GPL)
## 用户操作
### 添加新的用户
~~~
mysql -u root -p
****
mysql> CREATE USER "test"@"localhost" IDENTIFIED BY "1234"; # 本地登录
// mysql> CREATE USER "test"@"%" IDENTIFIED BY "1234"; # 远程登录
Query OK, 0 rows affected (0.01 sec)
quit;
// 测试是否创建成功
mysql -u test -p 1234;
~~~
### 为用户授权
#### ``授权格式：grant 权限 on 数据库.*to 用户名@登录主机  identified by "密码"``
##### 1，用root登录
~~~
mysql -u root -p
~~~
##### 2，为用户创建一个数据库(testDB):
~~~
create database testDB;
create database testDB default charset utf8 collate utf8_general_ci;
~~~
##### 3，授权test用户拥有testDB数据库的所有权限
~~~
grant all privileges on testDB.* to "test"@"localhost" identified by "1234";
flush privileges;
~~~
#### 4，指定部分权限给用户：
~~~
grant select,update on testDB.*to  "test"@"localhost" identified by "1234";
~~~
#### 5，授权test用户拥有所有数据库的某些权限：
~~~
grant select,delete,update,create,drop on .to test@"%" identified by "1234"; # "%"表示对所有非本地主机授权，不包括localhost
~~~
### 删除用户
~~~
mysql -u root -p
Delete  FROM mysql.user Where User="test" and Host="localhost";
flush privileges;
drop database testDB;
~~~
##### 删除账户及权限
~~~
drop user 用户名@"%";
drop user 用户名@ localhost;
~~~
### 修改指定用户密码
~~~
mysql -u root -p
update mysql.user set authentication_string=password("新密码") where User="test" and Host="localhost";
~~~


# Windows
window 可视化根据 轻量级 HeidiSQL
## 1，初始密码不知道
~~~
1，关闭服务 net stop MySQL
2，用管理员身份打开cmd，输入 mysqld --skip-grant-tables
3，打开另一个cmd，登录 mysql -u root -p   密码为空，直接回车，就可以进去了。
~~~
## 2，Error: ER_NOT_SUPPORTED_AUTH_MODE: Client does not support authentication protocol requested by server; consider upgrading MySQL client
### 起因：mysql8.0加密方式的原因报错。
~~~
解决方法：
mysql> use mysql;
mysql> alter user 'root'@'localhost' identified with mysql_native_password by 'root的密码';
mysql> flush privileges;
~~~
### 3，查看mysql端口号
~~~
mysql> show global variables like 'port';
~~~
### 4，启动mysql 
~~~
net start mysql
~~~
