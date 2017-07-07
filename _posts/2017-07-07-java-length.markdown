---
layout:     post
title:      "Java 浅谈 length 与 length() 区别"
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


### 为什么 String 有 length() 方法？

- String 内部数据结构是一个 char 数组。

- 该属性已经在 char 数组中提供了。

`因此，没有必要定义一个已经存在的属性`

`但是 Java 中的 char 数组并不等于 String 字符串，尽管 String 内部结构是 char 数组来实现的`


        char []s = {'a','b','c’};
        String string1 = s.toString(); // char 转换为 String 字符串
        String string2 = new String(s); // char 转换为 String 字符串
        String string3 = String.valueOf(s); // char 转换为 String 字符串

        System.out.println(s); // abc
        System.out.println(string1); // [C@511d50c0
        System.out.println(string2); // abc  -> 字符串
        System.out.println(string3); // abc  -> 字符串


