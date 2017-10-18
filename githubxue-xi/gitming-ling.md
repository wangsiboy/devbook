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

---

#### 创建和删除分支

```
// 创建a分支，但当前还在master主分支上
git branch a

//切换到a分支
git checkout a

// 合起来的命令, 代替前面的两次命令操作
git checkout -b a

//查看分支情况
git branch
```

在a分支上编写完，测试ok，就可以合并到主分支master上。

```
// 删除a分支
git branch -d a

// 有未合并到master的内容，删除不了
// 强制删除
git branch -D a
```

#### 合并分支

```
// 先切换到主分支
git checkout master

//合并a分支, 文件不冲突的话这就成功了
git merge a
```

---

#### 版本概念\(标签\)

```
// 当前代码状态下新建一个v1.0.0标签
git tag v1.0.0

// 查看tag记录
git tag

//多个tag时，切换某个tag
git checkout v1.0.0

```

 

 

 

 

 

 



