### LooBack的使用

开发环境下改变以下目录的用户权限：

➜ sudo chown -R $USER \/usr\/local\/bin

➜ sudo chown -R $USER \/usr\/local\/lib\/node\_modules

安装`StrongLoop sudo npm install -g strongloop`

创建一个应用 `slc loopback`

创建一个Model `slc loopback:model`

plural指的是RESTful API的route名，一个Model对应的route默认情况下会被plural（复数化），比如Post的路径是Posts。

访问[http:\/\/127.0.0.1:3000\/explorer](http://127.0.0.1:3000/explorer) 就能看到一个用Swagger做的API dashboard。

API Explorer

如何连Database

如何在前端使用创建出来的API

创建自己的SDK lb-ng server\/server.js client\/lb-services.js

SDK文档？执行 lb-ng-doc client\/lb-services.js 有时候需要在前面添加sudo（不知道为啥），然后访问 [http:\/\/localhost:3030\/](http://localhost:3030/) 就能看到文档啦～这个功能是基于Docular做的。

