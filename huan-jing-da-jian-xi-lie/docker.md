一个开源的容器引擎，有助于更快地交付应用。

### 安装和卸载

https://docs.docker.com/engine/installation/

#### CentOS 7 安装Docker 64位平台

* 移除老版本

```
sudo yum -y remove docker
```

/var/lib/docker目录下的内容不会被删除

* 设置Yum源

1. 安装yum-utils，这样就能使用yum-config-manager工具设置Yum源。

```
sudo yum install -y yum-utils
```

2. 执行以下命令，添加Docker的Yum源。

```
sudo yum-config-manager --add-repo https://docs.docker.com/engine/installation/linux/repo_files/centos/docker.repo
```

3. \[可选\]启用测试仓库。默认禁用的。

```
sudo yum-config-manager --enable docker-testing
// 禁用
sudo yum-config-manager --disable docker-testing
```

* 安装Docker

1. 更新Yum包的索引。

```
sudo yum makecache fast
```

2. 安装最新版本的Docker。

```
sudo yum -y install docker-engine
```

3. 可能需要安装指定版本的Docker

```
//列出可用的Docker版本。
yum list docker-engine.x86_64 --showduplicates |sort -r
//安装指定版本的
sudo yum -y install docker-engine-<版本号>
```

4. 启动

```
sudo systemctl start docker
```

5. 验证安装是否正确。

```
sudo docker run hello-world
//////////类似以下结果///////
Unable to find image 'hello-world:latest' locally
...
```

6. 查看Docker版本。

```
docker version
```

* 卸载Docker

```
// 卸载Docker软件包
sudo yum -y remove docker-engine

// 如果删除镜像、容器、卷以及自定义的配置文件
sudo rm -rf /var/lib/docker
```



