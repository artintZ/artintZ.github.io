---
layout: post
title: python编写的汉诺塔的算法（递归）
date: 2019-03-27 12:51:59 +0800
categories: python
tag: note
---

* content
{:toc}


## 概述

> 汉诺塔：汉诺塔（又称河内塔）问题是源于印度一个古老传说的益智玩具。大梵天创造世界的时候做了三根金刚石柱子，在一根柱子上从下往上按照大小顺序摞着64片黄金圆盘。大梵天命令婆罗门把圆盘从下面开始按大小顺序重新摆放在另一根柱子上。并且规定，在小圆盘上不能放大圆盘，在三根柱子之间一次只能移动一个圆盘。

当然，若是真的移动64个圆盘的话，需要移动2^64-1次，那需要的时间不是人类可以等得起的……

## 汉诺塔图片

![baa991e1b58c9addb84ea8fb1104ac75-6fcfd236-0554-48e9-bda7-377c0bfd818c](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/baa991e1b58c9addb84ea8fb1104ac75-6fcfd236-0554-48e9-bda7-377c0bfd818c.jpg)
![6b84d5e8b8cab11fecd29e4d4b39e845-a7257789-1529-4054-a9b1-3253da1cb436](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/6b84d5e8b8cab11fecd29e4d4b39e845-a7257789-1529-4054-a9b1-3253da1cb436.gif)

## 代码实现

```py
def hanoi(n, a, b, c):
    if n == 1:
        print(a, '->', c)
        move(a, c)
    else:
        hanoi(n-1, a, c, b)
        print(a, '->', c)
        move(a, c)
        hanoi(n-1, b, a, c)
```

参数n为汉诺塔的圆盘数，a、b、c分别为三个柱子，本文默认为'A'、'B'、'C'。其中`move()`函数为

```py
def move(sa, sc):
    global l1, l2, l3
    if sa == 'A' and sc == 'B':
        l2.append(l1.pop())
    elif sa == 'A' and sc == 'C':
        l3.append(l1.pop())
    elif sa == 'B' and sc == 'A':
        l1.append(l2.pop())
    elif sa == 'B' and sc == 'C':
        l3.append(l2.pop())
    elif sa == 'C' and sc == 'A':
        l1.append(l3.pop())
    else:
        l2.append(l3.pop())
```

用来移动列表里的元素，即模拟移动柱子上的圆盘。假设初始圆盘数n=4，执行结果如下图
![搜狗截图20190327132731-86199075-b498-4046-b974-85a8f088562a](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/搜狗截图20190327132731-86199075-b498-4046-b974-85a8f088562a.png)

## 知识丶总结

* 运用递归很容易解出汉诺塔的问题，此外类似的还有阶乘的算法
* 在递归次数较大时，会很明显的感觉到效率的降低，因此在对效率要求较高的场景中，要把递归转换为非递归算法

## 源代码

[https://github.com/artintZ/python/blob/master/day10/tower_of_hanoi.py](https://github.com/artintZ/python/blob/master/day10/tower_of_hanoi.py)