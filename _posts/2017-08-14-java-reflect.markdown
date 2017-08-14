---
layout:     post
title:      "Java Reflect"
subtitle:   "反射机制"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Reflect
    - 反射机制
---

### Reflect 反射机制

`Java反射是Java被视为动态（或准动态）语言的一个关键性质。`

这个机制允许程序在运行时透过 `Reflection` 取得任何一个已知名称的class的内部信息，

包括其 `modifiers`（public, static 等）、`constructors` 、`superclass`（例如Object）、实现之`interfaces`（例如Cloneable），
也包括 `fields` 和 `methods` 的所有信息，并可于运行时改变 `fields` 内容或唤起 `methods` 。

Java反射机制允许程序在运行时加载、探知、使用编译期间完全未知的classes。

换言之，Java可以加载一个运行时才得知名称的class，获得其完整结构。


### Fields 类

- getFields() 获取当前 `非 private` 域

- getDeclaredFields() 获得所有域 包括 `private`

### Methods 类





