## 简介
  google-breakpad client是用来监控应用崩溃和异常的工具，当发生异常时会产生dump文件并提供上传至crash报告中心的方法。这些任务在客户端这边被分成两个大模块，前者追踪并产生dump的任务交给exception handler来处理，而后者上传的任务交给sender来处理。

## exception handler
  以后简称handler，handler既可以被动地捕捉到异常后产生dump文件，也可以手动触发产生。在产生dump文件后
  ，handler可以执行用户定义的回调函数。

## 使用breakpad的典型例子
  在被监控的程序主函数中建立breakpad的handler，并注册发生异常的回调函数。一般回调函数会启动上报程序，
  会将生成的dump上传至所需的地方。一般我们推荐在fork出来的子进程处理，因为发生异常的进程总不会是稳定的。

## dump生成
  当异常触发，handler会在程序员预先设定的目录下写下dump信息，写dump的方法在不同平台上的实现方式均不同，但基本思路一致
  都是进程枚举所有正在执行的线程，并捕捉它们的状态，包括处理器的寄存器信息和相关的堆栈信息，为了避免在内存中分配空间，dump信息
  被写道硬盘中。
## exception handling
  
