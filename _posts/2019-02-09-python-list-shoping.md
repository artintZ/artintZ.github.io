---
layout: post
title:  python编写的一个购物车小程序（列表练习）
date:   2019-02-09 21:08:40 +0800
categories: python
tag: note
---

* content
{:toc}


## 题目

运用python中的`list`、`tuple`等知识编写一个购物车程序，要求如下：

1. 进入程序用户首先输入工资总额
2. 显示商品列表，含编号、商品、价格等参数
3. 用户输入编号，若余额充足则直接购买，否则提示余额不足
4. 可多次购买并且可随时退出
5. 退出前打印购物清单

## 流程图

![python-list-购物车程序](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python-list-购物车程序-7342231f-3bb4-4d92-a430-460c30a2df3e.png)

## 主要功能

### 显示菜单

* 就是用`for`循环打印商品清单元组`goods`。考虑到菜单的排版以及要将编号加进去，我首先想到的是两层循环：

```py
def menu():
    print('\n编号','商品',' 价格')
    for i in range(goods.__len__()):
        print('\n', i + 1,'、', end = '')
        for j in range(2):
            print(goods[i][j],' ', end = '')
    print('\n 0 、退出')
    n = int(input('请输入想要购买的商品的编号:'))
    return n
```

效果如下：

![菜单1](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/菜单-c22f6dd1-75f5-4c14-b9fe-6d6d73eef2d3.png)

因为有C语言的基础，惯性思维就想到了两层循环，但是这不符合python的风格，不够简单粗暴！

* 通过网上查资料，我找到了python的解决方法，只需要一层循环！

```python
def menu():
    print('\n编号','商品','价格')
    for i,(j, k) in enumerate(goods):
        print(i+1, j, k)
    print('0 退出')
    n = int(input('请输入想要购买的商品的编号:'))
    return n
```

效果如下：

![菜单2](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/菜单-0b0b1be0-71c2-4101-b679-39abd2e5b976.png)

这种方法用到了多个变量的`for`循环，其中`enumerate()`函数的作用是在列表（可迭代的数据类型）中的每个元素前面添加一个索引值，如下所示：

```py
name = (('a', 100), ('b', 50),('c',200))
for i in enumerate(name):
    print(i)
```

![菜单3](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/菜单-10b62b03-75a8-4742-9327-6ab8a7455cec.png)

### 购买商品

购买功能很简单，主要是判断价格与余额（我把`while`循环模块放在主框架了），若购买成功则计算余额和编辑已买商品列表`goods_bought`。

```py
def buy(n):
    global BALANCE
    if goods[n-1][1] <= BALANCE:
        BALANCE = BALANCE - goods[n-1][1]
        goods_bought.append(goods[n-1])
        print('购买成功！花了{}元，余额为{}元'.format(goods[n-1][1], BALANCE))
    else:
        print('余额不足！价格为{}元，余额为{}元'.format(goods[n-1][1], BALANCE))
    input('继续')
```

**注**：在函数内部修改全局变量赋值时，要用`global`提前声明。

### 结账功能

退出时打印一份购物清单，注明总计消费和余额。功能类似`menu`模块，不作赘述。

```py
def balance():
    print('\n购物清单：')
    for i,(j,k) in enumerate(goods_bought):
        print(i+1, j, k)
    print('您一共消费{}元，您的余额{}元'.format(SALARY - BALANCE, BALANCE))
    input('按任意键退出')
```

## 知识丶总结

这个购物车小程序是在刚学完列表、元组的时候编写的，通过完成这个题目，我不仅练习巩固了刚学的python语法，还扩展学习了一些实用的函数方法：

1. 列表嵌套
2. 字符串的`format()`格式化应用
3. 多个变量的`for`循环，变量个数和列表元素对应
4. `enumerate()`函数在列表（可迭代的数据类型）中的每个元素前面添加一个索引值，可用于`for`循环。
5. 在函数内部修改全局变量赋值时，要用`global`提前声明。

## 源代码

[https://github.com/artintZ/python/blob/master/day2/shopping.py](https://github.com/artintZ/python/blob/master/day2/shopping.py)