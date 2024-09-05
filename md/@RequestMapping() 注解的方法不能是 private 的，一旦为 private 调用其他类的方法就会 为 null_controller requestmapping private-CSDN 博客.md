> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/131962653?spm=1001.2014.3001.5502)

### Controller 中 @RequestMapping() 注解的方法不能是 private 的，一旦为 private 调用其他类的方法就会 为 null

##### 问题分析：

当在使用 `@RequestMapping` 注解（或其他类似的注解，如 `@GetMapping`、`@PostMapping` 等）时，被注解的方法不能设置为 `private` 私有访问权限，因为这将导致 Spring 框架无法访问和调用该方法。这样会导致在处理 HTTP 请求时出现问题，因为 Spring 无法触发该方法来处理请求。相反，它应该至少是 `protected` 受保护的、 `package-private` （默认，即不写访问修饰符）或者 `public` 公共的访问权限。

![image](https://github.com/user-attachments/assets/b1d0ca7c-1781-4666-b95f-cfffcbb3ecad)


##### 原因：

**当你试图从其他类调用一个私有方法时，如果你得到的结果是 `null`，通常有以下几个可能的原因：**

1.  ** 访问权限：** 私有方法只能在所属类中访问，其他类无法直接调用私有方法。如果你在其他类中尝试调用一个私有方法，Java 编译器会报错或者直接拒绝访问。
2.  ** 错误调用：** 如果在其他类中通过反射或其他手段强制调用私有方法，这可能导致方法的上下文和状态不正确，从而导致返回 `null` 或抛出异常。

##### **注意**：

Spring 框架是通过反射来调用使用 `@RequestMapping` 注解的方法的，而反射需要对目标方法具有足够的访问权限。如果方法是私有的，Spring 将无法通过反射找到并调用这些私有方法，因此会导致问题。

因此，为了使 `@RequestMapping` 注解的方法能够被 Spring 正确调用来处理 HTTP 请求，应该将这些方法设置为 `protected`、`package-private` （默认）或 `public` 访问权限。这样，Spring 框架就能够访问和调用这些方法，并能够正确地处理 HTTP 请求和返回响应。
