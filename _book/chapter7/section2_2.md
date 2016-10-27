# HTTP基础鉴权

这是HTTP标准提供的最简单形式的鉴权。它将用户名和密码组合为一个`Authorization`报文头传递给HTTP请求，这个HTTP请求来执行鉴权。

当客户端发起一个需要验证的请求给端点，服务器将返回一个带有`HTTP 401 Not Authorized`的响应。这个响应将包含下面的头部：

```
WWW-Authenticate:	Basic	realm="myRealm" 
```

这个头部告诉客户端，用户必须使用基础模式鉴权。现代浏览器在接收了这样的请求之后会自动提示用户输入凭证，并使用`Authorization`头部重新发布请求。这个头部将包含用户名和密码组合（username:password的模式），这个组合使用Base64加密。举个例子，让我们考虑一个包含下面头部的请求：

```
Authorization:	Basic	cmVzdDpyb2Nrcw== 
```

一旦完成编码，服务器需要检查用户的用户名，rest，和密码，rocks。

### 技巧
虽然这种模式是很容易实现的，但是没有提供保密手段来保护凭证。的确，凭证只是编码了，并没有加密，并且十分容易被破解。因此，这个模式必须和HTTPS一起使用来保证安全。
