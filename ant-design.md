#开发环境

```
#安装脚手架
npm install dva-cli -g
dva -v 

#创建应用
dva new dva-start
cd dva-start

#按需加载
npm install antd babel-plugin-import --save

```
编辑  .roadhogrc ，使 babel-plugin-import 插件生效。 

```
 "extraBabelPlugins": [

- "transform-runtime"

+ "transform-runtime",

+ ["import", { "libraryName": "antd", "style": "css" }]

 ],
```


