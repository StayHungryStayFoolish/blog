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

        class Parent{
            // 静态变量
            public static String p_StaticField = "父类-静态变量";
            // 变量
            public String p_Field = "父类-变量";

            public static final String p_Field1 = "父类-终态常量";
            // 不初始化时，输出为该类型的默认值  String -- null  int -- 0
            public static String string;
            // 静态初始化块
            static{
                // 块输出的顺序按语句先后顺序输出。
                System.out.println(p_StaticField);
                System.out.println("父类-静态初始块");
             // 注意：sout 不能输出 p_Field，因为类型不一样。static 只能输出static语句
                System.out.println(p_Field1);
                System.out.println(string);
            }
            // 初始化块
            {   // 初始化块可以输出静态的。可以被类的所有实例共享，静态变量无需获得其所属类的对象就可以访问。
                // 块输出的顺序按语句先后顺序输出。
                System.out.println(string);
                System.out.println(p_Field);
                System.out.println("父类-初始化块");
            }

            public Parent(){
                System.out.println("父类-无参构造器");
            }

            public Parent(String p_Field){
                this.p_Field = p_Field;
                System.out.println("父类-有参构造器");
            }

            public static void main(String[] args){
                new Parent();
                new Parent(string);
            }
            {
                System.out.println("----------");
            }
        }

        public class VariableOrder extends Parent{
            // 静态变量
            public static String s_StaticField = "子类-静态变量";
            // 变量
            public String s_Field = "子类-变量";
            // 静态初始化块
            static{
                System.out.println(s_StaticField);
                System.out.println("子类-静态初始块");
            }
            // 初始化块
            {
                System.out.println(s_Field);
                System.out.println("子类-初始化块");
            }

            public VariableOrder(){
                System.out.println("子类-构造器");
            }

            // 程序入口
            public static void main(String[] args){
                new VariableOrder();
            }
        }

        运行结果：  注意：子类的 静态变量 和 静态初始化块 的初始化是在父类的变量、初始化块和构造器初始化之前就完成了
                                        父类-有参构造器   没有输出，是因为子类继承的父类的无参构造
        父类-静态变量
        父类-静态初始块
        父类-终态常量
        null
        子类-静态变量
        子类-静态初始块
        null
        父类-变量
        父类-初始化块
        ----------
        父类-无参构造器
        子类-变量
        子类-初始化块
        子类-构造器

        class X{
            static String xVar = "x static value";
            static{
                System.out.println(xVar);
                System.out.println("X static block");
                xVar = "static value";
        // 输出的是 "static value",而不是"x static value"
                //System.out.println(xVar);
        }

            public X(){
                System.out.println("无参构造");
            }
        }

        public class Z extends X{
            static String z = "Z static value";
            static{
                System.out.println("Z static block");
            }
            public static void main(String[] args){
                System.out.println(z);
                System.out.println(xVar);
            }
        }

        运行结果： 注意输出顺序：父类静态块先输出，再输出子类静态块。
                如果 public static void main(String []args){ 括号内什么不写，还是会输出三个静态块 }
        x static value
        X static block
        Z static block
        Z static value
        static value  --- 最后输出是因为在 父类 static 块里，但是没有调用。所以在程序入口，按照输出先后顺序输出， z 先输出，再输出 xVar ,xVar 被重新赋值

