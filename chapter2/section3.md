# 我们简单Web服务的结构

在第一章，_几个基础中_，我们将这个应用分成四部分：
* Inventory服务
* Availability服务
* Booking服务
* Billing服务

一个可以用于构建我们项目的办法是，把它们作为作为单一模块，并且四个服务在一起编码。
虽然这样使得配置很简单，但是它也导致了单独部署整个模块的阻碍，处于对扩展性要求的考虑（参见第10章_扩展RESTful Web服务_，将讨论扩展性）。替代方案是，我们将把每个服务组织成单独的模块。

本书的目的，重点在于Maven。我们的项目将由六个独立的Maven模块组成：
* common：这个模块包含公共代码和将会用到的Hibernate设置
* inventory：这个是inventory服务的实现
* availability：这个是availability服务的实现
* booking：这个是booking服务的实现
* billing：这个是billing服务的实现
* all：出于开发和单独部署的原因，这个模块将被组织为使用四个服务的单独的Web应用

### 注意

关于使用Maven模块的更多信息可以在<https://maven.apache.org/guides/mini/guide-multiple-modules.html>找到文档参考。

因此我们的父POM看起来将是这样的：
```
<project... //出于可读性的目的省略
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.packtpub.rest-with-spring</groupId>
	<artifactId>rest-with-spring</artifactId>
	<version>1.0.0-SNAPSHOT</version>
	<packaging>pom</packaging>

	<modules>
		<module>common</module>
		<module>inventory</module>
		<module>availability</module>
		<module>booking</module>
		<module>billing</module>
		<module>all</module>
	</modules>

</project>
```

正如前面列出的，我们的模块声明在顶级pom.xml中。common模块是一个简单的JAR模块，而inventory，availability，booking，billing，和all都是声明为WAR模块。

### 技巧
完整的Maven设置可以下载** TODO **。
