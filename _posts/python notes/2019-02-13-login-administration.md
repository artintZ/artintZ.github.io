---
layout: post
title: python编写的用户登录管理小程序（文件练习）
date: 2019-02-13 22:07:22 +0800
categories: python
tag: note
---

* content
{:toc}


## 题目

用python的文件操作方法写一个用户登录管理程序：

1. 有用户和管理员两个登录接口
2. 数据存在文件，仅管理员可操作
3. 用户登录验证用户名和密码，密码错误三次锁定
4. 管理员可添加、删除数据，并可解锁

## 流程图

![python-file-登录管理小程序](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python-file-登录管理小程序-44bdc69e-45a3-4298-872d-1a7163b257b5.png)

## 主要功能

### 