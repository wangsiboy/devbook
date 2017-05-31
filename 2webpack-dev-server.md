仅用在开发环境，提供一个支持热部署的服务端

HotModuleReplacementPlugin 即时刷新

npm i webpack-dev-server --save-dev
```
"scripts": {
 "build": "webpack",
 "start": "webpack-dev-server --content-base build"
},
```
npm start

http://localhost:8080/

netstat -na | grep 8080

webpack-dev-server –port 3000

---
### 开发运行环境的配置，和编译项目的配置
分离配置的方式有很多种：
* 在多个文件中维护配置，通过引入模块共享配置。

 [react-starter](https://github.com/webpack/react-starter)
webpack命令传入配置参数的方式
* 单个文件，创建不同分支的方式。
 
 作者提供的 npm i webpack-merge --save-dev

```
const merge = require('webpack-merge');
const webpack = require('webpack');
const TARGET = process.env.npm_lifecycle_event;
const path = require('path');
const PATHS = { 
  app: path.join(__dirname, 'app'), 
  build: path.join(__dirname, 'build')
}; 

const common = {
 entry: { app: PATHS.app },
 output: { path: PATHS.build, filename: 'bundle.js' } 
};

// Default configuration 
if(TARGET === 'start' || !TARGET) {
  module.exports = merge(common, {
    devServer: {
      contentBase: PATHS.build,
      // Enable history API fallback so HTML5 History API based 
      // routing works. This is a good default that will come 
      // in handy in more complicated setups.
      historyApiFallback: true,
      hot: true, 
      inline: true, 
      progress: true,

      // Display only errors to reduce the amount of output.       
      stats: 'errors-only',

      // Parse host and port from env so this is easy to customize. 
      // 
      // If you use Vagrant or Cloud9, set 
      // host: process.env.HOST || '0.0.0.0';
      //
      // 0.0.0.0 is available to all network devices unlike default 
      // localhost 
      host: process.env.HOST,  
      port: process.env.PORT
    },
    plugins: [
      new webpack.HotModuleReplacementPlugin() 
    ]
  }); 
}

if(TARGET === 'build') { 
  module.exports = merge(common, {});
}

```
配置了contentBase，修改package.json的

 "start": "webpack-dev-server --content-base build"

```
"scripts": {
 "build": "webpack"
 "start": "webpack-dev-server"
},
```

看到服务端的文件
local- host:8080/webpack-dev-server/

改端口
process.env.PORT || 3000

windows环境下的问题，
"start": "webpack-dev-server --watch-poll --inline --hot"

### 自动刷新CSS

npm i css-loader style-loader --save-dev

```
module: {
  loaders: [ {
    // Test expects a RegExp! Note the slashes!
    test: /\.css$/, 
    loaders: ['style', 'css'], 
    // Include accepts either a path or an array of paths.  
    include: PATHS.app
  } ]
}

```
所有.css结尾的文件都要从右到左运行loaders里的处理。

css-loader will resolve @import and url statements in our CSS files.
 
style-loader deals with require statements in our JavaScript.

A similar approach works with CSS preprocessors, like Sass and Less, and their loaders.

http://webpack.github.io/docs/list-of-loaders.html

### Enabling Sourcemaps
```
if(TARGET === 'start' || !TARGET) { 
  module.exports = merge(common, {
    devtool: 'eval-source-map',
    ... 
  });
}
```
https://webpack.github.io/docs/configuration.html#devtool

### 自动安装加载npm包
npm i npm-install-webpack-plugin --save-dev

```
const NpmInstallPlugin = require('npm-install-webpack-plugin');
...
if(TARGET === 'start' || !TARGET) {
...
plugins: [
  new webpack.HotModuleReplacementPlugin(),
  new NpmInstallPlugin({
    save: true // --save 
  })
]
```
