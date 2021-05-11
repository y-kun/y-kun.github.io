---
title: jar中没有主清单属性
categories: java
abbrlink: 2929262520
date: 2021-05-11 09:14:07
tags:
---

## pom.xml添加插件：

```yaml
<build>
　<!--自定义打包文件名-->
　<finalName>dinService</finalName>
　　<plugins>
　　　<plugin>
　　　　<groupId>org.springframework.boot</groupId>
　　　　<artifactId>spring-boot-maven-plugin</artifactId>
　　　　<configuration>
　　　　　<fork>true</fork>
　　　　　<!-- 如果没有该配置，devtools不会生效 -->
　　　　　<!-- 指定该Main Class为全局的唯一入口 -->
　　　　　<mainClass>cool.kunkun.service.ServiceApplication</mainClass>
　　　　　<layout>ZIP</layout>
　　　　</configuration>
　　　　<executions>
　　　　　<execution>
　　　　　　<goals>
　　　　　　　<goal>repackage</goal><!-- 可以把依赖的包都打包到生成的Jar包中 -->
　　　　　　</goals>
　　　　　</execution>
　　　　</executions>
　　　</plugin>
　　</plugins>
</build>
```