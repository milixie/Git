# Git

## Git是什么

git 是一个分布式版本控制系统，可以查看 谁 在哪个时间段 修改了什么内容，查看特定版本修订情况的系统

### 集中式 vs 分布式

#### 集中式版本控制系统：CVS/SVN

特点：

- 版本库存放在中央服务器，工作的时候，每个人都需要从中央服务器中获取最新的代码库，然后干活，干完活儿后将代码推送到中央服务器

- 必须在联网的状态下才可以进行，网速慢的话提交起来特别慢

- 不安全，如果中央服务器出问题了，所有人都没办法工作了

![http://www.liaoxuefeng.com/files/attachments/001384860735706fd4c70aa2ce24b45a8ade85109b0222b000/0](http://www.liaoxuefeng.com/files/attachments/001384860735706fd4c70aa2ce24b45a8ade85109b0222b000/0)

#### 分布式版本控制系统：Git

特点：

- 分布式版本控制系统通常也有一台充当“中央服务器”的电脑，但这个服务器的作用仅仅是用来方便“交换”大家的修改，没有它大家也一样干活，只是交换修改不方便而已，所以没有真正中央服务器的概念

- 不需要联网就可以干活儿

- 安全性高，每个人的电脑都是一个版本库，每次从远程 clone 代码仓库的时候都是把对代码库的完整备份，每次提交保存的都是一系列不同时刻的文件快照，如果一个人的电脑坏掉或者代码污染了，都可以直接 copy 一份其他人的代码，或者使用版本管理找到之前的代码

- 强大的分支管理(允许成千上万个并行开发的分支)

![http://www.liaoxuefeng.com/files/attachments/0013848607465969378d7e6d5e6452d8161cf472f835523000/0](http://www.liaoxuefeng.com/files/attachments/0013848607465969378d7e6d5e6452d8161cf472f835523000/0)

=============

## Git 安装 and 设置用户

- 可以直接去 git 官网去下载：[https://git-scm.com/](https://git-scm.com/) 

- 可以直接使用 git Bash 去操作命令行 git，也可以下载类似于 sourceTree 这样的图形化 git 操作界面去操作

- linux 系统中可以使用命令行直接安装

```
sudo apt-get install git  //ubuntu、debian等
sudo yum install git  //redHat等
```

### 远程仓库
可以自己搭建，也可以使用像 github 这样的提供 git 仓库托管服务的远程仓库。
Github 网站提供 git 仓库托管服务的，本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
```
ssh-keygen -t rsa -C "youremail@example.com"
```

查看 id_rsa.pub
```
cat ~/.ssh/id_rsa.pub
```
把里面的内容粘贴到 github 里面的 ssh-key 里面

- 安装 git 后需要自报家门，设置自己的相关信息，包括 name 和 email，每一个 Git 的提交都会使用这些信息，并且它会写入到你的每一次提交中

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

```

=============

## Git 的状态、工作区域、工作流以及文件的生命周期

#### git 有三种状态： 

已提交`committed`，已修改`modified`，已暂存`staged`

- 已提交 `committed`: 表示数据已经安全的保存到本地的数据库中，执行 `git commit -m 'msg'`后就是提交状态

- 已修改 `modified`: 已经修改，但是还没有保存到数据库，对本地文件修改

- 已暂存 `staged`: 表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中，在暂存区域，执行`git add file` 后就暂存了

#### git 工作区域：

Git 项目的三个工作区域的概念：
- Git 仓库: Git 仓库目录是 Git 用来保存项目的元数据和对象数据库的地方。 这是 Git 中最重要的部分，从其它计算机克隆仓库时，拷贝的就是这里的数据。

- 工作目录: 工作目录是对项目的某个版本独立提取出来的内容。 这些从 Git 仓库的压缩数据库中提取出来的文件，放在磁盘上供你使用或修改。

- 暂存区域: 暂存区域是一个文件，保存了下次将提交的文件列表信息，一般在 Git 仓库目录中。 有时候也被称作`‘索引’`，不过一般说法还是叫暂存区域。

![https://git-scm.com/book/en/v2/images/areas.png](https://git-scm.com/book/en/v2/images/areas.png)

#### git 工作流：

- 在工作目录中修改文件。

- 暂存文件，将文件的快照放入暂存区域。

- 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

![http://www.liaoxuefeng.com/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0](http://www.liaoxuefeng.com/files/attachments/001384907720458e56751df1c474485b697575073c40ae9000/0)

#### 使用git时文件的生命周期

工作目录中的文件状态有两种：已跟踪、未跟踪

已跟踪文件：指那些被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区

未跟踪文件：已跟踪以外的文件，它们既不存在于上次快照的记录中，也没有放入暂存区

初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态

![https://git-scm.com/book/en/v2/images/lifecycle.png](https://git-scm.com/book/en/v2/images/lifecycle.png)

## 常用 git 命令行

### 项目创建相关

- 克隆一个已经创建的远程项目

```
git clone git@github.com:milixie/Git.git
git clone git@github.com:milixie/Git.git new_name (把仓库名称变更为new_name)
```

- 把一个目录变成使用 git 管理的本地仓库

```
git init
```
这个时候仓库就创建好了，是一个空的仓库，里面有一个文件`.git`，可以使用`ls -ah`命令可以看见隐藏的文件

- 如果不小心将文件目录 init，那么撤销初始化后的目录文件命令是：把里面的`.git`文件删除即可

```
rm -rf .git
```

### 分支相关

* git 强大的一个原因就是它有强大的分支管理，打个比方：使用 github 为 git 的远程仓库，开发一个网站，每个人都基于 product branch 生产环境的主分支去新建一个新的分支，在各自的分支上进行开发，突然线上有一个紧急 bug 需要修复，你可以切换到主分支上，再切出一个新分支进行 hotfix，修复完成测试成功后，可以将这个分支合并到主分支上，然后再切换到你的原来的那个分支上，可以 merge 一下主分支，然后继续工作

- 创建并切换新分支

```
git checkout -b mas-git-learn
```

- 基于当前分支创建新分支，不会切换到新的分支上

```
git branch mas-new-branch
```

- 查看本地分支

```
git branch
```

- 查看远程所有分支

```
git branch -r
```
比如说你刚 clone 了一个新的项目，本地只有 master 分支，想要拉取远程分支的话

1.可以先查看远程分支，再直接`git checkout mas-git-learn`

2.也可以先新建一个同名的分支`git checkout -b mas-git-learn`， 然后 `pull` 一下远程的分支`git pull origin mas-git-learn`

3.可以这样：`git checkout -b dev origin/dev`

- 查看每一个分支的最后一次提交

```
git branch -v
```
- 查看合并分支/未合并分支
```
git branch --merged
git branch --no-merged
```

- 切换分支

```
git checkout branch_name
```

- 删除分支，切换到另一个分支上去删除一个分支

```
git branch -d mas-git-learn
git branch -D mas-git-learn （强行删除分支）
```

- 基于远程分支创建新的可追溯的分支，新建的分支相当于是远程分支一个备份

```
git branch new_branch_name remote_branch_name
```

### 本地修改与提交

- 查看本地状态

```
git status
git status -s (一种更为紧凑的格式输出)
git status --short (一种更为紧凑的格式输出)
```

- 查看本地文件变更

```
git diff  （modified）
git diff --staged (暂存区)
git diff --cached (暂存区)
```

- 查看本地所有文件（包括已经存在暂存区的但是还没commit的文件）与commit的不同

```
git diff HEAD -- README.md
```

- 把本地提交修改添加到暂存区中

```
git add .
git add home/index.html
```

- 提交暂存区文件，附加消息提交

```
git commit -m 'update readme'
```

- 将暂存状态中的文件还原成修改状态的文件

```
git reset .
git reset home/index.html
```

- 将修改的文件（包括暂存区staged和modified 状态的文件）回退到上一个版本

```
git reset --hard HARD
```

- 将(本地所有修改的、暂存的、提交的文件)回退到当前的版本

```
git reset --hard HARD^
```

- 将内容回退到某个之前的版本

```
git reset --hard 'commit id'/'hash'
git reset --hard d75126c2a57c58f69ad77255b25c4edc9b98c5ef
git reset --hard 73057a8
```

- 将回退后的版本再更新到最新的，可以先使用一个命令查看你的每一次命令，找到最新的 commit id

```
git reflog
git reset --hard 'commit id'
```

- 将本地修改的文件重置成没有修改的，但是会暂存到本地

```
git stash
git stash list
```

- 放弃本地文件的修改，不会暂存到本地

```
git checkout . (放弃所有文件)
git checkout HEAD fila_name (放弃某个文件)
git checkout -- fila_name (放弃某个文件)
```

- stash后再次还原修改后的内容（暂存到本地）
```
git stash pop (内容恢复后，stash内容会删除)
git stash apply (内容恢复后，stash 内容不会删除)
git stash drop (可以把stash 在某个地方的内容删掉)
```

- 将 stash 后暂存到本地的数据清除掉

```
git stash clear
```

### 搜索相关

- 搜索某个单词(在某个版本)
```
git grep html
git grep html v0.01
```

### 提交历史相关

- 查看提交历史记录

```
git log
git log --oneline (仅显示提交的 hash 和 message)
git log --pretty=oneline (仅显示提交的 commit id 和 message)
git log --oneline --decorate --graph --all (输出你的提交历史、各个分支的指向以及项目的分支分叉情况)
git log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit (更详细的提交历史，类似于 sourceTree)
git log --author="milixie" (查看本作者提交记录)
git log -p (显示所有提交的文件的具体修改)
git log -p README.md (显示某个文件的所有修改)
git log -p -2 (加参数-2表示显示最近两次提交)
git log --stat (所有提交的简略的统计信息)
git blame README.md (显示 某个作者、在什么时间修改了这个文件的具体内容)
```

### 更新与发布

- 列出当前配置的远程端

```
git remote -v
```

- 重命名远程仓库的名称

```
git remote rename up(旧名称) upstream(新名称)
```

- 显示远程端的具体信息

```
git remote show origin 
```

- 添加新的远程端

```
git remote add mili git@github.com:milixie/forestry.git
```

- 移除一个本地仓库

```
git remote rm up
```

- 下载远程端版本，并自动与HEAD版本合并：
```
git remote pull remote_name url
```

- 从远程端拉取最新的代码，也就是从服务器上抓取本地没有的数据，它并不会修改工作目录中的内容，它只会获取数据然后让你自己合并
```
git fetch 
git fetch remote_name
```

- 从远程端拉取最新的代码，并且合并到本地

```
git pull
这个命令相当于：
git fetch 
git merge branch_name
```
- 将本地版本发布到远程端

```
git push 
git push origin master 
```
- 删除远程端分支

```
git push origin --delete mas-new-branch
git push origin:mas-new-branch   (试了这个不行)
```

### 合并、变基与重置

整合来自不同分支的修改主要有两种方法：merge合并 以及 rebase变基

#### 合并

- 将本地的某个分支合并到当前分支中：
```
git merge mas-new-branch
```
- 解决冲突

```
<<<<<<< HEAD
本地文件冲突内容
=======
合并的文件冲突内容
>>>>>>> feature1
```
这里 HEAD 表示当前分支的内容，后面的表示合并文件中冲突的内容，可以选择性的留下其中一个，也可以手动合并其中的内容

- 查看解决冲突的合并情况

```
git log --graph --pretty=oneline --abbrev-commit
git log --graph
```
- 合并时候提交 commit 内容，合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并

```
git merge --no-ff -m "merge with no-ff" dev
```

![合并图](http://www.liaoxuefeng.com/files/attachments/001384909239390d355eb07d9d64305b6322aaf4edac1e3000/0)

#### 变基

在某一个子分支上 rebase 它的父分支，那么将会在父分支上把本子分支的 commit 重演一遍，如果子分支上提交的 commit 比较多，那么可能会出现比较多的冲突，变基操作的实质是丢弃一些现有的提交，然后相应地新建一些内容一样但实际上不同的提交，rebase 命令重新整理了提交并再次推送，所以如果别人会基于一个分支去拉取代码进行开发，最好不要在该分支上进行 rebase 操作

```
git rebase origin/master
```
- 在 rebase 过程中一个 commit 成功后转到下一个 commit 的时候使用
```
git rebase --continue
```
- 在 rebase 过程中如果想退出

```
git rebase --abort
```

- rebase 完成后，使用 `git push` 后会不成功，需要强推才会成功，但是要注意，如果这个分支别其他伙伴正在上面修改内容，这个他在推送他的提交的时候可能会出问题，所以如果这个分支只有自己在用的话，可以 rebase 也可以强推，但是如果和别人合作的话最好不要使用 rebase，而要使用 merge

![变基图例](https://git-scm.com/book/en/v2/images/interesting-rebase-4.png)

- 重置已经提交的文件，比如说你有一个文件已经提交了，但是想重置掉

```
git revert commit_id
```

### 移动文件

```
git mv file_name file_to
```

### 删除文件

```
rm text.txt
git add text.txt
git commit -m 'delete'
git push 
```
或
```
git rm text.txt
git commit -m  'delete'
git push 
```

## 标签相关

- 查看标签

```
git tag
```
- 打标签

```
git tag -a v0.0.1 -m 'version0.0.1'
```
- 显示标签详细信息

```
git show v0.0.1
```
- 把标签推送到远程，成为了共享标签
```
git push origin v0.0.1
git push origin --tags (所有标签)
```

 











=============

## Git别名的设置

- 查看配置信息
```
git config --list
```
- 给一些配置设置别名
```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```
访问的时候直接可以使用简称，这样节省时间
```
git co / gco
git br / gbr
git ci 
git st / gst
```
- 帮助
```
git help 
git help name
```

=============

## Git多人协作时应该注意的问题：

- 多人并行开发，分布式 git 提供了很好的分支管理，但是在解决冲突和合并的过程中，还是会造成很多困扰，也可能会出现很多问题，所以在开发过程中，需要去关注主分支的变化，并且能够及时的将主分支的内容 merge 到本地正在开发的分支，这样有冲突了也可以及时解决，不至于本地分支与线上分支差距太大，造成冲突太多难以解决

- 合并分支时如果有冲突，根据`<<<<<<< HEAD`/`====`/`>>>>>>>>>`去划分，`HEAD`里面的是本地正在开发的修改，后面的是合并分支的修改，依情况而定，去删除其中一个，留下正确的内容

- 主分支合并子分支时，最好是先在子分支的基础上去合并主分支，有冲突解决冲突，这样再在主分支上合并子分支时就没冲突了


参考文献：
[https://git-scm.com/book/zh/v2](https://git-scm.com/book/zh/v2)











