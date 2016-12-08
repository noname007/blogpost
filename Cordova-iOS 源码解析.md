# Cordova-iOS 源码解析

## CDVAAppDelegate

应用启动主要做了三件事

- init 申请了cookie存储空间、url缓存空间
- 注册了URL SCHEMA
- 注册了低内存事件(清空 NSURLCACHE)


## CDVViewController




## CDVCommandQueue

描述了如何执行JS侧发来的原生调用请求

## CDVInvokedUrlCommand


## CDVCommandDelegateImpl

## CDVURLProtocol
用来注册解析schema请求的黑科技,苹果允许的官方的中间人攻击方式
