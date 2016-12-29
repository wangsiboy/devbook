5.5.3版

参考 http://blog.csdn.NET/convict_eva/article/details/53306388

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
3、安装solr到tomcat

下载solr(和tomcat 在同一个目录下， solr 各版本下载地址：http://archive.apache.org/dist/lucene/solr/)
```
#wget http://apache.fayea.com/lucene/solr/5.5.3/solr-5.5.3.tgz
```
解压

```
# tar -zxf solr-5.5.3.tgz 
```
将solr-5.5.3/server/solr-webapp/webapp下的文件拷贝到tomcat/webapps/solr目录下
```
#mkdir ./tomcat/webapps/solr -p;cp solr-5.5.3/server/solr-webapp/webapp/* ./tomcat/webapps/solr -r 
```
复制solr相关的jar到solr工程下
```
#cp solr-5.5.3/server/lib/*.jar ./tomcat/webapps/solr/WEB-INF/lib/#cp solr-5.5.3/server/lib/ext/*.jar ./tomcat/webapps/solr/WEB-INF/lib/
```
复制字典（如果有重复的不替换）
```
#cp solr-5.5.3/dist/*.jar ./tomcat/webapps/solr/WEB-INF/lib/
```
复制log4j.properties 到solr工程classes下
```
#mkdir ./tomcat/webapps/solr/WEB-INF/classes -p#cp solr-5.5.3/server/resources/log4j.properties ./tomcat/webapps/solr/WEB-INF/classes/
```

创建solrhome:
```
#mkdir solrhome
```

将solr-5.5.3/server/solr下的所有文件拷贝到 solr-cloud/solrhome 目录中

```
#cp solr-5.5.3/server/solr/* ./solrhome/ -r;
```


复制依赖的jar到solrhome 目录
```
#cd solrhome

#cp ../solr-5.5.3/contrib/ ./ -r

#cp ../solr-5.5.3/dist/ ./ -r

#cd ..
```

修改 solr-cloud/tomcat/webapps/solr 下的web.xml，修改solr/home
```
<env-entry>

<env-entry-name>solr/home</env-entry-name>

<env-entry-value>/opt/solr-cloud/solrhome</env-entry-value>

<env-entry-type>java.lang.String</env-entry-type>

</env-entry>

```

启动tomcat，访问http://192.168.41.131:8080/solr/index.html

如果不能访问关闭防火墙

```
#server iptables stop
#chkconfig iptables off
```


创建core:

创建目录new_core（默认会初化此core）
```
#mkdir ./solrhome/new_core -p
```
复制配置文件
```
#cp ./solrhome/configsets/basic_configs/conf/ ./solrhome/new_core/ -rf
```

修改solrconfig.xml 依赖的配置文件
```
<lib dir="${solr.install.dir:..}/dist/" regex="solr-dataimporthandler-.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/extraction/lib" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-cell-\d.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/langid/lib/" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-langid-\d.*\.jar" />

<lib dir="${solr.install.dir:..}/contrib/velocity/lib" regex=".*\.jar" />

<lib dir="${solr.install.dir:..}/dist/" regex="solr-velocity-\d.*\.jar" />
```

把new_core 复制一份，修改名称为test-core，同样可创建test-core

https://code.google.com/p/ik-analyzer/downloads/list
