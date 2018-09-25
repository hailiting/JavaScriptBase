## 1,下载并安装MySQL官方Yum Repository
下载
~~~
wget -i -c https://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
~~~
安装Yum Repository
~~~
yum -y install mysql57-community-release-el7-10.noarch.rpm
~~~
安装MySQL服务器
~~~
yum -y install mysql-community-server
~~~
## 2，MySQL数据库设置
启动MySQL
~~~
systemctl start mysqld.service
~~~
查看MySQL运行状态
~~~
systemctl status mysqld.service
~~~
登陆mysql
~~~
mysql -uroot -p // 这里需要密码
~~~
方法1,找到root的密码
~~~
grep "temporary password" /var/log/mysqld.log
// root@localhost: 后的全部字符串
~~~
方法2,强制修改mysql密码
~~~
1,systemctl stop mysqld
2,systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"
3,systemctl start mysqld
4,mysql -u root
5,UPDATE mysql.user SET authentication_string=PASSWORD('MyNewPassword')WHERW User='root' AND Host='localhost';
注： ERROR 1819(HY000),说明密码不符合安全要求
6，FLUSH PRIVIEGES;
7 quit
~~~
 

