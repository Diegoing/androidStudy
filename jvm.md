# 自动内存管理

## 一：Java内存区域与内存溢出异常

### 1.运行时数据区域

* 由所有线程共享的数据区—方法区（Methed Area）、堆（Heap）、执行引擎、本地库接口
* 线程隔离的数据区—虚拟机栈（VM Stack）、本地方法栈（Native Method Stack）、程序计数器（Program Counter Register）。

### 1.1 程序计数器

* 定义：当前线程所执行的字节码的行号指示器
* 使用原因：JVM的多线程是通过**CPU时间片轮转**（线程轮流切换并分配处理器执行时间）实现的。某个线程时间片耗尽会被挂起，下次再获取到时间片的时候就要从上次执行的位置开始，就是通过程序计算器记录位置。
* 特点：
  * 每个线程有属于自己的计数器。
  * 程序计数器的只为正在执行的字节码的地址
  * 执行native本地方法时，程序计数器的值为空
  * 是唯一一个在java虚拟机规范中中没有oom的区域

### 1.2 java虚拟机栈

* 定义：每个方法被执行的时候，Java虚拟机都会同步创建一个栈帧用于存储局部变量表、操作数栈、动态链接、方法出口等信息。

### 1.3 本地方法栈

* 为虚拟机使用到本地（Native）方法服务的，和虚拟机栈发挥的作用一样

### 1.4 java堆

