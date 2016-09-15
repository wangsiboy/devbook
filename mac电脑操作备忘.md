**指定xcode**

>sudo xcode-select -switch \/Applications\/Xcode.app\/Contents\/Developer

**指定区域截图**：

>Command-Shift-4

**批处理还原指定的图片**:

>sudo /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/usr/bin/pngcrush -dir /data -revert-iphone-optimizations -q /Users/si/myapp/例子/掌上生活apk/ios/utils/*.png

**导入路径到当前命令行窗口**

>source ~/.bash_profile

* 显示：

>defaults write com.apple.finder AppleShowAllFiles -bool true

>killall Finder

* 隐藏：

>defaults write com.apple.finder AppleShowAllFiles -bool false

****常用命令****

```
ls -la
cp
sudo mv -v
rm -rf
pwd
```
