# git常用命令

安装
---

> `GitHub Desktop` 提供了包含图形界面的桌面客户端，通过客户端可以完成大部分常用的仓库操作，同时可以自动更新Git的命令行版本，以适应新的场景。

Git 全平台版

https://git-scm.com

GitHub Desktop

https://desktop.github.com

配置
---

> 对所有本地仓库的用户信息进行配置

对你的 commit 操作设置关联的用户名

```shell
git config --global user.name "[name]"
```

对你的 commit 操作设置关联的邮箱地址

```shell
git config --global user.email "[email address]"
```

更新默认编辑器

```shell
git config --global core.editor "vim"
```

**创建 SSH 连接**

默认全局

```shell
ssh-keygen -t rsa -C "[your github email]"
```

指定别名

```shell
ssh-keygen -t rsa -C "[your github email]" -f ~/.ssh/github-rsa
```

**更新仓库地址为 SSH 连接**

获取远程连接信息

```shell
git remote -v
```

更新远程 url 

```shell
git remote set-url [remote] git@github.com:[your repository].git
```

**remote 的默认别名是 origin**

检查是否连接到 GitHub 

```shell
ssh -T git@github.com
```

增加代理

```shell
git config --global http.proxy 'socks5://127.0.0.1:1080'
git config --global https.proxy 'socks5://127.0.0.1:1080'
```

根据 .gitignore 更新文件缓存

```shell
git rm -r --cached . && git add . && git commit -m 'update .gitignore'
```

创建
---

创建一个本地的仓库，并设置名字

```shell
git init [project-name]
```

下载一个项目以及它所有的版本历ß史

```shell
git clone [url]
```

更改
---

> 检查已有的编辑并执行 commit 操作

列出所有新建或者更改的文件，这些文件需要被 commit

```shell
git status
```

展示那些没有暂存文件的差异

```shell
git diff
```

将文件进行快照处理用于版本控制

```shell
git add [file]
```

展示暂存文件与最新版本之间的不同

```shell
git diff --staged
```

将文件移除暂存区，但是保留其内容

```shell
git reset [file]
```

将文件快照永久地记录在版本历史中

```shell
git commit -m "[descriptive message]"
```

分支
---

> 分支的常见操作

列出当前仓库中所有的本地分支

```shell
git branch
```

建立一个新分支

```shell
git branch [branch-name]
```

切换到一个特定的分支上并更新工作目录

```shell
git checkout [branch-name]
```

从当前分支建立一个新的子分支并切换到子分支

```shell
git checkout -b [branch-name]
```

合并特定分支的历史到当前分支

```shell
git merge [branch-name]
```

删除特定的分支

```shell
git branch -D [branch-name]
```

删除所有含关键字的分支

```shell
git branch | grep '[key]' | xargs git branch -D
```

重构
---

> 重定位并移除版本文件

从工作目录中删除文件并暂存此删除

```shell
git rm [file]
```

从版本控制中移除文件，并在本地保存文件

```shell
git rm --cached [file]
```

改变文件名并准备 commit

```shell
git mv [file-original] [file-renamed]
```

忽略
---

> 不包含临时文件和路径

文本文件 .gitignore 可以防止一些特定的文件进入到版本控制中

```shell
*.log
build/
temp-*
```

列出所有项目中忽略的文件

```shell
git ls-files --others --ignored --exclude-standard

参考网址

​```shell
https://github.com/github/gitignore

https://www.gitignore.io
```

暂存
---

> 暂存一些未完成的更改

临时存储所有修改的已跟踪文件

```shell
git stash
```

重新存储所有最近被stash的文件

```shell
git stash pop
```

列出所有被stash的更改

```shell
git stash list
```

放弃所有最近stash的更改

```shell
git stash drop
```

历史
---

> 浏览并检查项目文件的发展

列出当前分支的版本历史

```shell
git log
```

列出文件的版本历史，包括重命名

```shell
git log --follow [file]
```

展示两个不同分支之间的差异

```shell
git diff [first-branch]...[second-branch]
```

输出元数据以及特定commit的内容变化

```shell
git show [commit]
```

撤销
---

> 擦除错误并更改历史

撤销所有 [commit] 后的的 commit ，在本地保存更改

```shell
git reset [commit]
```

还原本地所有未 commit 的修改

```shell
git checkout .
```

放弃所有更改并回到某个特定的 commit ，不保留任何历史文件

```shell
git reset --hard [commit]
```

放弃所有更改并回到某个特定的 commit ，保留历史文件

```shell
git reset --soft [commit]
```

同步
---

> 注册一个远程的链接，交换仓库的版本历史

下载远程仓库的所有历史

```shell
git fetch [remote]
```

合并远程分支到当前本地分支

```shell
git merge [remote]/[branch]
```

上传所有本地分支commit到GitHub上

```shell
git push [remote] [branch]
```

下载书签历史并合并更改

```shell
git pull
```