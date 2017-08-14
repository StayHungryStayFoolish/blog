---
layout:     post
title:      "Java Reflect"
subtitle:   "反射机制"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Reflect
    - 反射机制
---

### Reflect 反射机制

`Java反射是Java被视为动态（或准动态）语言的一个关键性质。`

这个机制允许程序在运行时透过 `Reflection` 取得任何一个已知名称的class的内部信息，

包括其 `modifiers`（public, static 等）、`constructors` 、`superclass`（例如Object）、实现之`interfaces`（例如Cloneable），
也包括 `fields` 和 `methods` 的所有信息，并可于运行时改变 `fields` 内容或唤起 `methods` 。

Java反射机制允许程序在运行时加载、探知、使用编译期间完全未知的classes。

换言之，Java可以加载一个运行时才得知名称的class，获得其完整结构。


### Fields 类

- getFields() 获取当前 `非 private` 域

- getDeclaredFields() 获得所有域 包括 `private`

### Methods 类

- getMethods()

- getDeclaredMethods()

### Constructors 类

- getConstructors()

- getDeclaredConstructors()

### Modifiers 类

- getModifiers() 获取修饰符


### 使用反射机制获取 java.lang.String 类的所有域、构造方法、成员方法

- 区别:

    get 方法 不带 Declared 时，只能获取当前 除 private 的 域、构造器、方法

    带 Declared 时，可以获得 private 的。

    设置访问权限 setAccessible(); true 时，只对 private 有效



### 例：

- Demo:

    ```java
         // super class Animals
         class Animals {
             public int age; // It's public
             private double weight;

             public Animals() {
             }

             public Animals(int age, double weight) {
                 this.age = age;
                 this.weight = weight;
             }

             public int sleep(int hours) {
                 return hours;
             }

             public void eat(String food) {
                 System.out.println("eating " + food);
             }

             // This's a private method!
             private void killHuman() {
                 System.out.println("killed a poor guy...");
             }

             // getters and setters
         }


         // sub class Human
          public final class Human extends Animals {
              public String name; // It's public!
              private boolean married;

              Human() { // It's package-private!
              }

              public Human(int age, double weight, String name, boolean married) {
                  super(age, weight);
                  this.name = name;
                  this.married = married;
              }

              @Override
              public void eat(String food) {
                  System.out.println(name + " is now eating " + food);
              }

              public void study(String course) {
                  System.out.println(name + " is now studying " + course);
              }

              // This's a private method!
              private void killAnimals(String animal) {
                  System.out.println(name + " is now killing " + animal);
              }

              // getters and setters
          }
    ```


- Fields，获取域

    ```java
        lass HumanTest {
          public static void main(String[] args) {
              Human human = new Human();
              Field[] fields = human.getClass().getFields();
              System.out.println("--- getFields() ---");
              for (Field field : fields) {
                  System.out.println(field.getName());
              }
              Field[] declaredFields = human.getClass().getDeclaredFields();
              System.out.println("--- getDeclaredFields() ---");
              for (Field declaredField : declaredFields) {
                  System.out.println(declaredField.getName());
              }
          }
        }

        /*
        --- getFields() ---
        name
        age
        --- getDeclaredFields() ---
        name
        married
        */
    ```

- Methods 获取方法

   ```java
        class HumanTest {
          public static void main(String[] args) {
              Human human = new Human();
              Method[] methods = human.getClass().getMethods();
              System.out.println("--- getMethods ---");
              for (Method method : methods) {
                  System.out.println(method);
              }
              Method[] declaredMethods = human.getClass().getDeclaredMethods();
              System.out.println("--- getDeclaredMethods ---");
              for (Method declaredMethod : declaredMethods) {
                  System.out.println(declaredMethod);
              }
          }
        }

        /*
        --- getMethods ---
        public int java1702.javase.regex.Human.sleep(int)
        public void java1702.javase.regex.Human.study(java.lang.String)
        public void java1702.javase.regex.Human.eat(java.lang.String)
        public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
        public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
        public final void java.lang.Object.wait() throws java.lang.InterruptedException
        public boolean java.lang.Object.equals(java.lang.Object)
        public java.lang.String java.lang.Object.toString()
        public native int java.lang.Object.hashCode()
        public final native java.lang.Class java.lang.Object.getClass()
        public final native void java.lang.Object.notify()
        public final native void java.lang.Object.notifyAll()
        --- getDeclaredMethods ---
        public int java1702.javase.regex.Human.sleep(int)
        public void java1702.javase.regex.Human.study(java.lang.String)
        private void java1702.javase.regex.Human.killAnimals(java.lang.String)
        public void java1702.javase.regex.Human.eat(java.lang.String)
        */
   ```

- Constructors 获取构造器

    ```java
       class HumanTest {
         public static void main(String[] args) {
             Human human = new Human();
             Constructor[] constructors = human.getClass().getConstructors();
             System.out.println("--- getConstructors ---");
             for (Constructor constructor : constructors) {
                 System.out.println(constructor.getName());
                 for (Parameter parameter : constructor.getParameters()) {
                     System.out.println("\t" + parameter);
                 }
             }

             Constructor[] declaredConstructors = human.getClass().getDeclaredConstructors();
             System.out.println("--- getDeclaredConstructors ---");
             for (Constructor declaredConstructor : declaredConstructors) {
                 System.out.println(declaredConstructor.getName());
                 for (Parameter parameter : declaredConstructor.getParameters()) {
                     System.out.println("\t" + parameter);
                 }
             }
         }
       }

       /*
       --- getConstructors ---
       Human
         int arg0
         double arg1
         java.lang.String arg2
         boolean arg3
       --- getDeclaredConstructors ---
       Human
       Human
         int arg0
         double arg1
         java.lang.String arg2
         boolean arg3
       */
    ```

- Modifiers 获取修饰符
