> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/125295825?spm=1001.2014.3001.5502)

#### 文章目录

*   *   [使用 PicGo + GitHub 打造图床](#_PicGo__GitHub__1)
    *   *   [一、 PicGo 下载安装](#_PicGo__13)
        *   [二、 GitHub 图床](#_GitHub_25)
        *   *   [1. 创建 GitHub 图床之前，需要注册 / 登陆 GitHub 账号](#1__GitHub__GitHub__27)
            *   [2. 创建 Repository](#2__Repository_29)
        *   [三、 配置 PicGO](#__PicGO_70)
        *   *   [1. 下载安装并运行 PicGo](#1_PicGo_72)
            *   [2. 配置图床](#2__74)
        *   [四、 进阶 Typora 自动上传图片](#__Typora__90)
        *   *   [Typora 的简单配置，配置完之后实现随写随黏贴 随粘随上传](#Typora___92)

### 使用 PicGo + GitHub 打造图床

额、GitEE 不能用了，所以换 GitHub 做图床了，（可能需要科学上网，嘿，不过主要还是取决于你的网速）。配置过程基本都是一样的，环境变量 和 其他的一些细节 会有连接参考下以前的配置 Git EE 图穿的过程吧。哈

*   开始之前你得先准备好 Node.js 配置好 Node.js 的环境变量
*   配置好他之后，利用 PicGo + github 搭建自己的图床，不再让图片上传影响我们起飞的速度。
*   [Node.js 环境变量配置](https://blog.csdn.net/qq_43371422/article/details/123241343)我偷个懒，这个是以前配置 GitEE 图床时 Node.js 的配置过程

#### 一、 PicGo 下载安装

**下载地址**：https://github.com/Molunerfinn/PicGo

就无脑安装就好了！！！

![](https://i-blog.csdnimg.cn/blog_migrate/b9689339ace0f9199c7b446cb813aa43.png)

#### 二、 GitHub 图床

##### 1. 创建 GitHub 图床之前，需要注册 / 登陆 GitHub 账号

##### 2. 创建 Repository

1.  就在头像旁边的 **+** 里面。

![](https://i-blog.csdnimg.cn/blog_migrate/842e5805e64daaa7086fc8b5e8ff4e08.png)

2.  填一下信息，点击创建

![](https://i-blog.csdnimg.cn/blog_migrate/6e7505a4f91b511ceb29b3254b9e41af.png)

3.  生成一个 Token 用于访问 GitHub 的图床

![](https://i-blog.csdnimg.cn/blog_migrate/2522fd06a2ac0e51713d798655b2168e.png)

![](https://i-blog.csdnimg.cn/blog_migrate/e9e7e931040ccb725ce134d70b2c8893.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6779efe544404303825429f24dbe319d.png)

![](https://i-blog.csdnimg.cn/blog_migrate/2f3a04598dd2796613cdfcc91857108f.png)

4.  **Token** 可一定要保存呀

好啦。填完描述，选择 “repo” 权限，然后点击 “Generate token” 按钮

**注：创建成功后，会生成一串 token，这串 token 之后不会再显示，所以第一次看到的时候，可以建个文本文件好好保存，忘记了只有重新生成，每次都不一样。**

![](https://i-blog.csdnimg.cn/blog_migrate/f9040f28d7cd73238383ba759b2ebb1e.png)

#### 三、 配置 PicGO

##### 1. 下载安装并运行 PicGo

##### 2. 配置图床

*   第一行仓库名：按照 Github 账户名 / 仓库名填写，比如我的就是 **XXXjike/XXXimg**
*   第二行分支名：统一填写 main 或者 master 都行
*   第三方 Token：都复制了吧？？贴在这就行
*   第四行储存路径可以不写
*   第五行自定义域名：就是 PicGo 会将 “自定义域名 + 上传的图片名” 生成的访问链接，放到剪切板上，自定义域名需要按照这样去填写：https://raw.githubusercontent.com / 账户名 / 仓库名 / master，那比如我的就是 https://cdn.jsdelivr.net/gh/XXXXe-jike/XXXCat-Img

![](https://i-blog.csdnimg.cn/blog_migrate/0087888b3a04dd62e5a2b6d61a3b3a07.png)

#### 四、 进阶 Typora 自动上传图片

##### Typora 的简单配置，配置完之后实现随写随黏贴 随粘随上传

打开 Typora > 文件 > 偏好设置 >

![](https://i-blog.csdnimg.cn/blog_migrate/c9157b765cac22af07bbbca5463c09e3.png)