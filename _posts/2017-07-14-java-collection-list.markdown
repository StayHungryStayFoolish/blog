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
    - ArrayList
    - LinkedList
    - Vector
    - Stack
    - 容量
---

### List

- List 是一个`接口`,继承于 Collection 的接口

- 有序队列 `index`

    - 次序是 List 最主要的特点

- 元素以线性方式存储，集合中可以存放`重复`元素

- 可以存在多个 `null`

### List 接口主要实现类

- ArrayList : 代表长度可以改变得数组。可以对元素进行随机的访问，向ArrayList()中插入与删除元素的速度慢。

- LinkedList : 在实现中采用链表数据结构。插入和删除速度快，访问速度慢。实现了 Deque 接口，`先进先出`原则。

- Vector : 向量，可以实现自增长的对象数组。JDK 早起版本存在，与上边两个不同的是，Vector 是同步的，保证了线程的安全。

- Stack : 堆栈，继承于 Vector，并进行扩展。采用`后进先出`原则。

### ArrayList

- 初始容量 `10`

    - 如果溢出，扩容为原来的1.5倍。原容量为奇数时，扩容时，取两者较小值。

    - 没有 capacity 容量方法。需要使用反射机制。

    - 无 capacity ，Vector 有。

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

- 因为没有索引，所以只能自己扩展几个关于 `first` `last` 方法装装样子咯。

    - addFirst()

    - addLast()

    - getFirst()

    - getLast()

    - removeFirst()

    - removeLast()

### Vector

- 初始容量 10

    - 如果溢出，扩容为原来的 2 倍。

    - 有 capacity 方法

- 同步，安全性高

### Stack

- 原理类似弹匣

- 了解几个方法

    - peek() 查看堆栈顶部对象

    - pop() 移除堆栈顶部对象

    - push() 压入堆栈顶部

### 方法介绍

- List 继承于 Collection，所以拥有 Collection 所有方法

- Collection 接口主要方法

    - add()

    - clear()

    - contains()

    - equals()

    - isEmpty()

    - iterator() `必须使用 Iterator 来接收返回值`

    - remove()

    - removeAll()

    - size()

    - toArray() `返回此集合中所有元素的数组`

        - 无参使用 Object 接收返回值

        - 有参使用参数类型接收返回值 `集合和数组之间转换桥梁`

- List 扩展后

    - get(int index)

    - indexOf() 返回第一次出现指定元素索引，无返回 -1

    - lastIndexOf() 同上，相反

    - remove(int index) 移除一定索引，`返回移除元素`

    - remove(Object o) 移除指定元素，返回布尔值

    - set(int index,E element) 替换指定索引，`返回被替换的 E`

    - subList(fromIndex , toIndex） 返回子集合视图，`左开右闭，即包含起始，不包含结束`

- ArrayList 扩展 List 后

    - removeRange(int formIndex ,int toIndex) 移除列表中起始索引到结束索引之间的所有元素 `左开右闭`

- LinkedList 不再介绍，请查看 API

- Vector

    - setSize() 设定向量大小

- Stack 略



