# Git

### Git是什么

git 是一个分布式版本控制系统，可以查看 谁 在哪个时间段 修改了什么内容，查看特定版本修订情况的系统

#### 集中式 vs 分布式

集中式版本控制系统：CVS/SVN

特点：

- 版本库存放在中央服务器，工作的时候，每个人都需要从中央服务器中获取最新的代码库，然后干活，干完活儿后将代码推送到中央服务器

- 必须在联网的状态下才可以进行，网速慢的话提交起来特别慢

- 不安全，如果中央服务器出问题了，所有人都没办法工作了

- 强大的分支管理

分布式版本控制系统：Git

特点：

- 没有中央服务器

- 不需要联网就可以就可以干活儿

- 安全性高，每个人的电脑都是一个版本库，如果一个人的电脑坏掉或者代码污染了，都可以直接 copy 一份其他人的代码

### 常用 git 命令行

#### 项目创建相关

- 克隆一个已经创建的远程项目

```
git clone git@github.com:milixie/Git.git
```

- 创建一个新的本地仓库

```
git init
```

- 如果不小心将文件目录 init，那么撤销初始化后的目录文件命令是：

```
rm -rf .git
```

#### 分支相关

- 创建并切换新分支

```
git checkout -b mas-git-learn
```

- 基于当前分支创建新分支

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
想要拉取远程分支的话
1.可以先查看远程分支，再直接`git checkout mas-git-learn`
2.也可以先新建一个同名的分支`git checkout -b mas-git-learn`， 然后 `pull` 一下远程的分支`git pull origin mas-git-learn`

- 切换分支

```
git checkout branch_name
```

- 删除分支，切换到另一个分支上去删除一个分支

```
git branch -d mas-git-learn
```

- 基于远程分支创建新的可追溯的分支，新建的分支相当于是远程分支一个备份

```
git branch new_branch_name remote_branch_name
```

#### 本地修改与提交

- 查看本地状态

```
git status
```
- 查看本地文件变更

```
git diff
```

- 把本地提交修改添加到提交中

```
git add .
git add home/index.html
```

- 提交本地修改，附加消息提交

```
git commit -m 'update readme'
```

- 将添加到提交中还原成未提交状态

```
git reset .
git reset home/index.html
```

- 将本地修改的文件重置成没有修改的

```
git stash
```
- stash后再次还原修改后的内容
```
git stash pop
```

#### 搜索相关

- 搜索某个单词(在某个版本)
```
git grep html
git grep html v0.01
```

#### 提交历史相关

- 查看提交历史记录

```
git log
git log --oneline (仅显示提交的hash和message)
git log --author="milixie" (查看本作者提交记录)
git log -p README.md (显示某个文件的所有修改)
git blame README.md (显示 某个作者、在什么时间修改了这个文件的具体内容)
```











### 二、命令行简写的设置


### 三、
