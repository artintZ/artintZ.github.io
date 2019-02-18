---
layout: post
title: python项目的一般目录结构
date: 2019-02-18 18:59:44 +0800
categories: python
tag: tutorial
---

* content
{:toc}


## 目录结构

```tree
Project_Name/
|--bin/
|  |--project_name
|
|--project_name/
|  |--tests/
|  |  |--__init__.py
|  |  |--test_main.py
|  |
|  |--__init__.py
|  |--main.py
|
|--docs/
|  |--config.py
|  |--abc.rst
|
|--setup.py
|--requirements.txt
|--README
```

## 简要阐释

* **bin/**：存放项目的一些可执行文件，亦可起名scripts/等。
* **project_name/**：存放项目的所有源代码。
  * 源代码中所有模块、包都应放在此目录；
  * 其子目录**tests/** 存放单元测试文件；
  * 程序主入口命名为**main.py**。
* **docs/**：存放一些文档。
* **setup.py**：安装、部署、打包的脚本。
* **requirements.txt**：存放软件依赖的外部python包列表。
* **README**：项目说明文件。
* 此外还可以有**LICENSE.txt**、Changelog.txt等。

## 关于README

README是每个项目都应该有的文件，让读者快速了解这个项目。

1. 软件定位，软件的基本功能。
2. 运行代码的方法：安装环境、启动命令等。
3. 简要的使用说明。
4. 代码目录结构说明，更详细点可以说明软件的基本原理。
5. 常见问题说明。
