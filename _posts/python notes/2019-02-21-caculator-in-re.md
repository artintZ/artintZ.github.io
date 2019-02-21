---
layout: post
title: python编写的简单计算器（re练习）
date: 2019-02-21 23:22:06 +0800
categories: python
tag: note
---

* content
{:toc}


## 题目

用python正则表达式`re`模块编写一个计算器：

* 可以计算字符串格式的算式，支持四则运算及小括号
* 要求使用`re`模块的功能，不能使用`eval()`等类似功能

## 流程图

![python-re-算式计算器](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python-re-算式计算器-305c29de-654e-4a49-ab82-24f41dda16f7.png)

## 主要功能

### 最短括号

算式中可能包含括号的嵌套，因此要取出括号里面没有括号的最短括号。我没有使用`re`不包含某字符的功能，我用了`p_brackets = re.compile(r'[(]([0-9+\-*/.]+)[)]')`来匹配最短括号，用`group()`函数就可以取出括号内的函数。

### 防止缺少'+'

我在计算的时候默认包含数字前的'-'号，因此有可能`3-2*-5`计算后为`310`，应该为`3+10`。解决方法就是计算前把'-'替换为'+-'。

```py
while True:  # 在减号前加个加号防止符号消失
    try:
        temp = p_subtraction.search(FORMULAS)
        FORMULAS = p_subtraction.sub(temp.group(
            1)+'+-'+temp.group(2), FORMULAS, count=1)
    except AttributeError:
        break
```

### 四则运算

运算顺序为`除法->乘法->减法->加法`，每次计算后会用结果替换掉原字符串的相应算式。

```py
def caculate(arith, form):
    """计算。parameter:
    arith: '/'或'*'或'-'或'+'
    form: 算式字符串"""
    # 匹配相应算术格式的算式并分组，其数可能为负
    p_arith = re.compile(r'([\-]?[0-9.]+)[%s]([\-]?[0-9.]+)' % (arith))
    while True:
        try:
            form_match = p_arith.search(form)
            if arith == '/':
                res = float(form_match.group(1))/float(form_match.group(2))
            elif arith == '*':
                res = float(form_match.group(1))*float(form_match.group(2))
            elif arith == '-':
                res = float(form_match.group(1))-float(form_match.group(2))
            else:
                res = float(form_match.group(1))+float(form_match.group(2))
            form = p_arith.sub(str(res), form, count=1)
        except AttributeError:
            # print(form)
            return form
```

## 知识丶总结

* `re`模块常用的模式（2月20日笔记有写）
* `try-except`可取异常并加以运用
* `re.sub()`默认替换所有，可用`count`参数控制

## 源代码

[https://github.com/artintZ/python/blob/master/day5/re_caculator.py](https://github.com/artintZ/python/blob/master/day5/re_caculator.py)