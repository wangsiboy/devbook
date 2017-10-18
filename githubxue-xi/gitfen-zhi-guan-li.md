## 分支的常用操作

默认都会有一个主分支叫 master

* 新建一个叫 develop 的分支

```
git branch develop # 新建分支的命令是基于当前所在分支的基础上进行的
```

即以上是基于mater 分支新建了一个叫做 develop 的分支，此时 develop 分支跟 master 分支的内容完全一样。

* 切换到 develop 分支

```
git checkout develop
```

* 把以上两步合并，即新建并且自动切换到 develop 分支：

```
git checkout -b develop    
```

* 把 develop 分支推送到远程仓库

```
git push origin develop
```

* 如果你远程的分支想取名叫 develop2 ，那执行以下代码：

```
git push origin develop:develop2 # 强烈不建议这样，这会导致很混乱，很难管理，所以建议本地分支跟远程分支名要保持一致。
```

* 查看本地分支列表

```
git branch
```

* 查看远程分支列表

```
git branch -r 
```

* 删除本地分支

```
git branch -d develop 
git branch -D develop # 强制删除
```

* 删除远程分支

```
git push origin :develop 
```

* 如果远程分支有个 develop ，而本地没有，你想把远程的 develop 分支迁到本地： 

```
git checkout develop origin/develop 
```

* 同样的把远程分支迁到本地顺便切换到该分支：

```
git checkout -b develop origin/develop
```



## 分支管理流程 Git Flow

一般开发来说，大部分情况下都会拥有两个分支 master 和 develop，他们的职责分别是： 

* master：永远处在即将发布\(production-ready\)状态
* develop：最新的开发状态

但是我们发布之后又会进行下一版本的功能开发，开发中间可能又会遇到需要紧急修复 bug ，一个功能开发完成之后突然需求变动了等情况，所以 Git Flow 除了以上 master 和 develop 两个主要分支以外，还提出了以下三个辅助分支：

* feature: 开发新功能的分支, 基于 develop, 完成后 merge 回 develop 
* release: 准备要发布版本的分支, 用来修复 bug，基于 develop，完成后 merge 回develop 和 master 
* hotfix: 修复 master 上的问题, 等不及 release 版本就必须马上上线. 基于 master, 完成后merge 回 master 和 develop

举个例子，假设我们已经有 master 和 develop 两个分支了，这个时候我们准备做一个功能A，第一步我们要做的，就是基于 develop 分支新建个分支：

```
git branch feature/A 
```

看到了吧，其实就是一个规范，规定了所有开发的功能分支都以 feature 为前缀。

但是这个时候做着做着发现线上有一个紧急的 bug 需要修复，那赶紧停下手头的工作，立刻切换到 master 分支，然后再此基础上新建一个分支：

```
git branch hotfix/B 
```

代表新建了一个紧急修复分支，修复完成之后直接合并到 develop 和 master ，然后发布。

然后再切回我们的 feature/A 分支继续着我们的开发，如果开发完了，那么合并回 develop 分支，现在 develop 分支属于测试环境，对接并且测试后，感觉可以发布到正式环境了，这个时候再新建一个 release 分支：

```
git branch release/1.0
```

这个时候所有的 api、数据等都是正式环境，然后在这个分支上进行最后的测试，发现 bug 直接进行修改，直到测试 ok 达到了发布的标准，最后把该分支合并到 develop 和 master 然后进行发布。

> Git Flow 的工具地址，https://github.com/nvie/gitflow
>
> 具体安装与用法，http://stormzhang.com/git/2014/01/29/git-flow/



