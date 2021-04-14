---
title: Git学习笔记
date: 2020-12-22 13:29:08
tags:
- Git
categories: 学习笔记系列
---

## Git简介

(Git官网：https://git-scm.com/)

Git是一款版本控制工具，它是分布式版本控制工具的代表。而SVN是集中式版本控制工具的代表。<!--more-->

### 版本控制

#### 集中式版本控制

- 工具：CVS、 SVN、 VSS

- 工作方式：有一台中心服务器，各终端把代码等资源集中上传到该服务器中，由该服务器来统一管理

- 缺点：有单点故障的问题。所谓单点故障即，当中心服务器损坏时，整个系统也随之全部瘫痪。

#### 分布式版本控制

- 工具：**Git**、 Mercurial、 Bazaar、 Darcs
- 工作方式：每个终端都可以在本地进行版本控制。各终端之间相互传递数据。但在实际应用上，git用远程库来管理。
- 优势：可以避免单点故障

### Git的优势

1. 大部分操作在本地完成， 不需要联网
2. 完整性保证（用哈希算法）
3. 尽可能添加数据而不是删除或修改数据
4. 分支操作非常快捷流畅
5. 与 Linux 命令全面兼容

### Git结构

（仅本地库的结构，不涉及远程库的）

{% asset_img 1.png %}

### Git和代码托管中心

代码托管中心的任务：维护远程库。

GitHub算是git的一个代码托管中心。但git还可以其他的代码托管中心

#### 局域网环境下

可以搭建GitLab服务器作为代码托管中心。

#### 外网环境下

GitHub、码云

## Git命令行操作

### 本地库初始化

git init

本地库初始化就是在本地创建一个.git目录，git 目录中存放的是本地库相关的子目录和文件， 不要删除， 也不要胡乱修改。

### 设置签名

- 形式

  用户名user.name:kcp28

  Email地址user.email:abc@123.com(有就行，存不存在都行)

- 作用：区分不同的开发人员的身份

- 注意：这里设置签名和登录远程库（代码托管中心）的账号密码没有任何关系。

- 命令：git config

#### 项目级别/仓库级别

- 仅在本地库范围内有效

- 命令

  git config user.name 用户名

  git config user.email Email地址

- 信息保存位置：./.git/config文件

#### 系统用户级别（一般用这个就够了）

- 登录当前操作系统的用户范围

- 命令

  git config --global user.name 用户名

  git config --global user.email Email地址

- 信息保存位置：~/.gitconfig文件

#### 级别优先级

就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名。

如果只有系统用户级别的签名，就以系统用户级别的签名为准。

二者都没有是不允许的

### 查看当前git状态（工作区、暂存区状态）

git status

### 将文件提交至暂存区

git add 文件名

### 将暂存区的文件提交至本地库

git commit [-m 提示信息] 文件名

输完命令后，如果没加-m选项，会自动进入vim编辑器，输入此次提交的一些提示信息，输完后保存退出即可。

### 查看历史记录

- git log       

  具有多频显示的功能。多频显示控制方式:空格向下翻页；b向上翻页；q退出

- git log --pretty=oneline     

   简洁的方式显示历史记录

- git log --oneline     

  更简洁的方式（显示部分哈希值）显示历史记录

- git reflog

  在oneline的基础上显示到以前的版本分别需要几步：

  HEAD@{移动到当前版本的步数}

### 前进后退

#### 基于索引值操作（推荐）

索引值就是提交时git告诉你的那串哈希值，这里索引值用oneline给的一部分即可，因为这一部分已经能唯一定位每一个版本。

命令：git reset --hard 索引值

#### 使用^符号

只能向后回退，后退几步加几个^

- git reset --hard HEAD^   

  后退1步

- git reset --hard HEAD^^^  

  后退3步

#### 使用~符号

只能后退

- git reset --hard HEAD~n  

  后退n步

- git reset --hard HEAD~3  

  后退3步

#### reset命令的三个选项

- --soft：只移动本地库的HEAD指针（HEAD指针指向当前版本的文件）
- --mixed：移动本地库HEAD指针，并重置暂存区
- --hard：移动本地库HEAD指针，同时重置暂存区和工作区。

### 删除本地库文件

- rm 文件名

删除后工作区就没有这个文件了

- 永久删除

永久删除需要将“删除文件”这条记录提交到本地库。

执行rm命令后 ：{% asset_img 2.png %}

将 deleted：aaa.txt 该条记录提交到本地库，来彻底删除文件：

（提交方式和提交aaa.txt文件时一样）：

​          git add aaa.txt

​          git commit -m “提示信息” aaa.txt

{% asset_img 3.png %}

### 永久删除文件后找回

前提：删除前，文件存在时的状态提交到了本地库。

一般删除文件是指将文件提交的本地库后，永久删除后找回。

找回方法就是把版本回退到删除前：git reset --hard 索引值。

因为git是不会去删除任何文件的，它永远都只添加，只要提交的本地库的文件，都能恢复。

#### 添加到暂存区的删除文件找回

前提：删除前，该文件提交到了本地库。

指**删除文件的记录**（deleted: aaa.txt）被提交到暂存区且还没有提交到本地库。

恢复方法：用reset 命令的--hard参数，重置暂存区

git reset --hard HEAD //此时本地库的HEAD指向的版本还有删除的那个文件。

#### 比较文件并找回

{% asset_img 4.png %}

工作区的文件和暂存区（默认）或本地库的文件进行比较。对于已经提交的文件而言，前有-号并标红色的内容表示工作区删除的，前有+号标绿色的表示工作区新添的。

**命令：git diff**

- git diff [文件名]

将工作区中的文件和暂存区的文件进行比较

- git diff [本地库中历史版本] 文件名

将工作区中的文件和本地库中指定历史版本的文件进行比较。

eg:git diff HEAD 文件名        ==>和本地库当前文件进行比较。

- 不加文件名，可以比较多个文件。

## 分支管理

### 分支概念

在版本控制中，使用多条线同时推进多个任务。

{% asset_img 5.png %}

- 热修复分支：当主干（master）出bug时，开启一个分支来修复bug，修复完成后与主分支合并。热修复指在出bug时，不关闭服务器来修复。关闭服务器修复叫冷修复。

- 功能分支：分支一般以feature开头，后面跟功能的名称，表示该分支是开发何种功能的。各个分支可以推进，互不影响。当某一分支功能开发完毕后，便将该分支与主干合并，此时，软件便会有较大的版本更新，如从1.0变到2.0。

### 分支好处

- 同时并行推进多个功能开发，提高开发效率
- 各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响。失败的分支删除重新开始即可。

### 分支操作

#### 查看所有分支

git branch -v

前加*并且名称标绿色的表示当前所在的分支

#### 创建新的分支

git branch 分支名称

当创建新分支时，会把当前主干分支的内容自动复制过来。

##### 当前分支改名

git branch -M 新分支名

-M 表示强制改名

#### 切换分支

git checkout 分支名称

{% asset_img 6.png %}

#### 合并分支：

1. 切换到接收修改的分支（被合并，增加新内容）上。

如要把hot_fix分支合并到master分支上，就需要先切换到master分支上。

2. 执行merge命令

**git merge 合并分支的名称**

eg：//将hot_fix分支合并到master分支（设当前所在的分支是：hot_fix）

​     git checkout master  ==>切换到被合并的分支master上

​     git merge hot_fix  ==>执行merge命令,把hot_fix分支合并到master分支上。

#### 解决冲突

##### 冲突的原因和表现

当合并分支时，可能产生冲突。如两个分支最新提交的版本是对同一个文件的同一行做了不同的修改，此时合并是便会产生冲突，git不知道该选哪个版本。所以，此时自动合并失败，需要手动合并。

{% asset_img 7.png %}

##### 解决冲突

1. 编辑冲突文件，删除特殊符号(人与人交流，达成共识，总之人决定合并后文件的内容)
2. git add 文件名
3. git commit –m “提示信息”

注意：此时提交一定不要加文件名，不然会报错，提交失败

{% asset_img 8.png %}

## Git保存版本的机制

Git 保存的是增量，保存快照。切换分支，版本就是修改指针。

## Git 远程操作

远程库使用GitHub

### 远程库的创建

1. 首先，要在GitHub上注册，在远程库上有账号。

2. 创建远程库

   {% asset_img 9.png %}

### Git远程库操作

#### 创建远程库地址别名

git remote -v   ==>查看当前所有远程地址别名

git remote add [别名] [远程地址]

#### 把本地库的内容推送到远程库

git push [远程库别名] [本地库的分支名]

#### 克隆

- 命令：git clone [远程库地址] [文件目录]

- 解决clone慢：把远程库地址中的github.com替换成github.com.cnpmjs.org

- 克隆效果

1. 完整的把远程库下载到本地指定目录

2. 创建远程地址别名：origin

3. 初始化本地库（克隆后会自动初始化本地库，远程库克隆下来后就成了本地库）

   {% asset_img 10.png %}

#### 邀请团队成员

- GitHub远程库邀请团队成员

1.进入项目仓库，点击settings

2.选择 “Manage access”/“Collaborators”，点击 “Invite a collaborators”绿色按钮。

{% asset_img 11.png %}

3.输入对方GitHub账号

{% asset_img 12.png %}

4.点击图标，复制邀请链接

{% asset_img 13.png %}

5.将复制的链接发给对方。对方登录自己的GitHub后，在地址栏输入邀请链接，进入确认页面，点击”Accept invitation”,确认邀请，加入团队。

{% asset_img 14.png %}

6.加入团队后，对方就可以把自己的本地库的东西push 到这个远程库中。

对方：git push 远程库别名 本地库分支名

#### 拉取

当对方提交修改后，必需先把修改拉取到本地，再push新的修改。

##### 拉取命令

**n git fetch [远程库地址别名] [远程分支名]**

git merge [远程地址别名/远程分支名]

执行fetch命令拉取，本地工作区的文件不会修改。fetch只是把远程库的内容下载到本地，下载后自动成为一个分支，*分支名称为：远程地址别名/远程分支名*。

##### 查看fetch拉取的内容

1.更改git 分支：git checkout [远程库别名/远程分支名]

2.正常查看内容

- 只有当执行完merge命令后，合并两个分支，本地工作区的文件才会修改成远程库的内容。

- 拉取下来后如果进入冲突状态， 则按照“分支冲突解决” 操作解决即可。

##### 同时拉取、合并—pull

**git pull [远程库地址别名] [远程分支名]**

pull = fetch+merge

执行pull 命令，相当于同时执行fetch和merge。pull执行完毕后，自动合并两个分支，工作区的内容变为远程库的内容。

#### 协同开发时冲突解决

##### 产生冲突

当两个人同时都修改同一个文件的相同位置时，产生冲突。解决方式是两个人沟通后，得出修改结果，上传两人认同的修改方案。

#### Git push文件夹到远程库

在git Bash中进入该文件夹目录

git add .     ==> ‘ .’ 表示上传该文件夹下所有问价至暂存区

git commit –m “提示信息”    ==>提交至本地库时，就不用输入文件名了

git push 远程库地址别名 本地库分支名 



## 创建新仓库的流程

1.创建初始化本地库

```git
git init
```

2.设置签名

```
git config user.name 用户名
git config user.email 邮箱
```

3.创建远程库

最好加一个readme文件，这样就直接创建了一个分支

4.创建远程库地址别名

```
git remote add [别名] [远程库地址]
如：git remote add origin 远程库地址
```

5.拉取远程库内容

如果创建远程库时，自动添加了readme文件，则需先拉取远程库的内容，让本地库取得远程库最新的版本，这样后续才能push成功，不然，push时会报如下的错误：

```
Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

在第一次pull时，若报了错误：

```
fatal: refusing to merge unrelated histories
```

这个意思是：本地库于远程库无关联，禁止合并，解决办法为：在pull的时候加上`--allow-unrelated-histories`，即允许无关联的情况下合并

```
git pull [远程库地址别名] [远程库分支名] --allow-unrelated-histories
如：
git pull origin main --allow-unrelated-histories
```

6.将文件上传至本地库

```
git add .
git commit -m '说明信息'
```

7.将本地库文件上传至远程库

```
git push -u [远程库别名] [本地库分支名]
如：
git push -u origin main
```

