# 路径映射

一般来说，在类层面，`@org.springframework.web.bind.annotation.RequestMapping`注解允许路由（动词）请求到特定的资源类（或者控制器）路径。举个例子，在前面的代码片段中，`RoomsResource`类声明了一个顶级的请求映射，`@RequestMapping("/rooms")`。由于这个主机，这个类将处理到rooms路径的所有请求。