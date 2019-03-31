---
layout: post
title: python编写一个ssh（socket练习）
date: 2019-03-07 17:57:41 +0800
categories: python
tag: note
---

* content
{:toc}


## 题目

用python的`socket`模块编写一个ssh，实现基本的cmd命令。

## 流程图

![python-socket-ssh](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/python-socket-ssh-9c3481f7-9380-4377-929c-b51178baf292.png)

## 主要功能

### 调用`os`模块

```py
import os
os.popen(cmd).read()
```

### socket发送和接收

```py
import socket
socket.send(bytes)
socket.recv(1024)  # 官方建议最大8192
```

## 知识丶总结

* `socket.send()`发送bytes数据类型，中文需要`encode()`
* 在发送前数据前先发送数据大小，给予接收方循环接收的满足条件
* 在发送数据大小后并不立即发送数据，以免数据大小和数据发生粘包（同时存入缓存区同时发送），要先接收一下对方的确认信号再发送数据。即，在发送数据大小和数据之间进行一次握手。

## 源代码

server: [https://github.com/artintZ/python/blob/master/day8/sock_server_ssh.py](https://github.com/artintZ/python/blob/master/day8/sock_server_ssh.py)

client: [https://github.com/artintZ/python/blob/master/day8/sock_client_ssh.py](https://github.com/artintZ/python/blob/master/day8/sock_client_ssh.py)