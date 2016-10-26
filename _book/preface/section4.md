# 排版约定

在本书中，你将找到多种文本格式，不同的格式区分不同的信息。这里是这些格式的一些示例，并解释了它们所代表的含义。

代码文字包括文本，数据库表名，文件夹名，文件名，文件类型名，路径名，URL，用户输入，和Twitter被显示为下面样子：“我们可以通过使用`include`关键字包含其他内容。”

一段代码被展示下面这样的：

```java
import org.springframework.web.bind.annotation.*;

@RestController
public class HelloWorldResource {
	@RequestMapping(method = RequestMethod.GET)
	public String helloWorld() {
		return "Hello, world!";
    }
}
```

当我们希望在一段代码中的某部分引起你的注意时，相关行或者项目将被设为黑体：

```
<dependency>
	<groupId>com.packtpub.rest-with-spring</groupId>
	<artifactId>rest-with-spring-billing</artifactId>
 	<version>1.0.0-SNAPSHOT</version>
	<classifier>classes<classifier>
</dependency>
```

命令行输入输出将被写成下面这样：

**mvn jetty:start**

**新术语**和**重要要的词语**将被加黑显示。 你将在屏幕上看到的单词，例如，在目录或者对话框中，显现这样一行文字：“举个例子，使用**IntelliJ IDEA**， 我们的简单Web服务项目可以被导入到IntelliJ IDEA中通过使用目录选项**文件|打开**。“

### 注意 ###
警告或者重要的笔记出现在类似这样的地方。

### 技巧 ###
技巧和小窍门出现在这里
