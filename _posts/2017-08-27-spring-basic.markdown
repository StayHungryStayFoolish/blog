---
layout:     post
title:      "Spring Framework --- Spring"
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

    ``