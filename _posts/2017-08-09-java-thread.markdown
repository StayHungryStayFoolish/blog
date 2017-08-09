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

    1.当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码。

    2.当两个并发线程访问同一个对象object中的这个synchronized同步代码块或同步方法时，一个时间内只能有一个线程得到执行。另一个线程必须等待当前线程执行完这个代码块或同步方法以后才能执行该代码块或同步方法。

    3.然而，当一个线程访问object的一个synchronized同步代码块或同步方法时，另一个线程仍然可以访问该object中的非synchronized同步代码块或非synchronized同步方法。

    4.尤其关键的是，当一个线程访问object的一个synchronized同步代码块或同步方法时，其他线程对object中所有其它synchronized同步代码块或同步方法的访问将被阻塞。

    - 1.以下这个例子可以说明synchronized方法的这些特性，同步代码块也是一样：

      I. synchronized方法表面上它只是锁定了当前的方法本身，实际上当synchronized方法起作用的时候，整个对象的带有synchronized的方法都将被锁定，这也就是为什么当一个线程执行一个synchronized方法时，其他的线程除了不能访问当前的同步方法外还并不能访问其他的同步方法，而只能访问非synchronized方法，因为这种锁定是对象级别的。

      ```java
            public class ThreadTest {
                    public static void main(String[] args) {
                           final MyTask myTask = new MyTask();
                          Thread thread1 = new Thread( new Runnable() {
                                  public void run() {
                                       myTask.doTask1();
                                 }
                          });
                          Thread thread2 = new Thread( new Runnable() {
                                  public void run() {
                                       myTask.doTask2();
                                 }
                          });
                          thread1.start();
                          thread2.start();
                   }
            }

            class MyTask{
                    public synchronized void doTask1() {
                           for ( int i = 0; i < 5; i++) {
                                 System. out.println( "1 This is real Tasking "+i);
                          }
                   }
                    public void doTask2() {
                           for ( int i = 0; i < 5; i++) {
                                 System. out.println( "2 This is real Tasking "+i);
                          }
                   }
            }
      ```

      II.如使在静态方法中用synchronized时，因为这个方法就不是仅属于某个对象而是属于整个类的了，所以一旦一个线程进入了这个代码块就会将这个类的所有对象的所有synchronized方法或synchronized同步代码块锁定，其他的线程就没有办法访问所有这些对象的synchronized方法和synchronized代码块（注意其他线程还是仍然能访问这些对象的非synchronized方法和synchronized代码块的），因此这种锁定是class级别的。

      ```java
            public class FormalThreadClass {
                    public static void main(String[] args) {
                          MyTask myTask1 = new MyTask();
                          MyTask myTask2 = new MyTask();
                          Thread thread1 = new Thread( new MyRunnable(myTask1));
                          Thread thread2 = new Thread( new MyRunnable(myTask2));
                          thread1.start();
                          thread2.start();
                   }
            }

            class MyRunnable implements Runnable {
                   MyTask myTask;
                    public MyRunnable(MyTask myTask) {
                           this. myTask = myTask;
                   }
                    @Override
                    public void run() {
                          MyTask. doTask();
                   }
            }

            class MyTask {
                    public static synchronized void doTask() {
                           for ( int i = 0; i < 5; i++) {
                                 System. out.println(Thread. currentThread().getName()+" running "+i);
                          }
                   }
            }
      ```

    - 2.synchronized同步代码块是对一个对象作为参数进行锁定。

     I. 如在使用synchronized(this)时，一旦一个线程进入了这个代码块就会将整个对象的所有synchronized方法或synchronized同步代码块锁定，其他的线程就没有办法访问这个对象的synchronized方法和synchronized代码块（注意其他线程还是仍然能访问这个对象的非synchronized方法和synchronized代码块的）。

     ```java
        public class ThreadTest {
                public static void main(String[] args) {
                       final MyTask myTask = new MyTask();
                      Thread thread1 = new Thread( new Runnable() {
                              public void run() {
                                   myTask.doTask1();
                             }
                      });
                      Thread thread2 = new Thread( new Runnable() {
                              public void run() {
                                   myTask.doTask2();
                             }
                      });
                      thread1.start();
                      thread2.start();
               }
        }

        class MyTask {
                public void doTask1() {

                       synchronized (this) {
                              for ( int i = 0; i < 5; i++) {
                                   System. out.println( "1 is running");
                             }
                      }

               }

                public void doTask2() {
                       for ( int i = 0; i < 5; i++) {
                             System. out.println( "2 is running");
                      }
               }
        }
     ```