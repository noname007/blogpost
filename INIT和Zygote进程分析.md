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
  3. 在CallStaticMethod中做了如下五种事情：这里已转为java层
    - 建立IPC通信服务端zygoteSocket，与其他进程间通信方式不同的是没有采用binder，而是使用了socket
    - 预加载类和资源 preloadClass文件由preload工具生成，它需要判断每个类加载的时间是否大于1259微妙，超过的话，就会被写到preload-classes文件中，最后由zygote预加载。这也是android系统启动慢的一个原因。
    - 启动system_server,这个会创建Java世界中系统service所驻留的进程system_server,若果该进程死了，那么就会导致zygote自杀。这里的system_server进程由zygote进程fork而来
    - 跑入runSelectLoopMode 多路复用I/O模型，等待select返回有效值
3. system_server的重要使命
  - 走入RuntimeInit，先做一些native层和其他初始化函数
    - NativeInit初始化设备某些设置和建立Binder线程，用于binder通信。
  - zygoteInit分裂产生的ss，其实就是为了调用com.andaroid.server.SystemServer的main函数。
  这里面主要的工作是创建一些关键服务，比如binder和surfaceflinger，还有开启一个线程用以启动java编写的一些服务
  如电源管理服务、电池服务、看门狗等，总之系统关键的服务都是在这里启动的。所以说ss算作开启java世界的大门
4. systemserver调用流程
  ![](http://ww2.sinaimg.cn/large/4483e99egw1etn819m1iwj20rk0ctdik.jpg)
5. 启动Activity的流程
  - ActivityManagerService是由SystemServer创建的，假设通过startActivity来启动新的Activity，而这个Activity附属于一个还未启动的进程。ActivityManagerService通过之前建立的socket终于向zygote发送请求了。
  - zygote接收请求后进行fork分裂出一个子进程，父进程做扫尾工作，子进程做创建了android.app.ActivityThread
  这个类实际上是Android中apk程序对应的进程，MAIN函数便是apk程序的main函数。
6. ![](http://ww1.sinaimg.cn/large/4483e99egw1etn8wazcn5j210g0qkdje.jpg)
zygote初始化dalvik虚拟机并预先加载相关类和核心类库，通过socket等待请求。而且java世界最重要systemserver也是由zygote fork而来。
