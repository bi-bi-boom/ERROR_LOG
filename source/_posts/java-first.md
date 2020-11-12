---
title: 遇见 JVM 的第一印象
date: 2020-11-13 01:22:48
categories: 
- Java
tags: 
- "author: zanxinz"
---

| 术语 | 全称 | 中文 |
| :---:|  :---: | :---: |
| JDK | Java Development Kit | Java 开发工具包 |
| JRE | Java Running Environment | Java 运行环境 |
| JVM | Java Virtual Machine | Java 虚拟机器 |
| JSR | Java Specification Requests| Java 规范提案|

***

<!-- More -->

## Java 具有跨平台特性（体现在 .class 和 JVM 的关系中）

- 真正在机器上运行的是二进制码。
- 本机的的编译器把源代码（程序员写的东西）翻译成二进制码。
- 以前的编译器（比如C、C++），编译之后的代码只能在同样的平台上运行（如 Windows 编译后的内容无法在 Linux 上使用）。这就是跨平台的问题。
- Java 通过 JVM（JAVA Virtual Machine）解决跨平问题。
- JVM 负责把 .java 格式文件编译成 .class 的文件。
- **.class 是通用的**。
  - 不管机器是哪个平台的（Window、Linux或是 MAC OS），只要机器中装有 JVM，JVM 就可以把 .class 翻译成适应本机的二进制代码，然后可以直接运行。这也正是 Java 的「编译一次，到处执行。」思想的所在。
- JDK（Java Development Kit） 包含了好几个工具。
  - javac：编译器，把 .java 编译成 .class
  - java：运行工具，直接运行 .class 后缀的文件
  - jar：打包工具，把相关类文件打包成 jar 包
  - javadoc：文档生成工具，从源码中提取注释，注释需要符合规范
  - 初学者常用的是上面这几个工具，后面还有十几个，这个留到学到的时候再做展开。

## Java 是一个标准

- 像System、out、println这些名称，都是标准中所规范的名称。前人依据 JSR 标准文件，写出了一套标准的程序库（如 Java SE API 里面就包含各种标准API，以 .class 的形式）。
- 需要有人写出 System.java 编译后为 System.class，第一个程序里面写这样，我才能使用 System类（class）里面的 out 对象（object）的 print 方法（Method）。
- 而 JRE（Java Running Environment）就包含了 Java SE API 和 JVM 。
  - 运行编译好的文件（.class），只需要 JRE ，因为自己写的程序里面调用了Java SE API里的方法。而如果要自己编写源程序并且进行编译（需要用到javac），则只需要 JDK。
  
***
