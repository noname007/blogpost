# Android Service

一个Service是一个应用组件，它们能够在应用背后进行长时间的运行操作，而且它们并不提供界面。

>> 要注意的是一个Service会运行在宿主进程的的主线程上，service并不会创建自己的线程，而且也不会运行在其他进程上(除非你指定) 也就是说如果你的service要运行CPU密集计算任务或者长时间的阻塞任务，你最好创建新的线程中运行你的service任务，这样可以有效降低出现ANR的危险并且也不会使应用的主线程发生过度卡顿的问题。

### 关键Service方法

- onStartCommand()
	- 当其他组件例如activity需要启动service时【调用startService()】，系统便会调用此函数，一旦此函数执行，整个service便会启动起来并立即运行。如果你实现了此方法，那么就需要你来在合适的时机调用stopself()或者stopService()【如果你需要binding，那么你不需要实现此方法】
- onBind()
	- 当其他组件需要绑定此服务时，例如RPC，那么就需要调用bindService(),在你实现方法中，你必须提供一个接口来供clients和service沟通的方法，我们把它叫做IBinder。除非你不允许binding(你可以返回null)，那么你必须实现此方法。 
- onCreate()
	- 当service第一次创建时，会进行一次初始化过程，并在onStartCommand或者onBind()之前，如果我们service的已经在跑了，那么这个方法并不会执行。
- onDestory()
	- 当service不再使用并会被销毁时，系统会调用此方法。你需要在里面释放一些诸如线程、注册的监听器等，这是service收到的最后的请求。

系统只有在可用内存非常少时为了响应用户的操作，会强制关闭service。当用户触发的Activity绑定了service的话，那么service基本上不会被系统杀死，当强制要求service运行在前台时，那么他们根本不会杀死。

另一方面，当service启动后并长时间运行后，系统会降低其在后台任务中的优先级并会很容易被系统杀死。如果你的service启动后你必须优雅的设计以便service被系统重启----因为当系统杀死你的service后，它会在资源可用时重启你的service，当然了这个也依赖这你在onStartCommand()中的返回值
