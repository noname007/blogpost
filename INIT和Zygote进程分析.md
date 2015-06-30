1. init进程工作
 - 解析两个配置文件
 - 执行各阶段工作，创建zygote进程就是其中工作
 - 初始化属性服务
 - 进入无限循环，等待处理某些事件
2. zygote进程启动分析:源文件是App_main:
  1. 创建AppRuntime，并由AppRuntime start调用"com.android.internal.os.ZygoteInit"中的main方法和SystemServer
  2. 在AppRuntime中的start方法中，创建了JVM虚拟机并注册了相关JNI函数
    1. 创建虚拟机
    2. 注册JNI函数，大部分为支持Dalvik虚拟机工作的函数
    3. 最后借助CallStaticVoidMethod最终将调用com.android.os.ZygoteInit的main函数，
  3.在CallStaticMethod中做了如下五种事情：
    - 建立IPC通信服务端
    - 
