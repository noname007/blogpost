# OBJC Block

## 变量访问
1. 全局变量、局部静态变量
2. 作为参数传入到block中的变量
3. 非静态的局部作用域<strong>!变!</strong>量(被当做常量用)
4. __blcok修饰的非静态局部作用域变量
5. block内部定义的变量

## 变量引用计数

当一个block被copied，这种行为会对所有在block内部使用的变量进行strong引用，当一个block变量在其他block中被引用时也会被copied。