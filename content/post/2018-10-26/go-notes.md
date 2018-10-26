---
title: "Go Notes"
date: 2018-10-26T13:56:31+08:00
draft: true
comments: true
adsense: true
categories:
    - Tech
tags:
    - Go
---

## 注释规范

- 注释语句以 `//` 开头
- 包声明前添加注释

## 输入源

### 命令行参数

首先看下 godoc 的输出文档：

```console
$ godoc os Args
var Args []string
    Args hold the command-line arguments, starting with the program name.
```

- 通过 `os.Args` 变量获取参数
    - 变量类型：字符串切片
    - os.Args[0]：程序名（包含路径）
    - os.Args[1:]：传递的参数序列