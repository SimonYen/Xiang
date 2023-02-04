---
title: "我的Deepin上编程环境搭建笔记"
date: 2023-02-04T23:25:02+08:00
math: false
tags: ['Linux','杂项']
categories: ['Linux环境折腾']
---

# snap安装及其配置

## 安装

由于Deepin基于Debian，Debian虽然稳如老狗，但是包的版本太低了，例如go才1.15，所以先安装snap，再使用它安装一些最新的包（主要还是出于方便的原因）。

apt安装

```bash
sudo apt update
sudo apt install snapd
```

接着更新内核

```bash
sudo snap install core    
```

最后测试一下

```bash
sudo snap install hello-world
```

## PATH配置

默认apt安装snap并没有加入到path中

在`~/.bashrc`或`/etc/environment`文件末尾加入

`export PATH="$PATH:/snap/bin"`

---

# golang语言安装及其配置

## 安装

采取最方便的方法，包管理器

`snap install golang --classic`

## goproxy设置

相当于设置go的模块源镜像，提高模块的下载速度，[官网](https://goproxy.cn/)

```bash
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.cn,direct
```

## PATH配置

snap安装的go没有将`$HOME/go/bin`目录加入到系统变量中，go语言源码编译的一些工具无法使用

在`~/.bashrc`或`/etc/environment`文件末尾加入

`export PATH="$PATH:$HOME/go/bin"`

---

# rust语言安装及其配置

## 安装

官方的安装方法在墙国行不通，这里采取代理的方法，[RsProxy](https://rsproxy.cn/)

因为rust编译依赖c编译器，事先`sudo apt install gcc g++ cmake`

在`~/.bashrc`末尾中添加代理

```bash
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"
```

然后安装rust，按默认的就好

```bash
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

重启终端使PATH修改生效

## crates.io镜像

编辑cargo配置文件`~/.cargo/config`

```toml
[source.crates-io]
# To use sparse index, change 'rsproxy' to 'rsproxy-sparse'
replace-with = 'rsproxy'

[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"

[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"

[net]
git-fetch-with-cli = true
```

****
