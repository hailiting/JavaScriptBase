# Windows
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
