# Git使用手册

>CHANGELOG
>
>2020/01/16    文档建立，添加 init，add，commit 命令
>
>2020/01/17    添加rm，diff，restore，reset，log命令
>
>2020/01/19    添加revert，branch，checkout，switch，merge，tag，stash，remote，fetch命令
>
>2020/01/20    添加pull，push命令

## 简单描述

git每次提交更新会对当时的文件制作一个快照，并保存该快照的索引，未改变的文件则会保留一个链接指向之前的文件。

git管理下的文件有三种状态：

- 已修改（modified）
- 已暂存（staged）
- 已提交（committed）

git管理下也相应有三种不同区域：

- 工作目录，对项目的某个版本独立提取出来的内容，放到了磁盘上以供修改
- 暂存区域，保存待提交的文件信息
- git仓库，保存项目元数据和对象数据库

`HEAD`特殊指针，指向当前所在的本地分支

## 版本控制

#### *git init*

在当前目录新建git版本库

#### *git clone*

将仓库克隆到本地

```shell
git clone <repository> [<directory>]

# 远程仓库支持4种url
git clone ssh://[user@]host.xz[:port]/path/to/repo.git/
git clone git://host.xz[:port]/path/to/repo.git/
git clone http[s]://host.xz[:port]/path/to/repo.git/
git clone ftp[s]://host.xz[:port]/path/to/repo.git/
# 其中，ssh有其简写形式：
git clone [user@]host.xz:path/to/repo.git/
```

#### *git add*

将文件的改动/新增/移除状态变化添加到暂存区

```shell
git add .
# <pathspec>使用.代指添加所有的文件状态变化

git add *.c
# <pathspec>使用文件匹配的形式添加某一类文件

git add dir
# <pathspec>为目录时，会添加指定目录下所有文件状态变化
```

#### *git commit*

将暂存区的内容提交到版本库，并附带一定的提交信息

注：使用`git commit`指令后，会自动打开配置默认的编辑器来编辑提交信息

```shell
git commit -m <msg>
git commit --message=<msg>
# 使用以上参数在commit命令中直接指定提交信息

git commit --amend
# 通过创建新的commit方式来替换上一次的commit，提交信息的编辑将以上次的提交信息作为起点
# 该命令会将暂存区的文件进行提交，但是如果暂存区为空，其效果只是修改提交信息

git commit -v
git commit --verbose
# 在commit输出信息的底部显示暂存区文件和当前分支顶端文件的差别
```

#### *git rm*

将文件工作区和索引中同时删除，近似于先`/bin/rm`再`git add .`

```shell
git rm -f <file>
git rm --force <file>
# 如果指定文件有未提交的改动，使用以上参数忽略检查，强制删除

git rm -r <file>
# 使用该参数可以迭代删除整个目录

git rm --cached <file>
# 使用该参数会将文件从索引中删除(包括暂存状态)，但工作区文件保留
```

#### *git diff*

显示工作区与索引中的文件差别或工作区和分支的文件差别，不指定文件即显示所有的变化，指定则只显示被指定文件的差异

```shell
git diff --no-index <path> <path>
# 显示2个指定文件的差别

git diff --cached [<commit>] [<path>...]
# 显示暂存区文件和指定commit的文件改动

git diff <commit> [<path>...]
# 显示工作区文件和指定commit的文件改动

git diff <commit> <commit> [<path>...]
# 显示2次commit之间的文件改动

git diff --stat
# 显示文件改动的总结(多少文件改变，几条增加，几条减少)
```

#### *git restore*

恢复工作区指定的文件，回归到上次commit的状态

```shell
git restore <pathspec>

git restore -S <pathspec>
git restore --staged <pathspec>
# 将暂存区的指定文件恢复到上次commit的状态

git restore -W <pathspec>
git restore --worktree <pathspec>
# 默认参数，将工作区的文件恢复到上次commit的状态

git restore -s <tree>
git restore --source=<tree>
# 将工作区的文件恢复到给定tree的状态，一般可以指定一次commit
```



#### *git reset*

```shell
git reset <pathspec>
# 将指定文件在暂存区的状态还原成为当前git仓库分支的状态，从作用上来看，基本等于git add的反向

git reset [<mode>] [<commit>]
# 将当前分支指针指向指定的commit，默认重置暂存区已暂存的文件改动
# mode参数:
--soft
# 不会影响暂存区和工作区的文件，只把当前分支的指针指向指定的commit
--mixed
# 重置暂存区，但不影响工作区，默认参数
--hard
# 同时重置暂存区和工作区
```

#### *git log*

显示commit日志

```shell
git log <file>
# 显示影响某单个文件的commit历史

git log -<number>
git log -n <number>
git log --max-count=<number>
# 限制log输出的最大数量

git log --author=<pattern>
git log --committer=<pattern>
# 显示指定author的comit历史

git log -p
# 额外显示提交差异差异

git log  --decorate
# 额外显示各个分支当前所指向的对象

git log --oneline 
# <abbrev hash> <title line>

git log --pretty=<format>
# 指定另一种格式
# format:
oneline
# <hash> <title line>
short
# commit <hash>
# Author: <author>
# 
# <title line>
medium
# commit <hash>
# Author: <author>
# Date: <author date>
# 
# <title line>
full
# commit <hash>
# Author: <author>
# Date: <author date>
# 
# <title line>
#
# <full commit message>
fuller
# commit <hash>
# Author: <author>
# Date: <author date>
# Commit:     <committer>
# CommitDate: <committer date>
# 
# <title line>
#
# <full commit message>
reference
# <abbrev hash> (<title line>, <short author date>)
```

*git revert \<commit\>*

