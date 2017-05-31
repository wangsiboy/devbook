### 安装tomcat

下载地址：http://tomcat.apache.org/download-70.cgi

##### 上传后解压

tar -zxf apache-tomcat-7.0.73.tar.gz

##### 挪一下

mv apache-tomcat-7.0.73 /usr/local/tomcat



##### 启动tomcat



/usr/local/tomcat/bin/startup.sh



#####看下端口号，tomcat默认使用了8080



netstat -tunlp



##### 查询防火墙是否有打开8080端口



/etc/init.d/iptables status



(腾讯云没有开防火墙，以下无效)

添加使防火墙开放端口

vi /etc/sysconfig/iptables


-A RH-Firewall-1-INPUT -m state --state NEW -m tcp -p tcp --dport 8080 -j ACCEPT


####腾讯云安全组打开端口

新增出入规则，开放tcp 8080


#### 热部署

配置maven操作tomcat的权限，

访问 http://ip地址:8080/manager 无法登陆，

需要配置conf/tomcat-users.xml

在<tomcat-users>节点下，新增：

```
<role rolename="manager-gui" />

<role rolename="manager-script" />

<user username="tomcat" password="tomcat" roles="manager-gui, manager-script"/>

```
manager-gui - allows access to the HTML GUI and the status pages

manager-script - allows access to the text interface and the status pages

关闭再启

pom.xml中tomcat7插件添加配置：

```

<!-- 系统热部署配置 -->

<url>http://ip:8080/manager/text</url>

<username>tomcat</username>

<password>tomcat</password>

```

初次部署可以使用 "tomcat7:deploy" 命令

如果已经部署过使用 "tomcat7:redeploy" 命令
