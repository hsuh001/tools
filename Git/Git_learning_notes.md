# Git学习笔记

*author: hsuh*

*creating time: 2021-01-03*

*finishing time: 2021-01-04*

*modifying time: 2021-01-04*

*reference:*

​	*[【教程】学会Git玩转Github【全】](https://www.bilibili.com/video/BV1Xx411m7kn?from=search&seid=13525408177496117075)*

---

## 1、使用Github

### 1.1 基本概念

1、仓库（Repository）

仓库即项目，用来存放代码。每个项目对应一个仓库，有多个开源项目则对应多个仓库。

2、收藏（Star）

收藏其他开发者的项目，方便后续查看。

3、复制 / 克隆项目（Fork）

复制其他开发者的仓库为自己的一个仓库，独立存在，可以进行修改。

4、发起请求（Pull request）

基于Fork，即在其他开发者项目的基础上进行了改进，效果很好，就可以考虑将这些改进合并到原有项目，这时可以向原有项目创建者发起pull request（简称PR）。原有项目创建者在review过改进后，通过测试，就会接受该PR，原有项目就会合并这些改进。

5、关注（Watch）

watch某个项目后，这个项目有任何更新，都会在第一时间收到通知。

6、Issue

项目当前存在的bug，暂时没有成型解决方案，需要讨论。

7、Github主页

在网页搜索`github`后即可进入github主页：

* 左侧显示用户动态、关注用户、关注仓库的动态

* 右侧显示所有的git库

  ![](D:\JLab\tools\Git\figs\1-1_1_github_mainpage.png)

* 仓库主页

  显示项目的信息，如code、版本、star / watch / fork情况

  ![](D:\JLab\tools\Git\figs\1-1_2_repository_mainpage.png)

* 个人主页

  个人信息（头像、简介）、关注用户、被关注用户、被关注git库、repositories、projects、packages、贡献的开源项目信息等、

  ![](D:\JLab\tools\Git\figs\1-1_3_user_mainpage.png)

## 2、Git安装与使用

### 2.1 Git安装

1、Git下载地址：https://git-scm.com/downloads

<img src="D:\JLab\tools\Git\figs\2-1_1_git_download_page.png" style="zoom:80%;" />

2、安装

* （1）step1：双击安装

  ![](D:\JLab\tools\Git\figs\2-1_2_git_setup_exe.png)

* （2）step2：点击`Next`

![](D:\JLab\tools\Git\figs\2-1_3_git_setup_next.png)

* （3）选择安装路径，点击`Next`

  ![](D:\JLab\tools\Git\figs\2-1_4_git_setup_dir.png)

* （4）选择安装组件，默认`Next`

  ![](D:\JLab\tools\Git\figs\2-1_5_git_setup_components.png)

* （5）选择开始菜单，默认`Next`

  ![](D:\JLab\tools\Git\figs\2-1_6_git_setup_start_menu.png)

* （6）选择编辑器，随后点击`Next`

  ![](D:\JLab\tools\Git\figs\2-1_7_git_setup_editor.png)

* （7）选择创建新repository的initial branch，默认为`master`

  ![](D:\JLab\tools\Git\figs\2-1_8_git_setup_intitial_branch.png)

  

* （8）选择使用Git时的命令行模式：

  ![](D:\JLab\tools\Git\figs\2-1_9_git_setup_path_environment.png)

* （9）选择HTTPS transport backend：

  ![](D:\JLab\tools\Git\figs\2-1_10_git_setup_openssl_library.png)

* （10）设置line ending conversions：

  ![](D:\JLab\tools\Git\figs\2-1_11_git_setup_line_ending.png)

* （11）设置terminal emualtor：

  ![](D:\JLab\tools\Git\figs\2-1_12_git_setup_terminal_emulator.png)

* （12）设置'git pull'为default：

  ![](D:\JLab\tools\Git\figs\2-1_13_git_setup_default_git_pull.png)

* （13）设置credential helper：

  ![](D:\JLab\tools\Git\figs\2-1_14_git_setup_credential_helper.png)

* （14）设置extra options：

  ![](D:\JLab\tools\Git\figs\2-1_15_git_setup_extra_options.png)

* （15）设置experimental options：

  ![](D:\JLab\tools\Git\figs\2-1_16_git_setup_experimental_options.png)

* （16）进行installing，

  ![](D:\JLab\tools\Git\figs\2-1_17_git_setup_installing.png)

* （17）安装完成，

  ![](D:\JLab\tools\Git\figs\2-1_18_git_setup_finish.png)

### 2.2 Git基本工作流程

1、Git提交文件流程

* （1）文件从工作区（working directory）--> 暂存区
  + step1：`git status`
  + step2：`git add file_name`

* （2）文件从暂存区 --> Git仓库（Git repository）
  + step1：`git status`
  + step2：`git commit -m 'description'`
  + step3：`git status`

2、Git基本信息设置

* （1）设置用户名

  ```shell
  git config --global user.name 'hsuh001'
  ```

* （2）设置用户名邮箱

  ```shell
  git config --global user.email 'h_su_h@126.com'
  ```

3、初始化一个新的仓库

* step1：新建文件夹

  ```shell
  mkdir test
  ```

* step2：在`test`文件夹内初始化git（创建git仓库）

  生成`.git`隐藏文件夹

  ```shell
  cd test
  git init
  ```

* step3：向仓库添加文件

  ```shell
  touch test_01.php
  git status
  #
  
  git add test_01.php
  
  git status
  #
  
  git commit -m 'add test_01.php'
  #
  
  git status
  #
  ```

4、修改仓库文件

* step1：修改文件

  ```shell
  ls
  # test_01.php
  
  vi test_01.php
  # 随后进行修改
  
  git status
  #
  ```

* step2：提交

  ```shell
  git add test_01.php
  git status
  git commit -m 'firstly modify test_01.php'
  git status
  ```

5、删除仓库文件

* step1：删除文件

  ```shell
  rm -rf test_01.php
  ```

* step2：从Git中删除文件

  ```shell
  git rm test_01.php
  git commit -m 'firstly delete test_01.php'
  git status
  ```

### 2.3 Git管理远程仓库

1、Git管理远程仓库

* step1：将项目Git克隆本地

  ```shell
  git clone url
  ```

* step2：进行增、删、改

* step2：提交到远程仓库

  ```shell
  git push
  ```

2、在`git push`遇到无法同步问题：

```
没有权限或者
The requested URL returned error: 403 Forbidden while accessing.
```

因为是私有项目，没有权限。可以输入用户名、密码；或者远程地址采用：

```shell
vi .git/config

# 将
# [remote "origin"]
#		url = https://github.com/用户名/仓库名.git
# 修改为：
# [remote "origin"]
# 		url = https://用户名:密码@github.com/用户名/仓库名.git
```

### 2.4 实战 | scRNA-seq

```shell
cd /d/JLab
mkdir -p scRNA-seq/{codes,data}
cd scRNA-seq

# 初始化基本信息，设置一次即可。后续均不用再重新设置。
git config --global user.name 'hsuh001'
git config --global user.email 'h_su_h@126.com'

# 修改默认分支为main，与远程github对应
# 这是因为在安装git时选的默认分支为master
git config --global init.defaultBranch main
git config --system init.defaultBranch main

# 查看config信息
git config --list
# diff.astextplain.textconv=astextplain
# filter.lfs.clean=git-lfs clean -- %f
# filter.lfs.smudge=git-lfs smudge -- %f
# filter.lfs.process=git-lfs filter-process
# filter.lfs.required=true
# http.sslbackend=openssl
# http.sslcainfo=D:/Program Files/Git/mingw64/ssl/certs/ca-bundle.crt
# core.autocrlf=true
# core.fscache=true
# core.symlinks=false
# pull.rebase=false
# credential.helper=manager-core
# credential.https://dev.azure.com.usehttppath=true
# init.defaultbranch=main
# user.name=hsuh001
# user.email=h_su_h@126.com
# init.defaultbranch=main

# 初始化，创建.init隐藏目录
git init

# add, delete, or modify files
cp /d/JLab/project/scRNA-seq/codes/* /d/JLab/scRNA-seq/codes/

git status
# On branch main
# 
# No commits yet
# 
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#         codes/
# 
# nothing added to commit but untracked files present (use "git add" to track)

# 提交到缓存区
git add codes
git status
#  On branch main
# 
# No commits yet
# 
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#         new file:   codes/dim_reduce_04.R
#         new file:   codes/hvg_selection_03.R
#         new file:   codes/normalization_02.R
#         new file:   codes/pkgs_install_00.R
#         new file:   codes/qc_01.R
#         new file:   codes/scRNA-seq_basic.R

# 提交到repository
git commit -m 'add first six R scripts'
# [main (root-commit) e95703a] add first six R scripts
#  6 files changed, 2155 insertions(+)
#  create mode 100644 codes/dim_reduce_04.R
#  create mode 100644 codes/hvg_selection_03.R
#  create mode 100644 codes/normalization_02.R
#  create mode 100644 codes/pkgs_install_00.R
#  create mode 100644 codes/qc_01.R
#  create mode 100644 codes/scRNA-seq_basic.R
git status
# On branch main
# nothing to commit, working tree clean

# 同步到远程github
# 第一步，需要在github上新建对应的repository
git remote add origin https://username:passwd@github.com/hsuh001/scRNA-seq.git

git push -u origin main
# 报错
# 背景：这个项目之前在 Github上推送过一次，但由于本地为master分支、远程为main分支
# 同时delete本地和远程之后，并且通过git config --global init.defaultBranch main设置默认分支为main
# 随后就报错
# To https://github.com/hsuh001/scRNA-seq.git
#  ! [rejected]        main -> main (fetch first)
# error: failed to push some refs to 'https://github.com/hsuh001/scRNA-seq.git'
# hint: Updates were rejected because the remote contains work that you do
# hint: not have locally. This is usually caused by another repository pushing
# hint: to the same ref. You may want to first integrate the remote changes
# hint: (e.g., 'git pull ...') before pushing again.
# hint: See the 'Note about fast-forwards' in 'git push --help' for details.

# 解决方法
# 原因：一开始在不同分支，main分支有README.md，但push的在master分支，所以可行
# 现在改为同为main分支，在远程github新建的README.md不在本地代码目录，所以需要先进行合并、再重新push
git pull --rebase origin main
# remote: Enumerating objects: 3, done.
# remote: Counting objects: 100% (3/3), done.
# remote: Compressing objects: 100% (2/2), done.
# remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
# Unpacking objects: 100% (3/3), 628 bytes | 0 bytes/s, done.
# From https://github.com/hsuh001/scRNA-seq
#  * branch            main       -> FETCH_HEAD
#  * [new branch]      main       -> origin/main
# Successfully rebased and updated refs/heads/main.

# 重新push
git push -u origin main
# Enumerating objects: 10, done.
# Counting objects: 100% (10/10), done.
# Delta compression using up to 8 threads
# Compressing objects: 100% (9/9), done.
# Writing objects: 100% (9/9), 22.20 KiB | 11.10 MiB/s, done.
# Total 9 (delta 0), reused 0 (delta 0), pack-reused 0
# To https://github.com/hsuh001/scRNA-seq.git
#    d1b68ef..3711d1c  main -> main
# Branch 'main' set up to track remote branch 'main' from 'origin'.
```

