> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/123372727?spm=1001.2014.3001.5502)

#### 文章目录

*   [Node.js 的下载与安装，Node 环境变量配置 -[搭建个人图床] [图片上传 CSDN]](#Nodejs_Node_CSDN_1)
*   *   [前言：看我的就看完，一篇文章解决问题](#_6)
    *   *   *   [1. Node.js 下载和安装](#1_Nodejs_12)
            *   *   [1.1 **Node.js 的下载:**](#11_Nodejs__14)
                *   [1.2 **Node.js 的安装:**](#12_Nodejs__30)
            *   [2. Node.js 的环境变量配置](#2__Nodejs_54)
            *   *   [2.1 跟着做吧，你的安装地址还记得嘛？？？](#21_56)
                *   [2.2 现在可以打开 cmd，查看一下我们的 Node.js 是否可用了](#22_cmdNodejs__70)
                *   [2.3 Node.js 环境变量配置到最后我们看看搞定没](#23_Nodejs__113)
            *   [3. 添加镜像](#3__123)

Node.js 的下载与安装，[Node 环境变量配置](https://so.csdn.net/so/search?q=Node%E7%8E%AF%E5%A2%83%E5%8F%98%E9%87%8F%E9%85%8D%E7%BD%AE&spm=1001.2101.3001.7020) -[搭建个人图床] [图片上传 CSDN]
----------------------------------------------------------------------------------------------------------------------------------------------------------------------

### 前言：看我的就看完，一篇文章解决问题

**环境变量千人千法，不尽相同**

[Node.js](https://nodejs.org/en/) ： **不要问:** 咱也不知道这是啥，属于知识盲区，据说上传图片他是必要工具，没有他，你 PicGo 用不起来，下载 [Node.js](https://nodejs.org/en/) ，配环境，用就完了。

##### 1. Node.js 下载和安装

###### 1.1 **Node.js 的下载:**

```
node官网：https://nodejs.org/zh-cn/download/
 
 想要自己电脑=干净没广告，能去官网就去官网，官网要￥来找我emm

```

![](https://i-blog.csdnimg.cn/blog_migrate/db231e67e0440863f6d7ddbf8850931a.png)

###### 1.2 **Node.js 的安装:**

下载完成后打开安装包，开始安装，C 盘大任性的兄弟，可以无脑下一步 ”next“，不太任性的同学还是改改自己的路径，记好别把路径搞丢了，一会儿有用。

**默认路径在这：** C:\Program Files

**我的在这：** D:\nodejs

看自己情况

![](https://i-blog.csdnimg.cn/blog_migrate/3bd220a77a40894602d07442a2f22f7b.png)

下面图框**我没有勾选**，就建个[图床](https://so.csdn.net/so/search?q=%E5%9B%BE%E5%BA%8A&spm=1001.2101.3001.7020)，我用不到它

![](https://i-blog.csdnimg.cn/blog_migrate/7669a110268e9a7305e96bed49cd6a19.png)

安装结束 finish

![](https://i-blog.csdnimg.cn/blog_migrate/f456c579e08b1b15b4daf9b8ea0f8836.png)

##### 2. Node.js 的环境变量配置

###### 2.1 跟着做吧，你的安装地址还记得嘛？？？

1.  **老套路：【个人电脑】 > 【右键】 > 【属性】 > 【高级系统设置】 > 【环境变量】**

![](https://i-blog.csdnimg.cn/blog_migrate/6cd2e7a58f442b11fefcd491a73b06fb.png)

2.  **双击 Path ，新建: 把自己 node.js 的安装路径填进去**

![](https://i-blog.csdnimg.cn/blog_migrate/59c3672c9d2ab122439e501130755f65.png)

3.  **这是我的 node.js 路径**：D:nodejs

![](https://i-blog.csdnimg.cn/blog_migrate/4a3af857733f17d0eb9712e4899887fa.png)

###### 2.2 现在可以打开 cmd，查看一下我们的 Node.js 是否可用了

1.  Win + R - cmd 打开，**node -v** 回车，有版本号就行了咱继续!!!

![](https://i-blog.csdnimg.cn/blog_migrate/56e7a61a9893ad3ccf27ad4f5c2df1bd.png)

2.  **打开自己的 node.js 的安装位置**，新建两个文件夹 node_cache； node_global，

![](https://i-blog.csdnimg.cn/blog_migrate/10320afbd4fd2e4897186655b5874a02.png)

3.  打开 cmd 命令窗口【**使用管理员权限打开 CMD**】，输入 npm config set prefix “你的路径 \ node_global”（`“你的路径”默认安装的状况下为 C:\Program Files\nodejs`)

```
npm config set prefix "D:\nodejs\nodejs\node_global"
npm config set cache "D:\nodejs\nodejs\node_cache"



```

![](https://i-blog.csdnimg.cn/blog_migrate/cf498439d08091493eca014c607f2287.png)

4.  **回到环境变量，新建 NODE_PATH，路径写自己的文件路径**

*   **这是我的 D:\nodejs\node_global\node_modules，可以把 D:\nodejs 改成自己的 nodejs 路径**

![](https://i-blog.csdnimg.cn/blog_migrate/3f8f6360faaa5b58eddbc15d22ca4925.png)

5.  打开**系统环境变量**的 Path ，把 **%NODE_PATH%** 添加进去  
    ![](https://i-blog.csdnimg.cn/blog_migrate/19264694b884bb658171f034894ec90a.png)
    
6.  最后打开**用户环境变量**的 **Path**，看好**不是**系统环境变量了，**是用户环境变量**哈看好了
    

![](https://i-blog.csdnimg.cn/blog_migrate/2d434200cc0289f498b85bc9b61804d7.png)

7.  把一下内容改成：自己的 node 安装位置 \ node_global。  
    ** 这个是我改的:**D:\nodejs\node_global  
    ![](https://i-blog.csdnimg.cn/blog_migrate/6bab3dc2e11bd3cfedea9f8acb818696.png)

![](https://i-blog.csdnimg.cn/blog_migrate/882b50a0acca3c296426d3aa7cc1ea87.png)

###### 2.3 Node.js 环境变量配置到最后我们看看搞定没

*   安装个 module 测试下，就安装最经常使用的 express，打开 cmd 窗口，输入以下命令进行模块的全局安装：有结果就对了。

```
npm install express -g 

```

![](https://i-blog.csdnimg.cn/blog_migrate/fdffac3a2c171c13264fa0a8c6905686.png)

##### 3. 添加镜像

经过 npm 安装模块时都是去国外的镜像下载的，有的时候由于网络等缘由致使安装模块失败，好在阿里有团队维护国内镜像 [淘宝 NPM 镜像](https://npmmirror.com/) ，都有使用说明，你们可自行查看，也可以现在添加一个阿里的镜像，给自己起飞的路上加个速。

1.  ** 添加国内镜像源：** 如果没有梯子的话，可以使用阿里的国内镜像进行加速。

```
npm config set registry https://registry.npm.taobao.org


```

2.  我用的**淘宝镜像**

```
npm --registry https://registry.npm.taobao.org install express

```