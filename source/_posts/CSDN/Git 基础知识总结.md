## 设置 Git 的名字和邮箱

```
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

*注意 ：git config 命令的 --global 参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。*

## 版本库基本操作
查看所有命令 ：`git --help`
记录的每一次命令 ：`git reflog`
创建文件夹 ：`mkdir 文件名`
切换到指定路径 ：`cd + 路径` 
显示当前目录 ：`pwd`
把目录变成 Git 可以管理的仓库 ：`git init` 

注意：
如果没有在版本库中看到 .git 目录，是因为这个目录默认是隐藏的，用 `ls -ah` 命令就可以看见。或者![点击文件夹上方的查看->显示隐藏文件夹](https://img-blog.csdnimg.cn/20200623161145587.png)


## 添加文件到仓库
第一步，把文件添加到仓库：

```
git add   要添加的文件名
git add . 添加全部文件
```

第二步，把文件提交到仓库：

```
git commit -m "注释说明"
```
git commit 命令，-m 后面输入的是本次提交的说明，可以输入任意内容。建议：提交的说明是描述本次的修改，短小详细，这样就能从历史记录里方便地找到改动记录。

***扩展 git commit 命令执行成功后会告诉你:***
1. file changed：1个文件被改动（我们新添加的readme.txt文件）；
2. insertions：插入了两行内容（readme.txt有两行内容）。

## 版本 / 回退
1 . 查看历史记录 

```
git log 
git log --pretty = oneline  在一行内显示历史记录
```

HEAD 表示当前版本
HEAD\^ 表示上一个版本
HEAD\^\^ 表示上上一个版本

2 . 回退

```
git reset --hard HEAD  返回最新版本
git reset --hard 1094a  (Git log出来的，前五个就可以)
```
3 . 查看文件内容

```
cat 文件名加后缀名 （查看文件内容）
```

## 删除文件
1 . 删除文件

```
git rm 文件名加后缀名 （用于删除一个文件）
```

## 远程推送
1.创建秘钥
```
ssh-keygen -t rsa -C "邮箱" 
```
创建的 SSH Key 文件，默认在用户主目录下.ssh文件夹下，文件夹里有 id_rsa 和 id_rsa.pub 这两个文件。在 GitHub 官网中找到添加 SSH Key 的文本框, 在 SSH Key 文本框里粘贴 id_rsa.pub 文件的内容。

2.关联远程库
```
git remote add origin 地址
```

3.推送分支的所有内容
```
第一次推送用: git push -u origin master 
之后可以用: git push origin master 推送最新修改
之后可以用: git push 推送最新修改
```

git pull 把最新的提交从 origin/dev 抓下来在本地合并，解决冲突，再推送。
rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

## 远程克隆
1 . 首先，登陆GitHub，获取仓库的地址
2 . 选择合适的位置运行下面代码
```
git clone 地址
```

## 创建与合并分支
1 . 创建 dev 分支

```
git checkout -b dev
```
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令

2 .  创建 

```
git branch dev  创建
```

3 .  切换

```
git checkout dev  切换
```

4 . 查看分支

```
git branch
```

git branch命令会列出所有分支，当前分支前面会标一个*号。然后，我们就可以在dev分支上正常提交

5 . 合并分支

```
git merge 命令用于合并指定分支到当前分支
```
6 . 删除分支 

```
git branch -d 分支名  
```

**总结 ： 
查看分支：`git branch`
创建分支：`git branch <name>`
切换分支：`git checkout <name>`
创建+切换分支：`git checkout -b <name>`
合并某分支到当前分支：`git merge <name>`
删除分支：`git branch -d <name>`**


## Bug 分支
工作现场还在，Git 把 stash 内容存在某个地方了，但是需要恢复一下，有两个办法：

一是用 git stash apply 恢复，但是恢复后，stash 内容并不删除，你需要用 git stash drop 来删除；

二是用 git stash pop，恢复的同时把 stash 内容也删了。修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再 git stash pop，回到工作现场开发最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。




## 创建标签
1 . 创建标签

```
git tag <name>
```
2 . 查看所有标签：

```
git tag
```

注：标签不是按时间顺序列出，而是按字母排序的。可以创建带有说明的标签，用 -a指定标签名，-m指定说明文字。

3 . 查看标签信息

```
git show <tagname>
```
4 . 查看说明文字

```
git show <tagname>
```

5 . 删除标签

```
git tag -d <tagname>
```

6 . 标签上传
如果要推送某个标签到远程，使用命令：

```
git push origin <tagname>
```

一次性推送全部尚未推送到远程的本地标签：

```
git push origin --tags
```

## 删除远程

```
git push origin :refs/tags/tagname
```

## Git 自定义上传文件：
在 Git 工作区的根目录下创建一个特殊的 .gitignore 文件，然后把要忽略的文件名填进去，Git就会自动忽略这些文件。


## 配置别名

```
git config --global alias.新名字 旧名字
```

--global 参数是全局参数，也就是说命令会影响到这台电脑所有 Git 仓库。
