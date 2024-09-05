> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/129758518?spm=1001.2014.3001.5502)

#### 文章目录

*   *   [对 JSONArray 对象数组处理出现乱码 **"\$ref" -> "\$[1][3]"** 的问题](#_JSONArray_ref__13_1)
    *   *   [问题描述:](#_30)
        *   [解决方案：](#_48)
        *   [总结:](#_71)
        *   [多比比一句：](#_74)

### 对 JSONArray 对象数组处理出现乱码 **“$ref” -> “$[1][3]”** 的问题

JSON 数组转 String 乱码 “ r e f " − > "ref"->" ref"−>"[1][3]”;

**这个问题是我在将 JSONArray 做循环处理转字符串的过程中遇到的，一开始以为是 Integer 类型数据处理不对，一直在纠结是不是转义的问题，事实证明完全错误。**

**根本原因是：**

​ 在 Java 中对像 Integer, Boolean, Byte, Character, Short 和 Long 这类简单类型的对象都是不可变的，这意味着一旦创建了它们的值就不能更改。因此，如果一个 JSONArray 中的两个对象引用了相同的 Integer 值，它们实际上引用的是内存中的相同对象。

“$ref” -> “$[1][3]” 实际是 JSON 指针语法。$ref 是一个 JSON 指针引用，可用于引用 JSON 文档中的另一个位置 的数据。

​ **用代码来讲：**

**“$[1][3]”** 在以下这个数组中表示为数字 **7**；

```
[
  [0, 1, 2, 3],
  [4, 5, 6, 7]
]

```

JSON 指针语法提供了这一种方法来引用 JSON 文档的特定部分，这在各种上下文中都很有用，但是有时也会为我们平添许多烦恼。

#### 问题描述:

**我在对 JSONArray 做循环处理的时候，将获取的对象转换成 json 字符串后，字符串中包括 “$ref” -> “$[1][3]” 符号，造成解析异常；**

示例代码如下：

```
List<List> lists = new ArrayList<>();
        jsonArray.forEach(item -> {
            List innerList = JSON.parseObject(String.valueOf(item), List.class);
            lists.add(innerList);
        });

```

一般情况下，这种 for-Each 是不会出现循环引用的问题的，但是 这里的 jsonArray 中有多个重复的 Integer 类型数据（我们已整数 1 为例），在进行第二次引用整数 1 做转字符串处理时，这里的 1 就变成了 JSON 指针引用的数据了，记录的是第一次出现 1 的位置；

#### 解决方案：

**这里为了展示直观选择了最笨重的方法：把整个 JSONArray 循环重新赋值后又做处理；**

```
for (int i = 1; i < jsonArray.size(); i++) {
            JSONArray innerArray = jsonArray.getJSONArray(i);
            for (int j = 0; j < innerArray.size(); j++) {
                Object value = innerArray.get(j);
                if (value != null) {
                    String strValue = value.toString(); // 将任意类型的对象转换成字符串
                    innerArray.set(j, strValue);
                }
            }
        }

```

Object value = innerArray.get(j); 将 JSONArray 中每一个对象重新赋值，成 Object 类型；

​ **这么做的原因是：** 在 Java 中，所有非基本类型都是对象，包括数组、集合和自定义的类。对于基本类型 (例如，int, double, boolean)，将一个变量的值赋给另一个变量时，将创建该值的新副本，并且这两个变量指向不同的内存位置。因此后续用 新赋值的 value 做其他处理时就不会再出现循环引用的问题了。

#### 总结:

​ 当创建某个类型的对象时，内存中会创建该类型的新实例，并获得对该实例的引用，这是指向该对象的内存地址。对于可变的对象，例如集合或自定义的类，则可以有多个引用指向内存中的同一个对象。当通过一个引用修改对象时，更改将通过对同一对象的所有其他引用可见。如果你不小心，这可能会导致意想不到的结果。

#### 多比比一句：

对付循环引用我们还可以通过添加序列化配置属性来关闭 FastJson 的引用检测：SerializerFeature.DisableCircularReferenceDetect；

​ 示例：取消 FastJson 的循环引用的检查；

```
 	Map map = new HashMap<>();
    List<Map> list = new ArrayList();

	map.put(1,1);
	list.add(map);
    list.add(map);
    
    System.out.println(list);
    System.out.println(JSON.toJSONString(list));
    System.out.println(JSON.toJSONString(list, SerializerFeature.DisableCircularReferenceDetect));


// 输出结果 ：
/**
	[{1=1},{1=1}]
	[{1:1},{ "$ref" :"$[0]"}]
	[{1:1},{1:1}]
*/

```