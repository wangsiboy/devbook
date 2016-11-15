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