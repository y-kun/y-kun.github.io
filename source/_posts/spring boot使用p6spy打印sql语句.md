---
title: spring boot使用p6spy打印sql语句
categoires: java
tags: spring boot
abbrlink: 1296037854
date: 2021-05-11 11:09:43
---

# 添加依赖

```java
<dependency>     
　<groupId>p6spy</groupId>     
　<artifactId>p6spy</artifactId>     
　<version>3.8.0</version> 
</dependency>
```


# 修改mysql数据库连接

```yaml
spring:   
　datasource:     
　　driver-class-name: com.p6spy.engine.spy.P6SpyDriver     
　　url: jdbc:p6spy:mysql://xx.xx.xx.xx:3306
```


# 添加<font color="#ff0000">spy.properties</font>配置文件

```yaml
#3.2.1以上使用
modulelist=com.baomidou.mybatisplus.extension.p6spy.MybatisPlusLogFactory,com.p6spy.engine.outage.P6OutageFactory
#3.2.1以下使用或者不配置
#modulelist=com.p6spy.engine.logging.P6LogFactory,com.p6spy.engine.outage.P6OutageFactory
# 自定义日志打印
logMessageFormat=com.baomidou.mybatisplus.extension.p6spy.P6SpyLogger
#日志输出到控制台
appender=com.baomidou.mybatisplus.extension.p6spy.StdoutLogger
# 使用日志系统记录 sql
#appender=com.p6spy.engine.spy.appender.Slf4JLogger
# 设置 p6spy driver 代理
deregisterdrivers=true
# 取消JDBC URL前缀
useprefix=true
# 配置记录 Log 例外,可去掉的结果集有error,info,batch,debug,statement,commit,rollback,result,resultset.
excludecategories=info,debug,result,commit,resultset
# 日期格式
dateformat=yyyy-MM-dd HH:mm:ss
# 实际驱动可多个
#driverlist=org.h2.Driver
# 是否开启慢SQL记录
outagedetection=true
# 慢SQL记录标准 2 秒
outagedetectioninterval=2
```