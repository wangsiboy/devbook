1、brew search nginx

2、brew install nginx

启动nginx ，sudo nginx ;

访问localhost:8080 发现已出现nginx的欢迎页面了。
备注： ln -s /usr/local/sbin/nginx /usr/bin/nginx 做个软连接。

常用的指令有： 
nginx -V 查看版本，以及配置文件地址
nginx -v 查看版本
nginx -c filename 指定配置文件
nginx -h 帮助

#重新加载配置|重启|停止|退出 nginx

nginx -s reload|reopen|stop|quit

#打开 nginx

sudo nginx

#测试配置是否有语法错误

nginx -t


另外附上Mac安装brew命令：

安装命令如下：curl -LsSf http://github.com/mxcl/homebrew/tarball/master | sudo tar xvz -C/usr/local --strip 1当brew安装成功后，就可以随意安装自己想要的软件了，例如wget，命令如下：sudo brew install wget 卸载的话，命令如下：sudo brew uninstall wget查看安装软件的话，命令如下：sudo brew search /apache*/注意/apache*/是使用的正则表达式，用/分割
