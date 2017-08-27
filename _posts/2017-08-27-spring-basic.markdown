---
layout:     post
title:      "Spring Framework --- Spring 引言"
subtitle:   "Spring Basic"
iframe:     ""
navcolor:   "invert"
author:     "Bonismo"
date:       2017-07-28
header-img: "img/java/hello-world-banner.jpg"
header-mask: 0.3
catalog:    true
tags:
    - Spring
    - IOC
    - AOP
---

### 强耦合

- 高层应用类 依赖于 底层模块类

- 底层模块类 控制 高层应用类

- 底层有改变，高层应用类需要大量更改代码

- `弊端：不适用大规模开发`

- 例：

    `底层模块应用类`

    ```java
        public class UsbWriter {
            public void saveToUsb(){
                System.out.println("save to USB");
            }
        }

        public class FloppyWriter {
            public void writeToFloppy(){
                System.out.println("save to floppy");
            }
        }
    ```

    `高层应用类`

    ```java
        public class Business {
            private FloppyWriter floppyWriter = new FloppyWriter();
            private UsbWriter usbWriter = new UsbWriter();

            // 构建 类 作为当前 类 的域时，创建域的实例，可以使用 有参构造
            //    public Business(FloppyWriter floppyWriter) {
            //        this.floppyWriter = floppyWriter;
            //    }

                // 构建 类 作为当前 类 的域时，创建域的实例，也可以使用 当前类的 set 方法
            //    public void setFloppyWriter(FloppyWriter floppyWriter) {
            //        this.floppyWriter = floppyWriter;
            //    }


            //    public void setUsbWriter(UsbWriter usbWriter) {
            //        this.usbWriter = usbWriter;
            //    }
            //
            //    public Business(UsbWriter usbWriter) {
            //        this.usbWriter = usbWriter;
            //    }
            public void saveData() {
                    floppyWriter.writeToFloppy();
            //        usbWriter.saveToUsb();
                }
            }
    ```

    `强耦合下`

    ```java
        public class BusinessTest {
            public static void main(String[] args) {
        //          利用有参构造调用方法
        //        Business business1 = new Business(new FloppyWriter());
        //        Business business2 = new Business(new UsbWriter());
        //        business1.saveData();
        //        business2.saveData();

                // 无参构造，为了下一步使用  set 方法生成 实例
                Business business = new Business();
                // set 方法生成实例
        //        business.setFloppyWriter(new FloppyWriter());
                // 调用方法
                business.saveData();
            }
        }

    ```

- `上边示例代码很乱，因为根据实际需求，需要不停的更改底层模块代码，从而导致高层应用类的代码也要跟着改变`

### 松散耦合

- 高层应用类 不依赖 底层模块类

- 底层模块类 不控制 高层应用类

- 底层由改变，高层应用类不需要更代码

- 例：

    `创建一个接口，抽象底层应用类方法`

    ```java
       public interface DeviceWriter {
           void writeToDevice();
       }
    ```

    `底层接口`

    ```java
        public class UsbWriter implements DeviceWriter {

            @Override
            public void writeToDevice() {
                System.out.println("write to Usb...");
            }
        }


        public class FloppyWriter implements DeviceWriter {

            @Override
            public void writeToDevice() {
                System.out.println("write to Floppy...");
            }
        }

    ```

    `松散耦合`

    ```java
        public class Business {
            // 接口可以作为 域
            private DeviceWriter deviceWriter;

            public void setDeviceWriter(DeviceWriter deviceWriter) {
                this.deviceWriter = deviceWriter;
            }

            public void saveData() {
                deviceWriter.writeToDevice();
            }
        }

    ```

    `应用类`

    ```java
        public class BusinessTest {
            public static void main(String[] args) {

                // 构建无参，set 方法，构建类的实例，通过类的实例调用方法
                Business business = new Business();
                // 如果更改需求，只需要更改 setDeviceWriter()内参数即可
                business.setDeviceWriter(new FloppyWriter());
                business.saveData();
            }
        }

    ```

- `注：松散耦合下，只需更改一行代码即可`

### 利用反射机制，不更改代码

- 使用属性文件注入

- 更改需求，只需要修改属性文件即可

- 例：

    `新建一个 config.properties` 文件 `[` K - V 结构，存储读取数据`]`
    `className 即 FQN 相对路径`

     ```java
        className = packageName.FloppyWriter
        methodName = writeToFloppy

        #className = packageName.UsbWriter
        #methodName = saveToUsb
     ```

    `底层模块`

    ```java
        public class FloppyWriter {
            public void writeToFloppy(){
                System.out.println("save to floppy");
            }
        }

        public class UsbWriter {
            public void saveToUsb(){
                System.out.println("save to USB");
            }
        }
    ```

    `利用反射机制，构建一个高层应用框架，比松散耦合，更适用与复杂场景应用`
    `Absolute_Path 是绝对路径地址`

    ```java
        public class BusinessSevice {
            private static final String CONFIG_BUSINESS = "Absolute_Path/config.properties";

            public void saveData() {

                // 实例化 Properties 类，保存属性持久的类
                Properties properties = new Properties();
                try {
                    // 从输入流中加载属性集，注意传参方法，new FileInputStream(属性地址FQN);
                    properties.load(new FileInputStream(CONFIG_BUSINESS));
                    // 获得 类 的名字，返回的是 String 类型 , 传参的 "className"，是 config 配置文件 类的路经地址
                    String className = properties.getProperty("className");
                    // 获得 方法 的名字，返回的是 String 类型
                    String methodName = properties.getProperty("methodName");

                    // 用 Class,反射机制获得 当前 类 ，传入 类的路径 className
                    Class clazz = Class.forName(className);

                    // 利用 类的实例化，获取当前  类的方法
                    Method method = clazz.getDeclaredMethod(methodName);

                    // 利用 类的实例化，获取当前  类的构造方法，主要是为了 invoke(); 传参使用
                    Constructor constructor = clazz.getDeclaredConstructor();

                    // 调用当前 类的方法 invoke(); 传入的参数，必须是构造器的实例化 即 constructor.newInstance()
                    // invoke();对带有指定参数的指定对象调用由此 Method 对象表示的底层方法。
                    method.invoke(constructor.newInstance());

                } catch (IOException | ClassNotFoundException | NoSuchMethodException | IllegalAccessException | InstantiationException | InvocationTargetException e) {
                    e.printStackTrace();
                }
            }
        }
    ```