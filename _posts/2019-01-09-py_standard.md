---
layout: post
title:  Python 学习笔记
date:   2019-01-09 18:00:00 +0800
categories: python
tag: 教程
---

* content
{:toc}

# 变量的命名规范

1. 模块名和包名：小写字母，单词之间用_分割 ***ad_stats.py***  
2. 类名：单词首字母大写（驼峰命名法）***AdStats，ConfigUtil***  
3. 全局变量名：大写字母，单词之间用_分割 ***NUMBER，COLOR_WRITE***
4. 普通变量或函数：小写字母，单词之间用_分割 ***this_is_a_var***
5. 实例变量：以_开头 ***_price，_instance_var***
6. 私有实例变量（外部访问会报错）：以__开头（2个下划线） ***__private_var***
7. 专有变量：__开头，__结尾，一般为python的自有变量 ***__doc__，__class__***

# 代码书写规范(基础)

1. Indentation 缩进：每一级缩进使用4个空格，不用使用Tab
2. Whitespace in Expressions and Statements 表达式和语句中的空格：二元运算符前后各加一个空格；在逗号、冒号、分号后加空格；紧贴函数或索引的左括号前不加空格
3. Comments 注释：#后要加一个空格；文档字符串用"""注释"""