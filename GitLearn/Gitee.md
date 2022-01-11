## 命令合集  

1.文件创建
```
$ mkdir learngit
//创建一个文件
$ cd learngit
//进入learngit文件夹
$ pwd
//显示当前目录
/Users/michael/learngit

```

2.初始化：初始化本地文件库
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/

```

3.提交过程
```
$ git add readme.txt
//添加文件
$ git add .
//将所有修改的都添加

$ git status
//查看当前库状态

$ git diff readme.txt 
//查看详细修改信息

$ git commit -m "wrote a readme file"
//提交到master分支

$ git log
//查看修改历史记录

$ git log --pretty=oneline
//查看复杂历史记录

$ git reset --hard HEAD^
//退回到上一个版本

$ git reset --hard 1094a
//跳转到指定版本1094a

$ git reflog
//记录每一次命令

```
3.删除文件
```

一、已经提交版本库
1.在文件中删除
$ rm test.txt

2.查看删除状态
$ git status

3.然后在版本库中删除，然后提交
$ git rm test.txt
$ git commit -m "remove test.txt"

二、误删版本库中还有文件可以恢复
$ git checkout -- test.txt
```

4.生成公钥
```
$ ssh-keygen -t rsa -C "208967048@qq.com"
//生成公钥

$ git remote add origin git@github.com:michaelliao/learngit.git

$ git remote add origingithub git@github.com:JuShuai-gif/learngit.git

$ git remote add origingitee git@gitee.com:JuShuai-gif/gitstudy.git

//添加远程库
//origin可以改
```

5.远程库
```
$ git push -u origin master
//提交（第一次提交）

$ git push origin master
//第二次以及以后提交


$ git remote -v
//查看远程库信息
origin  git@github.com:michaelliao/learn-git.git (fetch)
origin  git@github.com:michaelliao/learn-git.git (push)

$ git remote rm origin
//根据名字删除远程库

$ git clone git@github.com:michaelliao/gitskills.git
//克隆库

$ git clone git@gitee.com:JuShuai-gif/LearnNote.git



https://gitee.com/JuShuai-gif/gitstudy.git
```

6.分支管理

```
$ git checkout -b dev
//创建Dev分支，并切换到Dev分支

$ git branch dev
$ git checkout dev
//上面一句相当于下面两句

$ git branch
//查看分支，*为当前分支
* dev
  master

$ git checkout master
//Dev分支完成之后，切换回master分支

$ git merge dev
//将Dev分支合并到当前分支

$ git branch -d dev
//合并完成之后就可以删除Dev分支

$ git switch -c dev
//创建并切换到新的Dev分支

$ git switch master
//切换到已有的master分支

```













## Git与gitee  
我们在gitee中建好项目之后，名称最好和本地库一样：

然后，我们在本地库上使用命令`git remote add`把它和`Gitee`的远程库关联：

```
git remote add origin git@gitee.com:JuShuai-gif/gitstudy.git
```

之后，就可以正常地用`git push`和`git pull`推送了！

如果在使用命令`git remote add`时报错：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
fatal: remote origin already exists.
```

这说明本地库已经关联了一个名叫`origin`的远程库，此时，可以先用`git remote -v`查看远程库信息：

```
git remote -v
origin	git@github.com:michaelliao/learngit.git (fetch)
origin	git@github.com:michaelliao/learngit.git (push)
```

可以看到，本地库已经关联了`origin`的远程库，并且，该远程库指向`GitHub`。


我们可以删除已有的`GitHub`远程库：

```
git remote rm origin
```

再关联`Gitee`的远程库（注意路径中需要填写正确的用户名）：

```
git remote add origin git@gitee.com:liaoxuefeng/learngit.git
```

此时，我们再查看远程库信息：

```
git remote -v
origin	git@gitee.com:liaoxuefeng/learngit.git (fetch)
origin	git@gitee.com:liaoxuefeng/learngit.git (push)
```

现在可以看到，`origin`已经被关联到`Gitee`的远程库了。通过`git push`命令就可以把本地库推送到`Gitee`上。

有的小伙伴又要问了，一个本地库能不能既关联`GitHub`，又关联`Gitee`呢？

答案是肯定的，因为git本身是分布式版本控制系统，可以同步到另外一个远程库，当然也可以同步到另外两个远程库。

使用多个远程库时，我们要注意，git给远程库起的默认名称是origin，如果有多个远程库，我们需要用不同的名称来标识不同的远程库。

仍然以learngit本地库为例，我们先删除已关联的名为origin的远程库：

```
git remote rm origin
```

然后，先关联GitHub的远程库：

```
git remote add github git@github.com:michaelliao/learngit.git
```

注意，远程库的名称叫`github`，不叫`origin`了。

接着，再关联`Gitee`的远程库：

```
git remote add gitee git@gitee.com:liaoxuefeng/learngit.git
```

同样注意，远程库的名称叫`gitee`，不叫`origin`。

现在，我们用`git remote -v`查看远程库信息，可以看到两个远程库：

```
git remote -v
gitee	git@gitee.com:liaoxuefeng/learngit.git (fetch)
gitee	git@gitee.com:liaoxuefeng/learngit.git (push)
github	git@github.com:michaelliao/learngit.git (fetch)
github	git@github.com:michaelliao/learngit.git (push)
```

如果要推送到`GitHub`，使用命令：

```
git push github master
```

如果要推送到`Gitee`，使用命令：

```
git push gitee master
```

这样一来，我们的本地库就可以同时与多个远程库互相同步：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220111061753.png)




























