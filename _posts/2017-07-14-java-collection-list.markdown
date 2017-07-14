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

- List 是一个`接口`,继承于 Collection 的接口

- 有序队列

    - 次序是 List 最主要的特点

- 元素以线性方式存储，集合中可以存放`重复`元素

- 可以存在多个 `null`

### List 接口主要实现类

- ArrayList : 代表长度可以改变得数组。可以对元素进行随机的访问，向ArrayList()中插入与删除元素的速度慢。

- LinkedList : 在实现中采用链表数据结构。插入和删除速度快，访问速度慢。

- Vector : 向量，可以实现自增长的对象数组。JDK 早起版本存在，与上边两个不同的是，Vector 是同步的，保证了线程的安全。

- Stack : 堆栈，继承于 Vector，并进行扩展。采用后进先出原则。

### ArrayList

- 初始容量 `10`

    - 如果溢出，扩容为原来的1.5倍。原容量为奇数时，扩容时，取两者较小值。

    - 没有 capacity 容量方法。需要使用反射机制。

- 底层由数组实现

- 索引 `index`

- 允许对元素进行快速、随机访问，因为有`索引`

- 插入、删除开销`大`

    - 因为插入、删除需要移动改元素后边所有元素

    - 操作元素越靠前，开销越大，反之亦然。


### LinkedList

- 底层由链表实现

- 对顺序访问进行了优化，但是随机访问较慢

    - 访问元素越靠前，开销越小，反之亦然

- 插入、删除数据开销`小`

    - 因为插入、删除任何元素，只需更改链表前后元素的指针指向即可（自行车链子）

