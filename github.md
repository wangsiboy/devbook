### github上下载单个文件夹

将 /tree/master/ 换成 /trunk/

svn checkout [https://github.com/aksonov/react-native-router-flux/trunk/Example/components](https://github.com/aksonov/react-native-router-flux/trunk/Example/components)

### 删除

```
# 恢复暂存区的指定文件到工作区 
$ git checkout [file] 

# 恢复某个commit的指定文件到暂存区和工作区 
$ git checkout [commit] [file] 

# 恢复暂存区的所有文件到工作区 
$ git checkout . 

# 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变 
$ git reset [file] 

# 重置暂存区与工作区，与上一次commit保持一致 
$ git reset --hard 

# 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变 
$ git reset [commit] 

# 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致 
$ git reset --hard [commit] 

# 重置当前HEAD为指定commit，但保持暂存区和工作区不变 
$ git reset --keep [commit] 

# 新建一个commit，用来撤销指定commit 
# 后者的所有变化都将被前者抵消，并且应用到当前分支 
$ git revert [commit] 

# 暂时将未提交的变化移除，稍后再移入 
$ git stash $ git stash pop
```



