---
title: "Make简易指北"
date: 2023-03-16T13:38:59+08:00
math: false
tags: ['make']
categories: ['CPP']
---

# 什么是make？

以我粗浅的理解来看，make是c,c++的一种自动化编译工具，通过在项目下的makefile文件，自动执行shell命令（大部分就是编译相关的命令啦）

# makefile文件

## 文件命名

makefile或者Makefile都行

## Makefile规则

一个Makefile文件中可以有一个或者多个规则

```makefile
target xxx: dependence hhh
	command
```

target：最终要生成的文件

dependence：生成目标所需的文件或是目标

command：通过执行命令对依赖操作来生成目标（前面必须加tab缩进）

## 变量

### 自定义变量

变量名=变量值		var=hello

### 预定义变量

- AR：归档维护程序的名称，默认值为ar
- CC：C编译器，默认值为cc
- CXX：C++编译器，默认值为g++
- $@：目标的完整名称
- $<：第一个依赖文件的名称
- $^：所有的依赖文件

### 如何获取变量的值

$(变量名)

懒得写了，具体可以看这个网站：[跟我一起写Makefile — 跟我一起写Makefile 1.0 文档](https://seisman.github.io/how-to-write-makefile/index.html)
