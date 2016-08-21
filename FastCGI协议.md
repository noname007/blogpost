# FastCGI协议

## 背景

FastCGI是相对于CGI这种协议来说是一种快速高效的协议。

## CGI协议 

CGI程序 Web服务器 Web页面 

传统的CGI是一种fork-and-execute的模式 ，频繁的切换进程会使执行效率大大下降。

## FastCGI
fastcgi程序是一种常驻的程序，FastCGI进程管理器负责分发不同的请求到不同的CGI子进程上。


## nginx

Nginx也有master和worker进程之分，不过跟fastcgi进程管理器和CGI子进程关系很接近，都是前者管理后者。不过任务不同，前者是nginx用来处理大量并发请求，worker用来真实处理各个进程，master用来读取执行配置并维护各个worker。

至于nginx和fastcgi程序的关系，参考官方文档:

```
nginx can be used to route requests to FastCGI servers which run applications built with various frameworks and programming languages such as PHP.

```