---
layout:     post
title:      "Java 值传递、参数传递 区别"
subtitle:   "传递方式"
date:       2017-07-09
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 值传递
    - 参数传递
    - 传递方式
---

### 基本数据作为参数传递

- 例：

        public class Test1 {
            public static void main(String[] args) {
                int n = 3;
            System.out.println("Before change, n = " + n);
                changeData(n);
            System.out.println("After changeData(n), n = " + n);
            }

             public static void changeData(int n) {
                 n = 10;
             }
        }
        // 输出结果：
        /*
        Before change, n = 3
        After changeData(n), n = 3

- `基本类型作为参数传递时，是传递值的拷贝，无论你怎么改变这个拷贝，原值是不会改变`