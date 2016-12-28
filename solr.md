http://lucene.apache.org/solr/

http://apache.fayea.com/lucene/solr/5.5.3/solr-5.5.3.tgz

```
<dependency>
 <groupId>org.apache.solr</groupId>
 <artifactId>solr-solrj</artifactId>
 <version>5.5.3</version>
</dependency>

```

服务器搭建

1. jdk、tomcat

修改URI编码配置
```
<Connector port="8080" protocol="HTTP/1.1"

connectionTimeout="20000"

redirectPort="8443" URIEncoding="UTF-8" useBodyEncodingForURI="true"/>
```

```
解压
tar -zxf solr-5.5.3.tgz

#新建solr
mkdir /usr/local/solr

#拷贝一份tomcat
cp -r apache-tomcat-7.0.73 /usr/local/solr/tomcat 

#拷贝webapp到tomcat下的webapps目录下，改名为solr。
cp -r solr-5.5.3/server/solr-webapp/webapp /usr/local/solr/tomcat/webapps/

mv webapp solr

#拷贝其它
cp -r solr-5.5.3/server/lib/ext/* /usr/local/solr/tomcat/webapps/webapp/WEB-INF/lib/

mkdir /usr/local/solr/tomcat/webapps/solr/WEB-INF/classes

cp solr-5.5.3/server/resources/log4j.properties /usr/local/solr/tomcat/webapps/solr/WEB-INF/classes/

cp solr-5.5.3/dist/solr-dataimporthandler-5.5.3.jar /usr/local/solr/tomcat/webapps/solr/WEB-INF/lib/

cp solr-5.5.3/dist/solr-dataimporthandler-extras-5.5.3.jar /usr/local/solr/tomcat/webapps/solr/WEB-INF/lib/

复制字典（如果有重复的不替换）
#cp solr-5.5.3/dist/*.jar ./tomcat/webapps/solr/WEB-INF/lib/

```

配置文件，索引库；一个solr服务对应一份solrhome

```
cp -r solr-5.5.3/server/solr /usr/local/solr/solrhome

```

修改web.xml配置solrhom路径
```
vim /usr/local/solr/tomcat/webapps/solr/WEB-INF/web.xml

<env-entry>
 <env-entry-name>solr/home</env-entry-name>
 <env-entry-value>/usr/local/solr/solrhome</env-entry-value>
 <env-entry-type>java.lang.String</env-entry-type>
</env-entry>

```

复制依赖的jar到solrhome 目录
```
#cd solrhome
#cp ../solr-5.5.3/contrib/ ./ -r
#cp ../solr-5.5.3/dist/ ./ -r
```

tomcat
```
bin/startup.sh
tail -f logs/catalina.out
bin/shutdown.sh
```

如果不能访问关闭防火墙
```
#server iptables stop
#chkconfig iptables off
```

创建core:

创建目录new_core（默认会初化此core）#mkdir ./solrhome/new_core -p复制配置文件#cp ./solrhome/configsets/basic_configs/conf/ ./solrhome/new_core/ -rf

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

```
<fieldType name="text_ik" class="solr.TextField"> 
<analyzer type="index" isMaxWordLength="false" class="org.wltea.analyzer.lucene.IKAnalyzer"/> 
<analyzer type="query" isMaxWordLength="true" class="org.wltea.analyzer.lucene.IKAnalyzer"/> 
</fieldType>

```

