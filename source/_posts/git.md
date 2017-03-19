---
title: Git深入浅出
date: 2016-05-18 22:16:21
categories:
- Git
tags:
- Git
- 基础技能
---

我个人认为Git的出现和普及是编程界的一个里程碑。
环境：Ubuntu 14.04
代码仓库： github

## 基础使用

### 安装和配置

1. 本地安装和配置
``` bash
$ sudo apt-get install git
$ git config --global user.name "richard"
$ git config --global user.email "richard.sun@birdycloud.com"
```
2. 生成秘钥对（SSH key）
``` bash
$ ssh-keygen -t rsa -C "richard.sun@birdycloud.com"
```
>建议一路回车（即不设置密码）,如果在此设置密码,使用 SSH方式 每次push代码也需要输入密码

3. 将生成的SSH key添加到github
``` bash
$ cat ~/.ssh/id_rsa.pub
```
将以上命令输出的内容添加到github —> setting -> SSH and GPG keys -> new SSH key

### 初始化项目

a. 如果代码库中已存在项目可采用下面方式
``` bash
$ git clone <repo> <directory> -b <branch>
```
> <repo> 两种方式的不同：
> 1. SSH方式  git://github.com/sunzh231/birdy-test.git（需要在代码库github中添加ssh key）
> 2. HTTP方式  git://github.com/sunzh231/birdy-test.git（每次push代码需要输入github的用户名和密码）

b. 本地新建项目
``` bash
$ git init birdy-test
```

### 基本操作
1. 查看修改的文件
``` bash
$ git status -s
```
> -s 参数可选，加上-s简化显示内容

2. 查看修改的文件
``` bash
$ git status -s
```
> -s 参数可选，加上-s简化显示内容

3. 将文件添加到缓存
``` bash
$ git add a.txt b.txt 或 git add -A
```

4. git diff查看执行 git status 的结果的详细信息
>1. 尚未缓存的改动：git diff
>2. 查看已缓存的改动： git diff --cached
>3. 查看已缓存的与未缓存的所有改动：git diff HEAD
>4. 显示摘要而非整个 diff：git diff --stat

5. 提交代码
```
$ git commit -m ""
```
>合并git add 和 git commit： git commit -a -m

6. 从缓存区中移除文件
```
$ git rm a.txt
```
> git rm file 会将文件从缓存区和你的硬盘中（工作目录）删除。
>如果你要在工作目录中留着该文件，可以使用 git rm --cached


7. 重命名 git mv

8. 同步代码到代码库
```
$ git push origin develop (git push <remote name> <branch>)
```


## 进阶

### 分支管理

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 搭建过程

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

## 代码库（github、gitlab、coding）

### 简介

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 搭建过程

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)


## 项目实践

### 本地多账号配置

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### git branch model

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

## Git Branch Model

### 简介

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 搭建过程

``` bash
$ hexo new "My New Post"
```

## 总结

### 简介

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)

### 搭建过程

``` bash
$ hexo new "My New Post"
```

More info: [Writing](https://hexo.io/docs/writing.html)
