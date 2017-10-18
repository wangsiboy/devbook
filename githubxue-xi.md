Mac默认安装了Git、SSH，安装略过



#### 向GitHub 提交代码

终端输入 ssh-keygen -t rsa ，什么意思呢？

就是指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），

然后就会生成两个文件 id\_rsa 和 id\_rsa.pub ，而 id\_rsa 是密钥， id\_rsa.pub 就是公钥。

这两文件默认分别在如下目录里生成：

Linux/Mac 系统在 ~/.ssh 下，

win系统在 /c/Documents and Settings/username/.ssh 下，

都是隐藏文件，相信你们有办法查看的。

接下来要做的是把 id\_rsa.pub 的内容添加到 GitHub 上，

这样你本地的 id\_rsa 密钥跟 GitHub 上的 id\_rsa.pub 公钥进行配对，授权成功才可以提交代码。



