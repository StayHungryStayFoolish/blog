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

- 构造方法

    - String() 初始化一个 String 对象，表示空序列

    - String(byte[ ] bytes) 使用字符集数组，构造一个新的 String

    - String(byte[ ] bytes, int offset, int length) ) 默认字符集解码指定的 byte 子数组，构造一个新的 String。

    - String(StringBuffer buffer)  分配一个新的字符串，它包含字符串缓冲区参数中当前包含的字符序列。

    - String(StringBuilder builder) 分配一个新的字符串，它包含字符串生成器参数中当前包含的字符序列。

    - .eg





