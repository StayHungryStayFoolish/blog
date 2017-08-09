---
layout:     post
title:      "Java 线程 "
subtitle:   "进程、线程"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - 进程
    - 线程
    - synchronized
---

### 进程、线程

- `进程是一个内存中运行的应用程序。一个进程中可以启动多个线程`

- `线程是指进程中的一个执行流程，一个进程中可以运行多个线程。`

`即：进程执行的是应用程序，线程是进程内部的一个执行序列`

### 线程分类

- 非守护线程（用户线程）

    - 用户自己创建的，用来运行应用程序。

- 守护线程

    - 只要当前 JVM 实例中，存在任何一个非守护线程没有结束，守护线程就不会停止工作。
        只有当最后一个非守护线程结束时，守护线程才会随着 JVM 一起结束工作。

    - 最典型应用：GC（垃圾回收期）

        - 也正是因为 GC 的机制存在，Java 不会出现内存泄漏。

### 多线程的实现

1.扩展 Thread 类

2.实现 Runnable 接口

- `一个类只能继承一个 Thread，这是 Thread 的局限，推荐使用 Runnable 接口`

- `Runnable 的好处在于`

    避免点继承的局限，一个类可以实现多个接口。

    适合资源的共享

 `Thread 是 Runnable 的接口的实现类`  public class Thread extends Object implements Runnable

### 例：

- 以售票为例

    - Thread

            class MyThread extends Thread{
                private int ticket=10;
                public void run(){
                    for(int i=0;i<20;i++){
                        if(this.ticket>0){
                        System.out.println("卖票：ticket"+this.ticket--);
                        }
                    }
                }
            };

            public class ThreadTicket {
                public static void main(String[] args) {
                    MyThread mt1=new MyThread();
                    MyThread mt2=new MyThread();
                    MyThread mt3=new MyThread();
                    mt1.start();//每个线程都各卖了10张，共卖了30张票
                    mt2.start();//但实际只有10张票，每个线程都卖自己的票
                    mt3.start();//没有达到资源共享
                }
            }

    - Runnable

            class MyThread implements Runnable{
                private int ticket=10;
                public void run(){
                    for(int i=0;i<20;i++){
                        if(this.ticket>0){
                        System.out.println("卖票：ticket"+this.ticket--);
                        }
                    }
                }
            }

            public class RunnableTicket {
                public static void main(String[] args) {
                    MyThread mt=new MyThread();
                    new Thread(mt).start();//同一个mt，但是在Thread中就不可以，如果用同一
                    new Thread(mt).start();//个实例化对象mt，就会出现异常
                    new Thread(mt).start();
                }
            };

    `虽然现在程序中有三个线程，但是一共卖了10张票，也就是说使用Runnable实现多线程可以达到资源共享目的。`

### 多线程同步 synchronized

- 为什么需要同步多线程？

    线程的同步是指让多个运行的线程在一起良好地协作，达到让多线程按要求合理地占用释放资源。我们采用Java中的同步代码块和同步方法达到这样的目的。

    例：

    ```java

        public class TwoThreadTest {
                         public static void main(String[] args) {
                               Thread th1= new MyThread1();
                               Thread th2= new MyThread2();
                               th1.start();
                               th2.start();
                        }
                 }

                 class MyThread2 extends Thread{
                         @Override
                         public void run() {
                                for( int i=0;i<10;i++)
                                      System. out.println( "thread 1 counter:"+i);
                        }
                 }

                 class MyThread1 extends Thread{
                         @Override
                         public void run() {
                                for( int i=0;i<10;i++)
                                      System. out.println( "thread 2 counter:"+i);
                        }
                 }
    ```

    `这种状态下多线程执行的结果是随机地去任意插入执行，这完全取决于JVM对于线程的调度，在很多要求定序执行的情况下，这种随机执行的状态显然是不合要求的。`

- 同步方法

    例：

    ``` java

        public class ThreadTest {
                public static void main(String[] args) {
                      MyThread thread = new MyThread();
                      Thread th1= new Thread(thread);
                      Thread th2= new Thread(thread);
                      th1.start();
                      th2.start();
               }

        }

        class MyThread implements Runnable{
                @Override
                public synchronized void run() {
                       for( int i=0;i<10;i++)
                             System. out.println(Thread. currentThread().getName()+" counter:"+i);
               }
        }

    ```

    `使用了同步方法后我们就可以控制线程独占执行体对象，这样在执行的过程中就可以使得线程将执行体上的任务一次性执行完后退出锁定状态，JVM再调度另一个线程进来一次性运行执行体内的任务。`

- synchronized关键字

    synchronized可以用来修饰方法以构成同步方法，还可以修饰对象构成同步代码块，最终的目的都是一样的：
    给要访问数据的线程添加一个规定：一次只允许一个线程访问数据。只有?当前正在访问数据”的线程结束访问之后，其他线程才允许访问这个数据