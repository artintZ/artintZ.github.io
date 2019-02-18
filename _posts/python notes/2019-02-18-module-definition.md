---
layout: post
title: python模块的定义、使用方法及原理
date: 2019-02-18 22:08:49 +0800
categories: python
tag: note
---

* content
{:toc}


## 定义

* **模块**：用来从逻辑上组织python代码（变量、函数、类等），本质是.py结尾的python文件。例：文件名：test.py；模块名：test。
* **包**：用来从逻辑上组织模块，本质是一个带有`__init__.py`文件的目录

## 使用方法

* import module_name1, module_name2
* import module_name as mod
* from module_name import m1, m2, m3, ...
* from module_name import *
* from module_name import func as f
* from . import module_name  # (其中 . 指当前路径)

## import本质

* 导入模块的本质就是把对应Python文件解释一遍
* 导入包的本质就是执行该包下的__init__.py文件

## 路径搜索

import导入模块时，是按照sys.path列表包含的路径执行的，其第一个元素就是当前文件目录，其他元素为python标准库及第三方库的路径。若要跨路径导入模块，方法如下：

```py
import os
import sys

__file__  # 当前文件的相对路径
os.path.abspath(__file__)  # 当前文件的绝对路径
os.path.dirname(os.path.abspath(__file__))  # 当前文件的上一级目录

# 当前文件的上上级目录
DIR = os.path.dirname(os.path.dirname(os.path.abspath(__file__)))

sys.path.append(DIR)  # 添加环境变量
```

## 导入优化

若多次用到某模块的单一功能，导入模块时用：

```py
# import module_name
from module_name import func
```

这样可以节省多次搜索路径的时间。

## 模块的分类

1. 标准库
2. 开源模块
3. 自定义模块

### 常用标准库模块

* **time** 和 **datetime**

时间的表示方法：格式化字符串 **Format string**、时间戳 **Timestamp**、结构化元组 **struct_time**。

![python模块时间表示方法与转换](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python模块时间表示方法与转换-da7378a6-b5bd-45cf-8013-d916f990f2ad.png)