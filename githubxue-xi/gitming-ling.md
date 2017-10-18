新建test目录，在目录下创建了a.md文件。

```
mkdir test
cd test
touch a.md
```

输入以下命令，查看当前git仓库的状态：

```
git status
```

提示当前目录还不是一个Git仓库。

```
// 初始化git仓库
git init
```

test目录已经是一个git仓库了。

git status查看下状态: 

默认为主分支。a.md文件没提交。

```
// 先把改动添加到一个[暂存区]
git add a.md
```

git status查看下状态: 

a.md文件等待被提交。git rm --cached &lt;file&gt;可以移出缓存。

```
// 提交，-m表示加上本次提交的说明信息
git commit -m 'first commit'
```

```
git log # 显示提交记录
```



