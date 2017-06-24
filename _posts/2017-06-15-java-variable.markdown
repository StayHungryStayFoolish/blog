---
layout:     post
title:      "Java 变量作用域范围"
subtitle:   ""
iframe:     ""
navcolor:   "invert"
date:       2017-06-15
author:     "Bonismo"
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 域
    - 静态变量
    - 成员变量
---

### Java 变量类型

- 域 也叫成员变量，属于某个对象的属性，必须创建实例对象，才会被 JVM 分配空间，这个实例变量才可以被使用。

- 静态变量是类级别变量[

- 局部变量 是方法内的变量


### 所有变量在使用前都必须声明

        int a, b, c; // 声明三个 int 型整数：a,b,c

        int d = 3, e = 4 ,f = 5; // 声明三个整数，并赋予初值

        byte g = 22 ; // 声明并初始化 g

        String s = “monaco” ; // 声明并初始化字符串 s

        double pi = 3.1314 // 声明双精度浮点型

        char x = ‘x’ ; // 声明变量 x 的值是字符 ‘x’ ，注意是 单引号 ‘’ char 字符类型只能在单引号内放一个字母、汉字

### 域 成员变量

- 声明在一个类中，但在方法、构造方法、语句块{ }之外

- 当一个对象被实例化后，值就会跟着确定

- 在对象创建时创建，对象被销毁时销毁。`跟随对象的状态`

- 至少被一个方法、构造方法、语句块引用

- 域可以声明在使用前或使用后 `因为在类中，所以在哪里声明，都可以被使用`

- 访问限制修饰符可以修饰 `public | protected | private | default`

- 域对类中的方法、构造方法。语句块可以见。通过使用访问修饰符使实例变量对子类可以见。 `一般用 private`

- 域具有默认值。如果不赋值，则 数值型默认值为 0，布尔默认值为 false,引用型为 null。

#### 例：

        public class Employee {
            // 这个实例变量对子类可见
            public String name;
            // 私有变量，仅在该类可见，用来隐藏实现细节，保护数据
            private double salary;
            // 在构造器中对name赋值，并重新定义了形参
            public Employee (String empName){
                name = empName;
            }
            // 设定salary的值，并重新定义了形参
            public void setSalary(double empSal){
                salary = empSal;
            }
            // 方法块，打印信息  ，方法功能调用入口  [‘sæləri] 薪水，加薪
            public void printEmp(){
                System.out.println("名字 : " + name );
                System.out.println("薪水 : " + salary);
            }
            // 程序入口
            public static void main(String args[]){
                // 输出方法块，首先要构造器必须用 new 来实现，并传参
                Employee empOne = new Employee("RUNOOB");
                // 调用 set 方法 ，private 修饰的变量，只能在所在类的外部 用 set 获得
                empOne.setSalary(1000);
                // 已经 new 新对象，所有可以调用方法块，输出
                empOne.printEmp();
            }
        }

        运行结果：
        名字 : RUNOOB
        薪水 : 1000.0

### 静态变量

 - 静态变量被该类所有对象共有，属于类的，

 - 不需要实例化就可以直接调用。可以在静态方法中调用，

 - 也可以在普通方法中被调用，但静态方法中不能存在实例变量，也不能调用实例方法。

 - 普通方法中可以调用静态变量、静态方法。

 静态方法调用：类名.静态方法名

 - 静态变量也成为类级别变量，必须在构造方法`构造函数]`语句块`非构造函数、普通方法`之外

 - 静态变量在类加载时创建，只有一份拷贝 copy ，分配空间，程序结束时释放。便随类。

 - 默认值跟实例变量相似。数值型变量默认是 0，布尔型默认是 false,引用型默认是 null。
   静态变量值可以在声明时知道，也可以在构造方法知道，也可以在静态语句块中初始化。

- 例：

        // 简单方式：
        public class Employee{
            //salary 是静态的私有变量
            private static double salary;
            //DEPARTMENT 是一个常量
            public static final String DEPARTMENT = "开发人员”;
            // 程序入口
            public static void main(Stringargs[]){
            // 直接程序入口，设置静态私有变量（不再需要在类中，构造 set方法，然后还要有 方法块输出，然后在程序入口，new 实例，再调用）
            salary = 10000;
            System.out.println(DEPARTMENT +  "平均工资:” + salary);
            }
        }


        // 复杂方式：
        public class Emplovee1{
            // 静态变量未赋值
            private static double salary;
            public static void setSalary(double salary1){
                salary = salary1;
            }
            void s(){
                System.out.println(" " + salary);
            }
            public static void main(String []args){
                // 必须 new 实例化，才可以给静态变量传值
                Emplovee1 emplovee1 = new Emplovee1();
                emplovee1.setSalary(1000);
                emplovee1.s();
            }
        }

### 局部变量

- 局部变量声明在方法块、构造方法块或语句块

- 局部变量只声明，不能使用，必须在使用之前进行赋值。

- 局部变量必须赋值，否则不能使用。`没有默认初始化值`。

- 只作用在所属区域，即 { } 内。

- 例：

        public class Test{
            public void dogAge(){
            // 局部变量必须赋值，不能初始化
            int age = 0;
             age = age + 7;
             System.out.println(“小狗年龄是：” + age)
            }

            public static void mani(String []args){
            Test test = new Test();
             test.dogAge();
            }
        }

        如果局部变量初始化， int age;  age = age + 7; 会提示运行错误
        Test.java:4:variable number might not have been initialized
        age = age + 7;

-----

### 三者之间的区别：

`局部变量`，`成员变量`，`静态变量`的定义，作用域或声明周期，访问权限，默认值，内存的分配.

||局部变量【方法体`内`】|成员变量（实例变量）【方法体`外`】|静态变量（`类级别变量`）|
|---|:---:|:---:|:---:|
|`声明或定义`|声明在方法体（方法，构造方法或代码块）内部，也就是`{ }`中|声明在类里面，一般就是类所定义的变量`描述类的属性`，这个容易理解。分为默认初始化和显示初始化，在方法体（方法，构造方法或代码块）之外|在类中以static关键字声明，在方法体（方法，构造方法或代码块）`之外`|
|`作用域或生命周期`|方法或块被执行时创建，执行完`{ }`就释放|成员变量创建时创建，对象销毁时释放|无论一个类创建了多少个对象，类只拥有类变量的一份拷贝，程序开始时创建，结束时释放|
|`访问权限`|`不能用修饰符`，方法体中可见|有修饰符，public修饰子类可见，private 修饰本类可见|有修饰符，但经常被修饰为public/private/final和static类型的常量|
|`初始化值或默认值`|`没有默认值`，必须初始化赋值|有默认值，引用类型为null，其他为基本数据类型默认值|有默认值，引用类型为null，其他为基本数据类型默认值|
|`内存分配`|局部变量在所在方法调用时，存在栈内存空间中|成员变量在所在类被实例化后，存在堆内存中|静态变量存放在内存的静态存储区|

- 注：`Java 数据类型的所有声明，只要是在方法内、构造器内，都必须初始化才可以输出值。不然会报编译错误。极端例子：没有初始化，但是不使用，不会报编译错误。`

-----

### 例：

- 局部变量

      public class TestPeople {
          public void people() {
               int age = 0;
            //int age；  //如果声明不初始化
              age = age + 18; //这里就会报错要initialized
              System.out.println("age=" + age);
          }
      }

      不能被输出，方法被调用 System.out.println(); 才会输出

- 成员变量，静态变量实例：

        public class TestPeople {
             public String name; //成员变量 ---- 初始化
            public String name = “张三”; // 成员变量 ---- 显示初始化
            private int age;//私有成员变量
            public static String sex="男"; //静态变量
            private static final String BIRTHDAY="xx月xx日"; //常量
        }

        注：静态变量可以用过 类的名字调用：
        语句语法： Class_name.variable_name
        TestPeople.sex