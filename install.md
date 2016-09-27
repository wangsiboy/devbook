1、下载MongoDB（64位）

curl https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.0.5.tgz > mongodb.tgz

2、解压下载下来的安装包

tar -zxvf mongodb.tgz

mv mongodb-linux-x86_64-3.0.5 mongo

cd mongo

mkdir db

mkdir logs

cd bin

vi mongodb.conf

dbpath=/yunpan/mongo/db

logpath=/yunpan/mongo/logs/mongodb.log

port=12345

fork=true

nohttpinterface=true
./mongod -f ./mongodb.conf

3、重新绑定mongodb的配置文件地址和访问IP./mongod --bind_ip localhost -f mongodb.conf./mongo localhost:12345/cailianposdb.shutdownServer()4、开机自动启动mongodbvi /etc/rc.d/rc.local/yunpan/mongo/bin/mongod --config /yunpan/mongo/bin/mongodb.conf

5、重启一下系统测试下能不能自启#进入mongodb的shell模式 /yunpan/mongo/bin/mongo localhost:12345/cailianpos#查看数据库列表 show dbs#当前db版本 db.version();
