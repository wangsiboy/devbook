* 新建并启动容器

-d 后台运行

-P 随机端口映射

-p 指定端口

--network 指定网络模式

...



**docker ps**

列出运行中的容器。-a

docker stop

docker kill

docker start

docker restart



进入运行中的容器

docker attach

使用nsenter进入容器。nsenter工具包含在util-linux2.23或更高版本中。为了连接到容器，需要找到容器第一个进程的PID，可通过以下命令获取：

docker inspect --format "{{.State.Pid}}" **$CONTAINER\_ID**

获得PID后，就可以：

nsenter --target **"$PID" **--mount --uts --ipc --net --pid



删除容器

docker rm

删运行的加-f



