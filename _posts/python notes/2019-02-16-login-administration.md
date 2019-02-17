---
layout: post
title: python编写的用户登录管理小程序（文件练习）
date: 2019-02-16 18:56:22 +0800
categories: python
tag: note
---

* content
{:toc}


## 题目

用python的文件操作方法写一个用户登录管理程序：

1. 有用户和管理员两个登录接口
2. 用户登录验证用户名和密码，密码错误三次锁定；用户可以注册
3. 管理员可添加、删除、解锁、锁定、查询用户

## 流程图

![python-file-登录管理小程序-ddd326d1-479f-4c01-9ac5-53831d175df5](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python-file-登录管理小程序-ddd326d1-479f-4c01-9ac5-53831d175df5.png)

## 主要功能

用户登录信息存储在`id_data`文件中，读取和追加写入文件分别用'r'和'a'打开文件，修改文件的方法则是新建文件，修改后的内容写入新文件，再使用`os`模块的`remove()`和`rename()`函数删除原文件和重命名新文件。

### 菜单

输入序号即可执行，注意`input()`默认为字符串类型，需要判断和转换为整型；以下展示主菜单，其他菜单同下。

```py
def main_menu():
    """主菜单，返回值'1. 登录', '2. 注册', '0. 退出'"""
    menu = ('1. 登录', '2. 注册', '0. 退出')
    print('\n\n', '主界面'.center(20, '-'))
    for i in menu:
        print(i)
    while True:
        choice = input('\n请输入你的选择：')
        if choice.isdigit() and int(choice) in range(3):
            return int(choice)
        else:
            print('输入不正确，请重新输入！\n')
```

显示效果：

![菜单-73eb3930-4188-4871-8105-621bcf314b14](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/菜单-73eb3930-4188-4871-8105-621bcf314b14.png)

### 登录

用户或管理员登录，主要判断用户名的状态以及密码，密码错误三次将被锁定。

```py
def login():
    '''登录过程，用户和管理员登录'''
    while True:
        print('\n\n', '登录界面/按b返回'.center(20, '-'))
        usrname = input('请输入用户名：')
        if usrname == 'b':
            break
        elif usrname == 'admin':
            for cnt in range(3):
                passwd = input('请输入管理员密码：')
                if passwd == 'admin':
                    administrator()
                else:
                    print('密码错误 %d 次，错误三次返回主菜单！\n' % (cnt+1))
            else:
                break
        elif isstatus(usrname) == 1:
            for cnt in range(3):
                passwd = input('请输入密码/按b返回：')
                if passwd == 'b':
                    break
                elif iscorrect(usrname, passwd):
                    exit('登录成功！正在退出……')
                else:
                    print('密码错误 %d 次，错误三次锁定用户！\n' % (cnt+1))
            else:
                lock(usrname)
        elif isstatus(usrname) == 2:
            print('用户已被锁定，请联系管理员解锁！\n')
        else:
            print('用户名不存在，请先注册！\n')
```

其中部分调用函数解释如下：

* isstatus()

```py
def isstatus(usrname):
    '''判断用户状态，若已注册且状态正常则返回1，\
        已注册并且被锁定返回2，未被注册返回0'''
    with open('id_data', 'r', encoding='utf-8') as f:
        for line in f:
            if usrname.join(['#', '#']) in line:
                return 1
            elif usrname.join(['$', '$']) in line:
                return 2
        else:
            return 0
```

* iscorrect()

```py
def iscorrect(usrname, passwd):
    '''判断用户名和密码是否正确，正确就返回1，否则返回0'''
    id_normal = '#'.join(['', usrname, passwd, ''])
    with open('id_data', 'r', encoding='utf-8') as f:
        for line in f:
            if id_normal in line:
                return 1
        else:
            return 0

```

* lock()和unlock()

```py
def lock(usrname, tag_old='#', tag_new='$'):
    '''锁定用户，即把标识#换成$'''
    id_normal = tag_old.join(['', usrname, ''])
    id_locked = tag_new.join(['', usrname, ''])
    with open('id_data', 'r', encoding='utf-8') as f,\
            open('id_data.bak', 'w', encoding='utf-8') as f_new:
        for line in f:
            if id_normal in line:
                line = line.replace(id_normal, id_locked)
            f_new.write(line)
    os.remove('id_data')
    os.rename('id_data.bak', 'id_data')
    if tag_old == '#':
        print('用户已被锁定，请联系管理员解锁！\n')
    else:
        print('用户已解锁，可以正常登录！\n')


def unlock(usrname):
    '''解锁用户'''
    lock(usrname, tag_old='$', tag_new='#')
```

### 管理

管理员操作界面，有添加、删除、解锁、锁定、查询用户等功能，其中调用的函数将不作赘述。

```py
def administrator():
    '''管理员操作过程，包括添加，删除，解锁，上锁，查询，退出'''
    while True:
        choice = admin_menu()
        if choice == 1:
            register()
        elif choice == 2:
            delete()
        elif choice == 3:
            while True:
                print('\n\n', '解锁/按b返回'.center(20, '-'))
                usrname = input('请输入用户名')
                if usrname == 'b':
                    break
                elif isstatus(usrname) == 2:
                    unlock(usrname)
                else:
                    print('该用户无需解锁！\n')
                    break
        elif choice == 4:
            while True:
                print('\n\n', '上锁/按b返回'.center(20, '-'))
                usrname = input('请输入用户名')
                if usrname == 'b':
                    break
                elif isstatus(usrname) == 1:
                    lock(usrname)
                else:
                    print('该用户无需上锁！\n')
                    break
        elif choice == 5:
            while True:
                print('\n\n', '查询/按b返回'.center(20, '-'))
                usrname = input('请输入用户名：')
                if usrname == 'b':
                    break
                elif isstatus(usrname) == 1:
                    print('该用户状态正常。\n')
                elif isstatus(usrname) == 2:
                    print('该用户已被锁定。\n')
                else:
                    print('没有找到该用户！\n')
        else:
            exit()
```

## 知识丶总结

* 文件修改方法：新建文件存储修改后的内容，再使用`os`模块的`remove()`和`rename()`函数删除原文件和重命名新文件。
* `input()`默认字符串类型，注意转换
* `str.center()`规定宽度把字符串放中间，不够的用字符填充
* `and`和`or`判断的时候，优先级小于`in`，并且`a in c and/or b in c`不可写作`a and/or in c`
* python中的条件语句可以用`if-elif-...-else`实现
* 利用函数(过程)让代码结构更清楚

这个小程序我花了三天才完成。虽然我首先画完了流程图整理了思路，但是在实际写代码的时候发现有好多重复代码，因此决定推翻之前的思路重新构写，其实大多数时间都是在优化函数结构，让代码条理更加清晰。虽然现在写完感觉还是有很多可优化的部分。

## 源代码

[https://github.com/artintZ/python/blob/master/day3/user_login.py](https://github.com/artintZ/python/blob/master/day3/user_login.py)