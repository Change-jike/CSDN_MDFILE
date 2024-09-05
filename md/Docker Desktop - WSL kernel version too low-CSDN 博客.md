> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/132491386?spm=1001.2014.3001.5502)

**报错信息：**

![](https://i-blog.csdnimg.cn/blog_migrate/71a17cd2113d2827c25c707c5577bffc.png)

**命令行运行**

```
wsl --update // 更新 WSL

```

![](https://i-blog.csdnimg.cn/blog_migrate/8e36027e904529b0ff7922d5e7729240.png)

**如果启动 docker 还是报连接错误，命令行执行以下命令并重启**

```
netsh winsock reset

```