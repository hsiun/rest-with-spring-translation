# Apache Maven

Maven是一个开源的项目管理工具。它在简化基于Ant项目构建的需求下诞生，并且配置文件的转换也很方便。在很多实际情况中，它对典型的工作流提供了额外的支持，如为构建Java Web应用，提供共同遵守的公约。然而，Maven对定制构建过程支持不是很友好，对这种设计的指责成为了不选择Maven的主要原因。

### 注意 ###
关于Maven的更多信息可以在<https://maven.apache.org>找到。

虽然Maven提供了很多特性，但它们都属于本章的范围。我们将专注它对构建Java Web应用的支持。

下面的**POM(Project Object Model)**文件展示了Maven（在一个叫做pom.xml的文件中）如何声明一个项目。

```
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
	http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>com.packtpub.rest-with-spring</groupId>
	<artifactId>rest-with-spring</artifactId>
	<version>1.0.0-SNAPSHOT</version>
	<packaging>war</packaging>

</project>
```

这个pom.xml文件通过gav（groupId，artifactID，version）定义了一个项目，他也申明应用的结果将会被打包（为一个war文件，在当前情况）。

### 技巧 ###
Maven的artifacts属于一个组（典型的如`com.company.application`），并且必需要有一个唯一的标识（一般是应用名字）。

开发者可以自由的选择他们的版本格式。然而，Maven对于x.y格式的版本号支持最好，x是主版本号，y是次版本号。

### 注意 ###
SNAPSHOT版本后缀告诉Maven这个项目目前正在开发中。这意味着artifacts是由依赖解析处理的，这将会在下节介绍。