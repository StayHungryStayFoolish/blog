---
layout:     post
title:      "Java 深入了解 length 与 length() 区别"
subtitle:   "结构"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-07
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 属性与方法
---

### 示例：

    // 数组的 length 不带括号
    int[] arr = new int[3];
    System.out.println(arr.length);

    // 字符串的 length() 带有括号
    String str = “abc”;
    System.out.println(str.length());

### 为什么数组的 length 是其属性？

- 数组是一个容器对象。

- 数组一旦诶创建，长度将是固定的。

- 数组长度可以作为 final。

`因此长度被视为数组的一个属性`


