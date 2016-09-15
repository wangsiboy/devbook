### SVN服务器

**安装smart svn软件**

___

#### MAC下命令行创建SVN服务器的方式
➜ mkdir ~/svn

➜ svnadmin create ~/svn/repository

➜ cd ~/svn/repository

#### 服务器配置

> /conf/authz文件，用来建立分组并设置组的读写权限：

[groups]

IT_group = wangsi

[/]

wangsi = rw

*=

> /conf/passwd文件，配置 ：

[users]

wangsi=12345678

> /conf/svnserve.conf

[general]

anon-access = read //拉分支出问题后改成none 

auth-access = write

password-db = passwd

authz-db = authz

>启动:
killall svnserve && svnserve –d –r ~/svn/

>脱离svn:
sudo find /XXX/XXX/xxx -name ".svn" -exec rm -r {} \;
