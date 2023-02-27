---
title: "华顺信安Golang面试题"
date: 2023-02-27T23:24:29+08:00
math: false
tags: ['go']
categories: ['面试']
---

# 

2023年2月27日晚六点面试，总共半小时（哎，还是我个人太菜了）。

## 第一题和切片相关题，考切片底层

```go
    a := []int{1, 2, 3, 4, 5}
    b := a[:3]
    fmt.Println(cap(a))
    fmt.Println(len(a))

    fmt.Println(cap(b))
    fmt.Println(len(b))
```

运行结果:

```
5
5
5
3
```

然后在上面的代码上添加一行

```go
b = append(b, 1, 2, 3)
```

运行结果

```
5
5
10
6
```

**结论：刚开始切片b指向的是原来的数组a，所以cap是一致的，但是当给b后面添加元素后，直接重新分配新的地址了！**

---

## 第二道题，考channel

```go
package main

import "fmt"

func main() {
    c := make(chan int)
    for i := 0; i <= 10; i++ {
        c <- i
    }
    go func() {
        for item := range c {
            fmt.Println(item)
        }
    }()
}
```

问，这代码的功能，打印的效果

尴尬了，刚刚运行了一下，是死锁🤣

---

## 第三道题，考go面向对象的

首先是问我面向对象的三大特征：封装，继承和多态。然后问我go怎么实现继承和多态，我说不会（😭我怎么什么都不会呀），然后就考了我下面的代码

```go
package main

import "fmt"

type P struct {
    name string
}

func (p P) setname(n string) string {
    p.name = n
    return n
}

func (p P) getname() string {
    return p.name
}

func main() {
    p := &P{name: "zhangsan"}
    fmt.Println(p.setname("lisi"))
    fmt.Println(p.getname())
}
```

问运行结果

```
lisi
zhangsan
```

具体怎么解释我也不会。哎
