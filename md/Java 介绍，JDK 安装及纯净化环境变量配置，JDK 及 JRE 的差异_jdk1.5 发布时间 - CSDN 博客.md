> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/123151607?spm=1001.2014.3001.5502)

#### 文章目录

*   *   *   *   [1. Java 介绍](#1_Java_1)
            *   *   [1.1 Java 历史](#11_Java_3)
                *   [1.2 Java 语言特征](#12_Java_14)
                *   [1.3 JDK 安装包获取和安装过程](#13_JDK_21)
                *   [1.4 JDK 和 JRE 名词解释](#14_JDK__JRE__39)
                *   [1.5 JDK 安装目录结构](#15_JDK__52)
                *   [1.6 JDK 环境变量配置](#16_JDK__73)
                *   *   [1.6.1 JAVA_HOME 配置](#161_JAVA_HOME__83)
                    *   [1.6.2 CLASS_PATH 配置](#162_CLASS_PATH__96)
                    *   [1.6.3 系统变量 Path 修改](#163__Path__111)
                    *   [1.6.4 测试环境变量配置情况](#164__125)

##### 1. Java 介绍

###### 1.1 Java 历史

```
Java元年 1995年
1996年1月发布 JDK1.0
2004年 JDK1.5 发布
2013年 ~ 2017年 JDK1.8 更新
2022年 目前JDK最新版本 17
	长期版本 JDK 8 11 17

```

###### 1.2 Java 语言特征

```
1. 较为简单，没有指针概念，内存管理方便(GC)
2. Java语言一处编译，处处使用！！！ JVM Java虚拟机

```

###### 1.3 JDK 安装包获取和安装过程

```
1. 所有软件都要官网获取！！！
2. 安装路径没有中文！！！
3. 安装路径不要在 C 盘！！！

```

![image](https://github.com/user-attachments/assets/0c497536-3419-4851-8ed4-09fbc4f974e0)

![image](https://github.com/user-attachments/assets/15715312-9c6d-4896-9bc9-02a7135cad64)

![image](https://github.com/user-attachments/assets/058861f3-4ad9-4ffb-8df8-21ad46016944)

![image](https://github.com/user-attachments/assets/f4af9edc-f07a-4f1c-9450-f869307c74f6)

![image](https://github.com/user-attachments/assets/9cce6f64-2dc4-4814-a6a2-c3a72286f9eb)


###### 1.4 JDK 和 JRE 名词解释

```
JDK:
	Java 开发工具集
	Java Development Kits
	JDK ==> JRE + Java开发工具
		关注的工具:	 javac java javap javadoc
JRE:
	Java 运行环境
	Java Runtime Environment
	JRE ==> JVM(Java虚拟机) + 虚拟机执行所需必要资源

```

###### 1.5 JDK 安装目录结构

![image](https://github.com/user-attachments/assets/2d56d304-f777-4ef0-9843-41c40312509b)


```
bin:
	binary (二进制文件) 目录，都是 Java 工具相关的可执行文件或者一些辅助内容。核心工具:
		java javac javap javadoc

include:
	计算机提供给 Java 使用硬件资源，系统资源的接口文件。都是使用 C 语言完成的。
   
jre:
	Java 运行环境，提供 Java 程序和 Java 开发工具运行的必要环境。

lib:
	Library JVM虚拟机执行所需的核心文件内容。

src.zip：
	Java 源代码！！！

```

###### 1.6 JDK 环境变量配置

```
使用 Java 开发工具更为方便

我的电脑 --> 空白处鼠标右键 --> 属性
	弹出系统详情页(CPU, 内存, 系统版本信息)
	Windows 10 左侧边栏 找到<<高级系统设置>> --> 环境变量

```

###### 1.6.1 JAVA_HOME 配置

```
明确当前 JDK 安装的根目录在哪里。

JAVA_HOME 配置
选择新建：
	变量名: JAVA_HOME
	变量值: D:\Program Files\Java\jdk1.8.0_241 [自己的安装路径]

```

![image](https://github.com/user-attachments/assets/7bfd97fd-a553-4368-b516-123965ab6d39)


###### 1.6.2 CLASS_PATH 配置

```
解决 JDK1.6 版本 JDK工具无法找到问题，在JDK1.7以上版本可以考虑不配置此项，建议配置CLASS_PATH

CLASS_PATH 配置
选择新建:
	变量名: CLASS_PATH
	变量值: .;%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar
【注意】
	从 . 开始复制，保证在变量值中，没有任何的空格

```
![image](https://github.com/user-attachments/assets/16525f3f-2454-4723-aef3-356bc97249e7)


###### 1.6.3 系统变量 Path 修改

```
修改Path路径
修改内容:
	在变量值末尾添加
	【注意】确定当前原始Path末尾是否有分号，如果没有添加一个英文分号
	%JAVA_HOME%\bin;%JAVA_HOME%\jre\bin;

```

![image](https://github.com/user-attachments/assets/1d6e1c2a-f5b1-4230-afcb-404fd03fff63)

![image](https://github.com/user-attachments/assets/c16b49bf-8096-4c03-92b5-e651e858be23)


###### 1.6.4 测试环境变量配置情况

```
打开命令提示符，测试 java 和 javac

```

![image](https://github.com/user-attachments/assets/3060af7d-d3ce-4fd4-a804-9a4c51e6b2ed)


![image](https://github.com/user-attachments/assets/8af13d0b-1c92-4dd8-996c-78063dfcba80)
