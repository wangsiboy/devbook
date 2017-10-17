Dockerfile 是一个文本文件，包含若干指令描述构建镜像的细节。

。。。。。。

### 将Spring Cloud微服务构建成Docker镜像

1 将项目构建成jar包

```
mvn clean package # 使用Maven打包项目
```

例子产生的文件是：target/eureka-server-0.0.1-SNAPSHOT.jar



2 在jar包所在目录，创建名为Dockerfile的文件。

`touch Dockerfile`

```
#基于那个镜像
FROM java:8

#将本地文件夹挂载到当前容器
VOLUME /tmp

# 复制文件到容器，也可以直接写成ADD eureka-server-0.0.1-SNAPSHOT.jar /app.jar
ADD eureka-server-0.0.1-SNAPSHOT.jar app.jar
RUN bash -c 'touch /app.jar'

# 声明需要暴露的端口
EXPOSE 8761

# 配置容器启动后执行的命令
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

3 使用docker build命令构建镜像。

```
docker build -t wangsi/eureka-server:0.0.1 .
# 格式: docker build -t 仓库名/镜像名(:标签) Dockerfile的相对位置
```

4 测试

```
#启动镜像
docker run -d -p 8761:8761 wangsi/eureka-server:0.0.1
```

访问http://Docker宿主机IP:8761/，正常显示Eureka Server主页。

