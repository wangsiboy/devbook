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
tomcat

bin/startup.sh
tail -f logs/catalina.out
bin/shutdown.sh


