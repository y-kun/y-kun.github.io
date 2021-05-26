---
title: spring-retry重试机制
categories: java
tags: spring
abbrlink: 3118246143
date: 2021-05-18 15:00:46
---

<meta name="referrer" content="no-referrer" />

# pom.xml添加jar包

```xml
<dependency>
    <groupId>org.springframework.retry</groupId>
    <artifactId>spring-retry</artifactId>
    <version>1.3.1</version>
</dependency>
```



# 启动类或配置类添加<font color="#ff0000">@EnableRetry</font>注解

# 需要重试的方法上添加<font color="#ff0000">@Retryable</font>注解（需要使用注入的方式调用该方法）

```java
@Retryable(recover = "testRecover", backoff = @Backoff(value = 3000L, multiplier = 1))
public void test(Integer userId) {
    log.info("测试spring-retry,Retryable");
}
```

被`@Retryable`注解的方法会在发生异常时进行重试

`@Retryable`注解部分参数说明：

| 注解参数    | 作用                                                         |
| ----------- | ------------------------------------------------------------ |
| @Backoff    | 重试补偿机制                                                 |
| recover     | 指定达到最大重试次数依然失败后所调用的方法                   |
| value       | 与include同义                                                |
| include     | 可重试的异常类型，默认为空（如果exclude也是空的，则重试所有异常） |
| exclude     | 不可重试的异常类型，默认为空（如果include也是空的，则重试所有异常） |
| maxAttempts | 最大重试次数（包含第一次失败），默认为3                      |

`@Backoff`注解部分参数说明：

| 注解参数   | 作用                            |
| ---------- | ------------------------------- |
| delay      | 重试间隔时间，默认1000L（毫秒） |
| value      | 与delay同义                     |
| maxDelay   | 两次重试之间的最大间隔时间      |
| multiplier | 重试间隔时间倍数，默认0         |

在指定方法上标记`@Recover`来开启重试失败后调用的方法

当重试次数达到`multiplier`指定次数时，会触发该方法

<font color="#ff0000">注：`@Recover`和`@Retryable`方法的入参和返回值必须一致</font>

```java
@Recover
private void testRecover(Exception e, Integer userId) {
    log.info("测试spring-retry,Recover");
}
```

[github地址](https://github.com/spring-projects/spring-retry)

[文档地址](https://docs.spring.io/spring-retry/docs/)（文档目前最新版本为：1.2.2.RELEASE）