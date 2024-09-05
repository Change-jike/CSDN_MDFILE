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
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/d5eb83c09a013489097eccd8a8fba659.png#pic_center)
    
    3.  单击 [Java (JDK) for Developers](https://www.oracle.com/java/technologies/javase-downloads.html)
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/3257e56b946e832a686ebf0f2b1cb279.png#pic_center)
    
    4.  跳转新页面后，找到自己需要的 JDK 版本 (学习用途建议使用 Java SE 8 版本，该版本比较稳定适合初学者)
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/b57c008e3bd18f1249eaa0801d4dff5e.png#pic_center)
    
    5.  点击 [JDK Dowload](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)
    
    我的系统是 Windows10 的 64 位所以选择 [jdk-8u301-windows-x64-demos.zip](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html#license-lightbox) 压缩版相对于程序来说，压缩版放在指定目录下，直接解压就能使用了。
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/22cb86b58adad556ccf34d89020cb8a3.png#pic_center)
    

#### JDK 的安装

**（如果下载的 JDK 安装程序安装步骤如下）**

1.  找到下载好的程序，双击运行安装包
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/64d34c4707703c222bcde30154b25ceb.png#pic_center)
    
2.  下一步，选择安装所有组件并更改安装路径
    
    (1)、这里显示要安装的三个组件：
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/8d8fe891cafc69bc0d9f0f04256b3ca4.png#pic_center)
    
    (2)、取消安装独立的 JRE，JDK 中已经包含 JRE，这里可以选择取消安装独立的 JRE：
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/9a23261b07a3332972c28b22a0e1c6e2.png#pic_center)
    
    (3)、更改 JDK 的安装路径（具体安装路径自己选择，以方便，好找为准，改了安装路径后记住安装路径，后面配置环境变量时还要用到）：
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/00df4c5dad7dbc85b52fce19e7f4367e.png#pic_center)
    
3.  下一步，根据提示安装完成
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/5765e2cf72664e17b21b0c69bb363879.png#pic_center)
    

#### JDK 运行环境变量配置

**1、桌面计算机右键–属性–高级系统设置–环境变量 (控制面板–系统–高级系统设置–环境变量)**

![](https://i-blog.csdnimg.cn/blog_migrate/940d580a2d3eaf7b05e84c2710a812f0.png#pic_center)

![](https://i-blog.csdnimg.cn/blog_migrate/f5ab50bef784d3580bae99f15744b7f6.png#pic_center)

![](https://i-blog.csdnimg.cn/blog_migrate/1cee2fadb298e00983eeace28e5179dd.png#pic_center)

**2、忽略用户变量，关注系统变量**

![](https://i-blog.csdnimg.cn/blog_migrate/35f5b9ecc5858e1049c0ddf3eb6b9d88.png#pic_center)

**3、点击 “新建”，新建系统变量 JAVA_HOME，值为 JDK 安装根目录**

![](https://i-blog.csdnimg.cn/blog_migrate/5386a1951d53100d95dff53ea607912d.png#pic_center)

**4、编辑 PATH 变量，将刚刚新建的 JAVA_HOME 变量加上 bin 目录设置到 PATH 中**【 %JAVA_HOME%\bin;%JAVA_HOME%\jre\bin; 】

![](https://i-blog.csdnimg.cn/blog_migrate/31f0a522f203deb8c358e3009bee8361.png#pic_center)

![](https://i-blog.csdnimg.cn/blog_migrate/7cc1b098c85c79ca06d491cd0c07ffaf.png#pic_center)

**5、为方便保险**，在系统变量中查找 Path，双击之后打开 “编辑环境变量”，点击新建，你所下载的 JDK 的目录下 bin 所在路径复制进去后保存

![](https://i-blog.csdnimg.cn/blog_migrate/137e0dc6fca5b93e970a99f13a055e21.png#pic_center)

以我的为例：D:\Program Files\Java\jdk1.8.0_251\bin

**注意设置时不要找错位置和 bin 的地址**

![](https://i-blog.csdnimg.cn/blog_migrate/a0435ca826f99889fe9b3e5379ffbea1.png#pic_center)

#### 如何确定 JAVA 的环境配置成功

Win+R 调出运行框，输入 cmd 运行调出命令窗，输入 javac 回车运行，编译器未报错即为配置成功

![](https://i-blog.csdnimg.cn/blog_migrate/5c61cdc3ca64756c05ebda5e0e92b546.png#pic_center)