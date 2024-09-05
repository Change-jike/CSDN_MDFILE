> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/123384330?spm=1001.2014.3001.5502)

#### 文章目录

*   *   [创建自己的图床，解决笔记上传 CSDN 的图片问题。PicGo-gitee](#_CSDN_PicGogitee_1)
    *   *   *   [1. Gitee 仓库的创建](#1__Gitee__8)
            *   [2. 配置最简单的 PicGo](#2_PicGo_31)
            *   [3. Typora 的简单配置，配置完之后实现随写随黏贴 随粘随上传](#3___Typora___69)

### 创建自己的[图床](https://so.csdn.net/so/search?q=%E5%9B%BE%E5%BA%8A&spm=1001.2101.3001.7020)，解决笔记上传 CSDN 的图片问题。PicGo-gitee

*   开始之前你得先准备好 Node.js 配置好 Node.js 的环境变量
*   最后配置好他们，利用 PicGo + gitee 搭建自己的图床，不再让图片上传影响我们起飞的速度。
*   [Node.js 环境变量配置](https://blog.csdn.net/qq_43371422/article/details/123241343)：https://blog.csdn.net/qq_43371422/article/details/123241343

##### 1. Gitee 仓库的创建

1.  你还没有 Gitee ？赶紧去注册吧。
2.  注册完成之后，打开码云（getee），

进入主页面，点击 + 创建仓库

![](https://i-blog.csdnimg.cn/blog_migrate/4d4645938d10f4ecb86e318a72f39799.png)

3.  新建仓库 > 创建

![](https://i-blog.csdnimg.cn/blog_migrate/f40da5c61ad81d60ecf674adc3313ae1.png)

4.  进入仓库点管理向下翻，私有改开源记得保存![](https://i-blog.csdnimg.cn/blog_migrate/76dd2e2f85aa1c0cd7bfe2c7b77e10c2.png)
    
5.  自己的设置里面找私人令牌，创建私人令牌保存好一会儿用
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/c29ebfa352f6231c9582b6aa1ebcc45e.png)
    

![](https://i-blog.csdnimg.cn/blog_migrate/138cce7a648e4b574b3094d69122fcc4.png)

![](https://i-blog.csdnimg.cn/blog_migrate/d071993bed73118f3cf69d14875b1f2e.png)

##### 2. 配置最简单的 [PicGo](https://so.csdn.net/so/search?q=PicGo&spm=1001.2101.3001.7020)

1.  手动安装 Pic GO 插件

首先确保安装 Node.js, Win+R 键 ，输入 cmd 调用 命令行窗口，然后 转到 windows 配置目录在 C:\Users \ 用户名 \ AppData\Roaming\picgo 下 ，用户名根据自己的情况修改即可  
执行命令：

```
cd C:\Users\用户名\AppData\Roaming\picgo


```

![](https://i-blog.csdnimg.cn/blog_migrate/02877592c2ef83bcfe8980732f2bc64f.png)

2.  最后执行命令安装 gitee 或 gitee-uploader 插件，你也可以选择在 PicGo 的插件里搜索，点击安装，你试试呗，反正我装不上。
    
    ```
    npm install picgo-plugin-gitee-uploader
    
    ```
    
    或
    
    ```
    npm install picgo-plugin-gitee
    
    ```
    
    装好了就这样了，我装的第二个，第一个我的图片传不上去
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/300e37d7fa4f0b6bd3b02e443ba9e591.png)
    
3.  配置 PicGo 的 Gitee 图床如图
    

![](https://i-blog.csdnimg.cn/blog_migrate/dfbed57faa470d23442bccf2b595b2dd.png)

自己试试能不能上传图片吧

##### 3. [Typora](https://so.csdn.net/so/search?q=Typora&spm=1001.2101.3001.7020) 的简单配置，配置完之后实现随写随黏贴 随粘随上传

打开 Typora > 文件 > 偏好设置 >

![](https://i-blog.csdnimg.cn/blog_migrate/df2ffb71ca1a2da3800e0a49a7442021.png)

好了，写你的博客去吧，歇着了您嘞！！