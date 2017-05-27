### mac上安装jdk


1. 命令行输入 java -version，没有会弹出提示框，点更多，链接到下载网页。
[jdk7下载](http://download.oracle.com/otn/java/jdk/7u80-b15/jdk-7u80-macosx-x64.dmg?AuthParam=1483000963_0925b1e49c7f86991a35028612827edf)

2. dmg安装完

3. 编辑 

vi ~/.bash_profile


```

export M2_HOME=/Users/si/devtool/apache-maven-3.3.9

export M2=$M2_HOME/bin

export PATH=$M2:$PATH

export NVM_DIR="/Users/si/.nvm"[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm

export JAVA_7_HOME=/Library/Java/JavaVirtualMachines/jdk1.7.0_80.jdk/Contents/Home
export JAVA_8_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home
export JAVA_HOME=$JAVA_8_HOME 
export CLASS_PATH=$JAVA_HOME/lib
#export PATH=$PATH:$JAVA_HOME/bin
alias jdk8='export JAVA_HOME=$JAVA_8_HOME;export CLASS_PATH=$JAVA_HOME/lib'
alias jdk7='export JAVA_HOME=$JAVA_7_HOME;export CLASS_PATH=$JAVA_HOME/lib'

alias subl='open -a "Sublime Text"'


```
:!wq

source ~/.bash_profile

