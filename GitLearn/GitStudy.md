## 在Windows上使用Git  

[直接从官网下载](https://git-scm.com/downloads)，进去直接安装就行，安装完成之后，在开始菜单里找到“Git->Git Bash”,就会出来一个命令行窗口的东西，说明安装成功！  
![image](https://www.liaoxuefeng.com/files/attachments/919018718363424/0)  
安装完成之后，还需要最后一步设置，命令行输入：  

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
上面的文件可以在我的电脑中可以找到，C:\Users\20896  中找到 **.gitconfig**  

什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。  
创建一个版本库很简单，首先，选择一个合适的地方创建一个空目录：（其实就是在你的电脑上创建一个文件夹，然后在哪个文件夹里面右键，选择git bash，然后执行下面的命令）  
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
```
pwd这个命令是显示当前这个仓库在电脑中的位置（切记这个路径是英文）  
第二步，通过`git init`命令把这个目录变成Git可以管理的仓库：
```
$ git init
```
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到`.git`目录，那是因为这个目录默认是隐藏的，用`ls -ah`命令或者在面板中设置一下就可以看见。  

### 把文件添加到版本库  
首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪Word文件的改动的，前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

因为文本是有编码的，比如中文有常用的GBK编码，日文有Shift_JIS编码，如果没有历史遗留问题，强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。  
  
<font face="黑体" color=red size=5>使用Windows要注意，不要用文本编辑器编辑文本文件容易出错</font>  
#### 把一个文件放在Git仓库只需两步  
##### 第一步，用命令`git add`告诉Git，把文件添加到仓库：
```
$ git add 笔记.md
//或者用下面这个
$ git add .
```
执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：
```
$ git commit -m "wrote a readme file"
//引号里面的是这次提交的信息
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```  
解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录。

`git commit`命令执行成功后会告诉你，`1 file changed：`1个文件被改动（我们新添加的readme.txt文件）；`2 insertions：`插入了两行内容（readme.txt有两行内容）。  

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：  
```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```  
### 小结
初始化一个Git仓库，使用`git init`命令。

添加文件到Git仓库，分两步：

1. 使用命令`git add <file>`，注意，可反复多次使用，添加多个文件；
2. 使用命令`git commit -m <message>`，完成。

我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改readme.txt文件,

现在，运行`git status`命令看看结果：

`git status`命令可以让我们时刻掌握仓库当前的状态，上面的命令输出告诉我们，`readme.txt`被修改过了，但还没有准备提交的修改。

尽管Git告诉我们`readme.txt`被修改了，但是具体修改了什么是不知道的，这时需要用`git diff` 这个命令查看：  
```
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
```
`git diff` 就是查看不同，看看和以往的文件有什么不同，知道对文件`笔记.md`做了什么修改  

**修改了文件之后我们就可以再次提交，这和新文件提交是一样的**  
命令如下：  
```
$ git add readme.txt
$ git status
$ git commit -m "add distributed"
```
每次修改完之后会出现下面：
```
$ git commit -m "增加了GPU"
[master 433e717] 增加了GPU
 1 file changed, 1 insertion(+), 1 deletion(-)
 //其中433e717就是这次提交的一个版本号，版本回退会用到
```
文件修改到一定程度的时候，就可以“保存一个快照”,这个快照在GIt中被称为`commit`。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个`commit`恢复，然后继续工作，而不是把几个月的工作成果全部丢失。

版本系统肯定有某个命令可以查看历史记录，在Git中，用`git log`命令查看:
```
$ git log
commit 4338ecc24997894b25a328418e6ab3f1ee86fe29 (HEAD -> master)
Author: 208967048@QQ.COM <208967048@QQ.COM>
Date:   Mon Jan 10 12:27:50 2022 +0800

    删除了一些文件

commit 2af9739449cfd8f7a195ad0f54007444a393ac5d
Author: 208967048@QQ.COM <208967048@QQ.COM>
Date:   Mon Jan 10 11:24:48 2022 +0800

    提交两次

commit 068ce7874fcbfac0ff8b1645379da5b86c08716c
Author: 208967048@QQ.COM <208967048@QQ.COM>
Date:   Mon Jan 10 11:13:03 2022 +0800

    测试提交
```
`git log`命令显示从最近到最远的提交日志,如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`--pretty=oneline`参数：
```
$ git log --pretty=oneline
433e717db47a4438857f59212cb152e2d4f385b9 (HEAD -> master) 增加了GPU
4338ecc24997894b25a328418e6ab3f1ee86fe29 删除了一些文件
2af9739449cfd8f7a195ad0f54007444a393ac5d 提交两次
068ce7874fcbfac0ff8b1645379da5b86c08716c 测试提交
```
**提示** :你看到的一大串类似1094adb...的是commit id（版本号），和SVN不一样，Git的commit id不是1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定冲突。

把readme.txt回退到上一个版本，也就是add distributed的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交1094adb...（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。

现在，我们要把当前版本append GPL回退到上一个版本add distributed，就可以使用git reset命令： 
```
$ cat readme.txt
Git is a distributed version control system.
Git is free software.
```
回退到上一个版本，如果后悔了依然可以回到刚才没退回的那个版本，可以查看`commit id`然后根据命令回退.
这时这个版本号就是`433e717`
```
$ git reset --hard 433e717
HEAD is now at 433e717 增加了GPU
```
**版本号不用写全，但是不能只写前两位**
Git的版本回退速度超级快，因为Git在内部有一个指向当前版本的`HEAD`指针，回退版本时就是回退的指针：
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110141027.png)
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110141128.png)

然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？

在Git中，总是有后悔药可以吃的。当你用`$ git reset --hard HEAD^`回退到`add distributed`版本时，再想恢复到`append GPL`，就必须找到`append GPL`的`commit id`。Git提供了一个命令`git reflog`用来记录你的每一次命令： 
```
$ git reflog
433e717 (HEAD -> master) HEAD@{0}: reset: moving to 433e717
4338ecc HEAD@{1}: reset: moving to HEAD^
433e717 (HEAD -> master) HEAD@{2}: commit: 增加了GPU
4338ecc HEAD@{3}: reset: moving to HEAD^
876fb3c HEAD@{4}: commit: 添加GPU
4338ecc HEAD@{5}: commit: 删除了一些文件
2af9739 HEAD@{6}: commit: 提交两次
068ce78 HEAD@{7}: commit (initial): 测试提交
```
**小结**

1. `HEAD`指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令`git reset --hard commit_id`。

2. 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本。

3. 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本。

## 工作区和暂存区 
### 工作区（Working Directory）
用户自己电脑上看到的目录就是工作区，比如我的`Gitcode`  
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110145122.png)
上图就是一个**工作区**  
### 版本库（Repository）  
工作区有一个隐藏目录`.git`，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为`stage`（或者叫`index`）的暂存区，还有Git为我们自动创建的第一个分支`master`，以及指向`master`的一个指针叫`HEAD`。
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110145511.png)

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：

第一步是用`git ad`d把文件添加进去，实际上就是把文件修改添加到暂存区；

第二步是用`git commit`提交更改，实际上就是把暂存区的所有内容提交到当前分支。

因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，`git commit`就是往`master`分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对`readme.txt`做个修改，比如加上一行内容：  
```
Git has a mutable index called stage.
```
然后再在Gitcode中添加一个文本文件license.md，然后用`git status`查看状态:
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   "\347\254\224\350\256\260.md"

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        License.md

no changes added to commit (use "git add" and/or "git commit -a")
```
Git非常清楚地告诉我们，`readme.txt`被修改了，而`LICENSE`还从来没有被添加过，所以它的状态是`Untracked`。

现在，使用两次命令`git add`，把`readme.txt`和`LICENSE`都添加后，用`git status`再查看一下：
```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   License.md
        modified:   "\347\254\224\350\256\260.md"
```
现在，暂存区的状态就变成下面这样：
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110151130.png)  

所以，`git add`命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，执行`git commit`就可以一次性把暂存区的所有修改提交到分支。
```
$ git commit -m "understand how stage works"
[master 6ff0349] understand how stage works
 2 files changed, 2 insertions(+)
 create mode 100644 License.md
```
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：
```
$ git status
On branch master
nothing to commit, working tree clean
```
就会变成下面这个样子：  
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110151508.png)

