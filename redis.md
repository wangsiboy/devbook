跨平台Redis桌面管理软件

https://github.com/uglide/RedisDesktopManager

gcc编译环境 yum install gcc-c++

https://redis.io/download 下载后解压编译

安装 make install PREFIX=/usr/local/redis

复制 redis.conf 到/usr/local/redis

修改配置

```
#是否作为守护进程运行
daemonize yes
port 6379
timeout 300
#密码
```
redis-server redis.conf

看下进程 ps aux|grep redis

redis-cli -h domain -p port -a password <-c 集群>

```
redis> set foo bar
OK
redis> get foo
"bar"
keys *
set a 100
get a 
incr a
decr a
del a
```


