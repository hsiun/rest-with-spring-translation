# Postman和安全

正如第七章，_处理安全_中描述的，为了安全的调用，我们需要指示Postman发送正确的头部。对HTTP基本的验证，我们首先需要一个Base64加密的用户和密码对（例如，cmVzdDpyb2Nrcw== for rest:rock），并在安全调用中添加`Authorization`头部：
![PostMan和安全](http://ofboy2upv.bkt.clouddn.com/PostMan3.PNG)