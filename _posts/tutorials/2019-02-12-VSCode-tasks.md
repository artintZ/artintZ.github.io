---
layout: post
title: VSCode配置任务运行python文件
date: 2019-02-12 23:33:33 +0800
categories: python VSCode
tag: tutorial
---

* content
{:toc}

## 前言

在VSCode写python时，每次使用调试功能就会打开一个新的终端，解决方法：把`launch.json`文件中的`console`改成`none`。除了调试功能，还可以配置任务来执行python文件。

## 配置任务

使用快捷键`Ctrl + Shift + B`或`终端 > 配置任务`，选择`Others`，进入`tasks.json`文件，或直接在`.vscode`文件中新建该文件，修改如下：

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
        {
            "label": "python",
            "type": "shell",
            "command": "${config:python.pythonPath} ${file}",
            "options": {
                "cwd": "${fileDirname}"
            },
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

在编写python文件时，使用快捷键`Ctrl + Shift + B`即可运行当前python文件。

## 常见问题

1. 退出代码：127：默认终端为powershell，不要改动
2. 退出代码：2：`tasks.json`文件编写有问题，主要语法
3. 退出代码：1：执行文件路径有问题或不能执行当前文件
4. 若想终端执行任务的目录为当前文件的目录（涉及到新建文件的默认目录问题），必须有如下代码：

```json
"options": {
    "cwd": "${fileDirname}"
}
```

## 参考

VSCode官方文档:

* [https://code.visualstudio.com/docs/editor/variables-reference](https://code.visualstudio.com/docs/editor/variables-reference)
* [https://code.visualstudio.com/docs/editor/tasks#vscode](https://code.visualstudio.com/docs/editor/tasks#vscode)

> **options**: Override the defaults for `cwd` (current working directory), `env` (environment variables), or `shell` (default shell). Options can be set per task but also globally or per platform.

> **${fileDirname}** - the current opened file's dirname


options的shell设置明天再研究