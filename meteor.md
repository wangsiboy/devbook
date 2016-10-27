### Install
curl https://install.meteor.com/ | sh

### 例子程序
meteor create --list

### create simple-todos

```
meteor create simple-todos
cd simple-todos
meteor npm install
meteor
```
http://localhost:3000/

---

### 遇到的问题

##### meteor-tool throw error

`meteor npm rebuild`

输入命令后就好了，还不行的话改hosts文件

sudo -i gedit /etc/hosts

Paste: "54.192.225.217 warehouse.meteor.com"

##### Unexpected mongo exit code 48. Restarting
sudo lsof -i :3001

然后我直接killall用到3001端口的进程，重新运行，问题解决了。
