---
layout:     post
title:      "Java Serializable "
subtitle:   "序列化、反序列化"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Serializable
    - 序列化
    - 反序列化
---


### Serializable

- 序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作,也可将流化后的对象传输于网络之间。

- 序列化是为了解决在对对象流进行读写操作时所引发的问题。

- java.io.Serializable 标识接口

    - 类通过实现 java.io.Serializable 接口以启用其序列化功能

    - 未实现此接口的类将无法使其任何状态序列化或反序列化

    - 可序列化类的所有子类型本身都是可序列化的

    - 序列化接口没有方法或字段，仅用于标识可序列化的语义

### 例：

    ```java
        public class User implements Serializable {
           private Integer id;
           private String name;
           private double height;
           private transient boolean isMarried;

           public User() {
           }

           public User(Integer id, String name, double height, boolean isMarried) {
               this.id = id;
               this.name = name;
               this.height = height;
               this.isMarried = isMarried;
           }

           @Override
           public String toString() {
               return "User{" +
                       "id=" + id +
                       ", name='" + name + '\'' +
                       ", height=" + height +
                       ", isMarried=" + isMarried +
                       '}';
           }
        }
    ```