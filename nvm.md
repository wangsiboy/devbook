# NVM管理NodeJS版本

> nvm 是 Mac 下的 node 管理工具，有点类似管理 Ruby 的 rvm，如果是需要管理 Windows 下的 node，官方推荐是使用 nvmw 或 nvm-windows 。

touch ~\/.bash\_profile

curl -o- https:\/\/raw.githubusercontent.com\/creationix\/nvm\/v0.32.1\/install.sh \| bash

安装命令到github上查看最新的。

[https:\/\/github.com\/creationix\/nvm](https://github.com/creationix/nvm)

[https:\/\/github.com\/hakobera\/nvmw](https://github.com/hakobera/nvmw)

[https:\/\/github.com\/coreybutler\/nvm-windows](https://github.com/coreybutler/nvm-windows)

nvm ls-remote

nvm install

nvm use

nvm alias default v6.9.1

---

> 卸载已安装到全局的 node\/npm

查看已经安装在全局的模块，以便删除这些全局模块后再按照不同的 node 版本重新进行全局安装

`npm ls -g --depth=0`

删除全局 node\_modules 目录

`sudo rm -rf /usr/local/lib/node_modules`

删除 node

`sudo rm /usr/local/bin/node`

删除全局 node 模块注册的软链

`cd /usr/local/bin && ls -l | grep "../lib/node_modules/" | awk '{print $9}'| xargs rm`

> sudo npm install 安装时报错，没有mkdir权限

`sudo npm cache clear`

> 淘宝镜像

`npm config set registry https://registry.npm.taobao.org`

`npm config set disturl https://npm.taobao.org/dist`

sudo chmod 777 \/Users\/si\/.babel.json

npm config set prefix \/Users\/si\/.nvm\/versions\/node\/v6.4.0

