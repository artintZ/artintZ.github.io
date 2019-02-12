---
layout: post
title:  LessOrMore主题的用法和配置
date:   2019-02-06 18:29:40 +0800
categories: jekyll
tag: 教程
---

* content
{:toc}

# 综述

LessOrMore是一种简洁美观的jekyll主题，非常适合博客网站。我使用的是GitHub Pages搭建的静态网站，集成了jekyll技术支持，因此不用安装jekyll和ruby环境。若你使用的其他网站，则需要安装jekyll（或者hexo），不作赘述。

# 主题下载

jekyllthemes官网：[http://jekyllthemes.org/themes/Less-Or-More/](http://jekyllthemes.org/themes/Less-Or-More/)

作者GitHub：[https://github.com/luoyan35714/LessOrMore](https://github.com/luoyan35714/LessOrMore)

# 个人配置

## 安装

将下载的zip压缩包解压，把文件夹里面的所有文件复制到你GitHub对应仓库的master分支下，或者直接fork作者的项目。安装好后就可以在网站看到效果了。

## 个人信息

打开`_config.yml`文件，按照如下进行配置。
> 特别注意`baseurl`的配置。如果是`***.github.io`项目，就修改为空''，否则会导致JS,CSS等静态资源无法找到。

```bash
name: 博客名称
email: 邮箱地址
author: 作者名
url: 个人网站
### baseurl修改为项目名，如果项目是'***.github.io'，则设置为空''
baseurl: "/LessOrMore"
resume_site: 个人简历网站
github: github地址
github_username: github用户名称
```

## 网站界面

![网站界面](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/网站界面-21bb306c-320b-4f59-be06-eb046d6c0f8f.png)

* 头像（序号1）：\styles\images\logo.jpg
* 网站描述（序号2）：_config.yml文件中的description
* 关于（序号3）：artintZ.github.io\_includes\header.html
* 网站统计（序号4，5）：这两项不用改。其中4为不蒜子统计，5为revolvermaps。还有[百度统计](https://tongji.baidu.com/)，注册账号后免费使用，在_config.yml文件中baidu_analysis修改ID，可在官网后台查看统计情况。
* 网页图标：\styles\images\favicon.jpg

![网站界面-1d5c2c26-53f0-4324-ae56-b5271c0b8605](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/网站界面-1d5c2c26-53f0-4324-ae56-b5271c0b8605.png)

* 分类页面描述（序号7）：_config.yml文件中的motto
* 分类页面描述（序号8）：_config.yml文件中的banner

# 发布文章

在`_posts`下新建文件（也可以创建文件夹并在文件夹中添加文件），命名格式示例：**`2019-02-06-example.md`**，在文件开头粘贴如下信息：

```bash
---
layout: post
#标题配置
title:  标题
#时间配置
date:   2016-08-27 01:08:00 +0800
#大类配置
categories: document
#小类配置
tag: 教程
---

* content
{:toc}


（以上至少空两行）正文从此处开始。
```

# 参考

[如何使用LessOrMore这个Jekyll模版](http://www.hifreud.com/LessOrMore/2016/08/26/how-to-use-this-jekyll-theme/)

附主题作者简介：[Freud Kang](http://www.hifreud.com/Resume.io/)