### mac上安装jdk


1. 命令行输入 java -version，没有会弹出提示框，点更多，链接到下载网页。

2. dmg安装完，编辑 vi /etc/profile


```

JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home"

CLASS_PATH="$JAVA_HOME/lib"

PATH=".;$PATH:$JAVA_HOME/bin"

```

搞定。。。