### 管理修改  
现在，假定你已经完全掌握了暂存区的概念。下面，我们要讨论的就是，为什么Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件。

你会问，什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对readme.txt做一个修改，比如加一行内容：  
```
Gpu
Git has a mutable index called stage.

add a line    //第一次修改的一行
```
然后进行添加：
```
$ git add .
```
然后查看状态：
```
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   "\347\254\224\350\256\260.md"
```
然后再修改：
```
Gpu
Git has a mutable index called stage.

add a line
add  two  line       //第二次修改的一行
```
提交：
```
$ git commit -m "git teack changes"
[master 4b0f4cd] git teack changes
 1 file changed, 3 insertions(+), 1 deletion(-)
```
提交后查看状态：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   "\347\254\224\350\256\260.md"

no changes added to commit (use "git add" and/or "git commit -a")
```

很明显第二次的修改没有提交。
操作过程：

第一次修改 -> `git add` -> 第二次修改 -> `git commit`

说明第二次修改确实没有被提交。

那怎么提交第二次修改呢？你可以继续`git add`再`git commit`，也可以别着急提交第一次修改，先`git add`第二次修改，再`git commit`，就相当于把两次修改合并后一块提交了：

第一次修改 -> `git add` -> 第二次修改 -> `git add -> `git commit`

