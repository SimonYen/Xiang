---
title: "CPP之动静态库相关"
date: 2023-03-15T14:53:39+08:00
math: false
tags: ['gcc']
categories: ['CPP']
---

# 静态库

## 命名规则

**libxxx.a**

其中lib为前缀，.a为后缀，固定的。

xxx库的名字。

## 生成方法

通过gcc获得.o文件（-c 参数）

使用ar命令打包

```shell
ar rcs libxxx.a xxx.o xxx.o
```

- r-将文件插入备存文件中
- c-建立备存文件
- s-索引

## 使用方法

假设静态库的名字为xxx,所在路径为当前路径。

```shell
g++ main.cpp -lxxx -L.
```

# 动态库

## 命名规则

**libxxx.so**

其中lib为前缀，.so为后缀，固定的。

xxx库的名字。

## 生成方法

gcc得到与位置无关的代码

```shell
gcc -c -fpic a.c b.c
```

gcc得到动态库

```shell
gcc -shared a.o b.o -o libxxx.so
```

## 使用方法

编译方法同静态库，但是运行该程序时要添加环境变量

```bash
export LD_LIBRARY_PATH=程序动态库所在目录
```

