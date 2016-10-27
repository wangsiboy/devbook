### webpack.config.js

```
const path = require('path'); 
const PATHS = { 
  app: path.resolve(__dirname, 'app'), 
  build: path.resolve(__dirname, 'build') 
};
 
var webpack = require('webpack');

module.exports = { 
  // Entry accepts a path or an object of entries.
  entry: { app: PATHS.app }, 
  output: { 
    path: PATHS.build, 
    filename: 'bundle.js' 
  },
  module: { 
    loaders: [ { 
      test: /\.css$/, 
      loaders: ['style', 'css']
    } ]
  }, 
  plugins: [
    new webpack.optimize.UglifyJsPlugin() 
  ]
};
```
1.添加代码后，执行命令

`kanban_app $ node_modules/.bin/webpack`

命令太麻烦了，在package.json中添加
```
"scripts": {
  "build": "webpack" 
},
```

2.浏览器中查看结果

`kanban_app $ open ./build/index.html`

