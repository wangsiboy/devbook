## alias

按自己的习惯配置别名，缩写命令，简单快捷。

```
git config --global alias.ck checkout
git config --global alias.st status
git config --global alias.br branch

git config --global alias.psm 'push origin master'
git config --global alias.plm 'pull origin master'
```

日志更清晰，一个很屌的命令

```
git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)% d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"
```

## 一些配置

```
git config --global core.editor "vim"  # 设置Editor使用vim
git config --global color.ui true      # 开启给 Git 着色
git config --global core.quotepath false # 设置显示中文文件名
```

默认这些配置都在 ~/.gitconfig 文件下的，你可以找到这个文件查看自己的配置，也可以输入 git config -l 命令查看。

## 提交之前需要确认下，用diff来查看做了哪些改动

```
git diff
```

直接输入 git diff 只能比较当前文件和暂存区文件差异，什么是暂存区？就是你还没有执行 git add 的文件。

```
git diff <$id1> <$id2>   # 比较两次提交之间的差异
git diff <branch1>..<branch2> # 在两个分支之间比较 
git diff --staged   # 比较暂存区和版本库差异
```

## checkout

```
git checkout develop # 切换到 develop 分支，
git checkout v1.0 # 切换tag
git checkout ffd9f2dd68f1eb21d36cee50dbdd504e95d9c8f7 # 后面的一长串是commit_id，是每次com mit的SHA1值，可以根据 git log 看到。
git checkout a.md # 还原，checkout 命令只能撤销还没有 add 进暂存区的文件。
```

## stash

假设我们正在一个新的分支做新的功能，这个时候突然有一个紧急的bug需要修复，而且修复完之后需要立即发布。

那么有没有一种比较好的办法，可以让我暂时切到别的分支，修复完bug再切回来，而且代码也能保留的呢？

这个时候 stash 命令就大有用处了，前提是我们的代码没有进行 commit ，哪怕你执行了add 也没关系，我们先执行

```
git stash
```

意思就是把当前分支所有没有 commit 的代码先暂存起来，这个时候你再执行 git status 你会发现当前分支很干净，几乎看不到任何改动，你的代码改动也看不见了，但其实是暂存起来了。执行

```
git stash list # 此时暂存区已经有了一条记录。
```

这个时候你可以切换会其他分支，赶紧把bug修复好，然后发布。之后一切都解决了，你再切换回来继续做你之前没做完的功能，但是之前的代码怎么还原呢？

```
git stash apply
```

你会发现你之前的代码全部又回来了，就好像一切都没发生过一样，紧接着你最好需要把暂存区的这次 stash 记录删除，执行：

```
git stash drop # 把最近一条的 stash 记录删除
```

还有更方便的，你可以使用：

```
git stash pop # 不但会帮你把代码还原，还自动帮你把这条 stash 记录删除。
```

drop 是只删除一条，当然后面可以跟 stash\_id 参数来删除指定的某条记录，不跟参数就是删除最近的，而 clear 是清空。

```
git stash clear # 清空所有暂存区的记录
```

## merge & rebase

merge 分支是合并的意思，我们在一个 featureA 分支开发完了一个功能，这个时候需要合并到主分支 master 上去

```
git checkout master 
git merge featureA
```

其实 rebase 命令也是合并的意思，上面的需求我们一样可以如下操作：

```
git checkout master 
git rebase featureA
```

rebase 跟 merge 的区别你们可以理解成有两个书架，你需要把两个书架的书整理到一起去，第一种做法是 merge ，比较粗鲁暴力，就直接腾出一块地方把另一个书架的书全部放进去，虽然暴力，但是这种做法你可以知道哪些书是来自另一个书架的；第二种做法就是rebase ，他会把两个书架的书先进行比较，按照购书的时间来给他重新排序，然后重新放置好，这样做的好处就是合并之后的书架看起来很有逻辑，但是你很难清晰的知道哪些书来自哪个书架的。

## 解决冲突

冲突的地方由 ==== 分出了上下两个部分，

上部分一个叫HEAD 的字样代表是我当前所在分支的代码，

下半部分是一个叫 XXX 分支的代码。

所以我们很容易判断哪些代码该保留，哪些代码该删除。



















