---
layout:     post
title:      "Java 集合框架之 -- List"
subtitle:   "List 列表"
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

### List

- List 是一个`接口`,继承于 Collection 的接口，代表有序队列。

- 底层是用`数组`来实现的

- 元素以线性方式存储，集合中可以存放`重复`元素

### List 接口主要实现类

- ArrayList : 代表长度可以改变得数组。可以对元素进行随机的访问，向ArrayList()中插入与删除元素的速度慢。

- LinkedList : 在实现中采用链表数据结构。插入和删除速度快，访问速度慢。

- Vector : 向量，可以实现自增长的对象数组。JDK 早起版本存在，与上边两个不同的是，Vector 是同步的，保证了线程的安全。

- Stack : 堆栈，继承于 Vector，并进行扩展。采用后进先出原则。

