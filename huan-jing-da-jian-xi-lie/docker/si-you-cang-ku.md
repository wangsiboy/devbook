

> 一个完整的应用可能包含上百个微服务，对应上百个镜像，如果考虑各个微服务的版本，会构建更多的镜像。管理这些镜像需要官方的Docker Hub或自己维护一个私有的Docker Registry。

### 用Docker Registry 2.0搭建一个私有仓库，然后将Docker镜像推送到私有仓库。



```
# 新建并启动一个Docker Registry 2.0
docker run -d -p 5000:5000 --restart=always --name registry2 registry:2

# Docker Hub是默认的Docker Registry，相当于默认为docker.io/wangsi/eureka-server:0.0.1
# 所以要修改下镜像标签
docker tag wangsi/eureka-server:0.0.1 localhost:5000/wangsi/eureka-server:0.0.1

#将镜像推送到私有仓库
docker push localhost:5000/wangsi/eureka-server:0.0.1
```



