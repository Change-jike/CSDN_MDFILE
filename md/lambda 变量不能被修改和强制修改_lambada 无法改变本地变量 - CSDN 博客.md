> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/128024160?spm=1001.2014.3001.5502)

lambda 内部类局部变量值为什么不能被修改和强制修改
----------------------------

#### 文章目录

*   [lambda 内部类局部变量值为什么不能被修改和强制修改](#lambda_0)
*   *   *   [内部类值无法修改原因](#_3)
    *   [问题描述](#_10)
    *   [原因分析](#_19)
    *   *   [原理](#_23)
        *   *   [内部类对象创建规则](#_25)
            *   [命名规则](#_33)
            *   [内部类 final 字段创建](#_final__62)
            *   [总结](#_112)
    *   [结果分析](#_127)
    *   *   *   *   [内部类外面的局部变量不能被重复赋值否则会报错](#_129)
                *   [如果为局部变量重新赋值会导致内部类和局部变量值不一致　容易造成误导](#_E3_80_80_133)
            *   [验证](#_147)
            *   *   [在内部类里面不能修改局部类外面定义的变量的值](#_178)

#### 内部类值无法修改原因

**分析**

*   内部类外面的局部变量不能被重复赋值否则会报错
*   在内部类里面不能修改局部类外面定义的变量的值

### 问题描述

当使用内部类时

内部类外面的局部变量不能被重复赋值否则会报错　为什么?

在内部类里面不能修改局部类外面定义的变量的值　为什么？  
![image](https://github.com/user-attachments/assets/5c733fbd-b5eb-4e84-854d-cd01e3d8afa0)


### 原因分析

想知道上面的原因需要知道编译器是怎么编译内部类的

#### 原理

##### 内部类对象创建规则

*   lambda 内部类  
    根据 javap　-p 反编译可以发现会生成方法 private static void lambda$test$0(int);  
    运行时会生成字节码创建对象
*   匿名内部类  
    编译器扫描到一个内部类时会在该类同包下创建一个 class 字节码文件

##### 命名规则

*   lambda 内部类  
    [外部类](https://so.csdn.net/so/search?q=%E5%A4%96%E9%83%A8%E7%B1%BB&spm=1001.2101.3001.7020)名称 lambda 内部类自增序号 / 随机值如 com.nailsoul.config.RedisConfiglambda 内部类自增序号 / 随机值　如 com.nailsoul.config.RedisConfiglambda 内部类自增序号 / 随机值　如 com.nailsoul.config.RedisConfigLambda$1/1535128843
    
*   普通内部类
    
    外部类名称 $ 普通内部类自增序号 / 随机值　如 com.nailsoul.config.[RedisConfig](https://so.csdn.net/so/search?q=RedisConfig&spm=1001.2101.3001.7020)$1
    
    > 通过下面代码来检查上面理论
    
    ```
    public void test(){
        int count = 1;
        Runnable l1 = ()->{ int t = count; };
        Runnable l2 = ()->{};
        Runnable r1 = new Runnable() {@Override public void run() { }};
        System.out.println(l1.getClass().getName()+"\n"+l2.getClass().getName()+"\n"+r1.getClass().getName());
    }
    
    ```
    
    > 结果
    
    ```
    com.nailsoul.config.RedisConfig$$Lambda$1/1535128843
    com.nailsoul.config.RedisConfig$$Lambda$2/1586270964
    com.nailsoul.config.RedisConfig$1
    
    ```
    

##### 内部类 final 字段创建

*   会为普通内部类创建一个类型为外部类的 final 成员变量并为它赋值
    *   lambda 内部类只有访问了外部类的成员属性或成员方法时才会创建 并且为私有的
    *   普通内部类不管有没有访问直接创建 为包访问
*   会为这个内部类访问的所有外部局部变量创建一个同类型的私有 final 成员变量并为它们赋值
    *   成员变量与成员方法通过外部类对象来访问 只会创建外部类对象 final 字段

> 可以通过反射来检查上面的理论

```
static int k1 = 2;
int v1 = 3;
public void test(){
    int tt = 1; 
    String xx="few";
    Runnable r = new Runnable() {
      	@Override 
        public void run() {
            
        }
    };
    
    Runnable lr = ()->{ String s = tt + xx + k1; }; 
    //访问了类变量Runnable lr2 = ()->{ String s = tt + xx + v1; }; 
    //访问类成员变量printFields(r,"//r"); printFields(lr,"//lr");printFields(lr2,"//lr2");
}
private void printFields(Runnable r, String tag) {
    Field[] fields = r.getClass().getDeclaredFields();
    System.out.println(tag);
    for (Field field : fields) {
        System.out.println(field);
    }
}

```

> 结果

```
//r
final com.nailsoul.config.RedisConfig$1.this$0
//lr
private final int com.nailsoul.config.RedisConfig$$Lambda$1/1535128843.arg$1
private final java.lang.String com.nailsoul.config.RedisConfig$$Lambda$1/1535128843.arg$2
//lr2
private final com.nailsoul.config.RedisConfig com.nailsoul.config.RedisConfig$$Lambda$2/1586270964.arg$1
private final int com.nailsoul.config.RedisConfig$$Lambda$2/1586270964.arg$2
private final java.lang.String com.nailsoul.config.RedisConfig$$Lambda$2/1586270964.arg$3

```

##### 总结

> 局部变量和内部[类成员](https://so.csdn.net/so/search?q=%E7%B1%BB%E6%88%90%E5%91%98&spm=1001.2101.3001.7020) final 变量**不是一个变量**

*   引用对象
    
    > 包含不可变对象　如 String Integer 等  
    > 局部变量和内部类成员 final 字段**指定的引用地址一样**  
    > **即 修改了任何一方的变量里面的属性　另一方也会被修改**
    
*   基本对象
    
    > 不包含包装对象　如 Integer 等  
    > 内部类变量和局部变量都执行同一个**字面常量值** 不管怎么搞都不会互相影响
    

### 结果分析

###### 内部类外面的局部变量不能被重复赋值否则会报错

> 通过上面的测试我们已经知道局部类中的变量和局部变量不是同一个变量

###### 如果为局部变量重新赋值会导致内部类和局部变量值不一致　容易造成误导

> java 可能不是应为该原因　只是我猜测　  
> 因为如果是这原因的话　在内部类被创建前局部变量被修改是安全的  
> 也有可能是为了方便　只要修改了值　就报错  
> 不一致推论如下

*   如果先定义局部变量 x 为３在创建内部类 task
*   为 task 定义 run 方法为打印变量 x
*   这时候 task 内的 x 为３
*   修改局部变量ｘ为５
*   调用 task 的 run 方法 　打印出来的会是３
*   反之　定义局部变量 x 为 3 内部类修改成５　局部变量还是３

##### 验证

```
public void test(){
    Integer x = 3;
    Runnable r = new Runnable() {
        @Override
        public void run() {
            int i = x;
            Class<? extends Runnable> aClass = getClass();
            Field field = ReflectionUtils.findField(aClass,"val$x");
            field.setAccessible(true);
            ReflectionUtils.setField(field,this,5);
        }};
    r.run();
    Field field = ReflectionUtils.findField(r.getClass(), "val$x");
    field.setAccessible(true);
    Object inner = ReflectionUtils.getField(field, r);
    System.out.println("inner:"+inner+",outer:"+x);
}

```

> 结果　因为内部类里的变量和局部变量不是同一个变量　  
> 所以修改内部类的变量的值　对局部变量没影响  
> 如果在内部类里修改 x 的 value 那就有影响了　  
> 因为它们指向的引用是同一个地址

```
inner:5,outer:3

```

###### 在内部类里面不能修改局部类外面定义的变量的值

> 经过前面发分析得知内部类里面的字段被 final 修饰　常规修改肯定会报错　  
> 通过反射可以修改　但是完全没必要　因为修改了没作用对局部变量没任何影响

**原文链接**：https://www.ngui.cc/el/931507.html
