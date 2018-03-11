

<a href="https://git-scm.com" target="_blank" title="git">
<img alt="git" width="60" height="60" src="./assets/git-icon-logo.svg"/>
</a>

在这里简单的讲解 Git 基础入门使用。

## 全局设置

```bash
$ git config --global user.name "wcj"              # 你需要告诉git你的名字，这个名字会出现在你的提交记录中。
$ git config --global user.email "wcj@nihaosi.com" # 然后是你的Email，同样，这个Email也会出现在你的提交记录中
```

## 已有项目

克隆项目提交代码

```bash
$ git clone git@g.xxxxxx.cn:wcj/test.git # 克隆仓库
$ cd test                                # 进入文件夹
$ touch README.md                        # 通过 touch 命令创建一个 README.md
$ git add README.md
$ git commit -m "add README"
$ git push -u origin master
```

## 文件夹与仓库关联

```bash
$ cd existing_folder
$ git init
$ git remote add origin git@git.xxxxxx.cn:wcj/test.git
$ git add .
$ git commit -m "Initial commit"
$ git push -u origin master
```

## 现有的Git存储库

```bash
$ cd existing_repo
$ git remote rename origin old-origin
$ git remote add origin git@git.xxxxxx.cn:wangchujiang/tests.git
$ git push -u origin --all
$ git push -u origin --tags
```

## SSH Keys

SSH key 可以让你在你的电脑和 Git 之间建立安全的加密连接。

```bash
$ ssh-keygen -t rsa -C "xxxxx@xxxxx.cn" 
# Creates a new ssh key using the provided email
# Generating public/private rsa key pair...
```

查看你的public key，并把他添加到 Git @ Gitlab 中

```bash
$ cat ~/.ssh/id_rsa.pub
# ssh-rsa AAAAB31yc2EAAAADAQABAAABAQCNzaC6eNtGpNGwstc....
```

添加后，在终端（Terminal）中输入

```bash
ssh -T git@git.xxxxxx.cn
# 若返回
# Welcome to Git@Gitlab, yourname! 
# 则证明添加成功。
```

## git 常用命令

### help

```bash
git help config # 获取帮助信息  
```

### status

```bash
git status     # 查看当前状态  
```

### add

```bash
git add file                         # .或*代表全部添加到暂存区
git rm --cached <added_file_to_undo> # 在commit之前撤销git add操作
git reset head                       # 好像比上面`git rm --cached`更方便
```

### diff

```bash
git diff file               # 查看指定文件的差异
git diff --stat             # 查看简单的diff结果
git diff branch1 branch2    # 比较两次分支之间的差异
git diff commit commit      # 比较两次提交之间的差异
```

### commit

```bash
git commit                  # 提交更新
git commit -m 'message'     # 提交说明
git commit --amend          # 修改最后一次提交
git commit log              # 查看所有提交，包括没有push的commit
git commit -m "#133"        # 关联issue 任意位置带上# 符号加上issue号码
git commit -m "fix #133"    # commit关闭issue
```

### pull

```bash
git pull origin master      # 拉取远端分支到本地分支
git pull --all              # 获取远程所有内容包括tag
git pull origin next:master # 取回origin主机的next分支，与本地的master分支合并
git pull origin next        # 远程分支与当前分支合并
```

### push

```bash
git push -u origin master   # push同时设置默认跟踪分支
git push origin master      # 提交暂存区代码到master分支
git push -f origin master   # 强制推送文件，缩写 -f（全写--force）
```

### remote
 
```bash
git remote add origin git@github.com:JSLite/test.git # 添加源
```

### rm

```bash
rm *&git rm *               # 移除文件
git rm -f *                 # 移除文件
git rm --cached *           # 取消跟踪
git mv file_from file_to    # 重命名跟踪文件
git log                     # 查看提交记录
```

### reset

```bash
git revert HEAD             # 撤销前一次操作
git revert HEAD~            # 撤销前前一次操作
git revert commit           # 撤销指定操作
git reset HEAD *            # 取消已经暂存的文件
git reset --soft HEAD *     # 重置到指定状态，不会修改索引区和工作树
git reset --hard HEAD *     # 重置到指定状态，会修改索引区和工作树
git reset -- files *        # 重置index区文件
```

### checkout

```bash
git checkout -- file                         # 取消对文件的修改（从暂存区——覆盖worktree file）
git checkout branch|tag|commit -- file_name  # 从仓库取出file覆盖当前分支
git checkout HEAD~1 [文件]                    # 将会更新 working directory 去匹配某次 commit
git checkout -- .                            # 从暂存区取出文件覆盖工作区
```

### stash

```bash
git stash                    # 将工作区现场（已跟踪文件）储藏起来，等以后恢复后继续工作
git stash list               # 查看保存的工作现场
git stash apply              # 恢复工作现场
git stash drop               # 删除stash内容
git stash pop                # 恢复的同时直接删除stash内容
git stash apply stash@{0}    # 恢复指定的工作现场，当你保存了不只一份工作现场时
```

## 分支branch

### 删除

```bash
git push origin :branchName     # 删除远程分支
git push origin --delete new    # 删除远程分支new
git branch -d branchName        # 删除本地分支，强制删除用-D
git branch -D test              # 强制删除本地test分支
git remote prune origin         # 远程删除了，本地还能看到远程存在，这条命令删除远程不存在的分支
```

### 提交

```bash
git push -u origin branchName   # 提交分支到远程origin主机中
```

### 分支合并

```bash
git merge branchName       # 合并分支 - 将分支branchName和当前所在分支合并
git merge origin/master    # 在本地分支上合并远程分支
```

### 查看

```bash
git branch       # 列出本地分支
git branch -r    # 列出远端分支
git branch -a    # 列出所有分支
git branch -v    # 查看各个分支最后一个提交对象的信息
```

### 连接

```bash
git branch --set-upstream dev origin/dev     # 将本地dev分支与远程dev分支之间建立链接
git branch --set-upstream master origin/next # 手动建立追踪关系
```

### 分支切换

```bash
git checkout test           # 切换到test分支
git checkout -b test        # 新建+切换到test分支
git checkout -b test dev    # 基于dev新建test分支，并切换
```

## 忽略特殊文件

有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件，等等。  
好在Git考虑到了大家的感受，这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的 `.gitignore` 文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。

举个例子：

```
*.log
node_modules
.vscode/
package-lock.json
```

上面代码忽略编译产生的.log、node_modules等文件或目录  
不需要从头写 `.gitignore` 文件，GitHub已经为我们准备了各种配置文件，只需要组合一下就可以使用了。所有配置文件可以直接[在线浏览](https://github.com/github/gitignore)
最后一步就是把 `.gitignore` 也提交到Git，就完成了！

## 参考资料

- [Git-文档](https://git-scm.com/docs)
