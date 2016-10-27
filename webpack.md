### 初始化一个工程

mkdir kanban_app

cd kanban_app 

npm init -y # -y gives you default *package.json*, skip for more control

npm i webpack --save-dev

`kanban_app $ node_modules/.bin/webpack`

目录结构

* /app
 - index.js
 - component.js 
* /build
 - index.html
* package.json
* webpack.config.js

In this case, we’ll generate bundle.js using Webpack based on our /app. To make this possible, we should set up some assets and webpack.config.js.



