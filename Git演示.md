# Git 演示

## Git是什么？

Git的三个概念：提交commit、仓库repository、分支branch

## 初始化一个仓库

git clone 和点下载有什么区别？

下载的文件夹需要**git init**才能变成一个仓库（即生成.git文件夹）

```
git clone <git地址>
git init
```

## 第一次提交

```
git add -A // 全部文件提交到暂存区
git commit -m "提交信息"
```

工作区----- git add \<file> \-\-\-\-> 暂存区 ----- git commit -----> 仓库

***一般不这么做***

***直接删除.git文件夹 = 删除仓库***

## 查看提交的历史

```
git log --stat
```

## 维护项目的日常

```
工作区回滚：// vs code 直接点图标 即可
git checkout <filename>

提交后撤回：
git reset HEAD^
```

## 分支

```
从当前分支为基础新建分支
git checkout -b <branchname>
列举所有的分支
git branch
单纯地切换到某个分支
git checkout <branchname>
删除特定的分支
git branch -D <branchname>
合并分支
git merge <branchname>
放弃合并分支
git merge --abort
```

*** 一般主分支main只作为能跑起来的***没有问题的代码

1. ***长周期在分支中完成***
2. 创建子分支一般在主分支上进行，因为主分支是代码分支的起点和终点

## git与GitHub远程仓库

```
推送
git push
拉取
git pull
```





# Git理论

## 一、Git基础

### 1、Git介绍

git是目前世界上最先进的***分布式版本控制系统***

### 2、Git与GitHub

#### 2.1 两者区别

Git是一个分布式版本控制系统，简单来说就是一个**软件**，用于记录一个或若干个文件内容变化，以便将来查阅特定版本修订情况的软件。

GitHub（https://www.github.com）是一个为用户提供Git服务的**网站**，简单来说就是一个可以放代码的地方（不过可以放的不仅是代码）。GitHub除了提供管理Git的web界面以外，还提供了订阅、关注、讨论组、在线编辑器等丰富的功能。GitHub被称之为全球最大的基友网站

#### 2.2 github账号注册

### 3、Git安装

1. 下载安装包
2. 选择安装位置，不要带中文和特殊符号
3. 选择需要安装的组件（默认即可）
4. 选择默认编辑器（vim，vscode等）
5. 使用openSSH（默认）
6. 选择OpenSSL
7. 样式和终端（默认）
8. 配置额外选项（默认）
9. 最后view Release Notes不用勾选

**几乎全都是默认**

# 二、Git的使用

## 1、本地仓库

### 1.1 工作流程

Git本地操作的三个区域

工作区（working directory）	添加、编辑、修改文件等动作

​	↓		git add <filename>

暂存区	暂存已经修改的文件最后统一提交到git仓库中

​	↓		git commit -m “提交描述”

Git repository	最终确定的文件保存到仓库，成为一个新的版本，并且对他人可见

```
git status // 查看当前仓库状态
```

### 1.2 本地仓库操作

仓库又名版本库，英文名repository，我们可以简单理解成一个目录，用于存放代码，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除等操作Git都能追踪到。

1. 在安装好后首次使用需要进行全局配置（一次性操作，除非换电脑或者重装系统）

桌面点击空白处，点击“git bash here”以打开Git命令行窗口

```
git config --global user.name "用户名"
git config --global user.email "邮箱地址"
```

修改用户名和邮箱参考帖子：https://www.php.cn/faq/528534.html

2. 创建仓库

当需要让git去管理某个新项目/已存在项目的时候，就需要创建仓库。注意，创建仓库时使用的目录不一定要求是空目录，选择一个非空目录也是可以的，但是不建议在现有现有项目上来学习git，造成的后果不可预计。

​	mkdir repo1

​	cd repo1

​	git init // Git仓库初始化，执行之后，会在项目目录下创建一个隐藏目录“.git”，这个目录是Git所创建的，不能删除，也不能**随意更改**其中的内容（可以更改，但不能随意）。

3. 常用指令

​	git status // 查看当前状态	

​	git add指令，可以添加一个文件，也可以同时添加多个文件

​		语法1：git add 文件名

​		语法2：git add 文件名1 文件名2 文件名3 …

​		语法3：git add .       // 添加当前目录到暂存区中

​	git commit -m “提交信息”

重复使用上述指令即可完成提交

### 1.3 版本回退

版本回退分为两个步骤：

1. 查看版本，确定需要回到的时间点

   指令：

   ​	git log

   ​	git log --pretty=oneline

2. 回退操作

   指令：

   git reset --hard 提交编号

   回到过去之后，要想再回到之前最新的版本的时候，则需要使用过指令去查看历史操作，以得到最新的commit id。commit id可以不用写全，Git会自动识别，至少写4位。

   git reflog

## 2、远程仓库

### 2.1 创建仓库

### 2.2 两种常规使用方式

1. 基于HTTP协议

   a. 创建空目录

   b. 使用clone指令克隆线上仓库到本地

   语法：git clone 线上仓库地址

   c. 在仓库上做对应的操作（提交暂存区、提交本地仓库，提交线上仓库、拉取线上仓库）

   ***提交到线上仓库的指令：***git push

   在首次往线上仓库提交内容时出现了403的致命错误，原因是不是任何人都可以往线上仓库提交内容，需要鉴权。

   需要修改“.git/config”文件内容：

   \# 将

   [remote “origin”]

   ​	url = https://github.com/用户名/仓库名.git

   修改为：

   [remote “origin”]

   ​	url = https://用户名:密码@github.com/用户名/仓库名.git

   ***拉取线上仓库：***git pull

   ***注意：***

   每天工作的第一件事就是先git pull拉取线上最新的版本：每天下班前要做的是git push，将本地代码提交到线上仓库

2. 基于SSH协议

   该方式与前面HTTPS方式相比，**只是影响GitHub对于用户的身份鉴权方式**，对于git的具体操作（如提交本地、添加注释、提交远程等操作）没有任何影响。

   生成公私钥对指令（需先自行安装OpenSSH）：ssh-keygen -t rsa -C “注册邮箱”

​		步骤：

​			1. 生成客户端公私钥文件

​			2. 将公钥上传到GitHub

### 2.3 分支管理

简单理解为项目里的**某个模块或功能**

每次提交后都会有记录，Git把它们串成时间线，形成类似于时间轴的东西，这个时间轴就是一个分支，称之为main分支（过去的master分支）

分支相关指令：

查看分支：git branch

创建分支：git branch 分支名

切换分支：git checkout 分支名

创建并切换分支：git checkout -b 分支名

删除分支：git branch -d 分支名

合并分支：git merge 被合并的分支名



git branch

***注意1：***当前分支前面有个标记“*”

git branch -d

***注意2：***在删除分支的时候，需要先退出要删除的分支，然后进行删除

### 2.4 冲突的产生与解决

模拟产生冲突

1. 同事在我下班之后修改了线上仓库的代码
   此时，本地仓库与线上仓库不一致
2. 第二天上班的时候，我没有做git pull操作，而是直接修改了本地的相应文件的内容
3. 下班时git push

解决冲突：

4. 先git pull
5. 打开冲突文件

​	解决方法：需要和同事（谁先提交的）进行商量，将改好的代码再次提交即可

6. 重新提交
