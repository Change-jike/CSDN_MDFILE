> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/128033852?spm=1001.2014.3001.5502)

SQL 语句中 where 1=1 是什么意思！
------------------------

**where 条件中 1＝1 之后的条件是通过 if 块动态变化的**。  
例如:

```
select friend_name
    from person where 1=1 
    <if test="friendId!=null and friendId!=''">
     and friend_id = #{friendId}
    </if>
    <if test="collectId!=null and collectId!=''">
     and collect_id = #{collectId}
    </if>

```

**where 1=1 是为了避免 where 关键字后面的第一个词直接就是 “and” 而导致语法错误。**

起到在动态 SQL 中连接 AND 条件

where 后面要有语句，加上了 1=1 后就可以保证语法不会出错!

select * from table where 1=1

因为 table 中根本就没有名称为 1 的字段，所以该 SQL 等效于 select * from table，

这个 [SQL 语句](https://so.csdn.net/so/search?q=SQL%E8%AF%AD%E5%8F%A5&spm=1001.2101.3001.7020)很明显是全表扫描，需要大量的 IO 操作，数据量越大越慢，

建议查询时增加必输项，即 where 1=1 后面追加一些常用的必选条件，并且将这些必选条件建立适当的索引，效率会大大提高