**提交时一次性把stage全部提交到master**  

### 撤销修改   
**小结**

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD <file>`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考`版本回退`一节，不过前提是没有推送到远程库。
### 删除文件
在Git中，删除也是一个修改操作，我们实战一下，先添加一个新文件`test.txt`到Git并且提交：  
```
$ git add test.txt

$ git commit -m "add test.txt"
[master b84166e] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
```

一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用rm命令删了：
```  
$ rm test.txt
```
这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：
```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    test.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
现在，文件就从版本库中被删除了。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：
```
$ git checkout -- test.txt
```
`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。

<font face="黑体" color=red size=5> 注意：从来没有被添加到版本库就被删除的文件，是无法恢复的！</font>  
**上面的过程就是，如果你再工作区创建了一个文件，你commit提交到版本库中，假如说你在电脑把这个文件删了，依然可以通过一些命令恢复这个文件**
## 远程仓库
Git是分布式版本控制系统，同一个Git仓库，可以分布到不同的机器上。怎么分布呢？最早，肯定只有一台机器有一个原始版本库，此后，别的机器可以“克隆”这个原始版本库，而且每台机器的版本库其实都是一样的，并没有主次之分。

你肯定会想，至少需要两台机器才能玩远程库不是？但是我只有一台电脑，怎么玩？

其实一台电脑上也是可以克隆多个版本库的，只要不在同一个目录下。不过，现实生活中是不会有人这么傻的在一台电脑上搞几个远程库玩，因为一台电脑上搞几个远程库完全没有意义，而且硬盘挂了会导致所有库都挂掉，所以我也不告诉你在一台电脑上怎么克隆多个仓库。

实际情况往往是这样，找一台电脑充当服务器的角色，每天24小时开机，其他每个人都从这个“服务器”仓库克隆一份到自己的电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库中拉取别人的提交。

完全可以自己搭建一台运行Git的服务器，不过现阶段，为了学Git先搭个服务器绝对是小题大作。好在这个世界上有个叫GitHub的神奇的网站，从名字就可以看出，这个网站就是提供Git仓库托管服务的，所以，只要注册一个GitHub账号，就可以免费获得Git远程仓库。

在继续阅读后续内容前，请自行注册GitHub账号。由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是`SSH Key`的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110161409.png)

点“Add Key”，你就应该看到已经添加的Key：
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110161435.png)

为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。

如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内部开发必备。
### 添加远程库
现在的情景是，你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举多得。

首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110161839.png)

在Repository name填入`learngi`t，其他保持默认设置，点击“Create repository”按钮，就成功地创建了一个新的Git仓库：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110161857.png)

目前，在GitHub上的这个`learngit`仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

```
$ git remote add origin git@github.com:JuShuai-gif/learngit.git

