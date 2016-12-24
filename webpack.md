### 初始化一个工程

mkdir kanban_app

cd kanban_app 

npm init -y 

`# -y gives you default *package.json*, skip for more control`

npm i webpack --save-dev

### 创建目录结构

* /app
 - index.js
 - component.js 
 - main.css
* /build
 - index.html
* package.json
* webpack.config.js

In this case, we’ll generate bundle.js using Webpack based on our /app. To make this possible, we should set up some assets and webpack.config.js.

#### app/component.js
```
module.exports = function () {
  var element = document.createElement('h1');
  element.innerHTML = 'Hello world'; 
  return element;
};
```

#### app/index.js
```
require('./main.css');

var component = require('./component'); 
var app = document.createElement('div');

document.body.appendChild(app); 
app.appendChild(component());
```
#### build/index.html
```
<!DOCTYPE html>
<html lang="en"> 
  <head> 
    <meta charset="utf-8"> 
    <title>Kanban app</title> 
  </head>
  <body>
    <div id="app"></div>
    <script src="./bundle.js"></script> 
  </body>
</html>
```

#### app/main.css
```
body {
  background: cornsilk;
}
```

