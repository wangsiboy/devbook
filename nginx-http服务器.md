#### nginx

yum install nginx

已安装:

 nginx.x86_64 0:1.10.2-1.el6


```
#试试：

service nginx status
nginx -t

vim /etc/nginx/conf.d/default.conf
listen 80;
#注释掉原来的listen，退出

service nginx start

```

浏览器里通过ip访问下，可以看到nginx界面初始安装成功。


##### nginx配置

```
upstream cailaobo.com { server 127.0.0.1:8080;}

server { listen 80; server_name cailaobo.com;

 location / { proxy_pass http://cailaobo.com; index index.html index.htm; }



 error_page 404 /404.html; location = /40x.html { }



 error_page 500 502 503 504 /50x.html; location = /50x.html { }



}

```
