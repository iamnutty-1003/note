# GitHub

## 介绍

Git是工具 GitHub是仓库

## 注册

pw: iamnutty-1003  nutty544475

地址[https://github.com/iamnutty-1003](https://github.com/iamnutty-1003)

+号 -->new repository



clone or download -->SSH(记住用户名和密码)

需要添加SSH key获取操作权限

## 克隆和基本操作

查看隐藏文件，发现.git文件夹，意思是成为了git工作区

工作区新建文件夹后，打开gitbash，输入

> git status

出现新建文件，以及

> Untracked files	未注册文件

输入

> git add first.txt
>
> git status

文件进入index暂存区，出现

> changes to be committed
>
> ​	new file: first.txt

输入

> git commit -m "first commit"	-m指"massage"，添加更改备注
>
> git status
>

后出现

> Your branch is ahead of 'origin/master' by 2 commits.
> (use "git push" to publish your local commits)	

意思是领先了两个commit

> git log	查看历史

> git reset + 命令号	取消操作

将commit推到仓库

> git push

## 如何解决冲突

### 示例:

> git clone ... other	自动创建一个other的文件夹存项目
>

other修改后

> git add .
>
> git commit -m ""
>
> git push

demo直接修改后,会出现conflict

> git pull	引入更新且合并自己的修改

## 团队协作开发

> git branch branch1	创建分支branch1
>
> git checkout branch1	切换到branch1
>
> git checkout -b branch2 创建branch2并切换到