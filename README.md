# Git 命令行

### 一、常用 git 命令行

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







### 二、命令行简写的设置


### 三、
