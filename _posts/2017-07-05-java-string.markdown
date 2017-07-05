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

### 常用方法

- charAt() 指定索引处的 chat 值

- concat() 在字符串末尾拼接

- contains() 是否包含

- endsWith() 是否以...结尾

- equals() 是否相等 （重要）

- equalsIgnoreCast() 忽略大小写比较

- format() 指定格式/语言环境返回格式化的字符串

- getBytes() 将字符集编码为 byte 序列，存储到 byte 数组中

- indexOf() 返回指定字符串在此字符串中第一次出现的索引，不存在返回 -1

- isEmpty() 当 length() 为0时，返回 true

- lastIndexOf() 返回指定字符串出现的最后一次索引

- length() 返回字符串长度

- matches

- replace

- replaceAll

- replaceFirst

- split

- startWith

- subString

- toCharArray

- toLowerCase

- toUpperCase

- trim

- valueOf