```
请千万注意，把上面的michaelliao替换成你自己的GitHub账户名，否则，你在本地关联的就是我的远程库，关联没有问题，但是你以后推送是推不上去的，因为你的SSH Key公钥不在我的账户列表中。

添加后，远程库的名字就是origin，这是Git默认的叫法，也可以改成别的，但是origin这个名字一看就知道是远程库。

下一步，就可以把本地库的所有内容推送到远程库上：

```
$ git push -u origin master
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支master推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

推送成功后，可以立刻在GitHub页面中看到远程库的内容已经和本地一模一样：
![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110162954.png)

从现在起，只要本地作了提交，就可以通过命令：

```
$ git push origin master
```
把本地master分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！

#### SSH 警告
当你第一次使用Git的`clone`或者`push`命令连接`GitHub`时，会得到一个警告：

```
The authenticity of host 'github.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is xx.xx.xx.xx.xx.
Are you sure you want to continue connecting (yes/no)?
```

这是因为Git使用SSH连接，而SSH连接在第一次验证GitHub服务器的Key时，需要你确认GitHub的Key的指纹信息是否真的来自GitHub的服务器，输入yes回车即可。

Git会输出一个警告，告诉你已经把GitHub的Key添加到本机的一个信任列表里了：

```
Warning: Permanently added 'github.com' (RSA) to the list of known hosts.
```

这个警告只会出现一次，后面的操作就不会有任何警告了。

如果你实在担心有人冒充GitHub服务器，输入yes前可以对照GitHub的RSA Key的指纹信息是否与SSH连接给出的一致。


#### 删除远程库
如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

```
$ git remote -v
origin  git@github.com:JuShuai-gif/learngit.git (fetch)
origin  git@github.com:JuShuai-gif/learngit.git (push)
```

然后，根据名字删除，比如删除`origin`：

```
$ git remote rm origin
```
此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

总结：
要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git；`

关联一个远程库时必须给远程库指定一个名字，`origin`是默认习惯命名；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；


### 克隆远程库
现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

首先，登陆GitHub，创建一个新的仓库，名字叫text-：

远程库建好之后，下一步是用命令`git clone`克隆一个本地库：

```
$ git clone git@github.com:JuShuai-gif/text-.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

注意把Git库的地址换成你自己的，然后进入`gitskills`目录看看，已经有`README.md`文件了：

```
$ cd text-
$ ls
README.md
```

如果有多个人协作开发，那么每个人各自从远程克隆一份就可以了。

你也许还注意到，GitHub给出的地址不止一个，还可以用https://github.com/michaelliao/gitskills.git这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。


## 分支管理

### 创建与合并分支

在版本回退里，你已经知道，每次提交，`Git`都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在`Git`里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，`Git`用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110171911.png)


每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长。

当我们创建新的分支，例如`dev`时，`Git`新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110172009.png)


你看，`Git`创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110172101.png)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。`Git`怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110172209.png)

所以`Git`合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110172247.png)

真是太神奇了，你看得出来有些提交是通过分支完成的吗？

下面开始实战。

首先，我们创建`dev`分支，然后切换到`dev`分支：

```
$ git checkout -b dev
Switched to a new branch 'dev'
```
`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后，用`git branch`命令查看当前分支：

```
$ git branch
* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个*号。

然后，我们就可以在dev分支上正常提交，比如对`readme.txt`做个修改，加上一行：

```
Creating a new branch is quick.
```

然后提交：

```
$ git add readme.txt 
$ git commit -m "branch test"
[dev b17d20e] branch test
 1 file changed, 1 insertion(+)
```

现在，`dev`分支的工作完成，我们就可以切换回`master`分支：

```
$ git checkout master
Switched to branch 'master'
```

切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：

