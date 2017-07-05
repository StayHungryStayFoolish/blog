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

- 内部结构

    - 字符数组构成的

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

- matches() 是否匹配给定正则表达式

- replace() 替换字符串

- replaceAll() 使用正则替换匹配的字符串

- replaceFirst 使用正则替换匹配的第一个字符串

- split() 使用正则拆分

- startWith 是否以...前缀开始

- subString() 根据给定索引起始，返回一个新的字符串

- toCharArray() 转换为一个新的字符数组

- toLowerCase() 转换为小写

- toUpperCase() 转换为大写

- trim() 裁剪首尾的空白

- valueOf() 返回 String 类型


### StringBuffer、StringBuilder

- 字符缓冲区，初始容量16个字符

- 可以使用 append、insert、delete、deleteCharAt、reverse 等方法改变长度、内容

### 三者区别

- 效率

    - String 最慢，但是稳定

    - StringBuffer 快，相对稳定

        - 保证同步，多线程安全。

    - StringBuilder 最快，稳定

        - 不是同步的，多线程不安全。


- 值变化

    - String 初始化之后，不可改变。

        - 因为在 字符串池中创建了一个对象。当又建一个值时，JVM 会先去池中，找是否有已经存在的，如果没有，会再创建一个对象。之前的将会一直存在。

        - 所以 String 的值不会被改变，是因为再创建一个，只是指向发生改变，其值还存在。

    - StringBuffer、StringBuilder 值会发生变化
