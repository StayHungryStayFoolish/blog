---
layout:     post
title:      "Java String 字符串"
subtitle:   "比较特殊的类"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-24
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 值不能发生改变
---

## String 字符串

- 官方类定义

    - public final class String extends Object

      implements Serializable, Comparable<String>, CharSequence

- 特性

    - 初始化后，其值不能改变

        - 因为是 final 修饰的

    - 共享性

        - 因为 String 创建后，对象是不可变的。




