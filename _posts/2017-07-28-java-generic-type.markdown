---
layout:     post
title:      "Java Generic Types"
subtitle:   "泛型简介"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 泛型
    - 类型安全
    - 类型检查
    - 简化代码
---

### Generic Types 泛型

- Since Java JDK 5

- 泛型，即泛化的类型

开篇之初，曾提到过基本数据类型、引用数据类型还有基本数据类型的自动拆箱和装箱。
其中提到过强转，包括精度损失问题。

仔细查看 API 文档会发现，Java 一切类的向上类最终都能追溯到一个父类，即`Object`类。
也就是说，所有的类都可以向上转为 Object 类。

但是如果不是向上转，而是不同类型之间转换呢？

所以 Java 自 JDK 5 以后引入了`Generic Types` 泛型的概念。

下边来看一段别人写好的代码：

例：

            假如我们现在要定义一个类来表示坐标，要求坐标的数据类型可以是整数、小数和字符串，例如：
            x = 10、y = 10
            x = 12.88、y = 129.65
            x = "东京180度"、y = "北纬210度"

            针对不同的数据类型，除了借助方法重载，还可以借助自动装箱和向上转型。
            我们知道，基本数据类型可以自动装箱，被转换成对应的包装类；
            Object 是所有类的祖先类，任何一个类的实例都可以向上转型为 Object 类型，例如：
            int --> Integer --> Object
            double -->Double --> Object
            String --> Object

            这样，只需要定义一个方法，就可以接收所有类型的数据。请看下面的代码：
            public class Demo {
                public static void main(String[] args){
                    Point p = new Point();
                    p.setX(10);  // int -> Integer -> Object
                    p.setY(20);
                    int x = (Integer)p.getX();  // 必须向下转型
                    int y = (Integer)p.getY();
                    System.out.println("This point is：" + x + ", " + y);

                    p.setX(25.4);  // double -> Integer -> Object
                    p.setY("东京180度");
                    double m = (Double)p.getX();  // 必须向下转型
                    double n = (Double)p.getY();  // 运行期间抛出异常
                    System.out.println("This point is：" + m + ", " + n);
                }
            }
            class Point{
                Object x = 0;
                Object y = 0;
                public Object getX() {
                    return x;
                }
                public void setX(Object x) {
                    this.x = x;
                }
                public Object getY() {
                    return y;
                }
                public void setY(Object y) {
                    this.y = y;
                }
            }


上面的代码中，生成坐标时不会有任何问题，但是取出坐标时，要向下转型，
在Java多态对象的类型转换一文中我们讲到，向下转型存在着风险，
而且编译期间不容易发现，只有在运行期间才会抛出异常，
所以要尽量避免使用向下转型。运行上面的代码，第12行会抛出 java.lang.ClassCastException 异常。

那么，有没有更好的办法，既可以不使用重载（有重复代码），又能把风险降到最低呢？
有，可以使用泛型类(Java Class)，它可以接受任意类型的数据。所谓“泛型”，就是“宽泛的数据类型”，任意的数据类型。
更改上面的代码，使用泛型类：

            public class Demo {
                public static void main(String[] args){
                    // 实例化泛型类
                    Point<Integer, Integer> p1 = new Point<Integer, Integer>();
                    p1.setX(10);
                    p1.setY(20);
                    int x = p1.getX();
                    int y = p1.getY();
                    System.out.println("This point is：" + x + ", " + y);

                    Point<Double, String> p2 = new Point<Double, String>();
                    p2.setX(25.4);
                    p2.setY("东京180度");
                    double m = p2.getX();
                    String n = p2.getY();
                    System.out.println("This point is：" + m + ", " + n);
                }
            }
            // 定义泛型类
            class Point<T1, T2>{
                T1 x;
                T2 y;
                public T1 getX() {
                    return x;
                }
                public void setX(T1 x) {
                    this.x = x;
                }
                public T2 getY() {
                    return y;
                }
                public void setY(T2 y) {
                    this.y = y;
                }
            }

            运行结果：
            This point is：10, 20
            This point is：25.4, 东京180度


- 这既是泛型的好处。

### 泛型定义

- class(interface) + 类名（接口名）+ < 类型参数列表 extends / super 类

  型 & 类型 & ...> {...}

- 常用泛型参数命名

    - E 元素

    - K Key

    - V Value

    - N Number

    - T Type

    - .eg

    是不是看到了 K、V ，对 Map 内的 K、V 就是泛型

- 可以定义有界类型

    - 比如：在定义泛型 T 时，扩展了 Number, ID 就被定义了一个边界条件

     `public interface GenericDemo < ID extends Number>`

### 泛型作用

- 类型安全，附加了类型检车，避免强制类型转换出现 ClassCastException

- 简化代码，优化结构，提高代码复用率




