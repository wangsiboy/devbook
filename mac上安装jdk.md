### mac上安装jdk


1. 命令行输入 java -version，没有会弹出提示框，点更多，链接到下载网页。
[jdk7下载](http://download.oracle.com/otn/java/jdk/7u80-b15/jdk-7u80-macosx-x64.dmg?AuthParam=1483000963_0925b1e49c7f86991a35028612827edf)

2. dmg安装完

3. 编辑 

sudo vi /etc/profile


```

JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home"

CLASS_PATH="$JAVA_HOME/lib"

PATH=".;$PATH:$JAVA_HOME/bin"

```
:!wq

source /etc/profile

搞定。。。
