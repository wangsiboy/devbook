###安装jdk


```
yum repolist
yum search jdk
yum install java-1.8.0-openjdk.x86_64

```

/目录下查看java相关路径

`find -name java`

在文件最后加入：

```

#set java environment

JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk.x86_64

PATH=$PATH:$JAVA_HOME/bin

CLASSPATH=.:$JAVA_HOME/lib

export JAVA_HOME CLASSPATH PATH

```

修改/etc/profile之后让其生效

. /etc/profile
