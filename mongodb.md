# mongoDB的使用

### 启动MongoDB

mongod -port 28008 --dbpath /data/db

### 停止MongoDB

shell进入MongoDB的bin目录，执行mongo

use admin

db.shutdownServer()

### javaScript shell命令

执行js脚本或文件：

mongo test --eval “printjson(db.getCollectionNames())”

load(“/tmp/db_update.js”)
