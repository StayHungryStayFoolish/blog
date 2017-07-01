---
layout:     post
title:      "Java 数组 - 基础"
subtitle:   "Basic Array"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-29
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 数组概念
    - 声明、初始化、创建
    - 特性
---

## 数组

- 同一类型值的集合

- 数组是静态的

- 数组的声明、初始化、创建是一个整体过程

- 数组具有索引（下标）index

- 数组是有长度的，length，推荐循环时，使用 length，不会出现下标越界

- 数组需要遍历

    - 循环来输出 for for-each 循环

- 一维数组、二维数组、多维数组

### 数组的定义方式

- 动态定义 String[ ] aArray = new String`[` 5 `]`;

- 静态定义 String[ ] bArray = {"a","b","c","d","e"}

- 静态定义 String[ ] cArray = new String[ ]{"a","b","c”,"d","e”}


        第一种定义了一个数组，并指定了数组的长度，属于动态定义。

        第二种和第三种在分配内存空间的同时，还初始化了值。

- 数组声明，创建，初始化必须都放在一条语句中，分开会出现语法错误。

- 典型错误：

int[ ] ints;

ints = {1,2,3,4,5};
语句分开，直接报错。

- 特殊情况

    二维、多维数组，只定义 行 就可以，不会报错。

    int[ ][ ] a = new int`[`3`]`[ ];
    System.but.println(a.length); // 3

    int[ ][ ] b = new int`[`3`]` `[`5`]`;
    System.out.println(b.length); // 3

    int[ ] arr = new int`[` 3 `]`;
    System.out.println(arr.getClass());

### 打印数组

- Arrays.toString(arr);

- Arrays.deepToString(arr);

    deepToString(); 更适合打印多维数组

        String[][] b = new String[3][4];
              for (int i = 0; i < 3; i++){
                  for (int j = 0; j < 4; j++){
                      b[i][j] = "A" + j;
                      }
                  }
                  System.out.println(Arrays.toString(b));
                  //输出[[Ljava.lang.String;@55e6cb2a, [Ljava.lang.String;@23245e75, [Ljava.lang.String;@28b56559]

                  System.out.println(Arrays.deepToString(b));
                  //输出[[A0, A1, A2, A3], [A0, A1, A2, A3], [A0, A1, A2, A3]]


- 数组输出形式

        class Demo{
            public static void main(String[] args) {
                int[] intArray = {1, 2, 3, 4, 5, 6};
                String intArrayString = Arrays.toString(intArray);

                System.out.println(intArray); // 输出的是一个 String 类型的 Hex 码
                System.out.println(intArrayString); // 输出的是一个 String 类型
            }
        }

        结果：
        [I@511d50c0
        [1, 2, 3, 4, 5, 6]

### 通过反射机制访问数组元素

- 反射机制 是通过 java.lang.reflect.Array 这个类来处理数组。

    reflect /rɪ'flekt/ 反射、反映

- 可以使用 Array.get(); Array.set(); 方法访问数组，设置数组。

