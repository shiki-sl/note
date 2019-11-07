# Pig技术文档V2.0

## 前言

### 集赞送文档

<https://pig4cloud.com/doc/support>

## 声明

- pig 功能已经**完全开源**
- 关于文档收费问题，**即使没有此文档，我相信大多数同学都能运行起来pig**，文档中书写花费了大量时间，也是对我们团队的支持。
- 关于文档内容问题，**基于pig而不仅限于pig** ,文档侧重于pig 功能实现原理的讲解，而非使用说明。是把我们在生产中实际做过的尝试整理出来，让你快速了解Spring Cloud 企业开发，而非各组件的简单认识。
- 关于价格，**全部章节 59.99元**

------

## 关于pigx

本人在pig 的基础进行**增强**开发了pigx。

- 前后端完全分离，前端使用avue即使没有前端开发经验也能快速上手
- 基于Spring Boot 2.1.6.RELEASE丶Greenwich.SR2
- 基于Spring Cloud Gateway 定制webflux网关
- 深度定义LCN 解决分布式事务问题
- 基于 Spring Security OAuth 深度权限定制,权限控制到菜单、token
- 完全打通常见社交登录，面对OAuth 前后端分离架构不在难办
- 封装部分Spring Cloud 原生组件，开发更加方便
- 去除了部分对于开发不友好的中间件,快速上手
- 完全开放源代码，持续更新
  [获取源码](https://pig4cloud.com/)

# 部署运行

[开发环境准备](https://www.kancloud.cn/lengleng/pig-guide/949161)
[服务端代码部署](https://www.kancloud.cn/lengleng/pig-guide/949162)
[前端代码部署](https://www.kancloud.cn/lengleng/pig-guide/949163)
[部署视频](https://www.kancloud.cn/lengleng/pig-guide/998966)

# 开发环境准备





### 特别说明

请务必按照本文档部署运行章节 进行操作，减少踩坑弯路！！

### 环境说明

| 中间件 | 版本  | 备注     |
| ------ | ----- | -------- |
| JDK    | 1.8   | 强制要求 |
| MySQL  | 5.7 + | 强制要求 |
| Redis  | 3.2 + |          |
| node   | 8.0 + |          |
| npm    | 6.0 + |          |

### JDK 说明

请使用mvn -v 命令查看关联的jdk版本，当开发环境存在多个版本jdk时候特别注意

```
mvn -v
```

![img](http://pic.pig4cloud.com/20190706121325_Y0LMV9_Screenshot.jpeg)

### Lombok 插件

当前你使用的ide未安装lombok. lombok能够达到的效果就是在源码中不需要写一些通用的方法，但是在编译生成的字节码文件中会帮我们生成这些方法,减少代码冗余.

[IDEA安装方法](https://blog.csdn.net/zhglance/article/details/54931430) |
[eclipse安装方法](https://blog.csdn.net/arkblue/article/details/52608213)

# 服务端代码部署





### 特别说明

请务必按照本文档部署运行章节 进行操作，减少踩坑弯路！！

### 一、服务端代码下载

```
git clone https://gitee.com/log4j/pig.git
```

### 二、配置本地hosts

[win配置方法](https://www.jb51.net/os/win10/395409.html) | [mac配置方法](https://www.jianshu.com/p/752211238c1b) | 建议使用 switchhost，开源群下载

```
# 本地测试环境  
127.0.0.1   pig-mysql
127.0.0.1   pig-redis
127.0.0.1   pig-gateway
127.0.0.1   pig-eureka
```

### 三、初始化数据库

- 参数说明

```
版本： mysql5.7+
默认字符集: utf8mb4
默认排序规则: utf8mb4_general_ci
```

- 脚本说明

```
pig/db/pig.sql
```

### 四、pig配置修改

- redis 密码配置
  pig/pig-config/src/main/resources/config/application-dev.yml

```
# redis 相关，无密码为空即可，不要修改成IP,修改hosts
spring:
  redis:
    password:
```

- 数据库密码配置
  pig/pig-config/src/main/resources/config/pigx-auth-dev.yml
  pig/pig-config/src/main/resources/config/pigx-upms-dev.yml
  pig/pig-config/src/main/resources/config/pigx-codegen-dev.yml

```
# 数据源,只需要修改密码即可，不要修改成IP,修改hosts
spring:
  datasource:
    username: root
    password: lengleng
```

### 五、启动顺序

```java
1. PigEurekaApplication   
2. PigConfigApplication  
3. PigGatewayApplication  
4. PigAuthApplication 
5. PigAdminApplication  

# 使用代码生成、监控时再启动~
6. PigCodeGenApplication  
7. PigMonitorApplication  
```

# 前端代码部署





### 特别说明

请务必按照本文档部署运行章节 进行操作，减少踩坑弯路！！

### 安装node & npm

官网下载node安装包，内置npm

```
https://nodejs.org/zh-cn/
```

### 检查安装是否正常

![img](http://pic.pig4cloud.com/20190706121205_8H0OG4_Screenshot.jpeg)

### 下载前端代码

```
git clone https://gitee.com/log4j/pig-ui.git
```

### 安装cnpm 镜像

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

### 安装依赖

```
cnpm install
```

### 启动

```
npm run dev
```

![img](http://pic.pig4cloud.com/20190706121243_i4QoZA_Screenshot.jpeg)

### 特别说明

npm install 过程中可能由于网络关系等，提示报错，请删除
pig-ui 根目录中 node_modules 重写执行 cnpm install 命令即可

# 部署视频





<https://www.bilibili.com/video/av39687329/?p=3>

# 开发契约





[Lombok 使用及其技巧说明](https://www.kancloud.cn/lengleng/pig-guide/949165)
[JAVA8的汇总资料](https://www.kancloud.cn/lengleng/pig-guide/949166)
[统一工具类使用说明](https://www.kancloud.cn/lengleng/pig-guide/949167)
[pig lambda 使用及其常用技巧汇总](https://www.kancloud.cn/lengleng/pig-guide/949168)
[pig stream api 使用及其常用技巧汇总](https://www.kancloud.cn/lengleng/pig-guide/949169)

# Lombok 使用及其技巧说明





### 为什么使用lombok

还在编写无聊枯燥又难以维护的POJO吗？ 洁癖者的春天在哪里？请看Lombok！在过往的Java项目中，充斥着太多不友好的代码：POJO的getter/setter/toString；异常处理；I/O流的关闭操作等等，这些样板代码既没有技术含量，又影响着代码的美观，Lombok应运而生。首先说明一下：任何技术的出现都是为了解决某一类问题的，如果在此基础上再建立奇技淫巧，不如回归Java本身。应该保持合理使用而不滥用。

### 如何安装

当前你使用的ide未安装lombok. lombok能够达到的效果就是在源码中不需要写一些通用的方法，但是在编译生成的字节码文件中会帮我们生成这些方法,减少代码冗余.

[IDEA安装方法](https://blog.csdn.net/zhglance/article/details/54931430) |
[eclipse安装方法](https://blog.csdn.net/arkblue/article/details/52608213)

### pig 中的使用例子，不讲常见的、技巧性的

- @AllArgsConstructor 替代@Autowired构造注入,多个bean 注入时更加清晰L

```
@Slf4j
@Configuration
@AllArgsConstructor
public class RouterFunctionConfiguration {
   private final HystrixFallbackHandler hystrixFallbackHandler;
   private final ImageCodeHandler imageCodeHandler;
   
}


@Slf4j
@Configuration
public class RouterFunctionConfiguration {
   @Autowired
   private  HystrixFallbackHandler hystrixFallbackHandler;
   @Autowired
   private  ImageCodeHandler imageCodeHandler;
}
```

- @SneakyThrows

```
@SneakyThrows
private void checkCode(ServerHttpRequest request) {
   String code = request.getQueryParams().getFirst("code");

   if (StrUtil.isBlank(code)) {
   	throw new ValidateCodeException("验证码不能为空");
   }

   redisTemplate.delete(key);
}


// 不使用就要加这个抛出
private void checkCode(ServerHttpRequest request) throws ValidateCodeException {
   String code = request.getQueryParams().getFirst("code");

   if (StrUtil.isBlank(code)) {
   	throw new ValidateCodeException("验证码不能为空");
   }
}
```

- @UtilityClass 工具类再也不用定义static的方法了，直接就可以Class.Method 使用

```
@UtilityClass
public class Utility {

    public String getName() {
        return "name";
    }
}

public static void main(String[] args) {
    System.out.println(Utility.getName());
}
```

- @CleanUp: 清理流对象,不用手动去关闭流，多么优雅

```
@Cleanup
OutputStream outStream = new FileOutputStream(new File("text.txt"));
@Cleanup
InputStream inStream = new FileInputStream(new File("text2.txt"));
byte[] b = new byte[65536];
while (true) {
   int r = inStream.read(b);
   if (r == -1) break;
   outStream.write(b, 0, r); 
}
```

### 总结

Lombok 常用的注解就那么几个，@Data 、@Getter/Setter ，Pig 使用例子中的几个可以让代码的更加优雅，建议在你的工程中使用

# JAVA8的汇总资料





| 课时数   | 课时标题                                                     | 在线播放                                                     | 源码位置                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 第 1 课  | [课程介绍](https://github.com/biezhi/learn-java8)            | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051513399&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_1.html#page=1) ¦ [Youtube](https://youtu.be/A733pQxiEDk) | 无                                                           |
| 第 2 课  | [Java 8 的发展](https://github.com/biezhi/learn-java8/blob/master/java8-growing/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051508577&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_2.html#page=2) ¦ [Youtube](https://youtu.be/fHhgm1AZzhs) | [java8-growing](https://github.com/biezhi/learn-java8/tree/master/java8-growing/src/main/java/io/github/biezhi/java8/growing) |
| 第 3 课  | [理解 lambda](https://github.com/biezhi/learn-java8/blob/master/java8-lambda/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051516241&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_3.html#page=3) ¦ [Youtube](https://youtu.be/VkdMeFEGDH8) | [lambda1](https://github.com/biezhi/learn-java8/tree/master/java8-lambda/src/main/java/io/github/biezhi/java8/lambda/lesson1) |
| 第 4 课  | [初尝 lambda](https://github.com/biezhi/learn-java8/blob/master/java8-lambda/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051511463&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_4.html#page=4) ¦ [Youtube](https://youtu.be/X7Zv5vygjTc) | [lambda2](https://github.com/biezhi/learn-java8/tree/master/java8-lambda/src/main/java/io/github/biezhi/java8/lambda/lesson2) |
| 第 5 课  | [lambda 进阶](https://github.com/biezhi/learn-java8/blob/master/java8-lambda/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051518174&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_5.html#page=5) ¦ [Youtube](https://youtu.be/3G83it4IASc) | [lambda3](https://github.com/biezhi/learn-java8/tree/master/java8-lambda/src/main/java/io/github/biezhi/java8/lambda/lesson3) |
| 第 6 课  | [默认方法的妙用](https://github.com/biezhi/learn-java8/blob/master/java8-default-methods/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051518175&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_6.html#page=6) ¦ [Youtube](https://youtu.be/sAuEnkWezDM) | [default-method](https://github.com/biezhi/learn-java8/tree/master/java8-default-methods/src/main/java/io/github/biezhi/java8/defaultmethods) |
| 第 7 课  | [干掉空指针之 Optional](https://github.com/biezhi/learn-java8/blob/master/java8-optional/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051511464&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_7.html#page=7) ¦ [Youtube](https://youtu.be/br4kqCXPB9A) | [optional](https://github.com/biezhi/learn-java8/tree/master/java8-default-methods/src/main/java/io/github/biezhi/java8/optional) |
| 第 8 课  | [理解 Stream](https://github.com/biezhi/learn-java8/blob/master/java8-stream/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051555343&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_8.html#page=8) ¦ [Youtube](https://youtu.be/NB9mGlNMl-w) | [stream](https://github.com/biezhi/learn-java8/tree/master/java8-stream/src/main/java/io/github/biezhi/java8/stream/lesson1) |
| 第 9 课  | [Stream API（上）](https://github.com/biezhi/learn-java8/blob/master/java8-stream/README.md#%E4%BD%BF%E7%94%A8%E6%B5%81) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051566020&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_9.html#page=9) ¦ [Youtube](https://youtu.be/mGwFJERNzmY) | [stream](https://github.com/biezhi/learn-java8/blob/master/java8-stream/src/main/java/io/github/biezhi/java8/stream/lesson2) |
| 第 10 课 | [Stream API（下）](https://github.com/biezhi/learn-java8/blob/master/java8-stream/README.md#collector-%E6%94%B6%E9%9B%86) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051571684&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_10.html#page=10) ¦ [Youtube](https://youtu.be/iubE0ezu-xI) | [stream](https://github.com/biezhi/learn-java8/tree/master/java8-stream/src/main/java/io/github/biezhi/java8/stream/lesson3) |
| 第 11 课 | [新的日期时间 API](https://github.com/biezhi/learn-java8/blob/master/java8-datetime-api/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051571688&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_11.html#page=11) ¦ [Youtube](https://youtu.be/hKXJvh-id1E) | [datetime](https://github.com/biezhi/learn-java8/tree/master/java8-datetime-api/src/main/java/io/github/biezhi/datetime) |
| 第 12 课 | [并发增强](https://github.com/biezhi/learn-java8/blob/master/java8-concurrent/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051682806&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_12.html#page=12) ¦ [Youtube](https://youtu.be/OYkToWIDEEI) | [concurrent](https://github.com/biezhi/learn-java8/tree/master/java8-concurrent/src/main/java/io/github/biezhi/java8/concurrent) |
| 第 13 课 | [CompletableFuture](https://github.com/biezhi/learn-java8/blob/master/java8-completablefuture/README.md) | [网易云课堂](http://study.163.com/course/courseLearn.htm?courseId=1005047049&utm_campaign=commission&utm_source=cp-400000000397038&utm_medium=share#/learn/video?lessonId=1051908792&courseId=1005047049) ¦ [哔哩哔哩](https://www.bilibili.com/video/av19287893/index_13.html#page=13) ¦ [Youtube](https://youtu.be/4reRygD1dGo) | [completablefuture](https://github.com/biezhi/learn-java8/tree/master/java8-completablefuture/src/main/java/io/github/biezhi/java8/completablefuture) |

# 统一工具类使用说明





### 统一工具类的意义

Hutool帮助我们简化每一行代码，减少每一个方法，然代码可读性、容错性更高。完整文档方便使用 [hutool-doc](https://hutool.cn/docs),避免每个开发乱引入造成辣鸡代码。

强制使用hutool工具类

### hutool 提供类哪些功能

一个Java基础工具类，对文件、流、加密解密、转码、正则、线程、XML等JDK方法进行封装，组成各种Util工具类，同时提供以下组件：

- hutool-aop JDK动态代理封装，提供非IOC下的切面支持
- hutool-bloomFilter 布隆过滤，提供一些Hash算法的布隆过滤
- hutool-cache 缓存
- hutool-core 核心，包括Bean操作、日期、各种Util等
- hutool-cron 定时任务模块，提供类Crontab表达式的定时任务
- hutool-crypto 加密解密模块
- hutool-db JDBC封装后的数据操作，基于ActiveRecord思想
- hutool-dfa 基于DFA模型的多关键字查找
- hutool-extra 扩展模块，对第三方封装（模板引擎、邮件、Servlet、二维码等）
- hutool-http 基于HttpUrlConnection的Http客户端封装
- hutool-log 自动识别日志实现的日志门面
- hutool-script 脚本执行封装，例如Javascript
- hutool-setting 功能更强大的Setting配置文件和Properties封装
- hutool-system 系统参数调用封装（JVM信息等）
- hutool-json JSON实现
- hutool-captcha 图片验证码实现
- hutool-poi 针对POI中Excel的封装
  可以根据需求对每个模块单独引入，也可以通过引入hutool-all方式引入所有模块。

### Pig 中的使用

业务模块使用 pig-common-security 的时候会自动引入
pig-common-core模块，引入最新的hutool-all 工具类

```
<!--hutool-->
<dependency>
	<groupId>cn.hutool</groupId>
	<artifactId>hutool-all</artifactId>
	<version>${hutool.version}</version>
</dependency>
```

### 使用例子

比如记录日志时候，从request获取参数的字符串

```
HttpUtil.toParams(request.getParameterMap())
```

获取当前时间

```
//当前时间，格式 yyyy-MM-dd HH:mm:ss
DateUtil.now()
```

### 个人建议

pig 在2.0 中尽量避免自己造轮子封装工具类，让代码可读性更高，所以我建议各位工程师在实际开发过程中一定要注意工具类这个问题。

# pig lambda 使用及其常用技巧汇总





## Mybatis Plus 3 的语法糖演示

```
@Override
@CacheEvict(value = "menu_details", allEntries = true)
@Transactional(rollbackFor = Exception.class)
public Boolean removeRoleById(Integer id) {
   sysRoleMenuMapper.delete(Wrappers
      .<SysRoleMenu>update().lambda()
      .eq(SysRoleMenu::getRoleId, id));
   return this.removeById(id);
}
```

## 命令式和函数式

**命令式编程**：命令“机器”如何去做事情(how)，这样不管你想要的是什么(what)，它都会按照你的命令实现。
**声明式编程**：告诉“机器”你想要的是什么(what)，让机器想出如何去做(how)。

## 什么是函数式编程？

每个人对函数式编程的理解不尽相同。 我的理解是：**在完成一个编程任务时，通过使用不可变的值或函数，对他们进行处理，然后得到另一个值的过程。**
不同的语言社区往往对各自语言中的特性孤芳自赏。现在谈 Java 程序员如何定义函数式编程还为时尚早，但是，这根本不重要！
我们关心的是如何写出好代码，而不是符合函数式编程风格的代码。

## 行为参数化

把算法的策略（行为）作为一个参数传递给函数。

## lambda 管中窥豹

- 匿名：它不像普通的方法那样有一个明确的名称：写得少而想得多！
- 函数：Lambda函数不像方法那样属于某个特定的类。但和方法一样，Lambda有参数列表、函数主体、返回类型，还可能有可以抛出的异常列表。
- 传递：Lambda表达式可以作为参数传递给方法或存储在变量中。
- 简洁：无需像匿名类那样写很多模板代码。

## 函数描述符

函数式接口的抽象方法的签名基本上就是Lambda表达式的签名，这种抽象方法叫作函数描述符。

## 函数式接口，类型推断

函数式接口定义且只定义了一个抽象方法，因为抽象方法的签名可以描述Lambda表达式的签名。
函数式接口的抽象方法的签名称为函数描述符。
所以为了应用不同的Lambda表达式，你需要一套能够描述常见函数描述符的函数式接口。

## Java 8中的常用函数式接口

| 函数式接口          | 函数描述符       | 原始类型特化                                                 |
| ------------------- | ---------------- | ------------------------------------------------------------ |
| `Predicate<T>`      | `T->boolean`     | `IntPredicate,LongPredicate, DoublePredicate`                |
| `Consumer<T>`       | `T->void`        | `IntConsumer,LongConsumer, DoubleConsumer`                   |
| `Function<T,R>`     | `T->R`           | `IntFunction<R>, IntToDoubleFunction,` `IntToLongFunction, LongFunction<R>,` `LongToDoubleFunction, LongToIntFunction,` `DoubleFunction<R>, ToIntFunction<T>,` `ToDoubleFunction<T>, ToLongFunction<T>` |
| `Supplier<T>`       | `()->T`          | `BooleanSupplier,IntSupplier, LongSupplier, DoubleSupplier`  |
| `UnaryOperator<T>`  | `T->T`           | `IntUnaryOperator, LongUnaryOperator, DoubleUnaryOperator`   |
| `BinaryOperator<T>` | `(T,T)->T`       | `IntBinaryOperator, LongBinaryOperator, DoubleBinaryOperator` |
| `BiPredicate<L,R>`  | `(L,R)->boolean` |                                                              |
| `BiConsumer<T,U>`   | `(T,U)->void`    | `ObjIntConsumer<T>, ObjLongConsumer<T>, ObjDoubleConsumer<T>` |
| `BiFunction<T,U,R>` | `(T,U)->R`       | `ToIntBiFunction<T,U>, ToLongBiFunction<T,U>, ToDoubleBiFunction<T,U>` |

## Lambdas及函数式接口的例子

| 使用案例              | Lambda 的例子                                                | 对应的函数式接口                                             |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 布尔表达式            | `(List<String> list) -> list.isEmpty()`                      | `Predicate<List<String>>`                                    |
| 创建对象              | `() -> new Project()`                                        | `Supplier<Project>`                                          |
| 消费一个对象          | `(Project p) -> System.out.println(p.getStars())`            | `Consumer<Project>`                                          |
| 从一个对象中选择/提取 | `(int a, int b) -> a * b`                                    | `IntBinaryOperator`                                          |
| 比较两个对象          | `(Project p1, Project p2) -> p1.getStars().compareTo(p2.getStars())` | `Comparator<Project> 或 BiFunction<Project,` `Project, Integer> 或 ToIntBiFunction<Project, Project>` |

## 方法引用

方法引用让你可以重复使用现有的方法定义，并像Lambda一样传递它们。

## 本节课小结

- lambda 表达式可以理解为一种匿名函数：它没有名称，但有参数列表、函数主体、返回 类型，可能还有一个可以抛出的异常的列表。
- lambda 表达式让你可以简洁地传递代码。
- 函数式接口就是仅仅声明了一个抽象方法的接口。
- 只有在接受函数式接口的地方才可以使用 lambda 表达式。
- lambda 表达式允许你直接内联，为函数式接口的抽象方法提供实现，并且将整个表达式作为函数式接口的一个实例。
- Java 8自带一些常用的函数式接口，放在 `java.util.function` 包里，包括 `Predicate<T>`、`Function<T,R>`、`Supplier<T>`、`Consumer<T>` 和 `BinaryOperator<T>`。
- Lambda表达式所需要代表的类型称为目标类型。
- 方法引用让你重复使用现有的方法实现并直接传递它们。
- `Comparator``、`Predicate`和`Function` 等函数式接口都有几个可以用来结合 lambda 表达式的默认方法。

# pig stream api 使用及其常用技巧汇总





### 什么是流？

先来看看Pig upms 中的使用

```
~~~
@Override
@Transactional(rollbackFor = Exception.class)
public Boolean saveUser(UserDTO userDto) {
   SysUser sysUser = new SysUser();
   BeanUtils.copyProperties(userDto, sysUser);
   sysUser.setDelFlag(CommonConstants.STATUS_NORMAL);
   sysUser.setPassword(ENCODER.encode(userDto.getPassword()));
   baseMapper.insert(sysUser);
   List<SysUserRole> userRoleList = userDto.getRole()
      .stream().map(roleId -> {
         SysUserRole userRole = new SysUserRole();
         userRole.setUserId(sysUser.getUserId());
         userRole.setRoleId(roleId);
         return userRole;
      }).collect(Collectors.toList());
   return sysUserRoleService.saveBatch(userRoleList);
}
~~~
```

流是Java8引入的全新概念，它用来处理集合中的数据，暂且可以把它理解为一种高级集合。
众所周知，集合操作非常麻烦，若要对集合进行筛选、投影，需要写大量的代码，而流是以声明的形式操作集合，它就像SQL语句，我们只需告诉流需要对集合进行什么操作，它就会自动进行操作，并将执行结果交给你，无需我们自己手写代码。
因此，流的集合操作对我们来说是透明的，我们只需向流下达命令，它就会自动把我们想要的结果给我们。由于操作过程完全由Java处理，因此它可以根据当前硬件环境选择最优的方法处理，我们也无需编写复杂又容易出错的多线程代码了。

### 流的特点

1. 只能遍历一次
   我们可以把流想象成一条流水线，流水线的源头是我们的数据源(一个集合)，数据源中的元素依次被输送到流水线上，我们可以在流水线上对元素进行各种操作。
   一旦元素走到了流水线的另一头，那么这些元素就被“消费掉了”，我们无法再对这个流进行操作。当然，我们可以从数据源那里再获得一个新的流重新遍历一遍。
2. 采用内部迭代方式
   若要对集合进行处理，则需我们手写处理代码，这就叫做外部迭代。
   而要对流进行处理，我们只需告诉流我们需要什么结果，处理过程由流自行完成，这就称为内部迭代。

### 流的操作种类

流的操作分为两种，分别为中间操作和终端操作。

1. 中间操作
   当数据源中的数据上了流水线后，这个过程对数据进行的所有操作都称为“中间操作”。
   中间操作仍然会返回一个流对象，因此多个中间操作可以串连起来形成一个流水线。
2. 终端操作
   当所有的中间操作完成后，若要将数据从流水线上拿下来，则需要执行终端操作。
   终端操作将返回一个执行结果，这就是你想要的数据。

### 流的操作过程

使用流一共需要三步：

1. 准备一个数据源
2. 执行中间操作
   中间操作可以有多个，它们可以串连起来形成流水线。
3. 执行终端操作
   执行终端操作后本次流结束，你将获得一个执行结果。

## 使用流

### 创建流

在使用流之前，首先需要拥有一个数据源，并通过StreamAPI提供的一些方法获取该数据源的流对象。数据源可以有多种形式：

**1. 集合**

这种数据源较为常用，通过stream()方法即可获取流对象：

```
List<Person> list = new ArrayList<Person>(); 
Stream<Person> stream = list.stream();
```

**2. 数组**

通过Arrays类提供的静态函数stream()获取数组的流对象：

```
String[] names = {"chaimm","peter","john"};
Stream<String> stream = Arrays.stream(names);
```

**3. 值**

直接将几个值变成流对象：

```
Stream<String> stream = Stream.of("chaimm","peter","john");
```

**4. 文件**

```
try(Stream lines = Files.lines(Paths.get(“文件路径名”),Charset.defaultCharset())){
    //可对lines做一些操作
}catch(IOException e){
}
```

**5. iterator**

**创建无限流**

```
Stream.iterate(0, n -> n + 2)
      .limit(10)
      .forEach(System.out::println);
```

> PS：Java7简化了IO操作，把打开IO操作放在try后的括号中即可省略关闭IO的代码。

### 筛选 filter

filter 函数接收一个Lambda表达式作为参数，该表达式返回boolean，在执行过程中，流将元素逐一输送给filter，并筛选出执行结果为true的元素。
如，筛选出所有学生：

```
List<Person> result = list.stream()
                    .filter(Person::isStudent)
                    .collect(toList());
```

### 去重distinct

去掉重复的结果：

```
List<Person> result = list.stream()
                    .distinct()
                    .collect(toList());
```

### 截取

截取流的前N个元素：

```
List<Person> result = list.stream()
                    .limit(3)
                    .collect(toList());
```

### 跳过

跳过流的前n个元素：

```
List<Person> result = list.stream()
                    .skip(3)
                    .collect(toList());
```

### 映射

对流中的每个元素执行一个函数，使得元素转换成另一种类型输出。流会将每一个元素输送给map函数，并执行map中的Lambda表达式，最后将执行结果存入一个新的流中。
如，获取每个人的姓名(实则是将Perosn类型转换成String类型)：

```
List<Person> result = list.stream()
                    .map(Person::getName)
                    .collect(toList());
```

### 合并多个流

例：列出List中各不相同的单词，List集合如下：

```
List<String> list = new ArrayList<String>();
list.add("I am a boy");
list.add("I love the girl");
list.add("But the girl loves another girl");
```

思路如下：

首先将list变成流：

```
list.stream();
```

按空格分词：

```
list.stream()
            .map(line->line.split(" "));
```

分完词之后，每个元素变成了一个String[]数组。

将每个 `String[]` 变成流：

```
list.stream()
            .map(line->line.split(" "))
            .map(Arrays::stream)
```

此时一个大流里面包含了一个个小流，我们需要将这些小流合并成一个流。

将小流合并成一个大流：用 `flatMap` 替换刚才的 map

```
list.stream()
    .map(line->line.split(" "))
    .flatMap(Arrays::stream)
```

去重

```
list.stream()
    .map(line->line.split(" "))
    .flatMap(Arrays::stream)
    .distinct()
    .collect(toList());
```

### 是否匹配任一元素：anyMatch

anyMatch用于判断流中是否存在至少一个元素满足指定的条件，这个判断条件通过Lambda表达式传递给anyMatch，执行结果为boolean类型。
如，判断list中是否有学生：

```
boolean result = list.stream()
            .anyMatch(Person::isStudent);
```

### 是否匹配所有元素：allMatch

allMatch用于判断流中的所有元素是否都满足指定条件，这个判断条件通过Lambda表达式传递给anyMatch，执行结果为boolean类型。
如，判断是否所有人都是学生：

```
boolean result = list.stream()
            .allMatch(Person::isStudent);
```

### 是否未匹配所有元素：noneMatch

noneMatch与allMatch恰恰相反，它用于判断流中的所有元素是否都不满足指定条件：

```
boolean result = list.stream()
            .noneMatch(Person::isStudent);
```

### 获取任一元素findAny

findAny能够从流中随便选一个元素出来，它返回一个Optional类型的元素。

```
Optional<Person> person = list.stream().findAny();
```

### 获取第一个元素findFirst

```
Optional<Person> person = list.stream().findFirst();
```

### 归约

归约是将集合中的所有元素经过指定运算，折叠成一个元素输出，如：求最值、平均数等，这些操作都是将一个集合的元素折叠成一个元素输出。

在流中，reduce函数能实现归约。
reduce函数接收两个参数：

1. 初始值
2. 进行归约操作的Lambda表达式

**元素求和：自定义Lambda表达式实现求和**

例：计算所有人的年龄总和

```
int age = list.stream().reduce(0, (person1,person2)->person1.getAge()+person2.getAge());
```

1. reduce的第一个参数表示初试值为0；
2. reduce的第二个参数为需要进行的归约操作，它接收一个拥有两个参数的Lambda表达式，reduce会把流中的元素两两输给Lambda表达式，最后将计算出累加之和。

**元素求和：使用Integer.sum函数求和**

上面的方法中我们自己定义了Lambda表达式实现求和运算，如果当前流的元素为数值类型，那么可以使用Integer提供了sum函数代替自定义的Lambda表达式，如：

```
int age = list.stream().reduce(0, Integer::sum);
```

Integer类还提供了 `min`、`max` 等一系列数值操作，当流中元素为数值类型时可以直接使用。

### 数值流的使用

采用reduce进行数值操作会涉及到基本数值类型和引用数值类型之间的装箱、拆箱操作，因此效率较低。
当流操作为纯数值操作时，使用数值流能获得较高的效率。

**将普通流转换成数值流**

StreamAPI提供了三种数值流：IntStream、DoubleStream、LongStream，也提供了将普通流转换成数值流的三种方法：mapToInt、mapToDouble、mapToLong。
如，将Person中的age转换成数值流：

```
IntStream stream = list.stream().mapToInt(Person::getAge);
```

**数值计算**

每种数值流都提供了数值计算函数，如max、min、sum等。如，找出最大的年龄：

```
OptionalInt maxAge = list.stream()
                                .mapToInt(Person::getAge)
                                .max();
```

由于数值流可能为空，并且给空的数值流计算最大值是没有意义的，因此max函数返回OptionalInt，它是Optional的一个子类，能够判断流是否为空，并对流为空的情况作相应的处理。
此外，mapToInt、mapToDouble、mapToLong进行数值操作后的返回结果分别为：OptionalInt、OptionalDouble、OptionalLong

## 中间操作和收集操作

| 操作        | 类型 | 返回类型      | 使用的类型/函数式接口    | 函数描述符       |
| ----------- | ---- | ------------- | ------------------------ | ---------------- |
| `filter`    | 中间 | `Stream<T>`   | `Predicate<T>`           | `T -> boolean`   |
| `distinct`  | 中间 | `Stream<T>`   |                          |                  |
| `skip`      | 中间 | `Stream<T>`   | long                     |                  |
| `map`       | 中间 | `Stream<R>`   | `Function<T, R>`         | `T -> R`         |
| `flatMap`   | 中间 | `Stream<R>`   | `Function<T, Stream<R>>` | `T -> Stream<R>` |
| `limit`     | 中间 | `Stream<T>`   | long                     |                  |
| `sorted`    | 中间 | `Stream<T>`   | `Comparator<T>`          | `(T, T) -> int`  |
| `anyMatch`  | 终端 | `boolean`     | `Predicate<T>`           | `T -> boolean`   |
| `noneMatch` | 终端 | `boolean`     | `Predicate<T>`           | `T -> boolean`   |
| `allMatch`  | 终端 | `boolean`     | `Predicate<T>`           | `T -> boolean`   |
| `findAny`   | 终端 | `Optional<T>` |                          |                  |
| `findFirst` | 终端 | `Optional<T>` |                          |                  |
| `forEach`   | 终端 | `void`        | `Consumer<T>`            | `T -> void`      |
| `collect`   | 终端 | `R`           | `Collector<T, A, R>`     |                  |
| `reduce`    | 终端 | `Optional<T>` | `BinaryOperator<T>`      | `(T, T) -> T`    |
| `count`     | 终端 | `long`        |                          |                  |

## Collector 收集

收集器用来将经过筛选、映射的流进行最后的整理，可以使得最后的结果以不同的形式展现。
`collect` 方法即为收集器，它接收 `Collector` 接口的实现作为具体收集器的收集方法。
`Collector` 接口提供了很多默认实现的方法，我们可以直接使用它们格式化流的结果；也可以自定义 `Collector` 接口的实现，从而定制自己的收集器。

### 归约

流由一个个元素组成，归约就是将一个个元素“折叠”成一个值，如求和、求最值、求平均值都是归约操作。

### 一般性归约

若你需要自定义一个归约操作，那么需要使用 `Collectors.reducing` 函数，该函数接收三个参数：

- 第一个参数为归约的初始值
- 第二个参数为归约操作进行的字段
- 第三个参数为归约操作的过程

## 汇总

Collectors类专门为汇总提供了一个工厂方法：`Collectors.summingInt`。
它可接受一 个把对象映射为求和所需int的函数，并返回一个收集器；该收集器在传递给普通的 `collect` 方法后即执行我们需要的汇总操作。

### 分组

数据分组是一种更自然的分割数据操作，分组就是将流中的元素按照指定类别进行划分，类似于SQL语句中的 `GROUPBY`。

### 多级分组

多级分组可以支持在完成一次分组后，分别对每个小组再进行分组。
使用具有两个参数的 `groupingBy` 重载方法即可实现多级分组。

- 第一个参数：一级分组的条件
- 第二个参数：一个新的 `groupingBy` 函数，该函数包含二级分组的条件

**Collectors 类的静态工厂方法**

| 工厂方法            | 返回类型               | 用途                                                         | 示例                                                         |
| ------------------- | ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `toList`            | `List<T>`              | 把流中所有项目收集到一个 List                                | `List<Project> projects = projectStream.collect(toList());`  |
| `toSet`             | `Set<T>`               | 把流中所有项目收集到一个 Set，删除重复项                     | `Set<Project> projects = projectStream.collect(toSet());`    |
| `toCollection`      | `Collection<T>`        | 把流中所有项目收集到给定的供应源创建的集合                   | `Collection<Project> projects = projectStream.collect(toCollection(), ArrayList::new);` |
| `counting`          | `Long`                 | 计算流中元素的个数                                           | `long howManyProjects = projectStream.collect(counting());`  |
| `summingInt`        | `Integer`              | 对流中项目的一个整数属性求和                                 | `int totalStars = projectStream.collect(summingInt(Project::getStars));` |
| `averagingInt`      | `Double`               | 计算流中项目 Integer 属性的平均值                            | `double avgStars = projectStream.collect(averagingInt(Project::getStars));` |
| `summarizingInt`    | `IntSummaryStatistics` | 收集关于流中项目 Integer 属性的统计值，例如最大、最小、 总和与平均值 | `IntSummaryStatistics projectStatistics = projectStream.collect(summarizingInt(Project::getStars));` |
| `joining`           | `String`               | 连接对流中每个项目调用 toString 方法所生成的字符串           | `String shortProject = projectStream.map(Project::getName).collect(joining(", "));` |
| `maxBy`             | `Optional<T>`          | 按照给定比较器选出的最大元素的 Optional， 或如果流为空则为 Optional.empty() | `Optional<Project> fattest = projectStream.collect(maxBy(comparingInt(Project::getStars)));` |
| `minBy`             | `Optional<T>`          | 按照给定比较器选出的最小元素的 Optional， 或如果流为空则为 Optional.empty() | `Optional<Project> fattest = projectStream.collect(minBy(comparingInt(Project::getStars)));` |
| `reducing`          | 归约操作产生的类型     | 从一个作为累加器的初始值开始，利用 BinaryOperator 与流中的元素逐个结合，从而将流归约为单个值 | `int totalStars = projectStream.collect(reducing(0, Project::getStars, Integer::sum));` |
| `collectingAndThen` | 转换函数返回的类型     | 包含另一个收集器，对其结果应用转换函数                       | `int howManyProjects = projectStream.collect(collectingAndThen(toList(), List::size));` |
| `groupingBy`        | `Map<K, List<T>>`      | 根据项目的一个属性的值对流中的项目作问组，并将属性值作 为结果 Map 的键 | `Map<String,List<Project>> projectByLanguage = projectStream.collect(groupingBy(Project::getLanguage));` |
| `partitioningBy`    | `Map<Boolean,List<T>>` | 根据对流中每个项目应用断言的结果来对项目进行分区             | `Map<Boolean,List<Project>> vegetarianDishes = projectStream.collect(partitioningBy(Project::isVegetarian));` |

### 转换类型

有一些收集器可以生成其他集合。比如前面已经见过的 `toList`，生成了 `java.util.List` 类的实例。
还有 `toSet` 和 `toCollection`，分别生成 `Set` 和 `Collection` 类的实例。
到目前为止， 我已经讲了很多流上的链式操作，但总有一些时候，需要最终生成一个集合——比如：

- 已有代码是为集合编写的，因此需要将流转换成集合传入；
- 在集合上进行一系列链式操作后，最终希望生成一个值；
- 写单元测试时，需要对某个具体的集合做断言。

使用 `toCollection`，用定制的集合收集元素

```
stream.collect(toCollection(TreeSet::new));
```

还可以利用收集器让流生成一个值。 `maxBy` 和 `minBy` 允许用户按某种特定的顺序生成一个值。

### 数据分区

分区是分组的特殊情况：由一个断言（返回一个布尔值的函数）作为分类函数，它称分区函数。
分区函数返回一个布尔值，这意味着得到的分组 `Map` 的键类型是 `Boolean`，于是它最多可以分为两组: true是一组，false是一组。

分区的好处在于保留了分区函数返回true或false的两套流元素列表。

### 并行流

并行流就是一个把内容分成多个数据块，并用不不同的线程分别处理每个数据块的流。最后合并每个数据块的计算结果。

将一个顺序执行的流转变成一个并发的流只要调用 `parallel()` 方法

```
public static long parallelSum(long n){
    return Stream.iterate(1L, i -> i +1).limit(n).parallel().reduce(0L,Long::sum);
}
```

将一个并发流转成顺序的流只要调用 `sequential()` 方法

```
stream.parallel().filter(...).sequential().map(...).parallel().reduce();
```

这两个方法可以多次调用，只有最后一个调用决定这个流是顺序的还是并发的。

并发流使用的默认线程数等于你机器的处理器核心数。

通过这个方法可以修改这个值，这是全局属性。

```
System.setProperty("java.util.concurrent.ForkJoinPool.common.parallelism", "12");
```

并非使用多线程并行流处理数据的性能一定高于单线程顺序流的性能，因为性能受到多种因素的影响。
如何高效使用并发流的一些建议：

1. 如果不确定， 就自己测试。
2. 尽量使用基本类型的流 IntStream, LongStream, DoubleStream
3. 有些操作使用并发流的性能会比顺序流的性能更差，比如limit，findFirst，依赖元素顺序的操作在并发流中是极其消耗性能的。findAny的性能就会好很多，应为不依赖顺序。
4. 考虑流中计算的性能(Q)和操作的性能(N)的对比, Q表示单个处理所需的时间，N表示需要处理的数量，如果Q的值越大, 使用并发流的性能就会越高。
5. 数据量不大时使用并发流，性能得不到提升。
6. 考虑数据结构：并发流需要对数据进行分解，不同的数据结构被分解的性能时不一样的。

**流的数据源和可分解性**

| 源                | 可分解性 |
| ----------------- | -------- |
| `ArrayList`       | 非常好   |
| `LinkedList`      | 差       |
| `IntStream.range` | 非常好   |
| `Stream.iterate`  | 差       |
| `HashSet`         | 好       |
| `TreeSet`         | 好       |

**流的特性以及中间操作对流的修改都会对数据对分解性能造成影响。 比如固定大小的流在任务分解的时候就可以平均分配，但是如果有filter操作，那么流就不能预先知道在这个操作后还会剩余多少元素。**

**考虑终端操作的性能：如果终端操作在合并并发流的计算结果时的性能消耗太大，那么使用并发流提升的性能就会得不偿失。**

# 网关功能





[网关限流使用](https://www.kancloud.cn/lengleng/pig-guide/949171)
[网关降级处理](https://www.kancloud.cn/lengleng/pig-guide/949172)
[路由转发配置](https://www.kancloud.cn/lengleng/pig-guide/949173)

# 网关限流使用





### POM 依赖

这里一定要注意，是网关引入的redis-reactive，背压模式的redis。

```
<!--基于 reactive stream 的redis -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis-reactive</artifactId>
</dependency>
```

#### 配置按照请求IP 的限流

```
spring:
  cloud:
    gateway:
      routes:
      - id: requestratelimiter_route
        uri: lb://pigx-upms
        order: 10000
        predicates:
        - Path=/admin/**
        filters:
        - name: RequestRateLimiter
          args:
            redis-rate-limiter.replenishRate: 1  # 令牌桶的容积
            redis-rate-limiter.burstCapacity: 3  # 流速 每秒
            key-resolver: "#{@remoteAddrKeyResolver}" #SPEL表达式去的对应的bean
        - StripPrefix=1
```

- 配置bean，多维度限流量的入口 对应上边key-resolver 【我自己哦

```
/**
* 自定义限流标志的key，多个维度可以从这里入手
* exchange对象中获取服务ID、请求信息，用户信息等
*/
@Bean
KeyResolver remoteAddrKeyResolver() {
    return exchange -> Mono.just(exchange.getRequest().getRemoteAddress().getHostName());
}
```

OK 完成。

#### 压力测试

并发5个线程。
![image](http://a.pig4cloud.com/jmeter.png)

#### Redis 数据变化

我们使用redis的**monitor** 命令，实时查看redis 的操作情况。
会发现在redis中会操作两个key

- request_rate_limiter.{xxx}.timestamp
- request_rate_limiter.{xxx}.tokens
  ![image](http://a.pig4cloud.com/redis_monitor.png)

### 实现原理

![image](http://a.pig4cloud.com/uml111.png)

Spring Cloud Gateway 默认实现 Redis限流，如果扩展只需要实现ratelimter接口即可。

### RedisRateLimter 的核心代码，判断是否取到令牌的实现，通过调用 redis的LUA 脚本。

```
public Mono<Response> isAllowed(String routeId, String id) {
	Config routeConfig = getConfig().getOrDefault(routeId, defaultConfig);
	int replenishRate = routeConfig.getReplenishRate();
	int burstCapacity = routeConfig.getBurstCapacity();

	try {
		List<String> keys = getKeys(id);
		returns unixtime in seconds.
		List<String> scriptArgs = Arrays.asList(replenishRate + "", burstCapacity + "",
				Instant.now().getEpochSecond() + "", "1");
		// 这里是核心，执行redis 的LUA 脚本。
		Flux<List<Long>> flux =
		this.redisTemplate.execute(this.script, keys, scriptArgs);
		return flux.onErrorResume(throwable -> Flux.just(Arrays.asList(1L, -1L)))
				.reduce(new ArrayList<Long>(), (longs, l) -> {
					longs.addAll(l);
					return longs;
				}) .map(results -> {
					boolean allowed = results.get(0) == 1L;
					Long tokensLeft = results.get(1);

					Response response = new Response(allowed, getHeaders(routeConfig, tokensLeft));

					if (log.isDebugEnabled()) {
						log.debug("response: " + response);
					}
					return response;
				});
	}
	catch (Exception e) {
		log.error("Error determining if user allowed from redis", e);
	}
	return Mono.just(new Response(true, getHeaders(routeConfig, -1L)));
}
```

#### LUA 脚本

![image](http://a.pig4cloud.com/lua.png)

# 网关降级处理





### 网关降级

当网关流量向后转发的时候，如果微服务模块不可用，则会触发降级事件

### Pig 中的使用讲解，以UPMS路由配置为例

```
spring:
  cloud:
    gateway:
      locator:
        enabled: true
      routes:
      #UPMS 模块
      - id: pig-upms      # 唯一的服务ID
        uri: lb://pig-upms # 注册中心的服务名称，实现负载均衡
        predicates:
        - Path=/admin/**  #所有业务的请求前缀
        filters:
        - name: Hystrix           #断路器降级策略
          args:
            name: default
            fallbackUri: 'forward:/fallback' # 降级接口的地址
```

### 原理

Spring Cloud Gateway 会自动寻找配置Hystrix的Filter，这个功能是内置的，然后回调我们提供fallbackUri,Pig 中的降级接口是使用weblflux 实现的

- 降级业务很简单，输出那个接口的异常日志

```java
@Slf4j
@Component
public class HystrixFallbackHandler implements HandlerFunction<ServerResponse> {
	@Override
	public Mono<ServerResponse> handle(ServerRequest serverRequest) {
		Optional<Object> originalUris = serverRequest.attribute(GATEWAY_ORIGINAL_REQUEST_URL_ATTR);

		originalUris.ifPresent(originalUri -> log.error("网关执行请求:{}失败,hystrix服务降级处理", originalUri));

		return ServerResponse.status(HttpStatus.INTERNAL_SERVER_ERROR.value())
			.contentType(MediaType.TEXT_PLAIN).body(BodyInserters.fromObject("服务异常"));
	}
}
```

- 降级入口。这里的意思类似于SpringMVC 定义一个 @GetMapping("/fallback") 接口

```java
@Slf4j
@Configuration
@AllArgsConstructor
public class RouterFunctionConfiguration {
	private final HystrixFallbackHandler hystrixFallbackHandler;
	private final ImageCodeHandler imageCodeHandler;

	@Bean
	public RouterFunction routerFunction() {
		return RouterFunctions.route(
			RequestPredicates.path("/fallback")
				.and(RequestPredicates.accept(MediaType.TEXT_PLAIN)), hystrixFallbackHandler)
	}

}
```

# 路由转发配置





### Spring Cloud Gateway

Pig 2.0 采用的是spring官方的网关组件，通过异步背压的高性能网关。
路由配置是整个微服务中最为核心的功能

### 配置路由

我们以UPMS 的路由为例子，注意注释

```
spring:
  cloud:
    gateway:
      locator:
        enabled: true
      routes:
      #UPMS 模块
      - id: pig-upms      # 唯一的服务ID
        uri: lb://pig-upms # 注册中心的服务名称，实现负载均衡
        predicates:
        - Path=/admin/**  #所有业务的请求前缀
        filters:
          # 限流配置
        - name: RequestRateLimiter    #限流策略           args:
            key-resolver: '#{@remoteAddrKeyResolver}'
            redis-rate-limiter.replenishRate: 10
            redis-rate-limiter.burstCapacity: 20
          # 降级配置
        - name: Hystrix           #断路器降级策略
          args:
            name: default
            fallbackUri: 'forward:/fallback'
```

### pig 默认提供了全局的路由过滤器原理

PigRequestGlobalFilter,对全部的微服务提供了安全过滤（这个后边会讲）和全局StripPrefix=1配置，**意味着你在使用Pig的时候，网关转发到业务模块时候会自动截取前缀，不用再每个微服务路由配置了StripPrefixFilter**

```java
public class PigRequestGlobalFilter implements GlobalFilter, Ordered {
	private static final String HEADER_NAME = "X-Forwarded-Prefix";

	@Override
	public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
		// 1. 清洗请求头中from 参数
		ServerHttpRequest request = exchange.getRequest().mutate()
			.headers(httpHeaders -> httpHeaders.remove(SecurityConstants.FROM))
			.build();

		// 2. 重写StripPrefix
		addOriginalRequestUrl(exchange, request.getURI());
		String rawPath = request.getURI().getRawPath();
		String newPath = "/" + Arrays.stream(StringUtils.tokenizeToStringArray(rawPath, "/"))
			.skip(1L).collect(Collectors.joining("/"));
		ServerHttpRequest newRequest = request.mutate()
			.path(newPath)
			.build();
		exchange.getAttributes().put(GATEWAY_REQUEST_URL_ATTR, newRequest.getURI());

		return chain.filter(exchange.mutate()
			.request(newRequest.mutate()
				.build()).build());
	}

	@Override
	public int getOrder() {
		return -1000;
	}
}
```

# 资源服务器配置





![img](http://pic.pig4cloud.com/20190220201356_PnWmp5_Screenshot.jpeg)

### 继承BaseResourceServerConfigurerAdapter即可实现接入oauth2

### 重写configure方法的意义

BaseResourceServerConfigurerAdapter提供了两种解析用户信息的方法

- 不获取用户详细 只有用户名

```
	protected void notGetUser(ResourceServerSecurityConfigurer resources) {
		DefaultAccessTokenConverter accessTokenConverter = new DefaultAccessTokenConverter();
		DefaultUserAuthenticationConverter userTokenConverter = new DefaultUserAuthenticationConverter();
		accessTokenConverter.setUserTokenConverter(userTokenConverter);

		remoteTokenServices.setRestTemplate(lbRestTemplate());
		remoteTokenServices.setAccessTokenConverter(accessTokenConverter);
		resources.authenticationEntryPoint(resourceAuthExceptionEntryPoint)
			.accessDeniedHandler(pigAccessDeniedHandler)
			.tokenServices(remoteTokenServices);
	}
```

- 上下文中获取用户全部信息，两次调用userDetailsService，影响性能

```
	private void canGetUser(ResourceServerSecurityConfigurer resources) {
		DefaultAccessTokenConverter accessTokenConverter = new DefaultAccessTokenConverter();
		DefaultUserAuthenticationConverter userTokenConverter = new DefaultUserAuthenticationConverter();
		userTokenConverter.setUserDetailsService(userDetailsService);
		accessTokenConverter.setUserTokenConverter(userTokenConverter);

		remoteTokenServices.setRestTemplate(lbRestTemplate());
		remoteTokenServices.setAccessTokenConverter(accessTokenConverter);
		resources.authenticationEntryPoint(resourceAuthExceptionEntryPoint)
			.accessDeniedHandler(pigAccessDeniedHandler)
			.tokenServices(remoteTokenServices);
	}
```

### 总结

- 这里也就是为什么SecurityUtils.getUser 有时候返回为空的原因。
- 默认（不重写）是可以换成全部信息，建议不重写；特殊接口为了追求QPS可以重写。

# 获取当前用户信息





### 获取当前用户

SecurityUtils.getUser()

```
public PigUser getUser(Authentication authentication) {
	Object principal = authentication.getPrincipal();
	if (principal instanceof PigUser) {
		return (PigUser) principal;
	}
	return null;
}
```

### 为什么CodenGen 获取用户为空

当在CodeGen模块，通过SecurityUtils.getUser() 的返回值始终为null,因为CodeGen重写了资源服务的配置,不通过pig获取用户信息提高性能
ResourceServerConfigurer

```
@Configuration
@EnableResourceServer
@AllArgsConstructor
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class ResourceServerConfigurer extends BaseResourceServerConfigurerAdapter {

	/**
	 * 重写抽象类实现，不需要调用feign 获取 userDetailsService
	 *
	 * @param resources
	 */
	@Override
	public void configure(ResourceServerSecurityConfigurer resources) {
		notGetUser(resources);
	}
}
```

可以提供一个获取用户名的方法

```
public String getUsername(Authentication authentication) {
	Object principal = authentication.getPrincipal();
	return principal.toString();
}
```

资源服务器配置章节会详细讲重写和不重写两个的区别

# API直接对外暴露





## 现象

如果微服务接入了资源服务器，那么全部的资源被spring security oauth 拦截，如果没有合法token 直接会被拒绝。
如下图,提示如下错误。
![img](http://pic.pig4cloud.com/20190220194244_ZKCblx_Screenshot.jpeg)

## 服务暴露

- 直接在对应微服务模块配置

```
ignore:
  urls:
    - 目标借口的Ant表达式即可
```

![img](http://pic.pig4cloud.com/20190220194439_rfhfV6_Screenshot.jpeg)

# token有效期及其个性化





## Token 有效期说明

```
 // 默认刷新token 的有效期
  private int refreshTokenValiditySeconds = 60 * 60 * 24 * 30; // default 30 days.
  // 默认token 的有效期
  private int accessTokenValiditySeconds = 60 * 60 * 12; // default 12 hours.
```

每个终端配置为空，去默认的时间设置 刷新token 30天，令牌12小时。
前端使用的客户端是pig，设置令牌失效等。
![img](http://pic.pig4cloud.com/20190220191931_N6Wv79_Screenshot.jpeg)

## 个性化Token 目的

- 默认通过调用 /oauth/token 返回的报文格式包含以下参数

```
{
    "access_token": "e6669cdf-b6cd-43fe-af5c-f91a65041382",
    "token_type": "bearer",
    "refresh_token": "da91294d-446c-4a89-bdcf-88aee15a75e8",
    "expires_in": 43199, 
    "scope": "server"
}
```

并没包含用户的业务信息比如用户信息、租户信息等。

- 扩展生成包含业务信息（如下）,避免系统多次调用，直接可以通过认证接口获取到用户信息等，大大提高系统性能

```
{
    "access_token":"a6f3b6d6-93e6-4eb8-a97d-3ae72240a7b0",
    "token_type":"bearer",
    "refresh_token":"710ab162-a482-41cd-8bad-26456af38e4f",
    "expires_in":42396,
    "scope":"server",
    "tenant_id":1,
    "license":"made by pigx",
    "dept_id":1,
    "user_id":1,
    "username":"admin"
}
```

## 密码模式生成Token 源码解析

![image](https://ws1.sinaimg.cn/large/007xHoylly1g09p76vupsj30l60cn416.jpg)

 主页参考红框部分

- ResourceOwnerPasswordTokenGranter （密码模式）根据用户的请求信息，进行认证得到当前用户上下文信息

  ```
  protected OAuth2Authentication getOAuth2Authentication(ClientDetails client, TokenRequest tokenRequest) {
      Map<String, String> parameters = new LinkedHashMap<String, String>(tokenRequest.getRequestParameters());
  	String username = parameters.get("username");
  	String password = parameters.get("password");
  	// Protect from downstream leaks of password
  	parameters.remove("password");
      Authentication userAuth = new UsernamePasswordAuthenticationToken(username, password);
     ((AbstractAuthenticationToken) userAuth).setDetails(parameters);
  		
      userAuth = authenticationManager.authenticate(userAuth);
  
      OAuth2Request storedOAuth2Request =  getRequestFactory().createOAuth2Request(client, tokenRequest);		
  		return new OAuth2Authentication(storedOAuth2Request, userAuth);
  }
  ```

- 然后调用AbstractTokenGranter.getAccessToken() 获取OAuth2AccessToken

  ```
  protected OAuth2AccessToken getAccessToken(ClientDetails client, TokenRequest tokenRequest) {
     return tokenServices.createAccessToken(getOAuth2Authentication(client, tokenRequest));
  }
  ```

- 默认使用DefaultTokenServices来获取token

  ```
  public OAuth2AccessToken createAccessToken(OAuth2Authentication authentication) throws AuthenticationException {
  
  	... 一系列判断 ，合法性、是否过期等判断	
  	OAuth2AccessToken accessToken = createAccessToken(authentication, refreshToken);
  		tokenStore.storeAccessToken(accessToken, authentication);
  		// In case it was modified
  		refreshToken = accessToken.getRefreshToken();
  		if (refreshToken != null) {
  			tokenStore.storeRefreshToken(refreshToken, authentication);
  		}
  		return accessToken;
  }
  ```

- createAccessToken 核心逻辑

  ```
  // 默认刷新token 的有效期
  private int refreshTokenValiditySeconds = 60 * 60 * 24 * 30; // default 30 days.
  // 默认token 的有效期
  private int accessTokenValiditySeconds = 60 * 60 * 12; // default 12 hours.
  
  private OAuth2AccessToken createAccessToken(OAuth2Authentication authentication, OAuth2RefreshToken refreshToken) {
      DefaultOAuth2AccessToken token = new DefaultOAuth2AccessToken(uuid);
      token.setExpiration(Date)
      token.setRefreshToken(refreshToken);
      token.setScope(authentication.getOAuth2Request().getScope());
      return accessTokenEnhancer != null ? accessTokenEnhancer.enhance(token, authentication) : token;
  }
  ```

  如上代码，在拼装好token对象后会调用认证服务器配置TokenEnhancer( 增强器) 来对默认的token进行增强。

- TokenEnhancer.enhance 通过上下文中的用户信息来个性化Token

  ```java
  public OAuth2AccessToken enhance(OAuth2AccessToken accessToken, OAuth2Authentication authentication) {
      final Map<String, Object> additionalInfo = new HashMap<>(8);
      PigxUser pigxUser = (PigxUser) authentication.getUserAuthentication().getPrincipal();
      additionalInfo.put("user_id", pigxUser.getId());
      additionalInfo.put("username", pigxUser.getUsername());
      additionalInfo.put("dept_id", pigxUser.getDeptId());
      additionalInfo.put("tenant_id", pigxUser.getTenantId());
      additionalInfo.put("license", SecurityConstants.PIGX_LICENSE);
      ((DefaultOAuth2AccessToken) accessToken).setAdditionalInformation(additionalInfo);
      return accessToken;
  }
  ```

# 服务间鉴权及其token 传递





## 客户端带Token 情况

1. 如下图客户端携带token访问A服务。
2. A服务通过FeginClient 调用B服务获取相关依赖数据。
3. 所以只要带token 访问A 无论后边链路有多长 ABCD 都可以获取当前用户信息
4. 权限需要有这些整个链路接口的全部权限才能成功

![img](http://pic.pig4cloud.com/20190220195248_W5WBhh_token%E4%BC%A0%E9%80%92.jpeg)

## 核心代码

fein 拦截器将本服务的token 通过copyToken的形式传递给下游服务

```
public class PigFeignClientInterceptor extends OAuth2FeignRequestInterceptor {

	@Override
	public void apply(RequestTemplate template) {
		Collection<String> fromHeader = template.headers().get(SecurityConstants.FROM);
		if (CollUtil.isNotEmpty(fromHeader) && fromHeader.contains(SecurityConstants.FROM_IN)) {
			return;
		}

		accessTokenContextRelay.copyToken();
		if (oAuth2ClientContext != null
			&& oAuth2ClientContext.getAccessToken() != null) {
			super.apply(template);
		}
	}
}
```

### 无token请求，服务内部发起情况处理。

![img](http://pic.pig4cloud.com/20190220195955_nDy07g_to.jpeg)

很多情况下，比如定时任务。A服务并没有token 去请求B服务，pig也对这种情况进行了兼容。类似于A对外暴露API，但是又安全限制。参考日志插入情况

- FeignClient 需要带一个请求token,FROM_IN 声明是内部调用

```
remoteLogService.saveLog(sysLog, SecurityConstants.FROM_IN);
```

- 参考API 对外暴露章节对外暴露目标接口

```
ignore:
  urls:
    - 目标借口的Ant表达式即可
```

- 目标接口对内外调用进行限制
  @Inner 注解，这样就避免接口对外暴露的安全问题。只能通过内部调用才能使用，浏览器不能直接访问该接口

```
	@Inner
	@PostMapping
	public R save(@Valid @RequestBody SysLog sysLog) {
		return new R<>(sysLogService.save(sysLog));
	}
```

### 后边会专门讲@Inner 注解

# postman等多终端接口调用





### 通过网关访问auth-server 获取access-token

- 请求地址为 <http://pig:9999/auth/oauth/token>
- headr参数为： Authorization Basic dGVzdDp0ZXN0， 这里为Base64(test:test),只能使用test终端，其他终端需要输验证码，可以参考 验证码处理章节
  ![img](http://pic.pig4cloud.com/20190220193045_WO4FXU_Screenshot.jpeg)
- 参数如下
  ![img](http://pic.pig4cloud.com/20190220193128_xICRpK_Screenshot.jpeg)

### 通过access-token 访问受保护的资源

![img](http://pic.pig4cloud.com/20190220193607_82J9x6_Screenshot.jpeg)

### 刷新token

- 请求接口通获取token接口一致，header参数一致
  ![img](http://pic.pig4cloud.com/20190220193837_cgrdQp_Screenshot.jpeg)
- 注意grant_type refresh_token
  ![img](http://pic.pig4cloud.com/20190220193926_VU9Xag_Screenshot.jpeg)

# pig生成token 详解





## pig的Oauth2.0认证流程详解

### Spring Security OAuth核心类图解析

关于Oauth2是什么以及Oauth2的四种授权模式请移步[Oauth2官网](https://oauth.net/2/)。

下面简单介绍一下关于Spring Security OAuth基本的原理。这也是理解pigx的第一步。

下面这张图涉及到了Spring OAuth的一些核心类和接口。

不多说，直接上图。

![20189104922](http://oss1.pig4cloud.com/20189104922.png)

上图蓝色的方块代表执行过程中调用的具体的类，绿色的方块代表整个执行流程中调用的类，绿色的括号中代表的是该接口调用的具体的实现类。

整个流程的入口点是在**TokenEndpoint**，由它来处理获取令牌的请求，获取令牌的请求默认是**/oauth/token**这个路径。

- 当TokenEndpoint收到请求时，它首先会调用ClientDetailsService,ClientDetaisService从名字上看就很可以知道是一个类似于UserDetailsService的接口，只不过UserDetailsService读取的是用户的信息，而ClientDetailsService读取的是第三方应用的信息。

- pigx会在**登录请求**头中带上Client的信息，而这个类就可以做到根据ClientId读取相应的配置信息。而ClientDetailsSevice读取到的信息都会封装到ClientDetails这个对象中。

- 同时，TokenEndpoint还会创建一个TokenRequests的对象，这个对象中封装了除了第三方应用以外的其他信息。比如说grant_type，scope,username,password(限密码模式)等等信息，而这些信息都是封装在TokenRequests里面的。同时，ClientDetails也会被放到TokenRequests中，因为第三方应用的信息也是令牌请求的一部分。

- 之后利用TokenRequests去调用一个叫做TokenGranter的令牌授权者的接口，这个接口其实是对四种不同的授权模式进行的一个封装。在这个接口里，它会根据请求传递过来的grant_type去挑一个具体的实现来执行令牌生成的逻辑。

- 不论采用哪种方式进行令牌的生成，在这个生成的过程中都会产生两个对象，一个是OAuth2Request,这个对象实际上是之前的ClientDetails和TokenRequests这两个对象的一个整合。另一个Authorization封装的实际上是当前授权用户的一些信息，也就是谁在进行授权行为，Authorization里封装的就是谁的信息。这里的用户信息是通过UserDetailsService进行读取的。

- OAuth2Request和Authorization这两个对象组合起来，会形成一个OAuth2Authorization对象，而这个最终产生的对象它的里面就包含了当前是哪个第三方应用在请求哪个用户以哪种授权模式（包括授权过程中的一些其他参数）进行授权，也就是这个对象会汇总之前的几个对象的信息都会封装到OAuth2Authorization这个对象中。

- 然后这个对象会传递到一个叫做AuthorizationServerTokenServices的接口的实现类，它拿到OAuth2Authorization中所有的信息之后最终会生成一个OAuth2的令牌OAuth2AccessToken。

  **Tips:** 个性化token生成

  **AuthorizationServerTokenServices**的接口的默认实现DefaultTokenServices中包含着其他两个接口的引用，TokenStore是用来定制token存储策略的，pigx用它实现了往redis里存放token,TokenEnhancer是token的增强器,pigx用它实现了返回的token的信息的增强。

### Spring Security OAuth的令牌生成过程————以pigx的登录过程为例

### 前期准备

光说不练假把式，下面我们结合pigx项目代码，来验证一下上面的过程。目前代码采用的是2018年9月1日最新的开发分支上的代码做演示，选择1.5.0的稳定版来复现以下的过程问题应该也不大，这部分逻辑最近几个版本也没啥变化。

首先启动核心的五个工程：注册中心，配置中心，认证中心，网关以及统一用户管理中心，同时启动前端工程以**避免跨域问题**。同时，为了避免影响测试结果请**先在redis-cli上执行flushall或者flushdb清空redis**。

个人建议萌新可以通过访问http://127.0.0.1:9999/swagger-ui.html,通过swagger上面的Authorization按钮进行登录，我这里选择和作者视频里相同的curl的方式进行登录。

### 开始学习

#### 客户端选择

我选择的应用是test,因为这个应用可以忽略验证码，关于这一块的配置可以参考pigx-gateway-dev.yml这个配置文件的ignore.clients属性，它可以接收一个想要忽略验证码的客户端的列表。至于为什么配置了这里的属性就可以忽略验证码也很简单。

网关工程有一个FilterIgnorePropertiesConfig类，这个类当配置文件里的ignore属性不为空时会生效。而验证码过滤器会对FilterIgnorePropertiesConfig中配置的客户端进行放行。如下所示:

```
// 终端设置不校验， 直接向下执行(1. 从请求参数中获取 2.从header取)
String clientId = request.getQueryParams().getFirst("client_id");
if (StrUtil.isNotBlank(clientId)) {
    if (filterIgnorePropertiesConfig.getClients().contain(clientId)) {
        return chain.filter(exchange);
    }
}
```

能够获取到token的姿势有很多，我这里就选择一种类似pigx前端工程登录的方式。

#### 前端密码加解密讲解

pigx大致的请求流程就是前端通过vue-router（模拟nginx）发送请求到后台网关，网关再根据配置的路由规则转发到各个微服务上。

根据pigx-gateway-dev.yml上的配置,可知经过认证中心的请求都需要经过两个过滤器，一个是验证码的处理，一个是将加密过的密码解密的过滤器。

```
routes:
# 认证中心
- id: pigx-auth
uri: lb://pigx-auth
predicates:
- Path=/auth/**
filters:
    # 验证码处理
- ImageCodeGatewayFilter
    # 前端密码解密
- PasswordDecoderFilter
- StripPrefix=1
```

验证码的过滤器已经被我们干掉了，密码解密的过滤器我这边不想处理，就直接网上搜个在线加密的链接手动加密了,我用的是这个[在线AES加密解密、AES在线加密解密、AES encryption and decryption](http://tool.chacuo.net/cryptaes)。

AES作为对称加密的方式，前后端的加解密方式肯定是一致的，我们先看看后端的解密逻辑，之后再看看前端的加密逻辑做验证。后端的解密逻辑位于PasswordDecoderFilter这个类中，解密的代码不长，如下：

```
/* 
 * AES/CBC/NoPadding 要求
 * 密钥必须是16字节长度的；Initialization vector (IV) 必须是16字节
 * 待加密内容的字节长度必须是16的倍数，如果不是16的倍数，就会出如下异常：
 * javax.crypto.IllegalBlockSizeException: Input length not multiple of 16 bytes
 * 
 *  由于固定了位数，所以对于被加密数据有中文的, 加、解密不完整
 *  
 *  可 以看到，在原始数据长度为16的整数n倍时，假如原始数据长度等于16*n，则使用NoPadding时加密后数据长度等于16*n，
 *  其它情况下加密数据长 度等于16*(n+1)。在不足16的整数倍的情况下，假如原始数据长度等于16*n+m[其中m小于16]，
 *  除了NoPadding填充之外的任何方 式，加密数据长度都等于16*(n+1).
 */
	
private static final String PASSWORD = "password";
private static final String KEY_ALGORITHM = "AES";
private static final String DEFAULT_CIPHER_ALGORITHM = "AES/CBC/NOPadding";
@Value("${security.encode.key:1234567812345678}")
private String encodeKey;

private static String decryptAES(String data, String pass) throws Exception {
    Cipher cipher = Cipher.getInstance(DEFAULT_CIPHER_ALGORITHM);
    SecretKeySpec keyspec = new SecretKeySpec(pass.getBytes(), KEY_ALGORITHM);
    IvParameterSpec ivspec = new IvParameterSpec(pass.getBytes());
    cipher.init(Cipher.DECRYPT_MODE, keyspec, ivspec);
    byte[] result = cipher.doFinal(Base64.decode(data.getBytes(CharsetUtil.UTF_8)));
    return new String(result, CharsetUtil.UTF_8);
}
```

Value注解是将配置文件中的security.encode.key的值作为参数注入，当这个参数不存在时，就会使用冒号后面的默认值1234567812345678，当然，在pigx的配置文件中这个参数值是肯定存在的，正是pigxpigxpigxpigx。这段解密逻辑说的就是采用AES的CBC加密方式，填充方式为零填充，密码和偏移量都是卸载配置文件中的pigxpigxpigxpigx。

接着我们去找一下前端的加密逻辑验证一下我们的判断，前端的加密逻辑位于util/util.js中，核心的加密代码如下:

```
/**
 * 加密处理
 */
export const encryption = (params) => {
    let {
        data,
        type,
        param,
        key
    } = params
    const result = JSON.parse(JSON.stringify(data))
    if (type === 'Base64') {
        param.forEach(ele => {
            result[ele] = btoa(result[ele])
        })
    } else {
        param.forEach(ele => {
            var data = result[ele]
            key = CryptoJS.enc.Latin1.parse(key)
            var iv = key
                // 加密
            var encrypted = CryptoJS.AES.encrypt(
                data,
                key, {
                    iv: iv,
                    mode: CryptoJS.mode.CBC,
                    padding: CryptoJS.pad.ZeroPadding
                })
            result[ele] = encrypted.toString()
        })
    }
    return result
}
```

我们可以很显然地看到，加密采用的正式无填充的CBC模式，偏移量就是传入的加密密钥，零填充，这个和后端的代码是一致的，所以我们可以大胆地在上面地网站上填入参数了，填写的参数如下：

![2018918137](http://oss1.pig4cloud.com/2018918137.png)

好了，密文：rKu1/348LvKp0rsVC06eCA==我们拿到了。

#### 构造请求参数

接着我们开始吧。

```
 curl -H "Authorization:Basic dGVzdDp0ZXN0" -d "username=admin&password=rKu1/348LvKp0rsVC06eCA==&grant_type=password&scope=server" http://localhost:8000/auth/oauth/token
```

通过curl构造以上的链接，这个链接中包含着请求头的信息，请求头是一个"Basic"加一个空格加"clientId:clientSecret"base64化的一个**Authorization**字段，请求的参数里包含了grant_type和scope以及在password模式下必须的username和password字段。顺带一提，如果是windows中文语言的系统建议执行命令：

```
chcp 65001
```

将你的shell临时的更换为UTF-8的编码避免中文乱码的问题，虽然生成token的过程中不涉及中文化的操作，但如果后期扩展了中文化可以避免问题。

下面的是一个标准的POST请求并且在URL中携带参数的请求，但是这个请求不符合我们这边测试的要求，原因看下面的注意事项。

```
 curl -H "Authorization:Basic dGVzdDp0ZXN0" -X POST http://localhost:8000/auth/oauth/token?username=admin&password=rKu1/348LvKp0rsVC06eCA==&grant_type=password&scope=server
```

所以我们把它改造一下。

```
 curl -H "Authorization:Basic dGVzdDp0ZXN0" -X POST http://localhost:8000/auth/oauth/token?username=admin\&password=rKu1/348LvKp0rsVC06eCA%3D%3D\&grant_type=password\&scope=server
```

回车以后我们可以看到首先会经过网关的密码解密过滤器,并且参数经过我们的一通改造之后已经可以获取到正确的值了。

![20189192927](http://oss1.pig4cloud.com/20189192927.png)

**注意:**
这个`url.getRawQuery()`方法会获取拼接到请求的URL后面的参数，这也是为什么我们之前构造的curl格式不是标准的把数据放入POST请求的请求体中的原因，标准的做法如下：

```
 curl -H "Authorization:Basic dGVzdDp0ZXN0" -d "username=admin&password=rKu1/348LvKp0rsVC06eCA==&grant_type=password&scope=server" http://localhost:8000/auth/oauth/token
```

但是这种方式会有问题，在这套密码解密过滤器的机制下将会获取不到任何的参数。而会出现这个问题的原因也正是因为这73行的代码。

![20189184037](http://oss1.pig4cloud.com/20189184037.png)

不过Spring的OAuth2.0本身是支持把数据放入POST请求体中的这种方式的。

**Tips:**

URL中用于拼接多个参数的符号:"&",在shell脚本中有特殊的意义（以daemon运行）,所以要在"&"前加上反斜杠""转义一下。

**Tips:**

URL中"="这个符号具有特殊的含义,可能在服务器端无法获得正确的参数值，所以我们也要用"%3D"转义一下。

继续我们刚才的过程，可以看到在密码解密过滤器接收到参数之后，就很简单了，整个密码解密过滤器的作用就是**对登录请求中发送过来的加密密码进行解密的操作**。我们直接看解密的结果。

![20189193358](http://oss1.pig4cloud.com/20189193358.png)

解密的结果对于不足16位的密码会填充空格到16位，trim之后我们就可以看到得到我们真正想要的密码"123456"了，这也侧面验证了我们之前生成的密码策略是正确的。

#### 认证过程详解

经过上面的一通操作，我们已经拿到了获取token的一些必要的请求了。clientId,clientSecret,grant_type,usename,password,scope,终于可以带着我们的参数深入源码啦！

**这里结合上文提到的核心类图来看效果更好**

上文提过,OAuth2.0的认证的入口点位于TokenEndPoint。我们也可以看到，代码确实已经进来了。

![201891105014](http://oss1.pig4cloud.com/201891105014.png)

我们可以看到这个类上有一个`@RequestMapping`注解，它来处理`/oauth/token`的POST请求。

1. 进来之后的第一步，就是在代码的95行，获取请求头中的clientId。
2. 然后在96行调用`getClientDetailsService().loadClientByClientId(clientId)`方法获取整个第三方应用的详细配置。

**扩展：**

第三方应用有非常丰富的配置项,如图所示：

![201891105839](http://oss1.pig4cloud.com/201891105839.png)

具体的参数的意义可以看[spring-oauth-server 数据库表说明](http://andaily.com/spring-oauth-server/db_table_description.html)

1. 在拿到客户端的信息之后在代码的98行通过传递进来的参数和查询出来的第三方应用信息构建TokenRequest。

创建TokenRequest的代码很简单，如下：

```
public TokenRequest createTokenRequest(Map<String, String> requestParameters, ClientDetails authenticatedClient) {

    String clientId = requestParameters.get(OAuth2Utils.CLIENT_ID);
    if (clientId == null) {
        // if the clientId wasn't passed in in the map, we add pull it from the authenticated client object
        clientId = authenticatedClient.getClientId();
    }
    else {
        // otherwise, make sure that they match
        if (!clientId.equals(authenticatedClient.getClientId())) {
            throw new InvalidClientException("Given client ID does not match authenticated client");
        }
    }
    String grantType = requestParameters.get(OAuth2Utils.GRANT_TYPE);

    Set<String> scopes = extractScopes(requestParameters, clientId);
    TokenRequest tokenRequest = new TokenRequest(requestParameters, clientId, scopes, grantType);

    return tokenRequest;
}
```

所以其实它就干了一件事，校验传递进来clientId和查询出来的clientId,如果匹配的话，就根据之前传递进来的clientId和和查询出来的第三方应用构建TokenRequest。

然后我们就拿到TokenRequest了，后面的代码很简单了:

![201891111934](http://oss1.pig4cloud.com/201891111934.png)

无非就是对下面这些参数的校验：

- clientId:是否有值，值是否和查询结果匹配
- scope:请求的一些授权内容，所请求的授权必须是第三方应用可以发送的授权集合的子集，否则无法通过校验)
- grant_type:必须显式指定按照哪种授权模式获取令牌
- 判断传递的授权模式是否是简化模式，如果是简化模式也会抛异常。因为简化模式其实是对授权码模式的一种简化:在用户的第一步的授权行为的时候就直接返回令牌,所以是不会有调用请求令牌服务的机会的
- 判断是不是授权码模式,因为授权码模式包含两个步骤，在授权码模式中发出的令牌中拥有的权限不是由发令牌的请求决定的，而是在发令牌之前的授权的请求里就已经决定好了。因此它会对请求过来的scope进行置空操作，然后根据之前发出去的授权码里的权限重新设置你的scope,因此它根本不会使用请求令牌的这个请求中携带的scope参数。
- 之后判断是不是刷新令牌的请求,应为刷新令牌的请求有自己的scope，所以也会进行重新设置scope的操作。

经过一系列的校验之后，最终TokenRequest会在132行传递给TokenGranter，然后由granter产生最终的accessToken。之后直接将accessToken写入响应里就可以了。

TokenGranter中总共封装了四种授权模式加一个刷新令牌的操作，我们看看其中的一些细节。

![201891114811](http://oss1.pig4cloud.com/201891114811.png)

CompositeTokenGranter中有一个集合，这个集合里封装着的就是五个会产生令牌的操作。

它会对遍历这五种情况，并根据之前请求中携带的grant_type在五种情况中挑一种进行最终的accessToken的生成。

然后我们看这个代码的第38行的具体的`grant`方法。
![201891115533](http://oss1.pig4cloud.com/201891115533.png)

![20189112212](http://oss1.pig4cloud.com/20189112212.png)

首先在org.springframework.security.oauth2.provider.token.AbstractTokenGranter中判断当前携带的授权类型和这个类所支持的授权类型是否匹配，如果不匹配就返回空值，如果匹配的话就进行令牌的生成操作。

59到第63行是重新获取一下clientId和客户端信息跟授权类型再做一个校验,67行的`getAccessToken`方法会产生最终的一个令牌。

这个方法也非常简单:

```
protected OAuth2AccessToken getAccessToken(ClientDetails client, TokenRequest tokenRequest) {
    return tokenServices.createAccessToken(getOAuth2Authentication(client, tokenRequest));
}
```

它实际上就是对tokenServices的一个调用，而tokenSerives其实就是从37行我们可以看到其实就是AuthorizationServerTokenServices。这个类要想创建accessToken需要一个OAuth2Authentication对象，所以createAccessToken中包含了一个方法`getOAuth2Authentication`。

这个方法不同的授权模式会有不同的实现。

![201891121611](http://oss1.pig4cloud.com/201891121611.png)

在**Spring Security OAuth核心类图解析**中我们已经知道最终产生的Oauth2Authorization包含两部分信息,一部分是请求中的一些信息，另一部分是根据请求获取的授权用户的信息。而在不同的授权模式下获取授权用户的信息的方式是不同的，比如说pigx所使用的密码模式就是使用请求中携带的用户名和密码来获取当前授权用户中的授权信息,而在授权码模式的两个步骤中是根据第一步发出授权码的同时会记录相关用户的信息，之后对第二步进行授权的时候根据第三方应用请求过来的授权码再读取该授权码对应的用户信息。所以getOAuth2Authentication对于不同的授权类型有不同的实现。

我们以pigx所使用的密码模式继续下面的流程。密码模式对应的是`org.springframework.security.oauth2.provider.password.ResourceOwnerPasswordTokenGranter`

![201891123119](http://oss1.pig4cloud.com/201891123119.png)

而这个方法我们可以看到它其实就是根据所请求的用户名和密码去创建UsernamePasswordAuthenticationToken,然后传递给authenticationManager做认证，在这个认证过程中它会去调用`com.pig4cloud.pigx.common.security.service.PigxUserDetailsServiceImpl`的`loadUserByUsername`方法，根据用户名和密码去读取用户的信息,之后我们其实就已经拿到Authorization的信息，而Oauth2Request根据第85行我们可以知道是根据传进来的第三方应用详情和tokenRequest产生出来的,而86行的`OAuth2Authentication`也是由`Oauth2Request`和`Authorization`这两个对象拼接起来的。而拼接的方式就是调用
`org.springframework.security.oauth2.provider.request.DefaultOAuth2RequestFactory`的`createOAuth2Request`方法。

```
public OAuth2Request createOAuth2Request(ClientDetails client, TokenRequest tokenRequest) {
    return tokenRequest.createOAuth2Request(client);
}
```

这个方法最终会创建一个由clientDetails和tokenRequest组合而成的OAuth2Request。

![201891125353](http://oss1.pig4cloud.com/201891125353.png)

拿到`OAuth2Request`就可以去生成`OAuth2Authentication`了。

而`OAuth2Authentication`就是`org.springframework.security.oauth2.provider.token.AbstractTokenGranter`第71到73行最终传递进去生成accessToken的对象。

而OAuth2Authentications生成成功之后进行返回的话就可以执行`AuthorizationServerTokenServices`的`createAccessToken`方法，而一旦这个access token生成成功并写入响应进行返回那么整个流程也就结束了，最终我们就拿到了想要的访问令牌。

```
protected OAuth2AccessToken getAccessToken(ClientDetails client, TokenRequest tokenRequest) {
    return tokenServices.createAccessToken(getOAuth2Authentication(client, tokenRequest));
}
```

具体创建accessToken的代码，我们需要仔细读一读`org.springframework.security.oauth2.provider.token.DefaultTokenServices`的`createAccessToken`方法。

![2018911396](http://oss1.pig4cloud.com/2018911396.png)

首先这个类一进来就会尝试在tokenStore中获取accessToken,因为同一个用户只要令牌没过期那么再次请求令牌的时候会把之前发送的令牌再次发还。因此一开始就会找当前用户已经存在的令牌。

如果已经发送的令牌不为空,那么会在87行判断当前的令牌是否已经过期,如果令牌过期了，那么就会在tokenStore里把accessToken和refreshToken一起删掉,如果令牌没过期，那么就把这个没过期的令牌重新再存一下。因为可能用户是使用另外的方式来访问令牌的，比如说一开始用授权码模式，后来用密码模式,而这两种模式需要存的信息是不一样的,所以这个令牌要重新store一次。之后直接返回这个不过期的令牌。

如果令牌已经过期了或者说这个是第一次请求，令牌压根没生成，就会走下面的逻辑。

![201891132620](http://oss1.pig4cloud.com/201891132620.png)

首先看看刷新的令牌有没有，如果刷新的令牌没有的话，那么创建一枚刷新的令牌。然后在121行根据authentication, refreshToken创建accessToken。而这个创建accessToken的方法也非常简单：

```
private OAuth2AccessToken createAccessToken(OAuth2Authentication authentication, OAuth2RefreshToken refreshToken) {
    DefaultOAuth2AccessToken token = new DefaultOAuth2AccessToken(UUID.randomUUID().toString());
    int validitySeconds = getAccessTokenValiditySeconds(authentication.getOAuth2Request());
    if (validitySeconds > 0) {
        token.setExpiration(new Date(System.currentTimeMillis() + (validitySeconds * 1000L)));
    }
    token.setRefreshToken(refreshToken);
    token.setScope(authentication.getOAuth2Request().getScope());

    return accessTokenEnhancer != null ? accessTokenEnhancer.enhance(token, authentication) : token;
}
```

OAuth2AccessToken其实就是用UUID创建一个accessToken,然后把过期时间，刷新令牌和scope这些OAuth协议规定的必须要存在的参数设置上，设置完了以后它会判断是否存在tokenEnhancer，如果存在tokenEnhancer它就会按照定制的**tokenEnhancer**增强生成出来的token。

拿到返回的令牌之后，在122行tokenStore会把拿到的令牌存起来,然后拿refreshToken存起来，最后把生成的令牌返回回去。

于是我们就获取到了令牌。

![201891133652](http://oss1.pig4cloud.com/201891133652.png)

**扩展:**

pigx对于查询JdbcClientDetailsService中的查询语句做了一些增强，为什么要做增强，下面来简单分析一下。

首先我们看用于处理认证的pigx-auth工程的WebSecurityConfigurer这个配置类中创建的是如下的一个PasswordEncoder：

```
@Bean
public PasswordEncoder passwordEncoder() {
    return PasswordEncoderFactories.createDelegatingPasswordEncoder();
}
```

这个类是Spring Security5新出的一个类，列出了SpringSecurity5支持的所有的密码匹配器。

```
public static PasswordEncoder createDelegatingPasswordEncoder() {
    String encodingId = "bcrypt";
    Map<String, PasswordEncoder> encoders = new HashMap<>();
    encoders.put(encodingId, new BCryptPasswordEncoder());
    encoders.put("ldap", new LdapShaPasswordEncoder());
    encoders.put("MD4", new Md4PasswordEncoder());
    encoders.put("MD5", new MessageDigestPasswordEncoder("MD5"));
    encoders.put("noop", NoOpPasswordEncoder.getInstance());
    encoders.put("pbkdf2", new Pbkdf2PasswordEncoder());
    encoders.put("scrypt", new SCryptPasswordEncoder());
    encoders.put("SHA-1", new MessageDigestPasswordEncoder("SHA-1"));
    encoders.put("SHA-256", new MessageDigestPasswordEncoder("SHA-256"));
    encoders.put("sha256", new StandardPasswordEncoder());

    return new DelegatingPasswordEncoder(encodingId, encoders);
}
```

具体创建密码编码器的过程也展示了要求的新密码的格式：

```
public class DelegatingPasswordEncoder implements PasswordEncoder {
    //密码匹配器id的前缀
	private static final String PREFIX = "{";
    //密码匹配器id的后缀
	private static final String SUFFIX = "}";
    //密码匹配器的类型
	private final String idForEncode;
	private final PasswordEncoder passwordEncoderForEncode;
	private final Map<String, PasswordEncoder> idToPasswordEncoder;


	/**
	 * 密码的格式匹配不上就会报错，相信每个人港升级的时候都经历过There is no PasswordEncoder mapped for the id “null”的绝望吧！
	 */
	private class UnmappedIdPasswordEncoder implements PasswordEncoder {

		@Override
		public String encode(CharSequence rawPassword) {
			throw new UnsupportedOperationException("encode is not supported");
		}

		@Override
		public boolean matches(CharSequence rawPassword,
			String prefixEncodedPassword) {
			String id = extractId(prefixEncodedPassword);
			throw new IllegalArgumentException("There is no PasswordEncoder mapped for the id \"" + id + "\"");
		}
	}
}
```

这个类就要求了密码必须符合带上{"具体的解密器id"}，最后根据这个id去找密码匹配器匹配，
clientSecret最终也是要参与解码的，所以它也需要带上{"id"},clientSecret我们并不需要做什么艰深的加密，所以使用原始密码就行，这个解密器就是NoOpPasswordEncoder，它的id从上文我们看到是"noop",也就是说数据库里的clientSecret要想在Spring Security5下正常工作，clientId应该是`test`clientSecret应该是`{noop}test`,但是我们可以看到数据库里存储的都是`test/test`那为什么进行解密的时候没有抛出PasswordEncoder mapped for the id “null”的异常呢？

原因很简单。

在`com.pig4cloud.pigx.common.core.constant.SecurityConstants`查询客户端信息的语句中，我们可以看到{noop}这个字段在查询出来注入JdbcClientDetailsService之前，作者已经利用Mysql的连接函数帮我们拼接好了。

```
String CLIENT_FIELDS = "client_id, CONCAT('{noop}',client_secret) as client_secret, resource_ids, scope, "
		+ "authorized_grant_types, web_server_redirect_uri, authorities, access_token_validity, "
		+ "refresh_token_validity, additional_information, autoapprove";
```

同样巧妙的设定也体现在了用户密码的加密上。
在upms模块的UserController模块中，作者显式指定了密码解密器为BCryptPasswordEncoder。

```
@Slf4j
@Service
@AllArgsConstructor
public class SysUserServiceImpl extends ServiceImpl<SysUserMapper, SysUser> implements SysUserService {
	private static final PasswordEncoder ENCODER = new BCryptPasswordEncoder();
	private final SysMenuService sysMenuService;
	private final SysUserMapper sysUserMapper;
	private final SysRoleService sysRoleService;
	private final SysUserRoleService sysUserRoleService;
	private final SysDeptRelationService sysDeptRelationService;
    // 其他代码省略
}
```

**Tips:**

为什么都声明成final级别变量，要结合上面的lombok的`@AllArgsConstructor`注解来看，其实就是为了使用Lombok的黑科技进行构造器注入，这也是Spring 5 推荐的一种注入方式。

但是很显然，这种密码解密器直接参与进Spring Security5的执行流程又会报喜闻乐见的There is no PasswordEncoder mapped for the id “null”错误，那么为什么没报呢？见代码的`com.pig4cloud.pigx.common.security.service.PigxUserDetailsServiceImpl`类的getUserDetails方法：

```
/**
    * 构建userdetails
    *
    * @param result 用户信息
    * @return
    */
private UserDetails getUserDetails(R<UserInfo> result) {
    if (result == null || result.getData() == null) {
        throw new UsernameNotFoundException("用户不存在");
    }

    UserInfo info = result.getData();
    Set<String> dbAuthsSet = new HashSet<>();
    if (ArrayUtil.isNotEmpty(info.getRoles())) {
        // 获取角色
        Arrays.stream(info.getRoles()).forEach(role -> dbAuthsSet.add(SecurityConstants.ROLE + role));
        // 获取资源
        dbAuthsSet.addAll(Arrays.asList(info.getPermissions()));

    }
    Collection<? extends GrantedAuthority> authorities
        = AuthorityUtils.createAuthorityList(dbAuthsSet.toArray(new String[0]));
    SysUser user = info.getSysUser();
    boolean enabled = StrUtil.equals(user.getDelFlag(), CommonConstant.STATUS_NORMAL);
    // 构造security用户

    return new PigxUser(user.getUserId(), user.getDeptId(), user.getUsername(), SecurityConstants.BCRYPT + user.getPassword(), enabled,
        true, true, true, authorities);
}
```

见构造security用户的部分，作者在构造Security的User对象进行认证之前，进行了和处理clientSecret类似的操作，手动拼接了"{bcrypt}"的字符。

作者的这两个操作，据我个人推测,应该是为了保证和Spring Security 4.x的密码格式的兼容性，隐藏密码变更的细节。

# pig CheckToken过程讲解





## CheckToken的目的

当用户携带token 请求资源服务器的资源时, **OAuth2AuthenticationProcessingFilter** 拦截token，进行token 和userdetails 过程，把无状态的token 转化成用户信息。

![image](http://a.pig4cloud.com/20190125162610.png)

## 详解

1. OAuth2AuthenticationManager.authenticate()，filter执行判断的入口
   ![image](http://a.pig4cloud.com/20190125160252.png)
2. 当用户携带token 去请求微服务模块，被资源服务器拦截调用RemoteTokenServices.loadAuthentication ,执行所谓的check-token过程。
   源码如下
   ![image](http://a.pig4cloud.com/20190125150127.png)
3. CheckToken 处理逻辑很简单，就是调用redisTokenStore 查询token的合法性，及其返回用户的部分信息 （username ）

![image](http://a.pig4cloud.com/20190125150237.png)

1. 继续看 返回给 RemoteTokenServices.loadAuthentication 最后一句
   tokenConverter.extractAuthentication 解析组装服务端返回的信息

![image](http://a.pig4cloud.com/20190125150335.png)
最重要的 userTokenConverter.extractAuthentication(map);

1. 最重要的一步，是否判断是否有userDetailsService实现，如果有 的话去查根据 返回的
   username 查询一次全部的用户信息，没有实现直接返回username，这也是很多时候问的为什么只能查询到username 也就是 EnablePigxResourceServer.details true 和false 的区别。

![image](http://a.pig4cloud.com/20190125150416.png)

1. 那根据的你问题，继续看 UerDetailsServiceImpl.loadUserByUsername 根据用户名去换取用户全部信息。
   ![image](http://a.pig4cloud.com/20190125150620.png)

# pig扩展支持oauth2客户端模式





客户端模式，没有具体用户信息，只有客户的client-id 信息，完成不了upms 的RBAC，现有认证中心不支持放发token。

怎么支持认证中心发放token，有了token ，我其他的微服务不用upms 是否可以？ 当然
AuthorizationServerConfig.java 修改token 增强逻辑，如果为客户端模式就不进行增强，即不维护用户信息。

```
	/**
	 * token增强，客户端模式不增强。
	 *
	 * @return TokenEnhancer
	 */
	@Bean
	public TokenEnhancer tokenEnhancer() {
		return (accessToken, authentication) -> {
			if (SecurityConstants.CLIENT_CREDENTIALS
					.equals(authentication.getOAuth2Request().getGrantType())) {
				return accessToken;
			}

			final Map<String, Object> additionalInfo = new HashMap<>(8);
			PigxUser pigxUser = (PigxUser) authentication.getUserAuthentication().getPrincipal();
			additionalInfo.put("user_id", pigxUser.getId());
			additionalInfo.put("username", pigxUser.getUsername());
			additionalInfo.put("dept_id", pigxUser.getDeptId());
			additionalInfo.put("tenant_id", pigxUser.getTenantId());
			additionalInfo.put("license", SecurityConstants.PIGX_LICENSE);
			((DefaultOAuth2AccessToken) accessToken).setAdditionalInformation(additionalInfo);
			return accessToken;
		};
	}
```

即可方法令牌了，只是这个令牌只有客户端信息。
为何不增强参考 源码DefaultTokenServices

```
	private OAuth2AccessToken createAccessToken(OAuth2Authentication authentication, OAuth2RefreshToken refreshToken) {
		DefaultOAuth2AccessToken token = new DefaultOAuth2AccessToken(UUID.randomUUID().toString());
		int validitySeconds = getAccessTokenValiditySeconds(authentication.getOAuth2Request());
		if (validitySeconds > 0) {
			token.setExpiration(new Date(System.currentTimeMillis() + (validitySeconds * 1000L)));
		}
		token.setRefreshToken(refreshToken);
		token.setScope(authentication.getOAuth2Request().getScope());

		return accessTokenEnhancer != null ? accessTokenEnhancer.enhance(token, authentication) : token;
	}
```

不修改，没有用户信息再去调用原有增强逻辑会报错。

# pig 扩展实现开放平台





本文单纯从简单的技术实现来讲，不涉及开放平台的多维度的运营理念。

## 什么是开放平台

通过开放自己平台产品服务的各种API接口，让其他第三方开发者在开发应用时根据需求直接调用，例如微信登录、QQ登录、微信支付、微博登录、热门等。
让第三方应用通过开发平台，使得自身海量数据资源得到沉淀（变现）
目前国内主流的网站的的开放平台，都是基于oauth2.0 协议进行做的开放平台

- 微信开放平台授权机制流程图

![img](http://pic.pig4cloud.com/20190409211723_sc4akR_Screenshot.jpeg)

- 微博开放平台授权机制流程图
  ![img](http://www.sinaimg.cn/blog/developer/wiki/oAuth2_01.gif)

## oauth2.0 授权码模式

授权码模式（authorization code）是功能最完整、流程最严密的授权模式。 它的特点就是通过客户端的后台服务器，与"服务提供商"的认证服务器进行互动,能够满足绝大多数开放平台认证授权的需求。
![img](https://box.kancloud.cn/2015-09-11_55f287e751a7a.png)

### 引入相关依赖

```
<dependency>
         <groupId>org.springframework.cloud</groupId>
         <artifactId>spring-cloud-starter-oauth2</artifactId>
 </dependency>
 
<dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-security</artifactId>
</dependency>
```

### 配置认证服务器

通过内存模式，初始化一个支持授权码模式的客户端

```
@Configuration
@AllArgsConstructor
@EnableAuthorizationServer
public class AuthorizationServerConfig extends AuthorizationServerConfigurerAdapter {

	@Override
	@SneakyThrows
	public void configure(ClientDetailsServiceConfigurer clients) {
		clients.inMemory()
				.withClient("pigx") // client_id
				.secret("pigx") // client_secret
				.authorizedGrantTypes("authorization_code") // 该client允许的授权类型
				.scopes("app"); // 允许的授权范围
	}
}
```

### 初步完成，测试一下

注意这里是 /oauth/authorize 不是 /oauth/token 接口，只需要带 client_id 即可。

```
localhost:9999/oauth/authorize?client_id=pigx&response_type=code&redirect_uri=https://pig4cloud.com
```

- 先进行basic 登录，默认用户user,密码已经打在控制台自己查即可
  ![img](http://pic.pig4cloud.com/20190409214134_9i7UDQ_Screenshot.jpeg)
- 授权确认
  ![img](http://pic.pig4cloud.com/20190409220222_k14sh4_Screenshot.jpeg)
- 登录成功带着code回调到目标接口
  ![img](http://pic.pig4cloud.com/20190409215127_XiQHtj_Screenshot.jpeg)
- 通过/oauth/token获取登录令牌

简单的几步就完成上图微信或者其他网站的授权流程，不过目前为止 略显简陋

1. 登录没有界面，用户密码数据库没有报错
2. 确认授权界面太丑，没有个性化

### 配置安全登录

- 配置未登录拦截重定向到 *loginPage*
- 配置登录完成提交的页面路径 这里会被spring security 接管

```
@Primary
@Order(90)
@Configuration
public class WebSecurityConfigurer extends WebSecurityConfigurerAdapter {
	@Override
	@SneakyThrows
	protected void configure(HttpSecurity http) {
		http
			.formLogin()
			.loginPage("/token/login")
			.loginProcessingUrl("/token/form")
			.and()
			.authorizeRequests()
			.anyRequest().authenticated();
	}
}
```

### 认证服务器配置用户加载规则实现

```
@Override
public void configure(AuthorizationServerEndpointsConfigurer endpoints) {
	endpoints.userDetailsService(pigxUserDetailsService)
}

// 通过这步去加载数据的用户名密码
public interface UserDetailsService {
    UserDetails loadUserByUsername(String var1) throws UsernameNotFoundException;
}
```

### 重写原有认证页面

默认逻辑/oauth/confirm_access，让他重定向到我们自己的路径，然后进行个性哈

```
@Override
	public void configure(AuthorizationServerEndpointsConfigurer endpoints) {
		endpoints
				.userDetailsService(pigxUserDetailsService)
				.pathMapping("/oauth/confirm_access", "/token/confirm_access")
	}
```

获取上下文中的授权信息，传给前端

```
	/**
	 * 确认授权页面
	 *
	 * @param request
	 * @param session
	 * @param modelAndView
	 * @return
	 */
	@GetMapping("/confirm_access")
	public ModelAndView confirm(HttpServletRequest request, HttpSession session, ModelAndView modelAndView) {
		Map<String, Object> scopeList = (Map<String, Object>) request.getAttribute("scopes");
		modelAndView.addObject("scopeList", scopeList.keySet());

		Object auth = session.getAttribute("authorizationRequest");
		if (auth != null) {
			AuthorizationRequest authorizationRequest = (AuthorizationRequest) auth;
			ClientDetails clientDetails = clientDetailsService.loadClientByClientId(authorizationRequest.getClientId());
			modelAndView.addObject("app", clientDetails.getAdditionalInformation());
			modelAndView.addObject("user", SecurityUtils.getUser());
		}

		modelAndView.setViewName("ftl/confirm");
		return modelAndView;
	}
```

## 最终效果

- 把用户头像等信息展示出来就蛮好看了
  ![img](http://pic.pig4cloud.com/20190409223622_C5nhJV_Screenshot.jpeg)

# pig服务端配置跨域





## PigX Gateway

### 网关跨域支持

> 如果不知道什么是跨域(CORS)，建议先阅读以下内容
>
> [跨域资源共享 CORS 详解](http://www.ruanyifeng.com/blog/2016/04/cors.html)
>
> [HTTP访问控制（CORS）](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Access_control_CORS)

#### 配置方式

在网关的配置文件中加入以下内容(请根据实际情况修改)

```
spring:
  cloud:
    gateway:
      globalcors:
        corsConfigurations:
          '[/**]':
            allowCredentials: true
            exposedHeaders: "Content-Disposition,Content-Type,Cache-Control"
            allowedHeaders: "*"
            allowedOrigins: "*"
            allowedMethods: "*"
```

> - 以上配置可作为开发环境使用，生成环境建议你根据实际情况修改（请先理解CORS，并参考`org.springframework.cloud.gateway.config.GlobalCorsProperties`）
> - 跨域时会产生预检请求(Pre-Flight Request)，这样就会对你的服务器产生额外的网络请求。如果可以通过部署手段解决跨域，则可以关闭跨域支持，方法是把以上配置信息清理掉。

#### 测试

为了演示跨域支持效果，可以修改一下前端项目(`PigX-ui`)的登录代码

```
export const loginByUsername = (username, password, code, randomStr) => {
  const grant_type = 'password'

  return request({
    // 原来的API接口地址
    //url: '/auth/oauth/token',
    // 为了触发造跨域，直接修改为网关的url,这里的IP需要改成你自己的，要用真实IP
    url: 'http://10.11.12.7:9999/auth/oauth/token',
    headers: {
      isToken:false,
      'TENANT_ID': '1',
      'Authorization': 'Basic cGlnOnBpZw=='
    },
    method: 'post',
    params: { username, password, randomStr, code, grant_type, scope }
  })
}
```

将前端项目跑起来，打开登录页面，观察点击登录按钮的XHR请求，你会发现浏览器发送了两次请求：

- 第一次是`OPTIONS`方式，这是因为浏览器检测到有一个请求跨域了，于是发出一个预检请求，问一问服务端"有啥处理意见"。
- 第二次是`POST`方式，也就是真正的需要执行的请求，这是因为“服务端的回答让浏览器满意”了，所以浏览器执行真正的请求。如果服务端（也就是`PigX Gateway`）没有进行相关配置，浏览器就没法得到它期望的答复，这一步便不会执行。

# 代码生成使用





### 功能支持

##### 前端：

- api.js
- crud.js
- index.vue

##### 后端

- entity
- mapper
- service
- Controller

### 开始使用

##### 项目启动

1. 启动 pig-eureka、pig-config、pig-gateway、pig-auth、pig-upms-biz
2. 启动 **PigCodeGenApplication**
3. 启动 **pig-ui**

##### 界面操作

1. 代码生成模块

![image](http://a.pig4cloud.com/20180803083802.png)

1. 选择要生成的表

   > 以下为空则从**pigx-codegen/generator.properties** 获取

   ![image](http://a.pig4cloud.com/20180803084058.png)

2. 解压下载的**pig_code_gen.zip**

   > 生成代码结构，安装前后端 maven 、vue-cli 目录生成，可以覆盖到指定业务模块

   ![image](http://a.pig4cloud.com/20180803084524.png)

3. **重点讲解生成的SQL使用**

   > 生成的SQL脚本，不要直接执行，完善 菜单、按钮的菜单ID 的层级
   >
   > PS: 为什么菜单ID 不自动生成呢？
   >
   > - 
   >
   >   ​	通过自己录入保证，数据库展示层级。
   >
   > - 
   >
   >   ​	比如 父菜单 ID 为 1,子菜单的ID 则为 11，按钮ID 为 12，13，14

   ```
   1
   ├── 11
   ├── 12
   ├── 13
   ├── 14
   ```

![image](http://a.pig4cloud.com/20180803084905.png)

1. **配置路由代理**
   前端 vue.config.js

```
  '/demo': {
      target: baseUrl,
      changeOrigin: true,
      pathRewrite: {
          '^/demo': '/demo'
      }
  },
```

网关新增路由

```
spring:
  cloud:
    gateway:
      locator:
        enabled: true
      routes:
      - id: pig-demo
        uri: lb://pig-demo
        predicates:
        - Path=/demo/**
```

##### 最后给角色分配，你新增的菜单和按钮喔

# EnablePigFeignClients原理解析





### 源码解析

只是给默认的EnableFeignClients 增加了一个默认值。

```
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@EnableFeignClients
public @interface EnablePigxFeignClients {

	String[] value() default {};
    
    // 指定默认的扫描范围
	String[] basePackages() default {"com.pig4cloud.pigx"};

	Class<?>[] basePackageClasses() default {};

	Class<?>[] defaultConfiguration() default {};

	Class<?>[] clients() default {};
}
```

### 以UPMS为例分析封装的好处

![img](http://pic.pig4cloud.com/20190220232605_DAHeuX_Screenshot.jpeg)

- 如果使用原生的EnableFeignClients 默认的扫描范围是 com.pig4cloud.pig.admin 包的所有FeignClient。
- 而由于微服务拆分所有的feignClient 都在 com.pig4cloud.pig.模块.api包里面，这样默认情况会扫描不到
- 除非明确指定扫描范围 @EnableFeignClients("com.pig4cloud.pig.模块.api")
- 使用了@EnablePigFeignClients 默认扫描 com.pig4cloud.pigx下边的feignClient 更为简洁

#### @EnableFeignClients

```
@EnableFeignClients
@SpringCloudApplication
public class PigAdminApplication {

}
```

#### @EnablePigFeignClients

```java
@EnablePigFeignClients
@SpringCloudApplication
public class PigAdminApplication {
	public static void main(String[] args) {
		SpringApplication.run(PigAdminApplication.class, args);
	}

}
```

# Pig 中FeignClient 使用说明





### 分包说明

![img](http://pic.pig4cloud.com/20190220232605_DAHeuX_Screenshot.jpeg)
具体参考上一章节[EnablePigFeignClients原理解析]

- main类 使用了@EnablePigFeignClients 默认扫描
- 出现FeignClient 调用报错等，请检查你的分包是否符合pig 的标准
- 包名 com.pig4cloud.pig.模块.api

### 新增feignClient

![img](http://pic.pig4cloud.com/20190221105453_xwRUY1_Screenshot.jpeg)

- RemoteXXXService FeignClient 客户端,声明具体的接口和降级工程

```
@FeignClient(value = ServiceNameConstants.UMPS_SERVICE, fallbackFactory = RemoteLogServiceFallbackFactory.class)
```

- 降级工厂类，注意这里的@Component 注入到Spring

```
@Component
public class RemoteLogServiceFallbackFactory implements FallbackFactory<RemoteLogService> {

	@Override
	public RemoteLogService create(Throwable throwable) {
		RemoteLogServiceFallbackImpl remoteLogServiceFallback = new RemoteLogServiceFallbackImpl();
		remoteLogServiceFallback.setCause(throwable);
		return remoteLogServiceFallback;
	}
}
```

- 具体的降级业务

```
@Component
public class RemoteLogServiceFallbackImpl implements RemoteLogService {
	@Setter
	private Throwable cause;
	public R<Boolean> saveLog(SysLog sysLog, String from) {
		log.error("feign 插入日志失败", cause);
		return null;
	}
}
```

### 为了保证引入api模块可以直接使用，在spring.factories 配置bean

![img](http://pic.pig4cloud.com/20190221105841_hJ0rah_Screenshot.jpeg)

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
  com.pig4cloud.pig.admin.api.feign.fallback.RemoteXXXServiceFallbackImpl,\
  com.pig4cloud.pig.admin.api.feign.factory.RemoteXXXServiceFallbackFactory
```

# 验证码配置及开关





验证码直接网关异步生成，基于webflux

### webflux 生成验证码的handler

```
public class ImageCodeHandler implements HandlerFunction<ServerResponse> {
	private final Producer producer;
	private final RedisTemplate redisTemplate;

	@Override
	public Mono<ServerResponse> handle(ServerRequest serverRequest) {
		//生成验证码
		String text = producer.createText();
		BufferedImage image = producer.createImage(text);

		//保存验证码信息
		String randomStr = serverRequest.queryParam("randomStr").get();
		redisTemplate.opsForValue().set(CommonConstants.DEFAULT_CODE_KEY + randomStr, text, 60, TimeUnit.SECONDS);

		// 转换流信息写出
		FastByteArrayOutputStream os = new FastByteArrayOutputStream();
		try {
			ImageIO.write(image, "jpeg", os);
		} catch (IOException e) {
			log.error("ImageIO write err", e);
			return Mono.error(e);
		}

		return ServerResponse
			.status(HttpStatus.OK)
			.contentType(MediaType.IMAGE_JPEG)
			.body(BodyInserters.fromResource(new ByteArrayResource(os.toByteArray())));
	}
}
```

### webflux 请求处理入口

```
public class RouterFunctionConfiguration {
	private final HystrixFallbackHandler hystrixFallbackHandler;
	private final ImageCodeHandler imageCodeHandler;

	@Bean
	public RouterFunction routerFunction() {
		return RouterFunctions.route(RequestPredicates.GET("/code")
				.and(RequestPredicates.accept(MediaType.TEXT_PLAIN)), imageCodeHandler);

	}

}
```

### 校验逻辑,通过oauth2 终端的client-id 来确定是否校验验证码

```
public class ValidateCodeGatewayFilter extends AbstractGatewayFilterFactory {
	@Override
	public GatewayFilter apply(Object config) {
		return (exchange, chain) -> {
			ServerHttpRequest request = exchange.getRequest();


			// 终端设置不校验， 直接向下执行
			String[] clientInfos = WebUtils.getClientId(request);
			if (filterIgnorePropertiesConfig.getClients().contains(clientInfos[0])) {
				return chain.filter(exchange);
			}

			//校验验证码
			checkCode(request);

			return chain.filter(exchange);
		};
	}
}
```

### 配置终端不校验验证码

```
pig-gateway-dev.yml

# 不校验验证码终端
ignore:
  clients:
    - 不校验验证码的终端client-id
        
```

# Pig配置加解密





# jasypt 的解决方案

1. Maven依赖

```
<dependency>
    <groupId>com.github.ulisesbocchio</groupId>
    <artifactId>jasypt-spring-boot-starter</artifactId>
    <version>1.16</version>
</dependency>
```

1. 配置

```
jasypt:
  encryptor:
    password: foo #根密码
```

3 调用JAVA API 生成密文

```
@RunWith(SpringJUnit4ClassRunner.class)
@SpringBootTest(classes = PigAdminApplication.class)
public class PigAdminApplicationTest {
	@Autowired
	private StringEncryptor stringEncryptor;

	@Test
	public void testEnvironmentProperties() {
		System.out.println(stringEncryptor.encrypt("lengleng"));
	}

}
```

或者直接使用JAVA 方法调用 （不依赖 spring 容器）

```
   /**
     * jasypt.encryptor.password 对应 配置中心 application-dev.yml 中的密码
     */
    @Test
    public void testEnvironmentProperties() {
        System.setProperty(JASYPT_ENCRYPTOR_PASSWORD, "lengleng");
        StringEncryptor stringEncryptor = new DefaultLazyEncryptor(new StandardEnvironment());

        //加密方法
        System.out.println(stringEncryptor.encrypt("123456"));
        //解密方法
        System.out.println(stringEncryptor.decrypt("saRv7ZnXsNAfsl3AL9OpCQ=="));
    }
```

4 配置文件中使用密文

```
spring:
  datasource:
    password: ENC(密文)

xxx: ENC(密文)
```

5 [其他非对称等高级配置参考](https://github.com/ulisesbocchio/jasypt-spring-boot)

## 总结

1. Spring Cloud Config 提供了统一的加解密方式，方便使用，但是如果应用配置没有走配置中心，那么加解密过滤是无效的；依赖JCE 对于低版本spring cloud的兼容性不好。
2. jasypt 功能更为强大，支持的加密方式更多，但是如果多个微服务，需要每个服务模块引入依赖配置，较为麻烦；但是功能强大 、灵活。
3. 个人选择 jasypt

# 前端报文加密及其解密处理





### 前端报文加密的业务

用户登录时，对登录密码进行加密传输

![img](http://pic.pig4cloud.com/20190220234340_GnCbD1_Screenshot.jpeg)

### 前端加密功能

前端提供简单的AES对称加密算法，注意key 和后端网关配置相同，这里打包混淆后，相对安全。
![img](http://pic.pig4cloud.com/20190220234539_fZpgwd_Screenshot.jpeg)

### 后端解密功能

使用hutool提供的工具类进行解密

```
public class PasswordDecoderFilter extends AbstractGatewayFilterFactory {
	@Override
	public GatewayFilter apply(Object config) {
		return (exchange, chain) -> {
			ServerHttpRequest request = exchange.getRequest();
			URI uri = exchange.getRequest().getURI();
			String queryParam = uri.getRawQuery();
			Map<String, String> paramMap = HttpUtil.decodeParamMap(queryParam, CharsetUtil.UTF_8);

			String password = paramMap.get(PASSWORD);
			if (StrUtil.isNotBlank(password)) {
				try {
					password = decryptAES(password, encodeKey);
				} catch (Exception e) {
					log.error("密码解密失败:{}", password);
					return Mono.error(e);
				}
				paramMap.put(PASSWORD, password.trim());
			}

			URI newUri = UriComponentsBuilder.fromUri(uri)
				.replaceQuery(HttpUtil.toParams(paramMap))
				.build(true)
				.toUri();

			ServerHttpRequest newRequest = exchange.getRequest().mutate().uri(newUri).build();
			return chain.filter(exchange.mutate().request(newRequest).build());
		};
	}
}
```

### 总结

杠精不要抬杠AES 是对称加密，不安全。

# 登录后置处理





用户登录成功、失败后，pig 捕获了spring security 发出的对应事件。

- 用户登录成功时，发布AuthenticationSuccessEvent事件

```
public class PigAuthenticationSuccessEventHandler extends AuthenticationSuccessEventHandler {

	/**
	 * 处理登录成功方法
	 * <p>
	 * 获取到登录的authentication 对象
	 *
	 * @param authentication 登录对象
	 */
	@Override
	public void handle(Authentication authentication) {
		log.info("用户：{} 登录成功", authentication.getPrincipal());
	}
}
```

- 用户登录失败时
  AuthenticationException 是登录异常信息，包括常见的用户密码不正确，用户信息不正确，用户状态不正确等

```
@Slf4j
@Component
public class PigAuthenticationFailureEvenHandler extends AuthenticationFailureEvenHandler {

	/**
	 * 处理登录失败方法
	 * <p>
	 *
	 * @param authenticationException 登录的authentication 对象
	 * @param authentication          登录的authenticationException 对象
	 */
	@Override
	public void handle(AuthenticationException authenticationException, Authentication authentication) {
		log.info("用户：{} 登录失败，异常：{}", authentication.getPrincipal(), authenticationException.getLocalizedMessage());
	}
}
```

- Authentication 用户身份认证信息

```
public interface Authentication extends Principal, Serializable {
    
    // 用户角色 + 权限信息（会包含用户的权限标志）
	Collection<? extends GrantedAuthority> getAuthorities();
    
    // 用户密码加密串
	Object getCredentials();
    
    // 用户名或者用户全部信息（参考资源服务配置章节说明）
	Object getPrincipal();
    
    // 是否认证
	boolean isAuthenticated();
	
	...

}
```

# 日志处理-Spring Event 处理机制





### POM依赖

```
<!--日志处理-->
<dependency>
	<groupId>com.pig4cloud</groupId>
	<artifactId>pig-common-log</artifactId>
	<version>${log.version}</version>
</dependency>
```

### @SysLog 注解

- 接口上使用@SysLog 注释当前接口的作用即可

```
@SysLog("添加终端")
@PostMapping
@PreAuthorize("@pms.hasPermission('sys_client_add')")
public R add(@Valid @RequestBody SysOauthClientDetails sysOauthClientDetails) {
	return new R<>(sysOauthClientDetailsService.save(sysOauthClientDetails));
}
```

### 原理讲解

- AOP 切面获取当前请求的注解值，并 **异步** 发送时间，减少日志操作的性能损耗

```
@Aspect
@Slf4j
public class SysLogAspect {

	@Around("@annotation(sysLog)")
	public Object around(ProceedingJoinPoint point, SysLog sysLog) throws Throwable {
		String strClassName = point.getTarget().getClass().getName();
		String strMethodName = point.getSignature().getName();
		log.debug("[类名]:{},[方法]:{}", strClassName, strMethodName);
		SpringContextHolder.publishEvent(new SysLogEvent(logVo));
		return obj;
	}

}
```

- 监听器在接收到日志事件后进行调用feign入口处理

```
@Slf4j
@AllArgsConstructor
public class SysLogListener {
	private final RemoteLogService remoteLogService;

	@Async
	@Order
	@EventListener(SysLogEvent.class)
	public void saveSysLog(SysLogEvent event) {
		SysLog sysLog = (SysLog) event.getSource();
		remoteLogService.saveLog(sysLog, SecurityConstants.FROM_IN);
	}
}
```

### 异步操作说明 @EnableAsync

@EnableAsync 注解启用了 Spring 异步方法执行功能，在[ Spring Framework API](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/scheduling/annotation/EnableAsync.html) 中有详细介绍。

# 监控模块二次认证





![img](http://pic.pig4cloud.com/20190221130907_7nb50u_Screenshot.jpeg)

### 为什么要做二次认证

spring boot admin 默认没有开启认证，也是就是别人知道了监控模块的IP:PORT 即可访问。监控功能在生产上又是必要的功能，所以需要有二次认证

### 实现原理

- 引入spring security

```
<!--security-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

- 配置spring security即可

```
@Configuration
public class WebSecurityConfigurer extends WebSecurityConfigurerAdapter {
	private final String adminContextPath;

	public WebSecurityConfigurer(AdminServerProperties adminServerProperties) {
		this.adminContextPath = adminServerProperties.getContextPath();
	}

	@Override
	protected void configure(HttpSecurity http) throws Exception {
		// @formatter:off
		SavedRequestAwareAuthenticationSuccessHandler successHandler = new SavedRequestAwareAuthenticationSuccessHandler();
		successHandler.setTargetUrlParameter("redirectTo");
		successHandler.setDefaultTargetUrl(adminContextPath + "/");

		http
			.headers().frameOptions().disable()
			.and().authorizeRequests()
			.antMatchers(adminContextPath + "/assets/**"
				, adminContextPath + "/login"
				, adminContextPath + "/actuator/**"
			).permitAll()
			.anyRequest().authenticated()
			.and()
			.formLogin().loginPage(adminContextPath + "/login")
			.successHandler(successHandler).and()
			.logout().logoutUrl(adminContextPath + "/logout")
			.and()
			.httpBasic().and()
			.csrf()
			.disable();
		// @formatter:on
	}
}
```

- 在对应的 pig-monitor-dev.yml 配置用户

pig 默认的登录用户 pig/pig，可以参考配置文件加解密章节

```
spring:
  security:
    user:
      name: ENC(8Hk2ILNJM8UTOuW/Xi75qg==)     # pig
      password: ENC(o6cuPFfUevmTbkmBnE67Ow====) # pig
```

# 监控模块使用之web展示实时日志





开启后可以在浏览器实时查看当前日志输出

### pig 默认没有开启 Logfile viewer

![img](http://pic.pig4cloud.com/20190706115555_pL1RHZ_Screenshot.jpeg)

### 以UPMS模块为例

在 bootstrap.yml 配置 logging.file 的配置即可开启Logfile viewr

```
# 配置Logfile Viewer

logging:
  file: logs/${spring.application.name}/debug.log
```

### 启动 pig-monitor

- 选中 PIG-UPMS 服务
  ![img](http://pic.pig4cloud.com/20190221130054_iVj4Yp_Screenshot.jpeg)
  ![img](http://pic.pig4cloud.com/20190221130140_1sByxe_Screenshot.jpeg)
  ![img](http://pic.pig4cloud.com/20190221130159_3qtI7c_Screenshot.jpeg)

# 监控模块使用之动态日志级别





pig默认的输出的日志级别是INFO，生产中建议使用ERROR级别。
当我们遇到某些bug 时，动态调整log 输出日志非常有效，spring boot admin 提供了这样的功能。

### 启动 pig-monitor

- 选中 PIG-UPMS 服务
  ![img](http://pic.pig4cloud.com/20190221130054_iVj4Yp_Screenshot.jpeg)
- 选择Loggers, 即可实现动态切换日志级别的需求
  ![img](http://pic.pig4cloud.com/20190221130731_kXf3xS_Screenshot.jpeg)

# 前端文档说明





1. 本项目前端工程基于 element-ui 2.4 、avue 1.5

- element 文件
  [element-ui 2.4](https://element.eleme.cn/2.4/#/zh-CN/component/installation)
- avue 文档
  由于avue 官网不在提供旧版本文档，特部署了一份旧版兼容 1.5.X-，地址不要分享
  [https://avue1.pig4cloud.com](https://avue1.pig4cloud.com/)

# 配置npm镜像





## 将 Npm 的源替换成淘宝的源

在墙内久了，难免会碰到撞墙的时候，所幸国内也有众多 NPM 镜像可供选择，在大多数情况下我们可以使用国内的源（比如 淘宝 NPM 镜像）去替换官方的源以加快下载包的速度。

### 开始

你可以使用我们定制的 cnpm (gzip 压缩支持) 命令行工具代替默认的 npm:

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

或者你直接通过添加 npm 参数 alias 一个新命令:

```
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"
```

# 登录详解





首先你要理解OAuth 2.0(自行百度把)

1.用户登录成功时调用——loginByUsername方法会返回token

vue中没有与服务器的交互，所以请求的是/api/user下的数据

2.将返回的token存到cookie里面，在src/store/modules/user.js——LoginByUsername方法

token为服务端返回的

```
...
LoginByUsername({ commit, state, dispatch }, userInfo) {
...
	commit('SET_TOKEN', token);
...
}
...
```

3.在调用同js文件里的SET_TOKEN方法，将token存到score里

```
...
mutations: {
        SET_TOKEN: (state, token) => {
            state.token = token;
            setStore({ name: 'token', content: state.token, type: 'session' })
        },
...
 }
```

4.在ajax拦截器里，将token携带到header里，服务器就会接受token，来区分那个用户，有那些权限

```
src/router /axios.js
...
//HTTPrequest拦截
axios.interceptors.request.use(config => {
	loadinginstace = Loading.service({
		fullscreen: true
	});
	if (store.getters.token) {
		config.headers['X-Token'] = getToken() // 让每个请求携带token-- ['X-Token']为自定义key 请根据实际情况自行修改
	}
	return config
}, error => {
	console.log('err' + error)// for debug
	return Promise.reject(error)
})
...
```

# 自定义返回码提示





### errorCode 直接根据code，定义如下图.

![img](https://box.kancloud.cn/a74423c9ebcba050da6737faa039f53f_1714x486.png)

### 服务端定义返回码

1. 借助response对象

```
response.setCharacterEncoding(CommonConstant.UTF8);
response.setContentType(CommonConstant.CONTENT_TYPE);
R<String> result = new R<>(e);
response.setStatus(478);
printWriter = response.getWriter();
printWriter.append(objectMapper.writeValueAsString(result));
```

1. 借助springMVC

```
    @RequestMapping(value="/response/entity/headers", method=RequestMethod.GET)  
    public ResponseEntity<String> responseEntityCustomHeaders() {  
        HttpHeaders headers = new HttpHeaders();  
        headers.setContentType(MediaType.TEXT_PLAIN);  
        return new ResponseEntity<String>("The String ResponseBody with custom header Content-Type=text/plain",  
                headers, HttpStatus.OK);  
    }  
```

# 按钮权限控制





# pig 如何控制菜单权限控制

## 后台声明一个按钮

![img](https://gitee.com/log4j/pig/raw/master/doc/images/6.png)

在后台菜单管理中给指定菜单添加 **按钮**节点 需要指定 **权限标志**
例如： sys_user_add

## 前端控制

前端主要使用vuex保存用户的权限信息，然后通过v-if 判断是否有权限，如果有权限就渲染这个dom元素。
我们以 用户管理页面来讲解

```
//按钮v-if使用
<el-table-column align="center" label="操作">
        <template slot-scope="scope">
          <el-button v-if="sys_user_upd" size="small" type="success" @click="handleUpdate(scope.row)">编辑
          </el-button>
          <el-button v-if="sys_user_del" size="small" type="danger" @click="deletes(scope.row)">删除
          </el-button>
        </template>
  </el-table-column>
  
  // 变量初始化
  created() {
    this.getList();
    this.sys_user_add = this.permissions["sys_user_add"];
    this.sys_user_upd = this.permissions["sys_user_upd"];
    this.sys_user_del = this.permissions["sys_user_del"];
  },
  
  // 从vuex 获取保存的permissions
  computed: {
    ...mapGetters(["permissions"])
  }
  
  //permissions获取
  getUserInfo(state.token).then(response => {
    commit('SET_PERMISSIONS', data.permissions)
})
```

## 后端权限控制

通过获取用户菜单列表，和请求的地址和请求方法对比判断有没有权限

```
    public boolean hasPermission(HttpServletRequest request, Authentication authentication) {
        Object principal = authentication.getPrincipal();
        List<SimpleGrantedAuthority> grantedAuthorityList = (List<SimpleGrantedAuthority>) authentication.getAuthorities();
        boolean hasPermission = false;

        if (principal != null) {
            if (CollectionUtil.isEmpty(grantedAuthorityList)) {
                return hasPermission;
            }

            Set<MenuVo> urls = new HashSet<>();
            for (SimpleGrantedAuthority authority : grantedAuthorityList) {
                urls.addAll(menuService.findMenuByRole(authority.getAuthority()));
            }

            for (MenuVo menu : urls) {
                if (StringUtils.isNotEmpty(menu.getUrl()) && antPathMatcher.match(menu.getUrl(), request.getRequestURI())
                        && request.getMethod().equalsIgnoreCase(menu.getMethod())) {
                    hasPermission = true;
                    break;
                }
            }
        }
        return hasPermission;
    }
```

# 图标引入





#### 步骤 1 :先去阿里巴巴图标库注册一个账号

[阿里巴巴图标库](http://www.iconfont.cn/)

#### 步骤 2 :完后选择自己喜欢的图标加入到项目中，点击生成在线链接

![img](https://box.kancloud.cn/0e41e5c3c4bb03a993e78431cea3fe1e_1485x648.png)

#### 步骤 3 :图标的加载

将红色框中的部分复制项目中，也就是‘617295_eq4dlr8rl7peqaor’在

/src/config/env.js

的iconfontVersion 的数组中

```
let iconfontVersion = ['567566_sch40o867ogk3xr','617295_eq4dlr8rl7peqaor'];
```

第一个数组的图标不能删除，那是支持avue框架的全局图标，如果多个图标库依次添加到数据中即可

#### 步骤 4 :图标的调用

输入在图标库中图标的名称即可

```
<i class="icon-bofangqi-suoping"></i>
```

##### ps，如果点击更新URL，更新env.js

阿里巴巴图标库的调用必须是有网情况

# Docker Compose 部署





Docker Compose 是 Docker 官方编排项目之一，负责快速的部署分布式应用。

## 安装Docker （centos7）

```
# 更新yum 源
yum update

#安装 Docker
yum -y install docker

#启动 Docker 后台服务
service docker start

#测试运行 hello-world,由于本地没有hello-world这个镜像，所以会下载一个hello-world的镜像，并在容器内运行。
docker run hello-world
```

## 安装docker-compose

```
$ sudo curl -L https://github.com/docker/compose/releases/download/1.20.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
```

## pig 打包

- pig 根目录

```
mvn clean install -Dmaven.test.skip=true
```

![img](http://pic.pig4cloud.com/20190221163545_ykCjD4_Screenshot.jpeg)

- 根目录执行 docker-compose 命令

```
# 构建镜像
docker-compose build

# 启动容器 （-d 后台启动，建议第一次不要加，方便看错误）
docker-compose up -d
```

## 等待3分钟

访问Centos7 IP:8761 查看eureka状态，确定所有服务全部启动。

## 总结

1. 服务端已启动完毕，前端请参考下一章节《前端部署》
2. 不要和开发环境一样，修改容器hosts,docker-compose 会根据容器名称自动处理

# 前端部署-打包





**npm打包**

```
# 执行打包命令
npm run build
```

**打包过程**
webpack会生成相应的目录结构(压缩和混淆的代码)

**打包产物**

![img](http://pic.pig4cloud.com/20190221132143_HSeTnP_Screenshot.jpeg)

# nginx





## nginx代理，前端请求，解决跨域

在生产中，我们建议使用nginx 代理前端请求，解决跨域。
并且把上步打包dist 目录的文件部署到nginx

## nginx.conf

```
location ^~/admin/ {
proxy_pass   http://127.0.0.1:9999/admin/;
}


location ^~/auth/ {
proxy_pass   http://127.0.0.1:9999/auth/;
}

location ^~/gen/ {
proxy_pass   http://127.0.0.1:9999/gen/;
}
```

以上配置类似于，vue-cli的proxy配置

## pig 演示环境的配置

```
server {
    listen 80;
    server_name xxxxx.com;
    
    # 讲打包好的dist目录文件，放置到这个目录下
    root /data/pig-ui/;
          
    location ~* ^/(code|auth|admin|gen) {
       proxy_pass http://127.0.0.1:9999;
       #proxy_set_header Host $http_host;
       proxy_connect_timeout 15s;
       proxy_send_timeout 15s;
       proxy_read_timeout 15s;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
} 
```

# PPT整理





### Spring Cloud中国社区文档

- 2017-0312-Spring Cloud中国社区成都站PPT

- 2017-0409-Spring Cloud中国社区上海站PPT

- 2017-0506-Spring Cloud中国社区北京站PPT

- 2017-0610-Spring Cloud中国社区深圳站PPT

- 2017-0820-Spring Cloud中国社区网关会议PPT

- Spring Cloud与摩拜单车Mobike-范文通.pdf

  [Spring Cloud中国社区线下沙龙文档](https://github.com/pig4cloud/spring-cloud-document)

### Arcm PPT 分享

- 01.keynote主题演讲
- 02.数据库架构
- 03.Fintech技术突围之道（解决方案专场）
- 04.大前端技术与管理
- 05.深入机器学习
- 06.架构升级与优化
- 07.金融应用架构
- 08.互联网产品与创业
- 09.互联网视频技术架构：优化和创新
- 10.云化架构的创新实践（阿里技术专场）
- 11.架构创新与演进（解决方案专场）
- 12.业务系统架构的蜕变与进化
- 13.大数据平台架构
- 14.人工智能与业务应用
- 15.新一代DevOps
- 16.个性化智能广告系统
- 17.国际化架构设计
- 18.大数据与云原生（解决方案专场）
- 19.容器云平台运维（解决方案专场）
- 20.微服务架构
- 21.内容分发与精准推荐
- 22.移动开发工程化实践
- 23.工程师文化与团队建设
- 24.深度培训

链接:<https://pan.baidu.com/s/1iTUMCGc7kJ3kLYH7vWEEFA> 密码:iddl
链接: <https://pan.baidu.com/s/1fr0S_vFYvrTOzR9sOG1hTA> 提取码: ixnt

# 博客整理

### 收藏栏

### 工具

[json](http://www.bejson.com/json2javapojo/)

[文本](http://wenbenbijiao.renrensousuo.com/#diff)

[Smallpdf.com – 您所有PDF问题的免费解决方案](https://smallpdf.com/cn)

[ProcessOn](https://www.processon.com/)

[全网VIP视频在线解析](http://csctc317.com/)

[Redis 命令参考 — Redis 命令参考](http://redisdoc.com/)

[在线工具](http://tool.lu/)

[爱莫助手](https://airmore.cn/)

[XMind Cloud](https://cloud.xmind.net/)

[Eureka Server](http://eureka.didispace.com/)

[HTML在线运行](http://www.w3school.com.cn/tiy/t.asp?f=html_basic)

[字帖](http://antidestiny.gitee.io/calligraphy)

[Mac软件破解库 · 看云](https://www.kancloud.cn/iyoco/macpojie#/reward)

[ASCIIFlow Infinity](http://asciiflow.com/)

[XDOC云服务 - 云文档、云报表、云表单](http://www.xdocin.com/index.html)

[临时邮箱-邮箱大全](http://www.benpig.com/linshi.htm)

[可以自己定义的邮箱](https://www.guerrillamail.com/zh/inbox)

[Bootstrap可视化布局系统](http://www.bootcss.com/p/layoutit/?)

[ShowDoc](https://www.showdoc.cc/web/#/)

[知笔墨](http://zhibimo.com/)

[冷冷的书籍 - 北半球](https://www.beibq.cn/user/lengleng)

[Readhub](https://readhub.me/)

### 收藏

其他

[微信公众平台开发者文档](https://mp.weixin.qq.com/wiki/home/)

[MySQL索引原理及慢查询优化 -](http://tech.meituan.com/mysql-index.html)

[ifeve.com](http://ifeve.com/)

[Pixabay](https://pixabay.com/)

[七牛云](https://portal.qiniu.com/signin)

[ztree](http://blog.csdn.net/cuiran/article/details/7659094)

[JavaFX](http://www.javafxchina.net/blog/)

[看云](http://www.kancloud.cn/)

[Insdep Theme - EasyUI美化主题 JQuery EasyUI Of Insdep theme](https://www.insdep.com/)

[sonar常见错误以及处理方案](http://blog.csdn.net/lifen0908/article/details/54575895)

[Redis 如何分布式，来看京东金融的设计与实践](https://mp.weixin.qq.com/s?__biz=MzIwMzg1ODcwMw==&mid=2247486811&idx=1&sn=5f8dda70bb78f310342d38ae5921fbf8&chksm=96c9bb3ba1be322d22f9e56fdb71e3946c12073037e616b2ca7f840e3aac44e42182a9352ba2#rd)

[分布式环境下限流方案的实现redis RateLimiter Guava,Token Bucket, Leaky Bucket - 沧海一滴 - 博客园](http://www.cnblogs.com/softidea/p/6229543.html)

[使用Redis实现分布式锁及其优化 | Mz's Blog](http://mzorro.me/2017/10/25/redis-distributed-lock/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

[限流](https://gitee.com/fuhai/jboot)

[Activiti工作流](http://yun.itheima.com/course/57.html)

[CentOS6.5下RabbitMQ安装](http://blog.csdn.net/mx472756841/article/details/50733886)

[程序员你为什么这么累？](https://zhuanlan.zhihu.com/p/28705206?refer=c_120823325)

[IntelliJ IDEA For Mac 快捷键 - IntelliJ IDEA 使用教程 - 极客学院Wiki](http://wiki.jikexueyuan.com/project/intellij-idea-tutorial/keymap-mac-introduce.html)

### java

[图解集合](http://www.importnew.com/?s=%E5%9B%BE%E8%A7%A3%E9%9B%86%E5%90%88)

[Java线程](http://www.importnew.com/12773.html)

[聊聊高并发](http://blog.csdn.net/column/details/loveconcurrency.html?&page=1)

[Java Concurrency](http://www.blogjava.net/xylz/archive/2010/07/08/325587.html)

[无信不立 - 博客园](http://www.cnblogs.com/shangxiaofei/p/3876330.html)

[Java面试题全集](http://mp.weixin.qq.com/s/elp-gBu_eF7CWLWaP31OQg)

### VUE

[VUE2](http://www.runoob.com/vue2/vue-tutorial.html)

[Vue.js](https://cn.vuejs.org/v2/guide/)

[Vue 2.0 Admin后台管理模板对比](http://lanyuanxiaoyao.com/2017/07/05/vue-admin/)

[Juicy](http://panjiachen.github.io/vue-element-admin/#/login)

[fetch](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise)

[javascript - vuejs2.0的element-ui组件select选择器无法显示选中的内容 - SegmentFault](https://segmentfault.com/q/1010000009295579?_ea=1885087)

[Hystrix/BasicCollapserTest.java at master · Netflix/Hystrix](https://github.com/Netflix/Hystrix/blob/master/hystrix-contrib/hystrix-javanica/src/test/java/com/netflix/hystrix/contrib/javanica/test/common/collapser/BasicCollapserTest.java)

### 微服务

### spring cloud

[Spring Cloud中文网-官方文档中文版](https://springcloud.cc/)

[Spring Cloud Dalston 中文文档 参考手册 中文版](https://springcloud.cc/spring-cloud-dalston.html)

[周立/spring-cloud-docker-microservice-book-code - 码云](http://git.oschina.net/itmuch/spring-cloud-docker-microservice-book-code)

[Category: Eureka | 芋道源码 —— 纯源码解析BLOG](http://www.iocoder.cn/categories/Eureka/)

[Spring Cloud](http://blog.csdn.net/u012702547/article/details/78043159)

[Spring Cloud git](https://github.com/spring-cloud/)

[spring cloud-江南](http://my.csdn.net/u012702547)

[史上最简单的 SpringCloud 教程 | 终章 - 方志朋的专栏 - CSDN博客](http://blog.csdn.net/forezp/article/details/70148833)

[JWT在Spring Cloud中的使用](http://blog.springcloud.cn/sc/sc-w-jwt/)

[如何架构一个合适的企业API网关](http://blog.csdn.net/zhengpeitao/article/details/72722301)

[Spring Cloud](http://blog.didispace.com/Spring-Cloud%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B/)

[Spring Cloud](https://github.com/spring-cloud)

[spring cloud sleuth | 网易乐得技术团队](http://tech.lede.com/2017/04/19/rd/server/SpringCloudSleuth/)

[微服务实践 - MSA的关键架构概念](https://wso2.com/whitepapers/microservices-in-practice-key-architectural-concepts-of-an-msa/#09)

[微服务-铁汤博客](http://tietang.wang/categories/)

[JHipster](http://www.jhipster.tech/)

[极客时间 | 微服务架构核心20讲](https://time.geekbang.org/course/intro/66)

### spring boot

[Spring Boot](http://blog.didispace.com/Spring-Boot%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B/)

[springboot · GitBook](http://doc.springboot.cn/IV.%20Spring%20Boot%20features/29.1.1.%20Connecting%20to%20Redis.html)

[Spring Boot2.0](https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/)

[spring-boot/spring-boot-samples at v2.0.0.RELEASE · spring-projects/spring-boot](https://github.com/spring-projects/spring-boot/tree/v2.0.0.RELEASE/spring-boot-samples/)

[Spring Security 参考手册](https://vincentmi.gitbooks.io/spring-security-reference-zh/content/4.4_method_security.html)

### docker

[Docker](https://yeasy.gitbooks.io/docker_practice/content/basic_concept/)

[src/page/index.vue · 云集汇通开发团队/vue-xinjiang - 码云 - 开源中国](https://gitee.com/yjht/kingvue/blob/master/src/page/index.vue)

[CentOS Docker 安装 | 菜鸟教程](http://www.runoob.com/docker/centos-docker-install.html)

[写在最前面 | shipyard中文文档](https://weilaihui.gitbooks.io/shipyard-doc/content/)

[Docker可视化管理工具shipyard安装 - Yang - CSDN博客](http://blog.csdn.net/masonqaq/article/details/78029444)

[shipyard](http://123.206.94.20:8080/)

[CentOS 7 配置Docker 远程API访问 - 老胡的笔记 - CSDN博客](http://blog.csdn.net/hjh00/article/details/77816661)

[Portainer](http://123.206.94.20:9000/)

[搭建私有仓库 - Humpback](https://humpback.github.io/humpback/#/zh-cn/build-registry)

### spring

[jetty 配置https](http://wiki.eclipse.org/Jetty/Howto/Configure_SSL#Redirecting_http_requests_to_https)

[Spring Projects](https://spring.io/projects)

[跟我学Shiro](http://jinnianshilongnian.iteye.com/blog/2018398)

### 其他

[碧桂园分布式事务](https://github.com/yu199195/happylifeplat-tcc)

[程立谈大规模SOA系统](http://www.infoq.com/cn/interviews/soa-chengli#downloadInterviewMp3,%20/cn/interviews/soa-chengli#downloadInterviewMp3,%20/cn/interviews/soa-chengli#downloadInterviewMp3)

[芋道源码](http://www.iocoder.cn/?vip)

[CentOS 7 安装配置分布式文件系统 FastDFS 5.0.5_服务器应用_Linux公社-Linux系统门户网站](http://www.linuxidc.com/Linux/2016-09/135537.htm)

[凤凰牌老熊的博客 | Shamphone Blog](http://blog.lixf.cn/)

[elastic-job与spring boot集成demo - CSDN博客](http://blog.csdn.net/u014401141/article/details/78972846)

[使用FastDFS搭建图片服务器单实例篇-老猫1981-51CTO博客](http://blog.51cto.com/oldcat1981/1766810)

[Redis Cluster](http://debugo.com/redis-cluster-note1/)

[spring security 的一些文档](https://gitee.com/shengzhao/spring-oauth-server/attach_files)

[JHipster - Generate your Spring Boot + Angular apps!](https://www.jhipster.tech/)

[安装 · jhipster开发笔记](https://jh.jiankangsn.com/install.html)

### service mesh

[Introduction · Istio官方文档中文版](http://istio.doczh.cn/)

### pinpoint

[分布式性能管理监控工具 Pinpoint 入门视频课程_共3课时-51CTO学院](http://edu.51cto.com/course/9181.html)

[PinPoint分布式全链路监控搭建_清屏网_在线知识学习平台](http://www.qingpingshan.com/rjbc/java/243263.html)

[Pinpoint安装部署 · Issue #166 · ameizi/DevArticles](https://github.com/ameizi/DevArticles/issues/166)

[pinpoint 安装部署 - ﹏猴子请来的救兵 - 博客园](http://www.cnblogs.com/yyhh/p/6106472.html)

### spring security

[Spring Security | 徐靖峰|个人博客](https://www.cnkirito.moe/categories/Spring-Security/)

[配置表单登录_Spring Security 4官方文档中文翻译与源码解读教程_田守枝Java技术博客](http://www.tianshouzhi.com/api/tutorials/spring_security_4/265)

[spring security](https://aquariuspj.gitbooks.io/spring-security-4-reference/content/)

[spring cloud 微服务整合oauth2 | 小明啊喂](http://sylarlove.coding.me/2016/11/26/spring-cloud-%E5%BE%AE%E6%9C%8D%E5%8A%A1%E6%95%B4%E5%90%88oauth2/)

[Categories — Blog_龙飞](https://longfeizheng.github.io/categories/#Security)

[Spring Security OAuth2](http://projects.spring.io/spring-security-oauth/docs/oauth2.html)

[通用密码加密 · Spring Security Tutorial](https://waylau.gitbooks.io/spring-security-tutorial/docs/password-encoder.html)

[新标签页](chrome://newtab/)

[spring security oauth2 password授权模式 - code-craft - SegmentFault 思否](https://segmentfault.com/a/1190000012260914)

### Python

- [Scrapy入门教程（Scrapy Tutorial） ·](https://oner-wv.gitbooks.io/scrapy_zh/content/%E7%AC%AC%E4%B8%80%E6%AD%A5/scrapy%E5%85%A5%E9%97%A8%E6%95%99%E7%A8%8B.html)
- [Python教程 - 廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000)



### Golang

- [Introduction | go语言入门](https://zengweigang.gitbooks.io/core-go/content/)



### pay

- [如何做一个对账系统](https://mp.weixin.qq.com/s/ZX-XSu5todaKuqSOWvTgxw)
- [高吞吐消息网关的探索与思考](https://mp.weixin.qq.com/s?__biz=MjM5MDI3MjA5MQ==&mid=2697266427&idx=2&sn=a7105705a1120908984088fd2bcdcfdf&chksm=8376fbcfb40172d98606e8e5de9bb8fd1d7f40652760269d6670d66f6c464b7ee9506a39c0c9&mpshare=1&scene=1&srcid=0908Vy3eSpKXQBlYSbEZptNQ&pass_ticket=j/zl3CHiE8bVLjqJOcjnBzLIIAkAdaYF9Utu+WqG+x8=#rd)
- [最全支付系统设计](https://mp.weixin.qq.com/s/XTJ7jjax4BPEzrflnWFPhA)
- [以太坊](http://wiki.jikexueyuan.com/project/ethereum/ethereum-go-java-client.html)
- [区块链](http://ethcast.com/?page=3)
- [[中文\] 以太坊白皮书](https://github.com/ethereum/wiki/wiki/%5B%E4%B8%AD%E6%96%87%5D-%E4%BB%A5%E5%A4%AA%E5%9D%8A%E7%99%BD%E7%9A%AE%E4%B9%A6)

# 热加载工具jrebel破解Dockerfile





## Dockerfile

```
FROM maven:3

MAINTAINER Pig lengleng <wangiegie@gmail.com>

# 安装git
RUN apt-get update && apt-get -y install git

#下载激活程序
RUN git clone https://gitee.com/hsLeng/JrebelLicenseServerforJava.git

RUN cd JrebelLicenseServerforJava \
    && mvn compile 
#创建启动脚本
RUN echo -e "\
echo 启动 \
	&& cd /JrebelLicenseServerforJava \
	&& mvn exec:java -Dexec.mainClass='com.vvvtimes.server.MainServer' -Dexec.args='-p 8888' \
">/start.sh \
&& chmod u+x /start.sh
EXPOSE 8888

ENTRYPOINT ["/bin/bash","/start.sh"]
```

## 使用

<https://hub.docker.com/r/pig4cloud/jrebel/>

```
docker run -d -it -p 8888:8888 --name jrebel pig4cloud/jrebel:2018.4
```

[http://IP:8888/GUID](http://ip:8888/GUID);公司里用的178有，也是8888端口
需要修改为 <http://xxx.com:8888/88414687-3b91-4286-89ba-2dc813b107ce> 这样的地址
后面的为GUID，随便找个GUID在线生成器生成个就行了

# JAVA全套





Java基础阶段
一、	20天横扫Java基础（课堂实录）
<https://pan.baidu.com/s/1htTzZRQ>

二、	尚硅谷Java基础实战——Bank项目
<http://pan.baidu.com/share/link?shareid=3690978764&uk=573533038>

三、	尚硅谷_ORACLE、SQL、PLSQL 视频教程
<https://pan.baidu.com/s/1ghb9ENL>

四、	尚硅谷JDBC视频教程
<https://pan.baidu.com/s/1c3XBTk8>

五、	Java8新特性
<http://pan.baidu.com/s/1cgWOH4>

六、	Java——JUC
<http://pan.baidu.com/s/1hsoh76k>

七、	Java——NIO
<http://pan.baidu.com/s/1c2N1ADy>

八、	最新Java9新特性 视频
链接: <https://pan.baidu.com/s/1ge85H4Z>
密码: 9e1k

JavaWeb阶段
一、	尚硅谷_JavaScript DOM编程视频教程
<https://pan.baidu.com/s/1dzPYA6>

二、	尚硅谷jQuery 视频教程
<https://pan.baidu.com/s/1jJkaWya>

三、	尚硅谷Ajax视频教程
<https://pan.baidu.com/s/1skDOKZ7>

四、	尚硅谷JavaWeb视频基础
（涵盖JavaWEB 企业级开发所需的Servlet、JSP、MVC 设计模式、EL 表达式、JavaBean、国际化、Cookie和HttpSession、JavaMail等全部核心技术。）
<https://pan.baidu.com/s/1kU6Ley7>

五、	尚硅谷JavaWEB 项目实战（图书商城）
<https://pan.baidu.com/s/1jIoAMKe>

JavaEE阶段
一、	尚硅谷Struts2视频教程
<https://pan.baidu.com/s/1jI6xxkE>

二、	尚硅谷Hibernate 4视频教程
<https://pan.baidu.com/s/1bqpEEej>

三、	尚硅谷Spring 4视频教程
<https://pan.baidu.com/s/1Qk_-M7AMg3mLJjarYsaNbQ>

四、	尚硅谷SSH整合&综合案例视频
<https://pan.baidu.com/s/1dFbTMxV>

五、	尚硅谷SVN视频教程
<https://pan.baidu.com/s/1kWZz9vp>

六、	尚硅谷SpringMVC视频教程
<https://pan.baidu.com/s/1gfoaUw7>

七、	尚硅谷JPA视频教程
<https://pan.baidu.com/s/1hsqGMOW>

八、	尚硅谷SpringData视频
<https://pan.baidu.com/s/1c38938W>

九、	尚硅谷SSSP整合&分页视频
<https://pan.baidu.com/s/1miEVgr2>

十、	尚硅谷Redis视频
<http://pan.baidu.com/s/1pLKsBOJ>

十一、 尚硅谷Maven视频
<https://pan.baidu.com/s/1dHfbx8d>

十二、 尚硅谷Shiro视频
<https://pan.baidu.com/s/1yXiOStKfxSCYoMHsNrnCFQ>

十三、 尚硅谷MySQL高级视频
<https://pan.baidu.com/s/1i7ircH3>

十四、 尚硅谷MyBatis 视频
<https://pan.baidu.com/s/1snbVg77>

十五、 尚硅谷SSM高级视频
<https://pan.baidu.com/s/1eTcHjRc>

十六、 尚硅谷MySQL基础视频178集
<https://pan.baidu.com/s/1mjCyBm4>
密码: p03n

十七、 最新尚硅谷Spring注解驱动开发
<https://pan.baidu.com/s/1SzHGre2Upj8NzzGZ_6qM4Q>

十八、 最新尚硅谷SpringBoot视频
<https://pan.baidu.com/s/1isXPv_NrBX2Fuf9pRLU2sQ>
密码: sya6

十九、最新尚硅谷Mapper视频
<https://pan.baidu.com/s/1yfzUkHjMiF613uiiM5KBYw>
密码：l0xw

二十、最新尚硅谷Linux视频
<https://pan.baidu.com/s/1AmDqMODihyifgW9gevrSwA>
密码：kxpp

二十、最新尚硅谷SVN高级视频
<https://pan.baidu.com/s/1ADe9Db5ZbcKC4I_V2RiwDw>
密码：6ean

二十一、最新尚硅谷SpringCloud视频
<https://pan.baidu.com/s/1nB23cEOZJmbCkJebAU4hCg>
密码：w4vq
【全套Android教程--打包下载地址】

Android核心技术
一、Android核心基础_15天精讲精练
<https://pan.baidu.com/s/1b86u2E>

二、Android自定义控件视频
<https://pan.baidu.com/s/1hrOVZd6>

三、Android—JNI视频
<http://pan.baidu.com/s/1kVqBCmr>

四、Android与H5互调
<https://pan.baidu.com/s/1miHaDbM>

五、Android常用第三方框架源码分析
<http://pan.baidu.com/s/1o789Vjc>

六、尚硅谷Android视频《多渠道打包》
<http://pan.baidu.com/s/1dEVpQyX>

Android项目实战
一、Android项目实战—手机影音
<http://pan.baidu.com/s/1i5wLMbN>

二、最新Android项目—硅谷新闻
<https://pan.baidu.com/s/1nvASXvF>

三、最新Android项目实战—硅谷社交
<https://pan.baidu.com/s/1dFyXZxR>

四、最新Android项目—硅谷商城[新]
<http://pan.baidu.com/s/1o8MyptC>

五、最新Android项目—硅谷P2P金融
<https://pan.baidu.com/s/1KJbXUd3ymMhmJUPCqT9gzA>

Android前沿技术
一、Android_软件框架搭建
<https://pan.baidu.com/s/1hsFIYig>

二、Android_OKHttp使用方法
<https://pan.baidu.com/s/1c5McVW>

三、Android_JSON解析
<http://pan.baidu.com/s/1c23eePE>

四、Android_xUtils3
<https://pan.baidu.com/s/1nvGsExF>

五、Android_Afinal
<http://pan.baidu.com/s/1c7lXH8>

六、Android_Volley
<http://pan.baidu.com/s/1jIkBalg>

七、Android_ButterKnife
<http://pan.baidu.com/s/1pKOgh9x>

八、Android_EventBus
<http://pan.baidu.com/s/1qXYTyA4>

九、Android_ImageLoader
<http://pan.baidu.com/s/1o7DsPmy>

十、Android_Picasso
<http://pan.baidu.com/s/1c1JITo8>

十一、Android_Glide
<http://pan.baidu.com/s/1hswlhu0>

十二、Android_Fresco
<http://pan.baidu.com/s/1qXHtwdA>

十三、Android_RecyclerView
<http://pan.baidu.com/s/1kVjTLJ5>

十四、Android_Pulltorefresh
<http://pan.baidu.com/s/1c20xVm4>

十五、 Android_UniversalVideoView
<http://pan.baidu.com/s/1mhEK9EK>

十六、 Android_JieCaoVideoPlayer
<https://pan.baidu.com/s/1geZZ1Ov>

十七、 Android_Banner
<https://pan.baidu.com/s/1nv2jpDB>

十八、CountdownView秒杀
<https://pan.baidu.com/s/1nvAWFMT>

十九、OpenDanmaku弹幕
<https://pan.baidu.com/s/1eS2x2Hc>

二十、TabLayout&ViewPager
<https://pan.baidu.com/s/1mhCKJag#list/path=%2F>

【全套H5前端教程--打包下载地址】

一、HTML & CSS 核心教程：（103集实战教学，从入门到精通）
<http://pan.baidu.com/s/1pLwKZN1>

二、尚硅谷JavaScript视频（140集实战教学，从入门到精通）
<https://pan.baidu.com/s/1gfh9q8r>

三、尚硅谷JavaScript高级视频
<https://pan.baidu.com/s/1cLhs0u>

四、尚硅谷jQuery视频
<https://pan.baidu.com/s/1i5Gjxlj>

五、最新尚硅谷NodeJS 视频
链接: <https://pan.baidu.com/s/1cnr0Cm>
密码: sqku

六、最新尚硅谷MongoDB 视频
链接: <https://pan.baidu.com/s/1mirGFyw>
密码: nwe1

七、最新尚硅谷Zepto 视频
链接: <https://pan.baidu.com/s/1o7PSymu>
密码: e86p

八、最新尚硅谷AngularJS 视频
链接: <https://pan.baidu.com/s/1o85jOVK>
密码: 7vi2

九、最新尚硅谷ES5_6_7 视频
链接: <https://pan.baidu.com/s/1i4Z5VNZ>
密码: 3fuy

十、最新尚硅谷JS模块化 视频
链接: <https://pan.baidu.com/s/1skO0tJZ>
密码: tekn

十一、最新尚硅谷自动化构建工具 视频
（1）webpack 链接: <https://pan.baidu.com/s/1kUG5cLT> 密码: ru45
（2）Gulp 链接: <https://pan.baidu.com/s/1hsMqZkS> 密码: nprj
（3）Grunt 链接: <https://pan.baidu.com/s/1bGhxL0> 密码: m7kq

十二、最新尚硅谷React视频
<https://pan.baidu.com/s/1MSNJW3Uw6g7y70nDRfF9Bg>
密码：rlhr

十三、最新尚硅谷CSS2.1 视频
链接：<https://pan.baidu.com/s/1ggA6SPt>
密码：jybl

十三、最新尚硅谷CSS3 视频
链接：<https://pan.baidu.com/s/1bqiUHYZ>
密码：jojr

十四、最新尚硅谷less 视频
链接：<https://pan.baidu.com/s/1jJFk5MI>
密码：izzk

十五、最新尚硅谷bootstrap 视频
链接：<https://pan.baidu.com/s/1eTxHHN8>
密码：hzet

十六、最新尚硅谷HTML5核心视频
<https://pan.baidu.com/s/18hy_J8FdmBYabVGU8BqVKA>
密码：3fhg

十七、最新尚硅谷HTML5实战视频
<https://pan.baidu.com/s/1ipfFFhtWGvNuCMicxnzQdw>
密码：dehi

十八、最新尚硅谷HTML5项目-谷粒音乐
<https://pan.baidu.com/s/1u6LBOWa9QCpETeC3gjzojw>
密码：plb6

【35季公开课教程-打包地址下载】

第1季：横扫Java基础核心技术
<https://pan.baidu.com/s/1cGZpyY>

第2季：Java基础加强
<https://pan.baidu.com/s/1qXNcgpu>

第3季：数据库关键技术
<https://pan.baidu.com/s/1dEHsT0H>

特别季：光棍节，4晚搞定面向对象
<https://pan.baidu.com/s/1skTfGyp>

第4季：Java就业面试攻略（含：简历模板、面试技巧)
<https://pan.baidu.com/s/1hsQWvVQ>

第5季：JavaWeb书城实战
<https://pan.baidu.com/s/1dFOuFbb>

第6季：Android从入门到实战
<https://pan.baidu.com/s/1pL7LnUN>

第7季：锋利的JavaScript
<https://pan.baidu.com/s/1bKgJxW>

第8季：从容面对Java基础笔试&面试
<https://pan.baidu.com/s/1slVxKjN>

附加课：最流行的JS框架_jQuery
<https://pan.baidu.com/s/1dEX7Ozv>

第9季：Android实战_来电拦截专家
<https://pan.baidu.com/s/1cAnHam>

第10季：Java基础实战_战队组建管理系统
<https://pan.baidu.com/s/1o7TlL2a>

第11季：深入解析Ajax网页无刷新技术与项目实战
<https://pan.baidu.com/s/1hs7Z3cK>

第12季：30分钟打造Android万能播放器
<https://pan.baidu.com/s/1gfq0FS3>

第13季：Android高薪就业攻略
<https://pan.baidu.com/s/1jIEbd4a>

第14季：客户信息管理系统
<https://pan.baidu.com/s/1c2niZJE>

辅导课：Android全套视频-学习指导&答疑
<https://pan.baidu.com/s/1b9X0Sm>

第15季：Android Studio入门及使用技巧
<https://pan.baidu.com/s/1nv63xHZ>

第16季：玩转Android与H5互调
<https://pan.baidu.com/s/1dFo2PNF>

第17季：HTML5实战_天猫商城品牌墙
<https://pan.baidu.com/s/1hr4v8Pm>

第18季：全栈开发_node服务端开发
<https://pan.baidu.com/s/1hrOEuuK>

第19季：实战：360度全景图片
<https://pan.baidu.com/s/1hsKkPJQ>

第20季：HTML5特效实战
<https://pan.baidu.com/s/1kVBrpZp>

第21季：3小时玩转微信小程序入门
<https://pan.baidu.com/s/1eUnMTii>

第22季：CSS3特效实战
<https://pan.baidu.com/s/1dESOjFr>

第23季：轻松搞定毕业设计:论文写作+项目实战
<https://pan.baidu.com/s/1eS2DVjW>

第24季：Java8新特性全剖析
<https://pan.baidu.com/s/1boL0IMr>

第25季：BAT前端面试揭秘
<https://pan.baidu.com/s/1i4WdO4t>

第26季：1小时带你走进大数据世界
<https://pan.baidu.com/s/1c4NYTC>

第27季：大数据项目实战--仿天猫用户行为分析
<https://pan.baidu.com/s/1dEKGHQL>

第28季：如何做互联网时代的“出彩”Java工程师
<https://pan.baidu.com/s/1nvFqWHF>

第29季：下一个风口--Python与人工智能
<https://pan.baidu.com/s/1nuS7Qwp>

第30季：1小时解密程序员的黑魔法Python
<https://pan.baidu.com/s/1kV9Voyj>

第31季：1小时参悟Java8面向对象
<https://pan.baidu.com/s/1hsAHvbI>

第32季：更好的Java IDE之争：IDEA挑战Eclipse
<https://pan.baidu.com/s/1c2LEPJ6>

第33季：Python学员作品之《雷电战机》
<https://pan.baidu.com/s/1o7Ha6eA>

第34季：HTML5实战之Canvas刮刮卡
<https://pan.baidu.com/s/1ge7Lw9l>

第35季：强大的R语言
<https://pan.baidu.com/s/1gfENmeR>

第36季：毕业的三岔口
<https://pan.baidu.com/s/1o8qmSlk>

第37季：模块化打包神器：pack
<http://pan.baidu.com/s/1nvxHvnz>

第38季：快速入门JVM
<http://pan.baidu.com/s/1pKHalAz>

第39季：抛开噱头，看大数据与人工智能
<https://pan.baidu.com/s/1c20dj1m>

第40季：Java8&9就业面试攻略
<https://pan.baidu.com/s/1nv45pZr>

第41季：大话浏览器渲染原理
<https://pan.baidu.com/s/1pMMz1I7#list/path=%2F>

第42季：	Python核心语法实战：学生管理系统
<https://pan.baidu.com/s/1dGmSNeh#list/path=%2F>

第43季：移动端重力感应：摇一摇的实现
<https://pan.baidu.com/s/1NcKhY5HAr0THWG-V22X0cg#list/path=%2F>

公开课：Spring Boot实战/Spring Cloud
<https://pan.baidu.com/s/1c-P-tKiRUfJsD4L7uKl7Ug#list/path=%2F>

公开课：大数据架构师课程：高薪实战课程
<https://pan.baidu.com/s/15mBp1rNPoOHMnlILDYQXjw#list/path=%2F>

公开课：大数据项目实战--智慧出行
<https://pan.baidu.com/s/19SncMsfajhDGIAzoFHlpdA>

公开课：从比特币到区块链
<https://pan.baidu.com/s/1Cv0lEq-5x8bYRHsLDKEe1g#list/path=%2F>

【开发工具、技术文档、jar包资料】：
Java：
java基础文档：<https://pan.baidu.com/s/1o8A5kKy>

JavaWeb技术文档：<https://pan.baidu.com/s/1c1KcMNu>

javaee技术文档：<https://pan.baidu.com/s/1dFwAuNR>

教学课件：<https://pan.baidu.com/s/1c2tUAHU>

就业相关：<https://pan.baidu.com/s/1slv5Yrz>

Java开发工具：<http://www.atguigu.com/opensource.shtml>

Jar: <https://pan.baidu.com/s/1jIKMHcM>

Android：
Android内部讲课文档：<https://pan.baidu.com/s/1bpnkZCV>

Android技术文档：<https://pan.baidu.com/s/1o78TbUM>

Android使用工具：<https://pan.baidu.com/s/1skZRoLZ>

Android框架包清单：<https://pan.baidu.com/s/1skLEly9>

前端H5：
开发工具：<https://pan.baidu.com/s/1jH8vplG>

技术文档：<https://pan.baidu.com/s/1mhZv3q4>

框架包： <https://pan.baidu.com/s/1nvBThmp>

Jar：<https://pan.baidu.com/s/1pKY9yAZ>

2018最新JavaEE、前端H5、Python、大数据学习路线图！

![img](https://box.kancloud.cn/f87120632cb75cd2a4a52006570ccefa_517x686.png)

# oAuth2开发指南





## 介绍

这是 [`OAuth 2.0`](http://tools.ietf.org/html/draft-ietf-oauth-v2)支持的用户指南. 对于 OAuth 1.0来说, 一切都是不同的, 所以 [see its user guide](https://www.kancloud.cn/lengleng/pig-guide/oauth1.html).

这个用户指南分为两个部分，第一个是OAuth 2.0提供者，第二个是OAuth 2.0客户端。 对于提供者和客户端， 示例代码的最佳来源是 [integration tests](https://github.com/spring-projects/spring-security-oauth/tree/master/tests) 和[sample apps](https://github.com/spring-projects/spring-security-oauth/tree/master/samples/oauth2).

## OAuth 2.0 提供者

OAuth 2.0提供者机制负责公开OAuth 2.0受保护的资源。配置包括建立OAuth 2.0客户端，可以独立地或代表用户访问其受保护的资源。提供者通过管理和验证用于访问受保护资源的OAuth 2.0令牌来实现这一点。在适用的情况下，提供者还必须为用户提供一个接口，以确认客户端可以访问受保护的资源(即确认页面)。

## OAuth 2.0 提供者实现类

OAuth 2.0中的提供者角色实际上是在授权服务和资源服务之间进行划分的，虽然它们有时是在同一个应用程序中，但在Spring Security OAuth中，您可以选择在两个应用程序之间进行拆分，并且拥有多个共享授权服务的资源服务。令牌的请求由Spring MVC控制器端点来处理，而对受保护资源的访问由标准Spring安全请求过滤器处理。为了实现OAuth 2.0授权服务器，Spring安全过滤器链中需要以下端点:

- [`AuthorizationEndpoint`][AuthorizationEndpoint] 用于服务请求的授权。默认URL: `/oauth/authorize`.
- [`TokenEndpoint`][TokenEndpoint] 用于服务访问令牌的请求。默认URL: `/oauth/token`.

下面的过滤器需要实现OAuth 2.0资源服务器:

- [`OAuth2AuthenticationProcessingFilter`][OAuth2AuthenticationProcessingFilter] 用于为请求提供一个经过身份验证的访问令牌进行身份验证。

对于所有OAuth 2.0提供者特性， 可以使用特殊的Spring OAuth `@Configuration` 适配器配置简化配置 . 还有一个用于OAuth配置的XML命名空间, 这个模式在 [<http://www.springframework.org/schema/security/spring-security-oauth2.xsd>][oauth2.xsd]. 命名空间是 `http://www.springframework.org/schema/security/oauth2`.

## 授权服务器配置

在配置授权服务器时，您必须考虑客户端用于从最终用户(例如授权代码、用户凭证、刷新令牌)中获得访问令牌的授权类型。 服务器的配置用于提供客户端详细信息服务和令牌服务的实现，并在全局范围内启用或禁用该机制的某些切面。但是，请注意，每个客户端都可以配置特定的权限，以便能够使用某些授权机制和访问授权。也就是说，仅仅因为您的提供者被配置为支持“客户端凭证”授予类型，并不意味着特定的客户端被授权使用该授予类型。

@EnableAuthorizationServer注释用于配置OAuth 2.0授权服务器机制，以及任何实现AuthorizationServerConfigurer的@ bean(有一个方便的适配器实现提供了空方法的实现) 。下面的特性被委托给由Spring创建的配置器，并传递给AuthorizationServerConfigurer`:

- `ClientDetailsServiceConfigurer`: 定义客户端详细信息服务的配置程序。客户端细节可以被初始化，也可以直接引用现有的存储。
- `AuthorizationServerSecurityConfigurer`: 定义令牌端点上的安全约束。
- `AuthorizationServerEndpointsConfigurer`: 定义授权和令牌端点和令牌服务。

提供者配置的一个重要方面是授权代码被提供给OAuth客户端（在授权代码授予中）。授权代码由OAuth客户端获得，它将终端用户引导到一个授权页面，用户可以在其中输入她的凭证，从而导致从提供者授权服务器重新定向到带有授权代码的OAuth客户端。在OAuth 2规范中详细说明了这一点。

在XML中，有一个< authorizationserver />元素，它以类似的方式用于配置OAuth 2.0授权服务器。

### 配置客户端详细信息

ClientDetailsServiceConfigurer(来自您的AuthorizationServerConfigurer的回调)可以用于定义客户端详细信息服务的内存或JDBC实现。客户端的重要属性是:

- `clientId`:(必需)客户id。
- `secret`: (需要信任的客户)客户的密钥，如果有的话。
- `scope`: 客户受限制的范围。如果作用域是未定义的或空的(默认的)，客户端不受范围限制。
- `authorizedGrantTypes`: 授权给客户端使用的授权类型。默认值是空的。
- `authorities`: 授权给客户的部门。(通常是 Spring Security authorities).

客户端详细信息可以在运行的应用程序中更新，通过直接访问底层存储（例如JdbcClientDetailsService案例中的数据库表）或通过ClientDetailsManager接口（ClientDetailsService的两个实现都实现了）。

> 注意:JDBC服务的模式并没有与库一起打包(因为在实践中可能会使用太多的变体)，但是有一个例子可以从 [test code in github开始。

### 管理令牌

[`AuthorizationServerTokenServices`][AuthorizationServerTokenServices] 接口定义了管理OAuth 2.0令牌所必需的操作。 请注意以下几点:

- 当创建访问令牌时，必须存储身份验证，以便稍后接受访问令牌的资源可以引用它。
- 访问令牌被用来加载用于授权其创建的身份验证。

在创建您的AuthorizationServerTokenServices实现时，您可能需要考虑使用具有许多策略的DefaultTokenServices来更改访问令牌的格式和存储。 默认情况下，它通过随机值创建令牌，并处理所有的东西，除了它委托给TokenStore的令牌的持久性。默认存储是[在内存中实现的][InMemoryTokenStore]，但还有一些其他实现可用。下面是对每种实现方式的一些讨论。

- 默认的`InMemoryTokenStore`对于单个服务器来说是完美的(例如，在失败的情况下，低流量和没有热交换到备份服务器)。大多数项目都可以从这里开始，并可能在开发模式中使用这种方式，从而能很容易的启动一个没有依赖关系的服务器。
- `JdbcTokenStore`和JDBC版本是同一种东西，它使用关系数据库来存储令牌数据。如果您可以在服务器之间共享一个数据库，那么可以使用JDBC版本，如果只有一个服务器，则可以扩展相同服务器的实例，如果有多个组件，则可以使用授权和资源服务器。为了使用 `JdbcTokenStore` ，您需要将 "spring-jdbc" 配置到classpath中.
- [JSON Web Token (JWT) version](https://www.kancloud.cn/lengleng/pig-guide/%60JwtTokenStore%60) 将所有关于grant的数据编码到令牌本身(因此没有任何后端存储，这是一个重要的优势)。 一个缺点是，您不能很容易地撤销访问令牌，因此它们通常在短时间内被授予，而撤销则在刷新令牌中处理。 另一个缺点是，如果您在其中存储了大量用户凭证信息，则令牌可以变得相当大。 `JwtTokenStore`并不是真正的“存储”，因为它没有保存任何数据，但是它在`DefaultTokenServices`中扮演了转换betweeen令牌值和身份验证信息的角色。

> 注意：JDBC服务的模式并没有与库一起打包（因为在实践中可能会用到太多的变体），但是有一个示例可以从github的 [test code in github开始。确保`@EnableTransactionManagement` 能够防止客户端应用程序在创建令牌时争用相同的行。 还要注意，示例模式有显式的主键声明——在并发环境中这些声明也是必需的。

### JWT令牌

要使用JWT令牌，您需要在授权服务器中使用`JwtTokenStore`。资源服务器还需要能够解码令牌，这样`JwtTokenStore` 就依赖于 `JwtAccessTokenConverter`，并且授权服务器和资源服务器都需要相同的实现。该令牌是默认签名的，并且资源服务器还必须能够验证签名，因此需要与授权服务器(共享私钥或对称密钥)相同的对称(签名)密钥，或者它需要与授权服务器(公私或非对称密钥)中的私钥(签名密钥)相匹配的公钥(验证器密钥)。公钥(如果可用)由`/oauth/token_key`端点上的授权服务器公开，该端点在默认情况下是安全的，具有访问规则“denyAll()”。您可以通过向`AuthorizationServerSecurityConfigurer`中注入标准的SpEL表达式来打开它。“permitAll（）”可能已经足够了，因为它是一个公钥。

要使用`JwtTokenStore` ，您需要在classpath上使用“Spring -security-jwt”(您可以在相同的github存储库中找到它，它与Spring OAuth相同，但有不同的发布周期)。

### 授权类型

`AuthorizationEndpoint` 支持的授权类型可以通过`AuthorizationServerEndpointsConfigurer`配置。默认情况下，除密码外，所有的授权类型都是受支持的(请参阅下面关于如何切换的详细信息)。以下属性影响授权类型:

- `authenticationManager`: 通过注入一个`AuthenticationManager`来打开密码授权。
- `userDetailsService`: 如果您注入了一个`UserDetailsService`，或者在全局上配置了一个(例如，在`GlobalAuthenticationManagerConfigurer`中)，那么刷新令牌授权将包含对用户详细信息的检查，以确保帐户仍然处于活动状态。
- `authorizationCodeServices`: 为身份验证代码授予定义授权代码服务(`AuthorizationCodeServices`)的实例)。
- `implicitGrantService`: 在imlpicit授权期间管理状态。
- `tokenGranter`: the `TokenGranter` (完全控制授予和忽略上面的其他属性)

在XML grant类型中，包括`authorization-server`元素。

### 配置的端点url

`AuthorizationServerEndpointsConfigurer` 有一个`pathMapping()`方法。它需要两个参数:

- 端点的默认(框架实现)URL路径。
- 需要的自定义路径(以“/”开头)

框架提供的路径是 `/oauth/authorize` (授权端点), `/oauth/token` (令牌端点), `/oauth/confirm_access` (用户在这里获得批准), `/oauth/error` (用于呈现在授权服务器错误), `/oauth/check_token` (用于资源服务器解码访问令牌。), and `/oauth/token_key` (如果使用JWT令牌，公开公钥进行令牌验证).

N.B. 应该使用Spring Security保护授权端点`/oauth/authorize`(或其映射的替代)，以便只有经过身份验证的用户才能访问它。 例如：使用标准的 Spring Security `WebSecurityConfigurer`:

```
@Override
protected void configure(HttpSecurity http) throws Exception {
	http
            .authorizeRequests().antMatchers("/login").permitAll().and()
        // default protection for all resources (including /oauth/authorize)
            .authorizeRequests()
            .anyRequest().hasRole("USER")
        // ... more configuration, e.g. for form login
}
```

> 注意:如果您的授权服务器也是一个资源服务器，那么还有另一个安全过滤器链，它的优先级较低，控制了API资源。 对于那些需要通过访问令牌来保护的请求，您需要它们的路径不能与主用户所面对的过滤器链中的那些相匹配，所以一定要包含一个请求matcher，它只挑选出上面的`WebSecurityConfigurer`中的非Api资源。

在`@Configuration`支持中，使用客户端机密的HTTP基本身份验证，Spring OAuth默认为您保护令牌端点。这不是XML中的情况(因此应该明确地保护它)。

在XML中，`<authorization-server/>` 元素有一些属性可用于以类似的方式更改缺省端点url。必须显式地启用`/check_token` 端点(使用`check-token-enabled` 的属性)。

## 定制用户界面

大多数授权服务器端点主要是由机器使用的，但是有一些资源需要一个UI，而这些资源是GET for `/oauth/confirm_access`和 `/oauth/error`的HTML响应。 它们在框架中使用了whitelabel实现，因此授权服务器的大多数真实实例都希望提供自己的实现，这样它们就可以控制样式和内容。 您所需要做的就是为这些端点提供一个带有`@RequestMappings`的Spring MVC控制器，而框架默认值将在调度程序中降低优先级。 在`/oauth/confirm_access`端点中，您可以预期一个`AuthorizationRequest`绑定到会话，该请求将携带需要获得用户批准的所有数据(默认的实现是`AuthorizationRequest`，因此要查看那里的起始点以复制)。您可以从该请求中获取所有的数据，并按您喜欢的方式呈现它，然后所有用户需要做的就是将批准或拒绝授予的信息发布回 `/oauth/authorize`。请求参数直接传递给`AuthorizationEndpoint`中的`UserApprovalHandler`，这样您就可以随意地解释数据了。 默认的`UserApprovalHandler`取决于您是否在`AuthorizationServerEndpointsConfigurer`中提供了`ApprovalStore`（在这种情况下，它是`ApprovalStoreUserApprovalHandler`）或not（在这种情况下，它是一个`TokenStoreUserApprovalHandler`）。标准审批处理程序接受以下内容:

- `TokenStoreUserApprovalHandler`: 通过`user_oauth_approval`的一个简单的yes/no决策等于“true”或“false”。
- `ApprovalStoreUserApprovalHandler`: 一组`scope.*` 参数键与所请求的作用域相等。 参数的值可以是“true”或“approved”（如果用户批准了授权），则用户被认为拒绝了该范围。 如果至少有一个范围被批准，那么授权是成功的。

> 注意:不要忘记将CSRF保护包含在您为用户呈现的表单中。Spring Security在默认情况下期望一个名为“_csrf”的请求参数(它提供了请求属性中的值)。 请参阅Spring安全用户指南以获得更多信息，或者查看whitelabel实现以获得指导。

### 执行SSL

普通HTTP可以用于测试，但是授权服务器只能在生产中使用SSL。 您可以在一个安全的容器或代理的后面运行该应用程序，如果您正确地设置了代理和容器(这与OAuth2无关)，那么它应该可以正常工作。 您还可能希望使用Spring Security `requiresChannel()`约束来保护端点。 对于`/authorize`端点，你要做的是作为你正常的应用程序安全的一部分。对于`/token`端点，在`AuthorizationServerSecurityConfigurer` 中有一个标记，您可以使用`sslOnly()`方法进行设置。在这两种情况下，安全通道设置都是可选的，但如果它在不安全的通道上检测到请求，则会导致Spring Security重定向到它认为是安全通道的安全通道。

## 自定义错误处理

授权服务器中的错误处理使用标准的Spring MVC特性，即端点中的`@ExceptionHandler`方法。 用户还可以为端点本身提供一个`WebResponseExceptionTranslator`，这是改变响应内容的最佳方式，而不是改变响应的方式。在授权端点的情况下，在令牌端点和OAuth错误视图(`/oauth/error`)的情况下，将异常委托委托给`HttpMesssageConverters`(可以添加到MVC配置)。为HTML响应提供了whitelabel错误端点，但是用户可能需要提供一个自定义实现(例如，只需添加一个`@RequestMapping("/oauth/error")`的 `@Controller`)。

## 将用户角色映射到作用域。

有时，限制令牌的范围不仅限于分配给客户端的作用域，还可以根据用户自己的权限来限制令牌的范围。 如果您在`AuthorizationEndpoint`中使用`DefaultOAuth2RequestFactory` ，那么您可以设置一个flag `checkUserScopes=true` ，从而将允许范围限制为与用户角色相匹配的范围。 您还可以将`OAuth2RequestFactory`注入到`TokenEndpoint`中，但是如果您还安装了一个`TokenEndpointAuthenticationFilter`(也就是使用密码授权)，那么您只需要在HTTP `BasicAuthenticationFilter`之后添加那个过滤器。当然，您也可以实现自己的规则，将范围映射到角色，并安装您自己的`OAuth2RequestFactory`版本。如果您使用`@EnableAuthorizationServer`,则`AuthorizationServerEndpointsConfigurer`允许您注入自定义的`OAuth2RequestFactory` ，这样您就可以使用该特性来设置一个工厂。

## 资源服务器配置

资源服务器(可以与授权服务器或单独的应用程序相同)提供由OAuth2令牌保护的资源。 Spring OAuth提供了一个实现此保护的Spring安全身份验证过滤器。您可以在 `@Configuration`类上使用`@EnableResourceServer` 来切换它，并使用`ResourceServerConfigurer`配置它（必要时）。他可以配置以下功能:

- `tokenServices`: 定义令牌服务的bean (ResourceServerTokenServices实例)。
- `resourceId`: 资源的id(可选，如果存在推荐并将由auth服务器验证)。
- 资源服务器的其他扩展点(例如从传入请求中提取令牌的`tokenExtractor`)。
- 请求受保护资源的请求者(默认为所有)
- 受保护资源的访问规则(默认为“已验证”)
- Spring Security中`HttpSecurity`配置程序允许的受保护资源的其他定制。

`@EnableResourceServer`注解自动将`OAuth2AuthenticationProcessingFilter`类型的过滤器添加到Spring Security过滤器链中。

在XML中有一个带有id属性的`<resource-server/>`元素——这是servlet过滤器的bean id，然后可以手工添加到标准Spring Security链中。

您的`ResourceServerTokenServices`是与授权服务器的契约的另一半。如果资源服务器和授权服务器都在同一个应用程序中，并且使用`DefaultTokenServices` ，那么您就不必对此进行过多的思考，因为它实现了所有必要的接口，因此它是自动一致的。 如果您的资源服务器是一个单独的应用程序，那么您必须确保与授权服务器的功能相匹配，并提供一个知道如何正确解码`ResourceServerTokenServices`。与授权服务器一样，您可以经常使用 `DefaultTokenServices`，而选择主要通过`TokenStore`(后端存储或本地编码)来表示。另一种选择是`RemoteTokenServices` ，它是一个Spring OAuth特性(不是规范的一部分)，允许资源服务器通过授权服务器上的HTTP资源(`/oauth/check_token`)来解码令牌。如果资源服务器中没有大量的流量(每个请求都必须与授权服务器进行验证)，或者如果您有能力缓存结果，那么`RemoteTokenServices`是很方便的。 要使用`/oauth/check_token`端点，您需要在`AuthorizationServerSecurityConfigurer`中通过更改它的访问规则来公开它(默认为“denyAll()”)。例如

```
@Override
public void configure(AuthorizationServerSecurityConfigurer oauthServer) throws Exception {
	oauthServer.tokenKeyAccess("isAnonymous() || hasAuthority('ROLE_TRUSTED_CLIENT')")
	.checkTokenAccess("hasAuthority('ROLE_TRUSTED_CLIENT')");
}
```

在这个例子中，我们配置了`/oauth/check_token` 端点和`/oauth/token_key`端点（因此可信资源可以获得JWT验证的公钥）。这两个端点通过使用客户端凭证的HTTP基本身份验证保护。

### 配置一个oauthaware表达式处理程序。

您可能想要利用Spring Security的基于表达式的访问控制。表达式处理程序将默认在@enableresourceserver设置中注册。 表达式包括 *#oauth2.clientHasRole*, *#oauth2.clientHasAnyRole*, 和_#oath2.denyClient_ 可以根据oauth客户端的角色来提供访问(请参阅完整列表的 `OAuth2SecurityExpressionMethods` )。在XML中，您可以使用常规的`<http/>`安全配置的 `expression-handler`程序元素注册一个oauth-aware表达式处理程序。

## OAuth 2.0客户端

OAuth 2.0客户端机制负责访问其他服务器的OAuth 2.0保护资源。 该配置涉及到建立用户可能访问的相关保护资源。 客户端还可能需要为用户提供存储授权代码和访问令牌的机制。

### 受保护的资源配置

可以使用[`OAuth2ProtectedResourceDetails的bean定义来定义受保护的资源(或“远程资源”)。受保护的资源具有以下属性:

- `id`: 资源的id。该id仅供客户端用于查找资源;在OAuth协议中从未使用过。它还被用作bean的id。
- `clientId`: OAuth客户端id。这是OAuth提供者识别您的客户端的id。
- `clientSecret`: 与资源有关的secret。默认情况下，没有secret是空的。
- `accessTokenUri`: 提供访问令牌的提供者OAuth端点的URI。
- `scope`: 逗号分隔的字符串列表，指定访问资源的范围。默认情况下，没有指定范围。
- `clientAuthenticationScheme`: 客户端用于验证访问令牌端点的方案。建议值:“http_basic”和“form”。默认值:“http_basic”。见OAuth 2规范第2.1节。

不同的grant类型有不同的`OAuth2ProtectedResourceDetails`的具体实现(例如，`ClientCredentialsResource` 用于“client_credentials”授权类型)。对于需要用户授权的授权类型，还有一个属性:

- `userAuthorizationUri`: 如果用户需要授权访问该资源，则将重定向用户的uri。注意，这并不总是必需的，这取决于所支持的OAuth 2配置文件。

在XML中，有一个`<resource/>`元素，可以用来创建一个`OAuth2ProtectedResourceDetails`的bean。它具有匹配上述所有属性的属性。

### 客户端配置

对于OAuth 2.0客户端，配置是使用`@EnableOAuth2Client`简化的。它做了两件事:

- 创建一个过滤器bean(带有ID `oauth2ClientContextFilter`)来存储当前请求和上下文。在需要进行身份验证的情况下，它管理对OAuth身份验证uri的重定向。
- 在请求范围内创建一个类型`AccessTokenRequest`的bean。这可以通过授权代码(或隐式)授予客户端来保持与单个用户之间的冲突。

过滤器必须连接到应用程序中(例如，使用Servlet初始化器或使用相同名称的`DelegatingFilterProxy`的`web.xml`配置)。

`AccessTokenRequest`可用于以下的`OAuth2RestTemplate`:

```
@Autowired
private OAuth2ClientContext oauth2Context;

@Bean
public OAuth2RestTemplate sparklrRestTemplate() {
	return new OAuth2RestTemplate(sparklr(), oauth2Context);
}
```

OAuth2ClientContext在会话范围内(为您)放置，以保持状态不同的用户分开。如果不这样做，您将不得不在服务器上管理等效的数据结构，将传入的请求映射到用户，并将每个用户与`OAuth2ClientContext`的单独实例关联起来。

在XML中，有一个带有id属性的`<client/>`元素—这是一个servlet过滤器的bean id，必须在`@Configuration`案例中映射到`DelegatingFilterProxy`(具有相同的名称)。

### 访问受保护的资源

一旦您提供了资源的所有配置，现在就可以访问这些资源了。访问这些资源的建议方法是使用Spring 3中引入的[RestTemplate][restTemplate]。Spring Security的OAuth提供了一个扩展的RestTemplate，它只需要提供 [`OAuth2ProtectedResourceDetails`][OAuth2ProtectedResourceDetails]的实例。要使用用户令牌(授权代码授权)，您应该考虑使用`@EnableOAuth2Client`配置(或XML等效的`<oauth:rest-template/>`)，它创建一些请求和会话范围的上下文对象，以便不同用户的请求在运行时不会发生冲突。

一般来说，web应用程序不应该使用密码授予，因此，如果您能够支持 `AuthorizationCodeResourceDetails`，请避免使用`ResourceOwnerPasswordResourceDetails`。如果您需要从Java客户端获得工作密码，那么使用相同的机制来配置`OAuth2RestTemplate`并将凭证添加到`AccessTokenRequest`(这是一个映射，并且是临时的)，而不是`ResourceOwnerPasswordResourceDetails` (它在所有访问令牌之间共享)。

### 在客户端持久化令牌

客户端不需要存留令牌，但对于用户来说，在每次重启客户端应用程序时都不需要批准新的令牌授权，这对用户来说是件好事。ClientTokenServices接口定义了为特定用户保存OAuth 2.0令牌所需的操作。这里提供了JDBC实现，但是如果您喜欢实现您自己的服务，以便在持久性数据库中存储存取令牌和相关的认证实例，您可以这样做。
如果您想使用这个特性，您需要为`OAuth2RestTemplate`提供一个特殊配置的`AccessTokenProvider`。

```
@Bean
@Scope(value = "session", proxyMode = ScopedProxyMode.INTERFACES)
public OAuth2RestOperations restTemplate() {
	OAuth2RestTemplate template = new OAuth2RestTemplate(resource(), new DefaultOAuth2ClientContext(accessTokenRequest));
	AccessTokenProviderChain provider = new AccessTokenProviderChain(Arrays.asList(new AuthorizationCodeAccessTokenProvider()));
	provider.setClientTokenServices(clientTokenServices());
	template.setAccessTokenProvider(provider);
	return template;
}
```

## 为外部OAuth2提供者的客户定制。

一些外部的OAuth2提供者（例如Facebook）并没有正确地实现该规范，或者他们只是被困在一个较旧版本的规范中，而不是Spring Security OAuth。要在客户端应用程序中使用这些提供者，您可能需要调整客户端基础结构的各个部分。

以Facebook为例，在tonr2应用程序中有一个Facebook特性（您需要更改配置以添加您自己的、有效的、客户id和secret——它们在Facebook的网站上很容易生成）。

Facebook令牌响应也包含一个不兼容的JSON条目，用于令牌的失效时间（它们使用`expires`而不是`expires_in`），因此，如果您想在应用程序中使用过期时间，您将不得不使用定制的`OAuth2SerializationService`来手动解码它。