#### 先尝试下git命令的本地操作

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

a.md文件等待被提交。`git rm --cached <file>`可以移出缓存。

```
// 提交，-m表示加上本次提交的说明信息
git commit -m 'hello github!'

// 哦，先配置下你的邮箱和用户名，以下是我的：
  git config --global user.email "50208308@qq.com"
  git config --global user.name "wangsiboy"
  // 每一次commit都会产生一条log，
  // 这条log标记了提交人的姓名与邮箱，
  // 以便其他人方便的查看与联系提交人，
  // 所以我们在进行提交代码的第一步就是要设置自己的用户名与邮箱。

  // 以上进行了全局配置，切换到你的项目要更换的话，以上代码把 --global 参数去除，再重新执行一遍就ok了。
```

```
git log # 显示提交记录
```

---

#### 关联远程仓库

第一步，在GitHub上建一个test项目

第二步，与本地关联

```
git remote and origin git@github.com:wangsiboy/test.git
```

即指定一个远程仓库，他的地址是 git@github.com:wangsiboy/test.git

origin 是给这个项目的远程仓库起的名字，是的，名字你可以随便取，只不过大家公认的只有一个远程仓库时名字就是 origin 。

为什么要给远程仓库取名字？

因为我们可能一个项目有多个远程仓库，比如 GitHub 一个，比如公司一个，这样的话提交到不同的远程仓库就需要指定不同的仓库名字了。

查看我们当前项目有哪些远程仓库可以执行如下命令：

```
git remote -v
```

#### 同步远程仓库

```
// 将远程仓库的最新代码拉过来，更新到本地。
git pull origin master
```

```
// 将本地代码推送到远程主分支上，更新到主分支。
git push origin master
```

一般push前先pull，这样不容易冲突。

现在，本地和远程一样喽～

---

#### Clone项目

```
//clone GitHub上的test项目到本地
git clone git@github.com:wangsiboy/test.git
```

git@github.com:&lt;你到账号&gt;/项目名.git

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

#### 



