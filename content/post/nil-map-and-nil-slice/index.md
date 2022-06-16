---
# Documentation: https://wowchemy.com/docs/managing-content/

title: "Nil Map and Nil Slice in Golang"
subtitle: "关于nil map和nil slice"
summary: "关于nil map和nil slice"
authors: [admin]
tags: [Golang]
categories: [Golang]
date: 2021-08-08T00:52:13+08:00
lastmod: 2021-08-08T00:52:13+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## 前言

我烂了

## Nil

`Golang`的`nil`是对于传统C系语言`null`所做的一个安全性优化，笔者在学习`map`和`slice`有一些相关的疑惑。

在如下代码运行后，`map0`和`slice0`的值均为`nil`：

```go
var map0 map[string]int
var slice0 []string
```

与之对应的是比较安全的建立方式，这种情况下建立的空`map`和空`slice`都非`nil`值：

```go
map1 := make(map[string]int, 0)
slice1 := make([]string, 0)
```

## 对`map == nil`

对于`map`增加键值对，前者会发生`panic`，而后者可以：

```go
map0['maths'] = 60	//panic: assignment to entry in nil map
map1['maths'] = 60	//OK
```

## 对`slice == nil`

对于`slice`的常规操作，则两者都可以进行：

```go
append(slice0, "maths")
append(slice1, "maths")
range(slice0)
range(slice1)
len(slice0)
len(slice1)
```

## 原因分析

`map`增加键值对的行为是在`Golang`底层实现的，而`slice`的`append`,`range`,`len`操作都是在`builtin`包内的函数实现的，对`nil`值情况做了差错控制。

## 结论

用`make`，请。
