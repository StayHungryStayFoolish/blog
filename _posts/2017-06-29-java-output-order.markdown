---
layout:     post
title:      "Java 静态、构造器、非静态之初始化顺序"
subtitle:   "有序输出"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-06-29
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 静态域
    - 静态块
    - 非静态块
    - 构造函数
---

## 块 概念

- 无名

- 无参数

- 无返回类型

- `静态块` 有 static 修饰

        {
            // 方法体
        }


        static{
            // 方法体
        }


## 标准类的初始化顺序

    public class InitialOrderTest{
    // 静态变量
        public static String staticField = "静态变量";
    // 变量
        public String field = "变量";

    // 静态初始化块
        static{
            System.out.println(staticField);
            System.out.println("静态初始化块");
        }

    // 初始化块 = 构造代码块
        {
            System.out.println(field);
            System.out.println("初始化块");
        }

    // 构造器
        public InitialOrderTest(){
            System.out.println("构造器");
        }

        public static void main(String[] args){
            new InitialOrderTest();
        }
    }

    运行结果：  注意： new InitialOrderTest();  输出的 初始化块  的内容，因为主方法是静态，不能输出不是静态的。

    静态变量
    静态初始化块
    变量
    初始化块
    构造器

## 类继承后的输出顺序



