Windows系统

安装：

* JAVA JDK

* tomcat

* mysql

* maven

配置JDK变量

* 在系统变量里新建变量名：JAVA\_HOME，变量值：E:\Development\Java\jdk1.8.0\_92

* 在系统变量里新建变量名：CLASSPATH，变量值：.;%JAVA\_HOME%\lib\dt.jar;%JAVA\_HOME%\lib\tools.jar;

* 在系统变量里打开PATH，添加“%JAVA\_HOME%\bin”和“%JAVA\_HOME%\jre\bin”

配置tomcat变量

* 在系统变量里新建变量名：CATALINA\_BASE，变量值：D:\tomcat\apache-tomcat-9.0.0.M9

在系统变量里新建变量名：CATALINA\_HOME，变量值：D:\tomcat\apache-tomcat-9.0.0.M9

在系统变量里打开PATH，添加变量值：%CATALINA\_HOME%\lib;%CATALINA\_HOME%\bin

* 打开cmd，进入tomcat下的bin目录，执行“service.bat install”

* 附：service卸载命令：service.bat remove

配置mysql

* 在系统变量里打开PATH，添加变量值：c:\mysql\mysql-5.7.21-winx64\bin

* 配置my.ini

```
[mysql]
#设置mysql客户端默认字符集
default-character-set=utf8
[mysqld]
#设置3306端口
port=3306
#设置mysql的安装目录
basedir=c:\mysql\mysql-5.7.21-winx64   --自己的路径
#设置mysql数据库的数据的存放目录
datadir=c:\mysql\mysql-5.7.21-winx64\data  --自己的路径
#允许最大连接数
max_connections=200
#服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8
#创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
```

管理员打开命令行：c:\mysql\mysql-5.7.21-winx64\bin&gt;mysqld --install mysql --defaults-file=C:\mysql\my.ini  
启动:net start MySQL \#\#\# 问题：mysqld --initialize-insecure --user=mysql 初始化data目录即可。

停止:net stop MySQL

卸载:sc delete MySQL, mysqld -remove

设置密码：

mysql -uroot -p

set password for root@localhost=password\(‘123'\);

# 解决远程连接mysql错误1130

```
mysql -u root -pvmware
mysql>use mysql;
mysql>update user set host = '%' where user = 'root';
mysql>flush privileges;
mysql>select host, user from user
```



配置maven

在系统变量里新建变量名：M2\_HOME和MAVEN\_HOME，变量值：C:\wangsi\apache-maven-3.5.2

PATH的最后添加：%M2\_HOME%\bin;%MAVEN\_HOME%\bin

