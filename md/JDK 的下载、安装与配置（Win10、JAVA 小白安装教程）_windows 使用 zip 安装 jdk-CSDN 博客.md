> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/119786726?spm=1001.2014.3001.5502)

#### 文章目录

*   *   [JDK 的下载、安装与配置](#JDK_2)
    *   *   [JDK 的下载](#JDK_6)
        *   [JDK 的安装](#JDK_34)
        *   [JDK 运行环境变量配置](#JDK_66)
        *   [如何确定 JAVA 的环境配置成功](#JAVA_116)

### JDK 的下载、安装与配置

【从 [Oracle](https://so.csdn.net/so/search?q=Oracle&spm=1001.2101.3001.7020) 官网下载 JDK，下载—> 安装—> 配置】

#### JDK 的下载

​ **（Oracle 官网下载 JDK 可能需要登录 Oracle 账号才能下载，没有账号可以跟着网站注册步骤新注册一个，软件是免费下载的。）**

1.  JDK 下载地址：[https://www.oracle.com/downloads/](https://www.oracle.com/downloads/)
    
2.  进入 Oracle 网页，向下找到 Developer Downloads 单击 Java：
    
    ![image](https://github.com/user-attachments/assets/9d442ba2-128a-4adc-ba25-68b5530064c1)

    
    3.  单击 [Java (JDK) for Developers](https://www.oracle.com/java/technologies/javase-downloads.html)
    
    ![image](https://github.com/user-attachments/assets/61078e32-a780-48a1-8804-bfe891dee66a)

    
    4.  跳转新页面后，找到自己需要的 JDK 版本 (学习用途建议使用 Java SE 8 版本，该版本比较稳定适合初学者)
    
    ![image](https://github.com/user-attachments/assets/0b5654a9-2c26-4aa2-9a0e-98a8725b1ef4)

    
    5.  点击 [JDK Dowload](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)
    
    我的系统是 Windows10 的 64 位所以选择 [jdk-8u301-windows-x64-demos.zip](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html#license-lightbox) 压缩版相对于程序来说，压缩版放在指定目录下，直接解压就能使用了。
    
    ![image](https://github.com/user-attachments/assets/a618f981-12fc-499a-9c06-b409db474376)

    

#### JDK 的安装

**（如果下载的 JDK 安装程序安装步骤如下）**

1.  找到下载好的程序，双击运行安装包
    
    ![image](https://github.com/user-attachments/assets/8184c180-32e1-44a6-a630-48d6cdfe0ca6)

    
2.  下一步，选择安装所有组件并更改安装路径
    
    (1)、这里显示要安装的三个组件：
    
   ![image](https://github.com/user-attachments/assets/fe32a0dc-0b12-4220-9829-36e459fd624b)

    
    (2)、取消安装独立的 JRE，JDK 中已经包含 JRE，这里可以选择取消安装独立的 JRE：
    
    ![image](https://github.com/user-attachments/assets/1b667158-fa48-46bd-ac7e-83c10df10556)


    
    (3)、更改 JDK 的安装路径（具体安装路径自己选择，以方便，好找为准，改了安装路径后记住安装路径，后面配置环境变量时还要用到）：
    
    ![image](https://github.com/user-attachments/assets/c816928e-7e3b-4ee2-b7dc-ef213e8dd8b3)


    
3.  下一步，根据提示安装完成
    
    ![image](https://github.com/user-attachments/assets/7c275ade-8dd4-4d95-a1d2-68e799ffc9e1)

    

#### JDK 运行环境变量配置

**1、桌面计算机右键–属性–高级系统设置–环境变量 (控制面板–系统–高级系统设置–环境变量)**

![image](https://github.com/user-attachments/assets/422f1246-d84c-4041-b059-2c9ce22826d2)


![image](https://github.com/user-attachments/assets/48a66bc2-c4cb-45bf-9d4c-a6e110d285b6)


![image](https://github.com/user-attachments/assets/dc5eecdb-70b8-4ecb-ae52-5df083bcc209)


**2、忽略用户变量，关注系统变量**

![image](https://github.com/user-attachments/assets/e91f3137-3c7d-42e0-9410-a4ec03437805)


**3、点击 “新建”，新建系统变量 JAVA_HOME，值为 JDK 安装根目录**

![image](https://github.com/user-attachments/assets/549b29a3-ae71-470d-a1b8-e777cf067565)


**4、编辑 PATH 变量，将刚刚新建的 JAVA_HOME 变量加上 bin 目录设置到 PATH 中**【 %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin; 】

![image](https://github.com/user-attachments/assets/3b7f6dd9-faf5-414d-9258-7f84c67054cd)


![image](https://github.com/user-attachments/assets/dfd6b715-c6ae-4a0f-9af0-6b089a358498)

**5、为方便保险**，在系统变量中查找 Path，双击之后打开 “编辑环境变量”，点击新建，你所下载的 JDK 的目录下 bin 所在路径复制进去后保存

![image](https://github.com/user-attachments/assets/6dc14f61-4ec1-4285-85db-7a66dd5a3236)


以我的为例：D:\Program Files\Java\jdk1.8.0_251\bin

**注意设置时不要找错位置和 bin 的地址**

![image](https://github.com/user-attachments/assets/1900ee94-03f3-4bea-bce4-1336114cb1c0)


#### 如何确定 JAVA 的环境配置成功

Win+R 调出运行框，输入 cmd 运行调出命令窗，输入 javac 回车运行，编译器未报错即为配置成功

![image](https://github.com/user-attachments/assets/400559ff-731d-4d01-ac1d-c132ed3a9901)
