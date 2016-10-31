# 定制JSON响应

为了符合大纲或满足要求，API设计者也许需要去控制怎样格式化JSON响应。正如在第三章，_第一个端点_中提到的，Spring Web使用Jackson来实现JSON的序列化。因此，定制我们的JSON格式，我们必需配置Jackson处理器。Spring Web提供了基于XML或者基于Java的方法来处理配置。在后面，我们将看到基于Java的配置方法。

我们假设我们请求属性名字是小写的带下划线字母，而不是驼峰命名法的情况。为了减少响应的大小，我们也要求不要包括为空的属性。

默认情况下，响应被格式化成下面这样：

```json
{    
	"status": "OK",    
	"data": {    
		"id": 1,    
		"name": "Room 1",    
		"roomCategoryId": 1,    
		"description": "Nice, spacious double bed room with usual amenities"    
	},    
	"error": null 
} 
```

首先我们创建一个`WebMvcConfigurerAdapter`的继承，然后我们提供指示给Jackson怎样格式化JSON信息：

```
@Configuration 
@EnableWebMvc 
public class JsonConfiguration extends WebMvcConfigurerAdapter {
	@Override  
	public void configureMessageConverters(List<HttpMessageConverter<?>> converters) {    
	converters.add(new MappingJackson2HttpMessageConverter(new Jackson2ObjectMapperBuilder()    .propertyNamingStrategy(PropertyNamingStrategy.CAMEL_CASE_TO_LOWER_CASE_WIT H_UNDERSCORES)    .serializationInclusion(Include.NON_NULL)    
	.build()));  
	} 
} 
```

当应用开始运行，Spring将发现这个类（感谢`@Configuration`注解），并且添加我们的转换器，`MappingJackson2HttpMessageConverter`。我们配置这个转换器格式名字属性为小写带下划线格式，且我们告诉Jackson忽略`null`属性。结果将被格式化为如下JSON：

```
{
	"status": "OK",  
	"data": {    
		"id": 1,    
		"name": "Room 1",    
		"room_category_id": 1,    
		"description": "Nice, spacious double bed room with usual amenities"  
	} 
}
```


我们可以看到`error`属性现在消失了，且客房目录ID属性名被格式化成了我们讨论过的格式。

### 注意

`org.springframework.http.converter.json.Jackson2ObjectMapperBuilder`提供了许多选项来控制JSON格式。Javadoc文档在<http://docs.spring.io/spring/docs/current/javadocapi/org/springframework/http/converter/json/Jackson2ObjectMapperBuilder.html>可用。


这一节给了控制响应格式基本的工具。这些响应格式应该被作为服务API的一部分来考虑，即修改已存在的响应应该被小心管理。下一节将讨论如何通过版本来管理响应格式。