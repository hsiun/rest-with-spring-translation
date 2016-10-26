# 存储敏感数据

在系统被破坏的情况下，另一个必要的加密点是在持久化层中。正如在本章前面提到的，加密保存数据库中的密码是一个最佳实践，这样一来即使数据库被未授权恶意用户访问，最敏感的信息依然是安全的。


Spring对加密数据库中的信息提供了很好的支持。API设计者可以借助`org.springframework.security.crypto.password.PasswordEncoder`。例如，`org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder`是计算数据库中密码哈希极好的选择。