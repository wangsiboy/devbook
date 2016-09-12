### 安卓模拟器

1. 安装java-sdk

`sudo vim etc/profile`

JAVA_HOME="/Library/Java/JavaVirtualMachines/
jdk1.8.0_20.jdk/Contents/Home/"
CLASS_PATH="$JAVA_HOME/lib"
PATH=".;$PATH:$JAVA_HOME/bin"

2. 安装android-sdk

`brew install android-sdk`

3. 使用android命令打开管理器，安装sdk和扩展

4. brew info android 查看安卓的安装地址

5. open /usr/local/Cellar/android-sdk/24.4.1_1/extras/intel ,dmg安装后就可以使用模拟器了。

`android avd`

`emulator @myProject`

`react-native run-android`




