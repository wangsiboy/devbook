### linux，不得不手动开启80端口的访问授权

查看CentOS防火墙信息：

`/etc/init.d/iptables status`

添加对80端口的开放：

`/sbin/iptables -I INPUT -p tcp --dport 80 -j ACCEPT`

然后保存规则并重启防火墙：

`/etc/rc.d/init.d/iptables save`

`/etc/init.d/iptables restart`

