1. 下载Maven [链接](http://maven.apache.org/download.cgi)
2. 我放置Maven的目录
/Users/wangsi/develop/apache-maven-3.3.9
3. 修改Maven配置文件

 vim ~/.bash_profile

```
export M2_HOME=/Users/wangsi/develop/apache-maven-3.3.9
export M2=$M2_HOME/bin
export PATH=$M2:$PATH
```
 source ~/.bash_profile

jar包配置搜索地址：http://mvnrepository.com/

4.用户配置：

拷贝一份全局配置到用户.m2目录下，

cp apache-maven-3.3.9/conf/settings.xml ~/.m2

```
<mirror>
  <id> maven-net-cn</id>
  <name> Maven China Mirror</name>
  <url> http://maven.net.cn/content/groups/public/</url>
  <mirrorOf>central</mirrorOf>
</mirror>
```

```
 <mirror>   <id>alimaven</id> <mirrorOf>central</mirrorOf> <name>aliyun maven</name> <url>http://maven.aliyun.com/nexus/content/groups/public/</url> </mirror> </mirrors>

```