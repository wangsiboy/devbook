### Nginx

Nginx是一款高性能的http 服务器/反向代理服务器及电子邮件（IMAP/POP3）代理服务器。

### Nginx的应用场景

* http服务器。Nginx是一个http服务可以独立提供http服务。可以做网页静态服务器。

* 虚拟主机。可以实现在一台服务器虚拟出多个网站。例如个人网站使用的虚拟主机。

* 反向代理，负载均衡。当网站的访问量达到一定程度后，单台服务器不能满足用户的请求时，需要用多台服务器集群可以使用nginx做反向代理。并且多台服务器可以平均分担负载，不会因为某台服务器负载高宕机而某台服务器闲置的情况。

### Nginx的安装

Nginx一般推荐安装到linux系统，而且要安装c语言的编译环境gcc。

### 下载：

进入http://nginx.org/en/download.html 下载nginx1.8.0版本（当前最新稳定版本）。

先安装nginx依赖的包：

nginx是C语言开发，建议在linux上运行，本教程使用Centos6.5作为安装环境。

gcc

 安装nginx需要先将官网下载的源码进行编译，编译依赖gcc环境，如果没有gcc环境，需要安装gcc：yum install gcc-c++

PCRE

 PCRE(Perl Compatible Regular Expressions)是一个Perl库，包括 perl 兼容的正则表达式库。nginx的http模块使用pcre来解析正则表达式，所以需要在linux上安装pcre库。

yum install -y pcre pcre-devel

注：pcre-devel是使用pcre开发的一个二次开发库。nginx也需要此库。

zlib

 zlib库提供了很多种压缩和解压缩的方式，nginx使用zlib对http包的内容进行gzip，所以需要在linux上安装zlib库。

yum install -y zlib zlib-devel


openssl

 OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。

 nginx不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在linux安装openssl库。

yum install -y openssl openssl-devel



## 安装步骤

第一步：把nginx的源码上传到linux系统

第二步：把压缩包解压缩。

第三步：进行configure。

./configure \

--prefix=/usr/local/nginx \

--pid-path=/var/run/nginx/nginx.pid \

--lock-path=/var/lock/nginx.lock \

--error-log-path=/var/log/nginx/error.log \

--http-log-path=/var/log/nginx/access.log \

--with-http_gzip_static_module \

--http-client-body-temp-path=/var/temp/nginx/client \

--http-proxy-temp-path=/var/temp/nginx/proxy \

--http-fastcgi-temp-path=/var/temp/nginx/fastcgi \

--http-uwsgi-temp-path=/var/temp/nginx/uwsgi \

--http-scgi-temp-path=/var/temp/nginx/scgi


注意：上边将临时文件目录指定为/var/temp/nginx，需要在/var下创建temp及nginx目录

第四步：make

第五步：make install

### Nginx的启动、停止

1、启动：进入nginx的sbin目录，./nginx就可以启动。
如果访问不到，首先查看防火墙是否关闭。
2、关闭nginx：
可以使用kill命令，但是不推荐使用。
推荐使用：./nginx -s stop

刷新配置：./nginx -s reload


## Nginx的配置

在/usr/local/nginx/conf目录下nginx.conf文件是nginx的配置文件。

使用nginx配置虚拟机

通过端口区分虚拟机

在nginx.conf文件中添加一个Service节点，修改端口号就可以
```
server {
 listen 81;
 server_name localhost;
 #charset koi8-r;
 #access_log logs/host.access.log main;
 location / {
   root html81;
   index index.html index.htm;
 }
 }

```

通过域名区分虚拟机

域名介绍

DNS服务器

DNS服务器

通过ip地址访问服务器

通过ip地址访问服务器

返回ip地址

返回ip地址

Pc机

Pc机

Web服务器

Web服务器



根据域名换ip地址

根据域名换ip地址

可以通过修改host文件指定域名的ip地址。

Host文件的位置：C:\Windows\System32\drivers\etc

可以使用工具：


配置基于域名的虚拟主机

需要修改nginx.conf配置文件。

```
server {
listen 80;
 server_name test3.taotao.com; #charset koi8-r; #access_log logs/host.access.log main;
   location / {
     root html-test3;
     index index.html index.htm;
   }
}```
修改配置后需要重新加载配置文件。
