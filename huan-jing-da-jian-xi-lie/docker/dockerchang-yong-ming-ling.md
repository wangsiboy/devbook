https://docs.docker.com/engine/reference/commandline/



docker search java

搜索java关键词的镜像仓库。



docker pull java

下载java镜像。如果慢，**配置阿里云加速器**

1. 注册 阿里云账号，进入控制台
2. https://cr.console.aliyun.com/?spm=5176.100239.blogcont29941.13.T97mvf

docker pull xxx.com/java:7

从指定的Docker Registry中下载标签为7的java镜像。



docker  images

列出已下载的镜像。

docker rmi hello-world

删除指定的hello-world镜像。

docker rmi -f $\(docker images\)

强制删除所有。