![](https://gitee.com/JuShuai-gif/blog-image/raw/master/20220110175310.png)

现在，我们把dev分支的工作成果合并到`master`分支上：

```
$ git merge dev
Updating d46f35e..b17d20e
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

`git merge`命令用于合并指定分支到当前分支。合并后，再查看`readme.txt`的内容，就可以看到，和`dev`分支的最新提交是完全一样的。

注意到上面的`Fast-forward`信息，`Git`告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。

当然，也不是每次合并都能`Fast-forward`，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除`dev`分支了：

```
$ git branch -d dev
Deleted branch dev (was b17d20e).
```

删除后，查看`branch`，就只剩下`master`分支了：

```
$ git branch
* master
```
因为创建、合并和删除分支非常快，所以`Git`鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。


## switch
我们注意到切换分支使用`git checkout <branch>`，而前面讲过的撤销修改则是`git checkout -- <file>`，同一个命令，有两种作用，确实有点令人迷惑。

实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的`Git`提供了新的`git switch`命令来切换分支：

创建并切换到新的`dev`分支，可以使用：

```
$ git switch -c dev
```

直接切换到已有的`master`分支，可以使用：

```
$ git switch master
```

使用新的`git switch`命令，比`git checkout`要更容易理解。


**总结**：

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`或者`git switch <name>`

创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`




This is an H1
=======

This is an H2
----------

# this is H1

## this is H2

###### this is H6  

**这是加粗**
__这也是加粗__
*这是倾斜*
_这也是倾斜_
***这是加粗倾斜***
~~fegthtrhd~~
* * *
***
**********
- - -
_________________
> This is a blockquote with two paragraphs. Lorem ipsum dolor sit amet,
> consectetuer adipiscing elit. Aliquam hendrerit mi posuere lectus.
> Vestibulum enim wisi, viverra nec, fringilla in, laoreet vitae, risus.
>
> Donec sit amet nisl. Aliquam semper ipsum sit amet velit. Suspendisse
> id sem consectetuer libero luctus adipiscing.  

- 列表内容

- 列表内容

- 列表内容

注意：- + * 跟内容之间都要有一个空格

1. Bird
1. McHale
1. Parish

- 一级无序列表内容

  - 二级无序列表内容
  - 二级无序列表内容
  - 二级无序列表内容  

- Lorem ipsum dolor sit amet, consectetuer adipiscing elit.
    Aliquam hendrerit mi posuere lectus. Vestibulum enim wisi,
    viverra nec, fringilla in, laoreet vitae, risus.
- Donec sit amet nisl. Aliquam semper ipsum sit amet velit.
    Suspendisse id sem consectetuer libero luctus adipiscing

表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

这是一个普通段落：

    这是一个代码区块。

这里有一句代码`代码内容`。

```
  代码...
  代码...
  代码...
```

是为了防止转译，实际是没有的。

<font face="黑体">我是黑体字</font>
<font face="微软雅黑">我是微软雅黑</font>
<font face="STCAIYUN">我是华文彩云</font>
<font color=red>我是红色</font>
<font color=#008000>我是绿色</font>
<font color=Blue>我是蓝色</font>
<font size=5>我是尺寸</font>
<font face="黑体" color=green size=5>我是黑体，绿色，尺寸为5</font>

<table><tr><td bgcolor=yellow>背景色yellow</td></tr></table>  
  

<center>居中</center>
<p align="left">左对齐</p>
<p align="right">右对齐</p>  


H<sub>2</sub>O  CO<sub>2</sub>
爆米<sup>TM</sup>  

This is [an example](http://example.com/ "Title") inline link.

[This link](http://example.net/) has no title attribute.

<a href="超链接地址" target="_blank">超链接名</a>


<http://example.com/>

![Alt pic](/path/to/img.jpg)

![Alt pic](/path/to/img.jpg "Optional title")

<div align=center>![Alt pic] (http:...)  

<img src="http:..." width = "100" height = "100" div align=right />  


插入到段落里面的
$ X\stackrel{F}{\longrightarrow}Y $  


 $(x,y)^{T}$