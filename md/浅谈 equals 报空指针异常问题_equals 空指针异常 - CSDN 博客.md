> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/126950772?spm=1001.2014.3001.5502)

#### 浅谈 equals 报[空指针异常](https://so.csdn.net/so/search?q=%E7%A9%BA%E6%8C%87%E9%92%88%E5%BC%82%E5%B8%B8&spm=1001.2101.3001.7020)问题

*   *   *   *   [1、常见格式](#1_1)
            *   [2、特殊格式](#2_13)
            *   *   [Tips：](#Tips_15)

##### 1、常见格式

**我们常见的 equals 都是这样用的：**

```
if("字符串".equals(info.getCode())){
    System.out.println("这俩一样啊！！！");
}

```

一般的 equals 前面是常量，比较内容在 equals 之后，这样一般不会出什么问题。

##### 2、特殊格式

###### Tips：

**当对象为 null 时，对象调用 普通方法 时就会出现 空指针异常问题（即 对象. 方法 时，会出现空指针异常），但调用静态方法时，可以正确执行。**

**因为静态方法属于类所有，不属于某个具体的实例对象，在类实例化前即可使用。一般调用静态方法的方式是 “类名”.“方法名”，当然也可以通过类的实例对象来调用，只不过不建议这么调用。**

**特殊格式如下：**

```
if(oldInfo.getCode().equals(info.getCode())){
    System.out.println("这俩一样啊！！！");
}

```

这种格式猛的一看没有什么区别，但实际上是有区别，equals 前面的值为变量，后面值也为变量，这就有问题了；

我们用 equals 判断前后值是否相等的时当然也是有这个前提条件的，那就是 equals 前边的值是不能为 null 的，如果前面的值为 null，就成了 null 调用 equals 方法了，所以会报 **空指针异常**；

也就是本文所说的 equals 空指针异常问题，看到这里大家也就明白了，我们使用 equals 的时候要保证前面值不为空，所以在我们不能确定的情况下我们可以加一层判断，如下：

```
if(null != oldInfo.getCode()){
	if(oldInfo.getCode().equals(info.getCode())){
		System.out.println("这俩一样啊!!!");
	}else{
		System.out.println("这俩 不 一样啊！！！");
	}
}

```

equals 后面的值不用进行 null 判断，后面的值不管是不是 null，不会出现 equals 空指针异常的问题，具体原理大家可以查看 equals 底层源码的很好理解的。

```
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}

```

这里用 if (anObject instanceof String) 来判断传入的对象是否是 String 类型，如果不是直接返回 false。

因此如果有一个数值可能为空的对象实例，调用 equals 方法时，一定要遵循 **“常量”.equals(“变量”)** 或者 **“后输入的”.equals(“之前的”)**。这样就可以尽量避免空指针错误。