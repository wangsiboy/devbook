1、安装jdk（略）

目录安排(自行创建目录)：

/opt

 solr-cloud

 solrhome 创建的solrhome

 tomcat 安装的tomcat

 solr-5.5.3 solr解压目录


2、安装tomcat

（wget http://mirrors.hust.edu.cn/apache/tomcat/tomcat-8/v8.5.8/bin/apache-tomcat-8.5.8.tar.gz）

修改URI编码配置，增加URIEncoding="UTF-8" useBodyEncodingForURI="true"，如下
```
<Connector port="8080" protocol="HTTP/1.1"

connectionTimeout="20000"

redirectPort="8443" URIEncoding="UTF-8" useBodyEncodingForURI="true"/>
```
