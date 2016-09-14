###查看安装的生成器版本

npm ls -g --depth=1 2>/dev/null | grep generator-

### 自动加浏览器前缀

`npm install autoprefixer-loader --save-dev` 

{

test:/\.css/,

loader: ‘style-loader!css-loader!autoprefixer-loader?{browsers:[“last 2 version”, “Firefox 15”]}!sass-loader?outputStyle=expanded’

}

### 加载json文件的loader 

`npm install json-loader --save-dev`

{

test:/\.json$/,

loader: ‘json-loader’

}

代码中require 使用json文件
