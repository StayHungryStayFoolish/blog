---
layout:     post
title:      "Java 集合框架之 -- Map"
subtitle:   "Map 映射"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-14
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - HashMap
    - LinedHashMap
    - Hashtable
    - TreeMap
---

### Map 映射

- Map 是一个`接口`，使用 Key - Value 键值对存储数据。相当于小型数据库。

- key 具有唯一性

- key -> value 正向，不可逆向，一个键只能映射一个值

- 不同于 Collection 接口添加元素的方法（add 操作），Map 统一使用 put（K，V）

    - put(K,V) 可以`覆盖原有值`

### Map 接口主要实现类

### HashMap 特性

- `无序`

- key，value 不能为 `null`

- 效率高

### Hashtable 特性

- `无序`

- key，value 不能为 `null`

- 初始容量是 `11`，（不同于 Collection 的初始化容量）加载因子0.75

  - `HashMap` `HashSet` `LinkedHashMap` 都是 `16`

- 同步，多线程是安全的。

### LinkedHashMap 特性

- 按`元素添加顺序`排序

- 底层使用 Hashtable 实现

- key，value 不能为 `null`

### TreeMap 特性

- 使用 红 - 黑 树结构存储元素

- 因为基于 NavigableMap 实现，所以按照`键的自然顺序`排序

- 一般用于单线程中，存储有序的映射。

###  方法介绍

- Map 方法

  - clear()

  - containsKey(Object key) 是否包含指定 `键`，无则返回 false

  - containsValue(Object vale) 是否包含一个或多个指定 `值`，无则返回 false

  - entrySet() 返回映射关系视图，使用 Set 来接收

  - equals()

  - get(Object key) 通过指定`键`获取`值`，返回的是 value

  - isEmpty()

  - keySet() 返回键的映射视图，使用 Set 来接收

  - put(K key，V value)

  - putAll(Map<? extends ,? extends V> m) 将指定 Map 放入当前 Map

  - remove(Object key)移除指定键

  - size()

  - values() 返回值得 Collection 视图，使用 `Collection` 接收

- HashMap 实现于 Map，拥有全部方法

- HashTable 实现于 Map，拥有全部方法

- LinkedHashMap 实现于 Map，拥有全部方法

- TreeMap 实现于 Map，拥有全部方法

    - firstEntry() 返回最小键关联的 K - V 映射关系，如果映射为空，返回 null ，使用 Map.Entry() 接收

    - firstKey() 返回第一个（也是最低的） 键

    - floorEntry(K key) 返回小于指定键最大的键-值映射关系，不存在返回 null，使用 Mpa.Entry() 接收

    - floorKey(K key) 返回小于指定键最大的关联键，不存在返回 null

    - lastKey() 返回最后一个（也是最高的）键

    - lowerKey(K key) 返回小于支顶尖的最大键

    - subMap(Key fromKey ,Key toKey) 返回映射视图`左开右闭`
