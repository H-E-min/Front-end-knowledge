## git操作

### 查看当前分支

```
git branch
```

### 查看远程所有分支

```
git branch -a
```

### 切换到远程XX分支

```
git checkout XXX
```

### 新建XX分支，并切换到该分支

```
git checkout -b XXX
```

### 从git上拉取指定分支的代码

```
git clone -b 分支名字 项目地址
```

### git clone后使用子分支

```
git clone 项目地址
git branch -a
git checkout 子分支名称
git pull
```

### git更新本地代码

```
git pull
```

### git使用tag给代码打标签(版本号)

```
//附注标签（输出打标签者的信息、打标签的日期时间、附注信息，然后显示具体的提交信息。）
git tag -a 版本号 -m 'XXXXX'

//轻量标签（只会显示出提交信息）
git tag 版本号

git push origin 版本号		-----------将标签提交到远程仓库

//一次性推送多个
git push origin --tags
```



假设提交历史是这样的：

> ```console
> $ git log --pretty=oneline
> 15027957951b64cf874c3557a0f3547bd83b3ff6 Merge branch 'experiment'
> a6b4c97498bd301d84096da251c98a07c7723e65 beginning write support
> 0d52aaab4479697da7686c15f77a3d64d9165190 one more thing
> 6d52a271eda8725415634dd79daabbc4d9b6008e Merge branch 'experiment'
> 0b7434d86859cc7b8c3d5e1dddfed66ff742fcbc added a commit function
> 4682c3261057305bdd616e23b64b0857d832627b added a todo file
> 166ae0c4d3f420721acbb115cc33848dfcc2121a started write support
> 9fceb02d0ae598e95dc970b74767f19372d61af8 updated rakefile
> 964f16d36dfccde844893cac5b347e7b3d44abbc commit the todo
> 8a5cbc430f1a9c3d00faaeffd07798508422908a updated readme
> ```

```
//后期打标签
$ git tag -a v1.2 9fceb02		
//相当于在9fceb02d0ae598e95dc970b74767f19372d61af8(倒数第二条)上打标签
```

```
//删除标签
//删除掉本地仓库上的标签
git tag -d 标签名
//移除远程仓库标签
第一种：git push <remote> :refs/tags/<tagname>
eg:git push origin :refs/tags/v1.4-lw
第二种：git push origin --delete 标签名
```

```
查看标签：git tag

查看指定版本号：git show 版本号
```

### **创建本地分支并推送到远程**

```
 1.本地创建并切换分支
       git checkout -b dev(分支名)
 //补充：子分支的内容要提交时
 		需要git add . 
 		 	git commit -m ''
 		 	然后再执行2的内容
       
2.将dev分支推送到远程
   git push origin dev:dev
 
              冒号前面的dev：推送本地的dev分支到远程origin
              冒号后面的dev：远程origin没有会自动创建
 
3.建立本地到上游（远端）仓的链接，这样代码才能提交上去
       git branch --set-upstream-to=origin/dev
 
       
4.取消对master分支的跟踪
       git branch --unset-upstream master

//貌似只执行前两部github上代码就发生更新
```

### 将分支上的开发进度合并到主分支

```
git checkout master  //切换到master分支

git merge child1    //将分支 child1 的开发进度合并到 master 分支

//合并之后，master分支和child1分支会指向同一个位置。
```

### 删除本地分支

```
git branch -d 分支名
```

### 删除远程分支

```
 git push origin --delete 分支名
```

### 出现 could not read from remote repository

```
git remote set-url origin github项目的地址

git push -u origin master
```

