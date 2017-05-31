### 安装Nginx

ssh连接服务器；

输入命令 vim /etc/yum.repos.d/nginx.repo添加一个资源库。
```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```
yum install nginx, 开始安装

Complete! 

测试下，

service nginx status

nginx -t

启动/停止 service nginx start/stop

---
安装命令：
sudo apt-get install nginx

/etc/nginx/sites-available 创建 x.conf
```
server {
 listen 80;
 server_name domain.com www.domain.com;

 location / {
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header Host $http_host;
  proxy_pass http://127.0.0.1:2345;
 }
}
```
把你的配置文件软链接到sites-enabled文件夹下：
sudo In -s /etc/nginx/sites-available/x.conf /etc/nginx/sites-enabled/x.conf

### 配置nginx虚拟主机

进入配置目录：cd /etc/nginx/conf.d

创建网站的配置：cp default.conf domain.name.conf

vim domain.name.conf

```
server {
  listen 80;
  server_name domain.com www.domain.com;
  root /site/path;
  
  if($http_host !~ "^www.domain.com$"){
    rewrite ^(.*) http://www.domain.com$1 permanent;
  }
  #charset koi8-r;
  #access_log /var/log/nginx/log/host.access.log main;

  location / {
    proxy_pass http://127.0.0.1:2345;
    index index.html index.js;
  }
  ...
}
```
以上为要修改的内容... 

按esc, 输入:wp保存并退出。

service nginx reload 重启生效。



### 阿里ECS挂载数据盘

若执行fdisk -l命令，发现没有/dev/xvdb表明无数据盘。

执行"fdisk -S 56/dev/xvdb"命令，对数据盘进行分区；

根据提示，依次输入"n","p","1",两次回车,分区开始。。。

查看下"fdisk -l",新的分区xvdb1已经建立完成。

新盘的格式化："mkfs.ext3/dev/xvdb1"

把数据盘挂载到文件夹，先创建文件夹 mkdir xxx

写入新分区信息：
echo '/dev/xvdb1 /xxx ext3 defaults 0 0'>>/etc/fstab

查看下写入了没，“cat /etc/fstab”

最后，“mount -a”命令挂在新分区，然后用“df -h”查看。