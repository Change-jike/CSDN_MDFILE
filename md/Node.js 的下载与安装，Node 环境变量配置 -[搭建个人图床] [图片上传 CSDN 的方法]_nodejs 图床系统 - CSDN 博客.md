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

![image](https://github.com/user-attachments/assets/4d89d24c-a856-429e-88af-62f4e233f0ec)


###### 1.2 **Node.js 的安装:**

下载完成后打开安装包，开始安装，C 盘大任性的兄弟，可以无脑下一步 ”next“，不太任性的同学还是改改自己的路径，记好别把路径搞丢了，一会儿有用。

**默认路径在这：** C:\Program Files

**我的在这：** D:\nodejs

看自己情况

![image](https://github.com/user-attachments/assets/6251992f-4bdc-4e1e-beae-180dba7bd30c)


下面图框**我没有勾选**，就建个[图床](https://so.csdn.net/so/search?q=%E5%9B%BE%E5%BA%8A&spm=1001.2101.3001.7020)，我用不到它

![image](https://github.com/user-attachments/assets/fc6b62bc-f7cb-411d-9920-fcf065e47167)


安装结束 finish

![image](https://github.com/user-attachments/assets/ba9abc8e-831f-424e-b42d-69742141292f)


##### 2. Node.js 的环境变量配置

###### 2.1 跟着做吧，你的安装地址还记得嘛？？？

1.  **老套路：【个人电脑】 > 【右键】 > 【属性】 > 【高级系统设置】 > 【环境变量】**

![image](https://github.com/user-attachments/assets/e1c8d3ba-2d4f-456d-b2ad-e27a3e325fe8)


2.  **双击 Path ，新建: 把自己 node.js 的安装路径填进去**

![image](https://github.com/user-attachments/assets/a2840c53-a036-4379-a551-0fca7a437a5e)


3.  **这是我的 node.js 路径**：D:nodejs

![image](https://github.com/user-attachments/assets/fae94254-0b8b-4008-a807-97ca158cdb03)


###### 2.2 现在可以打开 cmd，查看一下我们的 Node.js 是否可用了

1.  Win + R - cmd 打开，**node -v** 回车，有版本号就行了咱继续!!!

![image](https://github.com/user-attachments/assets/9be1d482-79da-4a66-8de3-5f828da932fa)


2.  **打开自己的 node.js 的安装位置**，新建两个文件夹 node_cache； node_global，

![image](https://github.com/user-attachments/assets/d9e8da64-5ed0-4b3f-aba9-21cb891816bb)


3.  打开 cmd 命令窗口【**使用管理员权限打开 CMD**】，输入 npm config set prefix “你的路径 \ node_global”（`“你的路径”默认安装的状况下为 C:\Program Files\nodejs`)

```
npm config set prefix "D:\nodejs\nodejs\node_global"
npm config set cache "D:\nodejs\nodejs\node_cache"



```

![image](https://github.com/user-attachments/assets/3e790e10-ee7e-49a6-9868-32b24cb1aac7)


4.  **回到环境变量，新建 NODE_PATH，路径写自己的文件路径**

*   **这是我的 D:\nodejs\node_global\node_modules，可以把 D:\nodejs 改成自己的 nodejs 路径**

![image](https://github.com/user-attachments/assets/254331b1-b429-4664-abe9-83aef660bd3b)


5.  打开**系统环境变量**的 Path ，把 **%NODE_PATH%** 添加进去  
    ![image](https://github.com/user-attachments/assets/f623d8fa-29b9-4c45-9bf4-5ae44ad1d9d6)

    
6.  最后打开**用户环境变量**的 **Path**，看好**不是**系统环境变量了，**是用户环境变量**哈看好了
    

![image](https://github.com/user-attachments/assets/003257f4-d26a-4b34-a884-5d9023d5779a)


7.  把一下内容改成：自己的 node 安装位置 \ node_global。  
    ** 这个是我改的:**D:\nodejs\node_global  
    ![image](https://github.com/user-attachments/assets/3df37dd9-6b1d-4ac3-b42e-c6faaaffe565)


![image](https://github.com/user-attachments/assets/ff899a13-1c43-4446-b3e7-7aeda83b7601)


###### 2.3 Node.js 环境变量配置到最后我们看看搞定没

*   安装个 module 测试下，就安装最经常使用的 express，打开 cmd 窗口，输入以下命令进行模块的全局安装：有结果就对了。

```
npm install express -g 

```

![image](https://github.com/user-attachments/assets/0277ac49-7cf2-4cc6-8150-e3d2dc1ef3dd)


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
