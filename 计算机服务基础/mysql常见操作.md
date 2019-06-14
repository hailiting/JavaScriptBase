# Server version: 5.7.26 MySQL Community Server (GPL)
## 1，用户操作
### 1.1  添加新的用户
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
### 1.2  为用户授权
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
##### 4，指定部分权限给用户：
~~~
grant select,update on testDB.*to  "test"@"localhost" identified by "1234";
~~~
##### 5，授权test用户拥有所有数据库的某些权限：
~~~
grant select,delete,update,create,drop on .to test@"%" identified by "1234"; # "%"表示对所有非本地主机授权，不包括localhost
~~~
### 1.3 删除用户
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
### 1.4 修改指定用户密码
~~~
mysql -u root -p
update mysql.user set authentication_string=password("新密码") where User="test" and Host="localhost";
~~~
## 2, 库操作
### 2.1.1 创建数据库
~~~
// mysql账户登录 
// 创建数据库
mysql> create DATABASE RUNOOB;
~~~
### 2.1.2 链接数据库，创建表单
~~~
// mysql
CREATE TABLE IF NOT EXISTS `runoob_tbl`(
  `runoob_id` INT UNSIGNED AUTO_INCREMENT,
  `runoob_title` VARCHAR(100) NOT NULL,
  `runoob_author` VARCHAR(40) NOT NULL,
  `submission_data` DATE,
  PRIMARY KEY ( `runoob_id` )
)ENGINE=InnoDB DEFAULT CHARSET=utf8;




// node
var mysql = require('mysql');
var connection =  mysql.createConnection({
  host: "localhost",
  user: "root",
  password: "******",
  database: "RUNOOB",
  port: "3306",
})
connection.connect(function(err){
  if(err){
    console.log("链接失败")
  } else {
    console.log("链接成功")
    connection.query("CREATE TABLE person(id int, user varchar(255), password varchar(255))", function(err,result){
      if(err){
        throw err;
      } else {
        console.log("创建表成功")
      }
    })
  }
})
~~~
### 2.1.3 删除数据库
~~~
mysql>drop table 库名
~~~

## 3，增删改查
###  3.1 增
#### 3.1.1 [插入单行]
~~~
insert into <表名> ( field1, field2, ...fieldN ) values ( value1, value2, ...valueN );
例：insert into runoob_tbl (runoob_title, runoob_author, submission_data) values ( "学习PHP", "cailiaojiaocheng", NOW() );

// => 读取数据
select * from runoob_tbl;
~~~


###  3.2 查
~~~
SELECT column_name,column_name 
FROM table_name
[WHERE Clause]
[LIMIT N][OFFSET M]
/* websites 表名    name alexa url country 字段 */
SELECT * FROM websites; /* 查询表所有数据 */
SELECT name FROM websites; /*查询表字段数据*/
SELECT * FROM website where name = "广西"; /*查询表字段下条件数据*/
SELECT * FROM website where like "_o%"; /*模糊查询*/
SELECT * FROM website where id BETWEEN "1" AND "5"; /*查询表下字段范围数据*/
SELECT * FROM websites WHERE name in ("广西","百度");    /* 查询表字段下固定条件数据 */
SELECT DISTINCT country FROM Websites;                  /* 查询去重值 */
SELECT * FROM Websites WHERE country = "USA" OR country="sh"; /* 查询表下条件不同值 */
SELECT * FROM Websites ORDER BY alexa;                      /* 查询表下值排序结果 */
SELECT * FROM Websites ORDER BY alexa DESC;                 /* 查询表下排序结果降序 */
SELECT * FROM Websites LIMIT 2;      /* 查询表下范围数据 */
SELECT name as zzz from websites;    /*别名查询表下数据*/
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
