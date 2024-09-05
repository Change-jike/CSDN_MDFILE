> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/qq_43371422/article/details/137474108?spm=1001.2014.3001.5502)

前言

**java.lang.ClassNotFoundException、java.lang.NoSuchMethodError、java.lang.NoClassDefFoundError** 这类的异常。这类异常一般都是 jar 包冲突导致的。那么 jar 包冲突的原因是什么？如何解决 jar 包冲突呢？

### 1、例：**idea 重复引用解决实例: NoSuchMethodError**

**1.1 确定重复引用问题:**  
![image](https://github.com/user-attachments/assets/a3e87c97-b561-4d46-8bf9-cec559403a49)
**1.2** **maven** **管理工具查找冲突**

![](https://i-blog.csdnimg.cn/blog_migrate/01f2fe5bfe0648dc2eceea784f2c36c8.png#pic_center)

**1.3 修改** **pom** **引用统一版本，解决问题；**

![](https://i-blog.csdnimg.cn/blog_migrate/22995023826a5ad7041bd5fac7cdb010.png#pic_center)

#### 2、更多问题排查、解决、了解；

**更多问题解决**

1） 如果有异常堆栈信息，根据错误信息便可定位致使冲突的类名，而后在 eclipse 中 CTRL+SHIFT+T 或者在 idea 中 CTRL+N 就可发现该类存在于多个依赖 Jar 包中

2）如果步骤 1 没法定位冲突的类来自哪一个 Jar 包，可在应用程序启动时加上 [JVM](https://so.csdn.net/so/search?q=JVM&spm=1001.2101.3001.7020) 参数 -verbose:class 或者 -XX:+TraceClassLoading，日志里会打印出每一个类的加载信息，如来自哪一个 Jar 包

3）定位了冲突类的 Jar 包以后，经过 mvn dependency:tree -Dverbose -Dincludes=: 查看是哪些地方引入的 Jar 包的这个版本

4）肯定 Jar 包来源以后，如果是第一类 Jar 包冲突，则可用 排除不须要的 Jar 包版本或者在[依赖管理](https://so.csdn.net/so/search?q=%E4%BE%9D%E8%B5%96%E7%AE%A1%E7%90%86&spm=1001.2101.3001.7020) 中申明版本；如果第二类 Jar 包冲突，可以排除的话，则用 排掉不须要的那个 Jar 包，如果不能排除，则需考虑 Jar 包的升级或换个别的 Jar 包。

### 一、Jar 包冲突问题

#### 1、什么是 Jar 包冲突问题

Jar 包冲突问题的本质：Java 应用程序因某种因素，加载不到正确的类而致使其行为跟预期不一致。

**具体来讲可分为两种状况：**

​ 1）第一类 Jar 包冲突问题：应用程序依赖的同一个 Jar 包出现了多个不一样版本，并选择了错误的版本而致使 JVM 加载不到需要的类或加载了错误版本的类；

​ 2）第二类 Jar 包冲突问题：一样的类（类的全限定名彻底同样）出现在多个不一样的依赖 Jar 包中，即该类有多个版本，并因为 Jar 包加载的前后顺序致使 JVM 加载了错误版本的类。

这两种状况所致使的结果实际上是同样的，都会使应用程序加载不到正确的类，那么其行为就会跟预期不一致了，下面对这两种类型进行详细分析。

##### 1.1 同一个 Jar 包出现了多个不一样版本

​ 随着 Jar 包不断升级，应用所依赖的 Jar 包会存在若干不一样的版本， 版本升级天避免不了类的方法签名变动，甚至于类名的更替，而当前的应用依赖特定版本的某个类 M ，因为 maven 的传递依赖而致使同一个 Jar 包出现了多个版本，当 maven 的仲裁机制选择了错误的版本时，而刚好类 M 在该版本中被去掉了，或者方法签名改了，致使应用程序因找不到所需的类 M 或找不到类 M 中的特定方法，就会出现第一类 Jar 冲突问题。

###### **可总结出该类冲突问题发生的如下三个必要条件：**

​ 1、因为 maven 的传递依赖致使依赖树中出现了同一个 Jar 包的多个版本

​ 2、该 Jar 包的多个版本之间存在接口差别，如类名更替，方法签名更替等，且应用程序依赖了其中有变动的类或方法

​ 3、maven 的仲裁机制选择了错误的版本

##### 1.2 同一个类出现在多个不一样 Jar 包中

​ 一样的类出现在应用程序所依赖的两个及以上的不一样 Jar 包中，这会致使什么问题呢？我们知道，同一个[类加载器](https://so.csdn.net/so/search?q=%E7%B1%BB%E5%8A%A0%E8%BD%BD%E5%99%A8&spm=1001.2101.3001.7020)对于同一个类只会加载一次（多个不一样类加载器就另说了，这也是解决 Jar 包冲突的一个思路，后面会谈到），那么当一个类出现在多个 Jar 包中，假设有 A 、 B 、 C 等，因为 Jar 包依赖的路径长短、声明的前后顺序或文件系统的文件加载顺序等缘由，类加载器首先从 Jar 包 A 中加载了该类后，就不会加载其他 Jar 包中的这个类了，那么问题来了：若是应用程序此时需要的是 Jar 包 B 中的类版本，而且该类在 Jar 包 A 和 B 中有差别（方法不一样、成员不一样等等），而 JVM 却加载了 Jar 包 A 的中的类版本，与期望不一致，自然就会出现各类诡异的问题。

###### **从上面的描述中，能够发现出现不一样 Jar 包的冲突问题有如下三个必要条件：**

​ 1、同一个类 M 出现在多个依赖的 Jar 包中，为了叙述方便，假设仍是两个： A 和 B

​ 2、Jar 包 A 和 B 中的该类 M 有差别，不管是方法签名不一样也好，成员变量不一样也好，只要能够形成实际加载的类的行为和指望不一致都行。若是说 Jar 包 A 和 B 中的该类彻底同样，那么类加载器不管先加载哪一个 Jar 包，获得的都是一样版本的类 M ，不会有任何影响，也就不会出现 Jar 包冲突带来的诡异问题。

​ 3、加载的类 M 不是所指望的版本，即加载了错误的 Jar 包

#### 2、为什么会产生 Jar 包冲突

##### 2.1 maven 仲裁机制

​ 传递性依赖是 Maven2.0 引入的新特性，让开发人员只需关注直接依赖的 Jar 包，对于间接依赖的 Jar 包，Maven 会经过解析从远程仓库获取的依赖包的 pom 文件来隐式地将其引入，为开发带来了极大的便利。但同时也带来了版本冲突的问题，即同一个 Jar 包出现了多个不一样的版本。针对该问题 Maven 也有一套仲裁机制来决定最终选用哪一个版本，但 Maven 的选择不一定是开发人员所指望的，这也是产生 Jar 包冲突最多见的原因。

###### ** 先来看下 Maven 的仲裁机制： **

​ 优先按照依赖管理 元素中指定的版本声明进行仲裁，此时下面的两个原则都无效了

​ 若无版本声明，则按照 “短路径优先” 的原则（Maven2.0）进行仲裁，即选择依赖树中路径最短的版本

​ 若路径长度一致，则按照 “第一声明优先” 的原则进行仲裁，即选择 POM 中最早声明的版本

​ 除了第一条仲裁规则（这也是解决 Jar 包冲突的经常使用手段之一）外，后面的两条原则，对于同一个 Jar 包不一样版本的选择，也许是 maven 研发团队在总结了大量的项目依赖管理经验后得出的两条结论，又或者是发现根本找不到一种统一的方式来知足全部场景以后的无奈之举。可能这对于多数场景是适用的，可是它不一定适合我们当前的应用。由于每一个应用都有其特殊性，该依赖哪一个版本，maven 没办法帮你彻底搞定，如果你没有规规矩矩地使用 来进行依赖管理，就注定了逃脱不了第一类 Jar 包冲突问题（同一个 Jar 包出现了多个不一样版本）。

##### 2.2 Jar 包的加载顺序

​ 对于第二类 Jar 包冲突问题，即多个不一样的 Jar 包有类冲突，这相对于第一类问题就显得更为棘手。在这种状况下，两个不一样的 Jar 包，假设为 A、 B，它们的名称互不相同，甚至可能彻底不沾边，若是不是出现冲突问题，你可能都不会发现它们有共有的类！对于 A、B 这两个 Jar 包，maven 就显得无能为力了，由于 maven 只会为你针对同一个 Jar 包的不一样版本进行仲裁，而这俩是属于不一样的 Jar 包，超出了 maven 的依赖管理范畴。此时，当 A、B 都出现在应用程序的类路径下时，就会存在潜在的冲突风险，即 A、B 的加载前后顺序就决定着 JVM 最终选择的类版本，若是选错了，就会出现诡异的第二类冲突问题。

###### **那么 Jar 包的加载顺序都由哪些因素决定的呢？具体以下：**

​ Jar 包所处的加载路径，或者换个说法就是加载该 Jar 包的类加载器在 JVM 类加载器树结构中所处层级。因为 JVM 类加载的双亲委派机制，层级越高的类加载器越先加载其加载路径下的类，顾名思义，引导类加载器（bootstrap ClassLoader，也叫启动类加载器）是最早加载其路径下 Jar 包的，其次是扩展类加载器（extension ClassLoader），再次是系统类加载器（system ClassLoader，也就是应用加载器 appClassLoader），Jar 包所处加载路径的不一样，就决定了它的加载顺序的不一样。

​ 文件系统的文件加载顺序。这个因素很容易被忽略，也是因环境不一致而致使各类诡异冲突问题的罪魁祸首。因 tomcat、resin 等容器的 ClassLoader 获取加载路径下的文件列表时是不排序的，这就依赖于底层文件系统返回的顺序，那么当不一样环境之间的文件系统不一致时，就会出现有的环境没问题，有的环境出现冲突。例如，对于 Linux 操做系统，返回顺序则是由 iNode 的顺序来决定的，若是说测试环境的 Linux 系统与线上环境不一致时，就极有可能出现典型案例：测试环境怎么测都没问题，但一上线就出现冲突问题，规避这种问题的最佳办法就是尽可能保证测试环境与线上一致。

#### 3、Jar 包冲突会导致什么问题

​ Jar 包冲突可能会导致哪些问题？一般发生在编译或运行时，主要分为两类问题：一类是比较直观的也是最为常见的错误是抛出各类运行时异常，还有一类就是比较隐晦的问题，它不会报错，其表现形式是应用程序的行为跟预期不一致。

**具体问题如下：**

1.  **java.lang.ClassNotFoundException**，即 java 类找不到。

这类典型异常一般是因为，没有在依赖管理中声明版本，maven 的仲裁的时候选取了错误的版本，而这个版本缺乏应用程序需要的某个 class 而致使该错误。例如 httpclient-4.4.jar 升级到 httpclient-4.36.jar 时，类 org.apache.http.conn.ssl.NoopHostnameVerifier 被去掉了，如果原本需要的是 4.4 版本，且用到了 NoopHostnameVerifier 这个类，而 maven 仲裁时选择了 4.6，则会致使 ClassNotFoundException 异常。

2.  **java.lang.NoSuchMethodError**，即找不到特定方法，第一类冲突和第二类冲突均可能致使该问题——加载的类不正确。

如果第一类冲突，则是因为错误版本的 Jar 包与所需要版本的 Jar 包中的类接口不一致致使，例如 antlr-2.7.2.jar 升级到 antlr-2.7.6.Jar 时，接口 antlr.collections.AST.getLine() 发生变更，当 maven 仲裁选择了错误版本而加载了错误版本的类 AST，则会致使该异常；如果第二类冲突，则是因为不一样 Jar 包含有的同名类接口不一致致使，典型的案例：Apache 的 commons-lang 包，2.x 升级到 3.x 时，包名直接从 commons-lang 改成 commons-lang3，部分接口也有所改动，因为包名不一样和传递性依赖，常常会出现两种 Jar 包同时在 classpath 下，org.apache.commons.lang.StringUtils.isBlank 就是其中有差别的接口之一，因为 Jar 包的加载顺序，致使加载了错误版本的 StringUtils 类，就可能出现 NoSuchMethodError 异常。

3.  **java.lang.NoClassDefFoundError，java.lang.LinkageError** 等，原因和上述雷同，就不做具体案例分析了。
4.  ** 没有报错异常，但应用的行为跟预期不一致。** 这类问题一样也是因为运行时加载了错误版本的类致使，但跟前面不一样的是，冲突的类接口都是一致的，但具体实现逻辑有差别，当应用程序加载的类版本不是实现逻辑，就会出现行为跟预期不一致问题。这类问题一般发生在应用程序本身内部实现的多个 Jar 包中，因为包路径和类名命名不规范等问题，致使两个不一样的 Jar 包出现了接口一致但实现逻辑又各不相同的同名类，从而引起此问题。

### 二、解决方案

#### 1、问题排查和解决

1） 如果有异常堆栈信息，根据错误信息便可定位致使冲突的类名，而后在 eclipse 中 CTRL+SHIFT+T 或者在 idea 中 CTRL+N 就可发现该类存在于多个依赖 Jar 包中

2）如果步骤 1 没法定位冲突的类来自哪一个 Jar 包，可在应用程序启动时加上 JVM [参数](https://so.csdn.net/so/search?q=%E5%8F%82%E6%95%B0&spm=1001.2101.3001.7020) -verbose:class 或者 -XX:+TraceClassLoading，日志里会打印出每一个类的加载信息，如来自哪一个 Jar 包

3）定位了冲突类的 Jar 包以后，经过 mvn dependency:tree -Dverbose -Dincludes=: 查看是哪些地方引入的 Jar 包的这个版本

4）肯定 Jar 包来源以后，如果是第一类 Jar 包冲突，则可用 排除不须要的 Jar 包版本或者在依赖管理 中申明版本；如果第二类 Jar 包冲突，可以排除的话，则用 排掉不须要的那个 Jar 包，如果不能排除，则需考虑 Jar 包的升级或换个别的 Jar 包。

#### 2、如何有效避免

​ 从上一节的解决方案能够发现，当出现第二类 Jar 包冲突，且冲突的 Jar 包又没法排除时，问题变得至关棘手，这时候要处理该冲突问题就须要较大成本了，因此，最好的方式是在冲突发生以前能有效地规避。那么怎样才能有效地规避 Jar 包冲突呢？

##### 2.1 良好的习惯：依赖管理

​ 对于第一类 Jar 包冲突问题，一般的作法是用 **** 排除不须要的版本，但这种作法带来的问题是每次引入带有传递性依赖的 Jar 包时，都需要一一进行排除，很麻烦。maven 为此提供了集中管理依赖信息的机制，即依赖管理元素 **** ，对依赖 Jar 包进行统一版本管理，一劳永逸。一般的作法是，在 parent 模块的 pom 文件中尽量地声明全部相关依赖 Jar 包的版本，并在子 pom 中简单引用该构件便可。

来看个示例，当确定开发时使用的 httpclient 版本为 4.5.1 时，可在父 pom 中配置以下：

```
    <properties>
      <httpclient.version>4.5.1</httpclient.version>
    </properties>
    <dependencyManagement>
      <dependencies>
        <dependency>
          <groupId>org.apache.httpcomponents</groupId>
          <artifactId>httpclient</artifactId>
          <version>${httpclient.version}</version>
        </dependency>
      </dependencies>
    </dependencyManagement>

```

而后各个需要依赖该 Jar 包的子 pom 中配置以下依赖：

```
 <dependencies>
      <dependency>
        <groupId>org.apache.httpcomponents</groupId>
        <artifactId>httpclient</artifactId>
      </dependency>
 </dependencies>

```

##### 2.2 冲突检测插件

**maven-enforcer-plugin**，这个强大的 maven 插件，配合 **extra-enforcer-rules** 工具，能自动扫描 Jar 包将冲突检测并打印出来。其原理其实也比较简单，经过扫描 Jar 包中的 class，记录每一个 class 对应的 Jar 包列表，如果有多个就是冲突了。

对于第二类 Jar 包冲突问题，前面也提到过，其核心在于同名类出现在多个不一样的 Jar 包中，若是人工来排查该问题，则需要逐个点开每一个 Jar 包，而后相互对比看有没同名的类，那得多么浪费精力啊？！好在这种费时费力的体力活能交给程序去干。

在最终需要打包运行的应用模块 pom 中，引入 maven-enforcer-plugin 的依赖，在 build 阶段便可发现问题，并解决它。好比对于具备 parent pom 的多模块项目，需要将插件依赖声明在应用模块的 pom 中。这里有童鞋可能会疑问，为何不把插件依赖声明在 parent pom 中呢？那样依赖它的应用子模块岂不是都能复用了？这里之因此强调 “打包运行的应用模块 pom”，是由于冲突检测针对的是最终集成的应用，关注的是应用运行时是否会出现冲突问题，而每一个不一样的应用模块，各自依赖的 Jar 包集合是不一样的，由此而产生的 **** 列表也是有差别的，所以只能针对应用模块 pom 分别引入该插件。

先看示例用法以下：

```
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-enforcer-plugin</artifactId>
  <version>1.4.1</version>
  <executions>
    <execution>
      <id>enforce</id>
      <configuration>
        <rules>
          <dependencyConvergence/>
        </rules>
      </configuration>
      <goals>
        <goal>enforce</goal>
      </goals>
    </execution>
    <execution>
      <id>enforce-ban-duplicate-classes</id>
      <goals>
        <goal>enforce</goal>
      </goals>
      <configuration>
        <rules>
          <banDuplicateClasses>
            <ignoreClasses>
              <ignoreClass>javax.</ignoreClass>
*              <ignoreClass>org.junit.*</ignoreClass>
              <ignoreClass>net.sf.cglib.</ignoreClass>
*              <ignoreClass>org.apache.commons.logging.*</ignoreClass>
              <ignoreClass>org.springframework.remoting.rmi.RmiInvocationHandler</ignoreClass>
            </ignoreClasses>
            <findAllDuplicates>true</findAllDuplicates>
          </banDuplicateClasses>
        </rules>
        <fail>true</fail>
      </configuration>
    </execution>
  </executions>
  <dependencies>
    <dependency>
      <groupId>org.codehaus.mojo</groupId>
      <artifactId>extra-enforcer-rules</artifactId>
      <version>1.0-beta-6</version>
    </dependency>
  </dependencies>
</plugin>

```

**maven-enforcer-plugin** 是经过不少预约义的标准规则（standard rules）和用户自定义规则，来约束 maven 的环境因素，如 maven 版本、JDK 版本等等，它有不少好用的特性，具体可参见官网。而 Extra Enforcer Rules 则是 MojoHaus 项目下的针对 maven-enforcer-plugin 而开发的提供额外规则的插件，这其中就包含前面所提的重复类检测功能，具体用法可参见官网，这里就不详细叙述了。

### **总结**

本文首先介绍了两类 Jar 包冲突问题：

第一类是同一个 Jar 包出现了多个不一样版本.

第二类是同一个类出现在多个不同的 Jar 包中.

然后介绍了第一类 Jar 包冲突问题的原因是是因为 Maven 仲裁机制并不能只能的判断应用真正需要的 Jar 包版本，第二类 Jar 包冲突问题的原因是受到 Jar 包的类加载器的加载顺序和操作系统的文件加载顺序的影响。

最后提出了问题排除和解决的方案，以及如何有效避免 Jar 包冲突问题的发生。

​

原文链接：https://blog.csdn.net/yuanmintao/article/details/134624215
