---
layout:     post
title:      "Java 接口比抽象更抽象"
subtitle:   "Interface"
iframe:     ""
navcolor:   "invert"
date:       2017-06-18
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 接口
    - 抽象类
    - 设计层次
    - 使用场景
---

## 接口 interface

- 接口是一种比抽象类更加抽象的 "类”。

- 接口不是类，是跟类同级别的一种存在。

- 接口中，只存在 常量 `static final` ，抽象方法`abstract`。

- 接口时对外提供服务的。

## 设计层次

- 抽象层次不同：

    - 接口是对行为抽象。

    - 抽象类是对类抽象。

- 跨域不同：

    - 接口跨域不同的类。

        - 实现接口的类之间可以不存在任何关系，共同之处，类似一种契约。例如：接口定义 fly(); 抽象方法，Animal 类的动物鸟，可以实现接口。Vehicle 类的飞机，可以实现接口。


        - 抽象类必须被子类实现，抽象类所体现的是一种继承关系，体现子父类之间的自上而下的关系。

    - 抽象类所跨域的是具有相似特点的类。Animal 类的鸟、狗都会叫，这个就是抽象方法。都可以吃东西，这个就是抽象方法。然后抽象出来一个 Animal 抽象类。

- 设计顺序不同

    - 接口是自顶向下设计出来的。先定义`一种契约`抽象方法，供所有的类去实现。

    - 抽象类是自下而上抽象出来的。根据一定范围的类，来抽取出一种抽象方法，来表述这些类的概念。

- 接口是用来建立 类 与 类 之间的协议，它所提供的只是一种形式，而没有具体的实现。所以，接口不能被实例化`new 接口`。

- 接口是用来被实现的，`implements` 关键字，表示该 类 要遵循该接口。实现该接口的所有抽象方法。

- 接口是抽象类的延伸，Java 为了保证数据的安全性，规定类不能多重继承。但接口弥补了抽象类不支持多继承的缺陷。

- 接口与抽象的不同点

    - 接口可以多继承，抽象类只能单继承

    - 接口只能存在 常量 ，抽象类 可以存在 普通域。

    - 接口的方法必须是抽象方法，抽象类可以有抽象方法，也可以含有非抽象方法 `甚至只有非抽象方法，但失去了意义`。

    - 接口是用来被实现的 关键词 implements 并实现其所有抽象方法，抽象类是用来被继承的，由子类实现其所有抽象方法 关键词 extends。


### 接口的继承过程

- 例

        public interface InterfaceDemo {
            int I = 100;
            void add();
            void m();
            void n();
        }

        class InterfaceClass implements InterfaceDemo{
            @Override
            public void add() {

            }

            @Override
            public void m() {

            }

            @Override
            public void n() {

            }
        }

### 场景模拟

- 场景设置：

    一个标准类，如果不想 实现 接口所有的抽象方法。

    1.可以让一个抽象类实现接口，然后把不需要的方法 实现 出来。

    2.该类再去继承抽象类，然后只有需要的抽象方法需要实现了。`因为普通类不会实现抽象类的普通方法`

    接口 A 拥有 a1,a2,a3,a4  四种抽象方法

    标准类 C 只想拥有 a3,a4 的两种抽象方法

- 方法：

    1.做一个抽象类 B，让 抽象 B 去 implements 接口 A，实现 a1,a2 两种方法。

    2.然后 标准类 C extends 抽象 B，实现 B的方法`抽象B默认拥有接口A的 a3,a4 两种抽象方法`，拥有了接口A的 a3,a4方法。

    抽象类B 对接口A而言，a3,a4的方法是继承关系。

- 例：

        // 接口A
        public interface InterfaceDemo {
            int I = 100;
            void add();
            void m();
            void n();
        }
        // 抽象类B实现接口A的一个标准类C不需要的方法,接口拿过来的方法属于继承关系
        abstract class InterfaceTest implements InterfaceDemo {
            @Override
            public void add() {

            }

        // 标准类C继承抽象类B，从而间接实现接口A的一些方法 [ 只实现自己需要的方法 ]
        class InterDemo extends InterfaceTest{
            @Override
            public void m() {

            }
            @Override
             public void n() {

            }
        }

-----

## 抽象类 abstract

- abstract 可以修饰类、方法。

- abstract 类，可以有抽象方法，非抽象方法。 `也可以只有非抽象方法，但失去意义`

- abstract 类，含有抽象方法的类，必须是抽象类。

- 抽象类是用来捕捉子类的通用特性的。不能被实例化，只能被子类继承。

- 特殊情况，抽象类可以被匿名内部类实例化。

- 特殊情况：


        public class AnonymousInner {
            public static void main(String[] args) {
                // 继承关系，匿名内部类 实例化 抽象类
                SuperClass superClass = new SuperClass() {
                    @Override
                    void method() {
                        System.out.print("抽象类实例化");            }
                }; // 一定要有分号，否则会报错
            }
        }

        abstract class SuperClass{
            abstract void  method();
        }

----

## 使用场景

1. 拥有一些方法，想让其中一些默认实现。      ———> 抽象类

2. 想实现多重继承，想从顶层设计几个抽象方法   ———> 接口


||抽象类|接口|
|---|:---:|:---:|
|默认方法|它可以有默认的方法实现(无参构造)|接口完全是抽象的。它根本不存在方法的实现|
|实现|子类使用`extends`关键字来继承抽象类。如果子类不是抽象类的话，它需要提供抽象类中所有声明的方法的实现。|子类使用关键字`implements`来实现接口。它需要提供接口中所有声明的方法的实现|
|构造器|`抽象类可以有构造器`|`接口不能有构造器`|
|与正常Java类的区别|除了你不能实例化抽象类之外，它和普通Java类没有任何区别|接口是完全不同的类型|
|访问修饰符|抽象方法可以有public、protected和default这些修饰符|接口方法默认修饰符是public。你不可以使用其它修饰符。|
|`main方法`|抽象方法可以有main方法并且我们可以运行它|接口没有main方法，因此我们不能运行它。|
|多继承|抽象方法可以继承一个类和实现多个接口|接口只可以继承一个或多个其它接口|
|效率|比接口效率高|接口是稍微有点慢的，因为它需要时间去寻找在类中实现的方法。|
|添加新方法|如果你往抽象类中添加新的方法，你可以给它提供默认的实现。因此你不需要改变你现在的代码。|如果你往接口中添加方法，那么你必须改变实现该接口的类。|