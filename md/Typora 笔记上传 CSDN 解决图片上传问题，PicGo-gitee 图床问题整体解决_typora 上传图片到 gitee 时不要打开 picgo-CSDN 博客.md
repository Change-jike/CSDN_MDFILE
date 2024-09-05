> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/123241343?spm=1001.2014.3001.5502)

#### 文章目录

*   [Typora 笔记上传 CSDN 解决图片上传问题，PicGo-gitee 图床解决](#Typora__CSDN_PicGogitee__1)
*   *   *   [前言：看我的就看完，一篇文章解决问题，千人千法，不尽相同](#_3)
        *   [文章有点儿长，但是解决问题](#_4)
        *   [1. 工具](#1__10)
        *   [2. 配置图床的步骤](#2__24)
        *   *   [2.1 下载安装 Node.js](#21_Nodejs_44)
            *   [2.2 Node.js 的环境变量](#22_Nodejs_84)
            *   *   [2.2.1 现在可以打开 cmd，查看一下我们的 Node.js 是否可用了](#221_cmdNodejs__98)
                *   [2.2.2 Node.js 环境变量配置到最后我们看看搞定没](#222_Nodejs__149)
            *   [2.3 Gitee 仓库的创建](#23_Gitee__178)
            *   [2.4 最后配置最简单的 PicGo](#24_PicGo_201)
            *   [2.5 Typora 的简单配置，实现随写随黏贴 随粘随上传](#25__Typora___239)

[Typora](https://so.csdn.net/so/search?q=Typora&spm=1001.2101.3001.7020) 笔记上传 CSDN 解决图片上传问题，PicGo-gitee 图床解决
------------------------------------------------------------------------------------------------------------

#### 前言：看我的就看完，一篇文章解决问题，千人千法，不尽相同

#### 文章有点儿长，但是解决问题

​ 利用 Typora ，写文章可以很方便的转换为有效的 XHTML 文件，跟更可以很方便将自己的离线博客文档上传 CSDN 。但是利用 Typora 的 Markdown 写文档避免不了插入图片，在上传 CSDN 过程中本地的图片往往不能自动上传到 CSDN 上，还需要自己重新上传一下本地图片很是麻烦。

​ 今天，我们利用 [PicGo](https://so.csdn.net/so/search?q=PicGo&spm=1001.2101.3001.7020) + gitee 搭建自己的图床，不再让图片上传影响我们起飞的速度。

#### 1. 工具

**安装准备：**

​ 操作系统 Window 10；

1.  [Typora](https://www.typora.io/#windows) ：文本编译器，用起来就一个字–爽！！！
    
2.  [Node.js](https://nodejs.org/en/) ： ** 不要问:** 我也不知道这是啥，属于我的知识盲区，但是没有它，你 PicGo 用不起来，跟着我下载 [Node.js](https://nodejs.org/en/) ，配环境，用就完了。
    
3.  [PicGo](https://molunerfinn.com/PicGo/) ：上传照片的工具就是了。
    
4.  [gitee](https://gitee.com/)：开源中国社区推出的代码托管云，不用科学上网就能上传图片，相对与 GitHub 的图床更方便，上传速度更快，成本更低。
    

#### 2. 配置图床的步骤

1.  下载安装 [Node.js](https://nodejs.org/en/) 、 [PicGo](https://molunerfinn.com/PicGo/) 、 [Typora](https://www.typora.io/#windows)
    
2.  配置 Node.js 的环境变量
    
3.  注册一个给 Gitee 账号，创建一个自己仓库
    
4.  配置 PicGo ，下载 gitee 插件
    
5.  如果你没发现上面的超链接的话，这有地址 emmm
    

Typora 下载地址：https://www.typora.io/#windows

Node 下载地址：https://nodejs.org/en/

PicGo 下载地址：https://molunerfinn.com/PicGo/

**注意** PicGo 默认没有 gitee 图床，但是可以搜索 gitee 图床的插件。请前是先安装过 Node.js 并配置好环境变量, 否则一直装不上。下载过 node 之后直接下载还是大概率失败’哈哈哈‘，但大家还是试试把，万一成功了呢，嘿，那不就省事了嘛！！下面我会教大家用 DOS 命令，用代码下载 PicGo 的 gitee 插件。

##### 2.1 下载安装 Node.js

1.  **Node.js 的下载:**

```
**node官网：**https://nodejs.org/zh-cn/download/
 
 想要自己电脑=干净没广告，能去官网就去官网，官网要￥来找我emm

```

![](https://i-blog.csdnimg.cn/blog_migrate/4f53e9a13bb6d30c483bf6e186f22095.png)

2.  **Node.js 的安装:**
    
    下载完成后打开安装包，开始安装，C 盘大任性的兄弟，可以无脑下一步 ”next“，不太任性的同学还是改改自己的路径，记好别把路径搞丢了，一会儿有用。
    
    ** 默认路径在这：**C:\Program Files
    
    **我的在这：** D:\nodejs
    
    看自己情况
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/a1273599b0ced1acefc0e92b6a7c3609.png)
    
    下面图框**我没有勾选**，就建个图床，我用不到它
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/5de412b7710638ed0be4c03e51e0f5ab.png)
    
    安装结束 finish
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/70ac7289f53d30f91860d0d37f630424.png)
    

##### 2.2 Node.js 的环境变量

```
1. 老套路：【个人电脑】 > 【右键】  > 【属性】 > 【高级系统设置】 > 【环境变量】

```

![](https://i-blog.csdnimg.cn/blog_migrate/f6ddecfe3d2726bc76ec2e889026fdc0.png)

2.  **双击 Path ，新建: 把自己 node.js 的安装路径填进去**

![](https://i-blog.csdnimg.cn/blog_migrate/c76b22b6e507a35d5213a3f029cc4f80.png)

3.  **这是我的 node.js 路径**：D:nodejs

![](https://i-blog.csdnimg.cn/blog_migrate/ab342aa935a37ef2f2664e9a03673c24.png)

###### 2.2.1 现在可以打开 cmd，查看一下我们的 Node.js 是否可用了

有版本号就行了，咱们继续

![](https://i-blog.csdnimg.cn/blog_migrate/36b995c43aa2590d4f39054959f5944c.png)

4.  **打开自己的 node.js 的安装位置**，新建两个文件夹 node_cache； node_global，
    
    再次打开 cmd 命令窗口，输入 npm config set prefix “你的路径 \ node_global”（`“你的路径”默认安装的状况下为 C:\Program Files\nodejs`）就是刚刚新建的俩文件夹
    
    ```
    npm config set prefix "D:\nodejs\nodejs\node_global"
    npm config set cache "D:\nodejs\nodejs\node_cache"
    
    
    
    ```
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/6e023bad32b4656c85f270c659f9ce5e.png)  
    再次打开 cmd 命令窗口 **【使用管理员权限打开 CMD】**，输入 npm config set prefix “你的路径 \ node_global”（`“你的路径”默认安装的状况下为 C:\Program Files\nodejs`) 就是刚刚新建的俩文件夹跟下图一样效果就行。
    
    ```
    npm config set prefix "D:\nodejs\nodejs\node_global"
    npm config set cache "D:\nodejs\nodejs\node_cache"
    
    
    
    ```
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/21d4df15fafe6164059c2836bf0b4f3d.png)
    
    5. **回到环境变量，新建 NODE_PATH，路径写自己的文件路径**
    
    **这是我的 D:\nodejs\node_global\node_modules，可以把 D:\nodejs 改成自己的 nodejs 路径**
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/9064b9164c48bb1d15d087f33b96dc1b.png)
    
    ​ 打开系统环境变量的 Path ，把 **%NODE_PATH%** 添加进去
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/cd9f3d7b0c887109f4f7c1157091358b.png)
    
    6.  最后打开**用户环境变量**的 **Path**，用户环境变量哈看好了
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/2940e5950df3e04d815b6be301c82f60.png)
    
    7.  把一下内容改成：自己的 node 安装位置 \ node_global。  
        ** 这个是我改的:**D:\nodejs\node_global  
        ![](https://i-blog.csdnimg.cn/blog_migrate/b81b7ec2d80418cfac8c508b40fd2d47.png)

![](https://i-blog.csdnimg.cn/blog_migrate/ab023caad83071f7f389a44d0f3200fa.png)

###### 2.2.2 Node.js 环境变量配置到最后我们看看搞定没

1.  安装个 module 测试下，就安装最经常使用的 express，打开 cmd 窗口，输入以下命令进行模块的全局安装：有结果就对了。

```
npm install express -g 

```

2.  最后经过 npm 安装模块时都是去国外的镜像下载的，有的时候由于网络等缘由致使安装模块失败，好在阿里有团队维护国内镜像 [淘宝 NPM 镜像](https://npmmirror.com/) ，都有使用说明，你们可自行查看，也可以现在添加一个阿里的镜像，给自己起飞的路上加个速。
    
3.  ** 添加国内镜像源：** 如果没有梯子的话，可以使用阿里的国内镜像进行加速。
    
    ```
    npm config set registry https://registry.npm.taobao.org
    
    
    ```
    
4.  我用的**淘宝镜像**
    
    ```
    npm --registry https://registry.npm.taobao.org install express
    
    ```
    

![](https://i-blog.csdnimg.cn/blog_migrate/d3082a36d0f8a730f08521d21947e48d.png)

##### 2.3 Gitee 仓库的创建

1.  你不得注册个 Gitee ？赶紧去吧。
2.  注册完成之后，打开码云，

进入主页面，点击 + 创建仓库

![](https://i-blog.csdnimg.cn/blog_migrate/852f5ce6d87cce9d7a7ff3350cbd72f9.png)

3.  新建仓库 > 创建

![](https://i-blog.csdnimg.cn/blog_migrate/bf990638ea220796eabd17097bb7eaa5.png)

4.  进入仓库点管理向下翻，私有改开源记得保存![](https://i-blog.csdnimg.cn/blog_migrate/0477cb77794a7bd2e01b9f9a97565334.png)
    
5.  自己的设置里面找私人令牌，创建私人令牌保存好一会儿用
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/dbd88a41d36fb81b3f330f8b4281c545.png)
    

![](https://i-blog.csdnimg.cn/blog_migrate/b76d3200ebd1e98bd3f209f8daee2b47.png)

![](https://i-blog.csdnimg.cn/blog_migrate/9cefd535169b425edf10ea8598adb33e.png)

##### 2.4 最后配置最简单的 PicGo

1.  手动安装 Pic GO 插件

首先确保安装 Node.js, Win+R 键 ，输入 cmd 调用 命令行窗口，然后 转到 windows 配置目录在 C:\Users \ 用户名 \ AppData\Roaming\picgo 下 ，用户名根据自己的情况修改即可  
执行命令：

```
cd C:\Users\用户名\AppData\Roaming\picgo


```

![](https://i-blog.csdnimg.cn/blog_migrate/5bef97c16b874f8734838fd6e1cd6a2e.png)

2.  最后执行命令
    
    ```
    npm install picgo-plugin-gitee-uploader
    
    ```
    
    或
    
    ```
    npm install picgo-plugin-gitee
    
    ```
    
    装好了就这样，我装的第二个，第一个我的图片传不上去
    
    ![](https://i-blog.csdnimg.cn/blog_migrate/2a21d68b88f84e5f21291e9494821bc4.png)
    
3.  配置 PicGo 的 Gitee 图床如图
    

![](https://i-blog.csdnimg.cn/blog_migrate/3876a38fedddaa08b1e563c173ea2d47.png)

自己试试能不能上传图片吧

##### 2.5 Typora 的简单配置，实现随写随黏贴 随粘随上传

打开 Typora > 文件 > 偏好设置 >

![](https://i-blog.csdnimg.cn/blog_migrate/3fc21b221144327a9c3a0bc866aaa38f.png)

好了，写你的博客去吧，歇着了您嘞！！