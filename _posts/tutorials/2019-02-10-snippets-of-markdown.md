---
layout: post
title: VSCode中markdown文件用户代码段无法生效的解决方法
date: 2019-02-10 13:52:18 +0800
categories: markdown VSCode
tag: tutorial
---

* content
{:toc}


## 综述

VSCode可以很方便地编辑用户自定义代码段，即`文件`>`首选项`>`用户代码片段`或直接在`命令面板`搜索`snippets`，根据示例编写代码段即可。但是我在编写markdown代码段后出现了问题：输入prefix没有自动提示，即markdown没有intellisense功能。

## 解决方法

* 在`文件`>`首选项`>`设置`中搜索`tabCompletion`选择`on`或者`onlySnippets`

![snippets-06b5e8cf-995a-455f-aa00-1122e3882065](https://md-image-1258527510.cos.ap-shanghai.myqcloud.com/snippets-06b5e8cf-995a-455f-aa00-1122e3882065.png)

* 或者直接在`settings.json`文件中添加如下代码：

```json
"editor.tabCompletion": "onlySnippets"
```

然后在编写markdown文件时输入相应的prefix按`Tab`键即可插入代码段。

## 参考

[VSCode官网文档](https://code.visualstudio.com/docs/editor/userdefinedsnippets)

>By default, tab completion is disabled. Use the editor.tabCompletion setting to enable it. These values exist:
>
>* off - (default) Tab completion is disabled.
>* on - Tab completion is enabled for all suggestions and repeated invocations insert the next best suggestion.
>* onlySnippets - Tab completion only inserts static snippets which prefix match the current line prefix.

>In Visual Studio Code, snippets show in IntelliSense (Ctrl+Space) mixed with other suggestions as well as in a dedicated snippet picker (Insert Snippet in the Command Palette). There is also support for tab-completion: Enable it with "editor.tabCompletion": "on", type a snippet prefix, and press Tab to insert a snippet.