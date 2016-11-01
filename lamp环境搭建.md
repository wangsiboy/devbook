
解压 tar -zxvf filename.tar.gz
删除 rm -rf filename.tar.gz


---
问题汇总
* 修复数据库

 * ps -ef|grep mysql ，没有发现mysql的进程

数据库脚本目录：/usr/bin/mysql

mysqld目录：/etc/init.d/mysqld

查看状态：`service mysql status`

查看日志 `cat /var/log/mysqld.log`

检查3360端口占用情况：`netstat -apn|grep 3360`

lsof -i:3360 有没有占用3360端口的进程

killall mysql

启动数据库：service mysqld start

* 解决“table is marked as crashed and should be repaired”，

cd /var/lib/mysql

myisamchk -c -r ./ims_core_sessions.MYI
