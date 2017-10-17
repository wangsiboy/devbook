https://github.com/spotify/docker-maven-plugin

1. pom.xml添加plugin
2. mvn clean package docker:build
3. docker images 查看刚构建的镜像
4. 启动，docker run -d -p 8761:8761 wangsi/eureka-server:0.0.1