通过创建一次新的commit，还原指定commit的改动

```shell
# examples:

git revert HEAD~3
# 还原过去的第4次commit

git revert -n master~5..master~2
# 还原master分支过去第5次commit到过去第2次commit所造成的改动
```

## 分支管理

#### *git branch*

显示，创建或删除分支

```shell
git branch
# 显示当前所在分支

git branch -r
# 显示已追踪的远程分支

git branch -a
# 同时显示本地分支和远程分支

git branch <branchname>
# 创建名为branchname的新分支，但不会切换到新的分支

git branch -m [<oldbranch>] <newbranch>
git branch -M [<oldbranch>] <newbranch> # forced
# 将旧分支改名为新分支

git branch -d [-r] <branchname>
# 删除指定分支，带上-r参数则指定删除远程分支

git banrch -u <upstream> [<branchname>]
git branch --set-upstream-to=<upstream> [<branchname>]
# 配置指定分支的追踪上游分支信息

git branch -v
git branch -vv
# 列出所有本地分支，并显示更多commit和跟踪的信息

git show-branch
# 列出所有分支(包括远程分支信息)
```

#### *git checkout*

切换分支或者恢复工作区域文件

```shell
git checkout [<branch>]
# 切换到指定分支
# 如果<branch>不存在，且存在一个远程分支下有同名的分支，将自动关联，相当于：
git checkout -b <branch> --track <remote>/<branch>

git checkout -b <new_branch> [<start point>]
git checkout -B <new_branch> [<start point>] # 已存在的分支会被重置覆盖
# 创建新的分支，并切换到新的分支下
```

#### *git switch*

切换分支

```shell
git switch <branch>
```

#### *git merge*

合并两个或多个分支

```shell
git merge <commit>
# 将指定commit合并到当前分支，使用分支名代表指定分支的指针所指向的commit
# 如果二者开发历史有分岔，将创建一次新commit来记录合并；
# 如果当前分支比指定commit老，则直接将最新的commit合并到当前分支；
# 如果当前分支比指定commit新，则不会产生变化

# 冲突状况
# 假如当前分支与指定commit分别对某一处代码进行了修改，将造成合并冲突
# 【解决方法】修改冲突代码，按照一次新commit过程进行提交，即解决冲突

git merge --abort
# 造成合并冲突时，中止合并的指令
```

#### *git stash*

将当前工作区域的改动暂时藏起来

```shell
git stash
# 将当前工作区域的区域的改动保存到stash区域

git stash list
# 将所有的stash内容列出来

git stash show [<stash>]
git stash drop [<stash>]
git stash pop [<stash>]
git stash apply [<stash>]
git stash clear
```

#### *git tag*

创建，列出，删除，或者验证标签

```shell
git tag <tagname> [<commit> | <object>]
# 为指定的commit或object添加一个tag引用，默认为HEAD
# 标签名不能重复，但是同一个commit可以打上多个标签

git tag -d <tagname>
git tag --delete <tagname>
# 删除存在的标签

git tag -l
git tag --list
# 列出所有的标签
# 以下为list的参数
git tag -l <pattern>
# 根据指定的pattern，可以只列出符合规则的tag
git tag -n<num>
```

## 远程开发

#### *git remote*

管理远程仓库

```shell
git remote [-v | --verbose]
# 显示已有的远程仓库，-v参数将提供关于fetch和push的更多信息

git remote add <name> <url>
# 添加名为<name>，位于<url>的远程仓库，使用git clone命令时会自动建立对应的默认远程仓库origin

git remote rename <old> <new>
# 修改指定远程仓库的命名

git remote show
# 显示更多的相关信息
```

#### *git fetch*

从远程仓库拉取本地没有的数据

```shell
git fetch [<repository>] [<refspec>]
# 从指定远程仓库路径拉取本地没有的数据，默认从origin拉取数据
# 如果<refspec>未指定，则将从remote.<reposiory>.fetch变量读取<refspec>数据
# <refspec>参数的完整格式为: [+]<src>:<dst>
# 	当<dst>为空时，":"可以省略
# 	tag <tag>相当于refs/tags/<tag>:refs/tags/<tag>
# 	TODO: 可选参数+
# fetch不会改变工作目录的内容，它会将拉取的内容保存到.git/FETCH_HEAD，并可以使用FETCH_HEAD指针接触它
```



#### *git pull*

```shell
git pull [<repository>] [<refspec>]
# 相当于2条命令的缩写形式
git fetch
git merge FETCH_HEAD

git pull --rebase
# 执行git rebase而非git merge
```

### *git push*

更新远程仓库

```shell
git push [<repository> [<refspec>]]
# 默认从branch.*.remote和remote.*.push参数获取推送配置

git push -f
git push --force
# 通常，push命令会拒绝更新不是本地仓库祖先的远程仓库，加上该参数会进行强制推送
```

#### *git rebase*

在另一个分支上重新应用提交

```shell
git rebase [<upstream> [<branch>]]
# 在指定的分支顶端，将当前分支所做的修改进行commit
# 在这个过程中也可能遇到冲突，同样使用参数：
git rebase --continue
git rebase --skip
git rebase --abort
```

## 常见问题

### 大致通用的参数选项

```shell
-q | --quiet
# 只输出错误信息

-v | --verbose
# 显示更加详细的信息
```

### ssh配置

```shell
git config --global user.name "your name"
git config --global user.email "email@example.com"
# 全局配置用户名和邮箱

ssh-keygen -o -t rsa -b 4096 -C "email@example.com"
# 生成RSA加密算法的ssh密钥，默认放在 
# ~/.ssh/id_rsa
# id_rsa.pub
# 把公钥上传到github或gitlab
```
