> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/125285214?spm=1001.2014.3001.5502)

#{}, ${} 的区别？
-------------

*   **#**{} 在 Mybatis 中就是 占位符 _?_ , 无论我们传递任何数据，都会 **只会被** 当成 **值** 来处理
    
*   $ {} 是简单的 **字符串 替换**，因为是 替换，所以 **${param}** 传递的参数会被当做 sql 中的一部分。
    
    其与原 SQL 语句只是 **sql 语句拼接形式** 的组合，那么 **${}** 传递的值中如果有 **其他 sql** 语句，也会被执行。这也就是黑客实现 **Sql 注入** 的机会所在。
    

**对照示例：**

```
${param} 传递的参数会被当成 sql 语句中的一部分，即使有一段完整的 SQL 语句他也会被执行。
    
以传入值为 id 为例，对照样本如下：
 
${param} 就是简单的 替换
	 
	select * from table where name = ${param}
	解析成的 sql 为：
	select * from table where name = id
 
        
#{parm} 传入的数据都当成一个字符串，会对自动传入的数据加一个双引号
 
	select * from table where name = #{param}
 	解析成的sql为：
	select * from table where name = "id"
 
为了安全，能用 # 就用 # 方式传参，有效的防止 sql 注入攻击。


```

**对于这个题目我感觉要抓住两点：**  
（1）$ 一般就作 **占位符**。既然是占位符，那就是被用来替换的。知道了这点就能很容易区分 **$** 和 **#** ，也就不容易记错了。  
（2）[预编译](https://so.csdn.net/so/search?q=%E9%A2%84%E7%BC%96%E8%AF%91&spm=1001.2101.3001.7020)的机制。 预编译是对 SQL 语句进行预编译，而其后注入的参数将不会再进行 SQL 编译。

​ 我们知道，SQL 注入是发生在编译的过程中，因为恶意注入了某些特殊字符，最后被编译成了恶意的执行操作。而预编译机制则可以很好的防止 SQL 注入。