> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/132742681?spm=1001.2014.3001.5502)

接口可视化引进 Swagger 的时候 Swagger 接口文档中 封装的返回对象变成 “object” 类型;

### **查询 Knife4j 文档之后找到原因：**

在 2.0.6 等后面的高版本中, 由于升级了 Springfox 基础组件，如果开发者使用类似 JRebel 这类热加载插件的时候，会出现类字段没有的情况，目前没有办法解决 springfox 项目与 JRebel 插件的冲突，**建议是不用 JRebel** 。https://doc.xiaominfo.com/docs/faq/swagger-des-not-found![](https://i-blog.csdnimg.cn/blog_migrate/505bdc9e2512c032b72bd81112d419cd.png)