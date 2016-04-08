title: Git的使用技巧
date: 2016-01-19 14:11:20
description: 
categories:
- HTML
tags:
- Git
toc: true
author:
comments:
original:
permalink: 
---
　　** Git的使用技巧:**
<!-- more -->

## GitHub简介

### Git SSH Key

```
Linux

$ ssh-keygen -t rsa -C "mail@gmail.com"

//这的密码不是我们，GitHub的密码，而是Git SSH的密码

//保存SSH密码
$ eval "$(ssh-agent -s)" //Linux
$ ssh-agent -s //Windows

$ ssh-add ~/.ssh/id_rsa

//打开Git生成的密码文件，将其复制到GitHub上
$ vim ~/.ssh/id_rsa.pub

//验证GitHub SSH是否成功
$ ssh -T git@github.com

## Git远程协作

git clone

//数据更新以及同步的协议
git clone


git fetch
git pull
```