# Android设备模拟用户操作

下面提供三种方法

## 方法一 使用内置API

这个方法具有一定的危险性，因为其使用了内置的未公开的API。

下面这个方法是获取了WindowsManager实例，然后触发injectKeyEvent/injectPointerEvent方法。

```
IBinder wmbinder = ServiceManagaer.getService("window");
IWindowManager m_WndManager = IWindowManager.Stub.asInterface(wmbinder);

```

ServiceManager和WindowsManager被定义为Stubs类，为了触发键盘的操作，代码类似如下

按下A键和松开A键

```
m_WndManager.injectKeyEvent(new KeyEvent(KeyEvent,ACTION_DOWN,KeyEvent.KEYCODE_A),true);
m_WndManager.injectKeyEvent(new KeyEvent(KeyEvent.ACTION_UP,KeyEvent.KEYCODE_A),true);

```
触发touch/mouse 事件的话使用如下

```
m_WndManager.injectPointerEvent(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(),MotionEvent.ACTION_DOWN,pozx,poxy,0),true);
m_WndManager.injectPointerEvent(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(),MotionEvent.ACTION_UP,pozx,0),true);
```

这种方法工作的很好，但是局限性在于只能在你的应用中，如果你想在别的应用window上触发这些injectKeys或者touch的事件，可能会导致发生以下错误

```
E/AndroidRuntime(4908):java.lang.SecurityException: Injecting to another application requires INJECT_EVENTS permission
```

**也许你需要两个东西**[How to compile Android Application with system permissions](http://stackoverflow.com/questions/3598662/how-to-compile-android-application-with-system-permissions)<br>[Android INJECT_EVENTS permission](http://stackoverflow.com/questions/5383401/android-inject-events-permission)

方法二 使用Instrumentation对象

下面的方法倒是非常清晰，使用的是公开的API，但是仍然需要INJECT_EVENTS权限

```
Instrumentation m_Instrumentation = new Instrumentation;
m_Instrumentation.sendKeyDownUpSync(KeyEvent.KEYCODE_B);
```

至于点击事件，你可以使用

```
m_Instrumentation.sendPointerSync(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(),MotionEvent.ACTION_DOWN,pozx,pozy,0);
m_Instrumentation.sendPointerSync(MotionEvent.obtain(SystemClock.uptimeMillis(),SystemClock.uptimeMillis(),MotionEvent.ACTION_DOWN,pozx,pozy,);

```

这个的用法是不是觉得跟第一种类似，事实上他们在底层实现是一样的，只不过有的做了封装。其底层实现如下

```
public void sendPointerSync(MotionEvent event){
	validateNotAppThread();
	try{
		(IWindowManafer.Stub.asInterface(ServiceManager.getService("window"))).injectPointerEvent(event,true);
	} catch (RemoteException e){
	
	}
}
```

方法三 直接将事件信息注入到/dev/input/eventX 

linux为每个输入设备直接向外暴露了一个输入事件接口，那就是/dev/input/eventX ,其中X代表整型数字，从0开始，升序增加。我们可以直接使用并越过Android平台的权限问题

当然了为了实现这个功能，我们需要root权限，所以我们只能跑在已经root的机器上。其中有两种实现方式，一种是通过Java代码来实现，另外一种实际上是直接使用C语言来实现。

下面来仔细解释一下这个方法
首先/dev/input/eventX是用来输入事件，通常他们的读写权限往往只属于其拥有者或者其所在的组

```
import java.lang.reflect.Method;

public class NativeInput {
	int m_fd;
	final static int EV_KEY = 0x01;
	
	public NativeInput() {
		intEnableDebug(1);
		m_fd = intCreate("/dev/input/event3", 1, 0);
	}
	
	public static int chmod(String path, int mode) throws Exception {
		  Class fileUtils = Class.forName("android.os.FileUtils");
		  Method setPermissions =
		      fileUtils.getMethod("setPermissions", String.class, int.class, int.class, int.class);
		  return (Integer) setPermissions.invoke(null, path, mode, -1, -1);
	}
	public int SendKey(int key, boolean state) {
		if (state)
			return intSendEvent(m_fd, EV_KEY, key, 1); //key down
		else
			return intSendEvent(m_fd, EV_KEY, key, 0); //key up
	}
	
	
							
	native int		intEnableDebug(int enabled); 	//1 will output to logcat, 0 will disable
	//
	native int 		intCreate(String dev, int kb, int mouse);
	native void		intClose(int fd);
	native int		intSendEvent(int fd, int type, int code, int value);
	
	static {
		System.loadLibrary("input");
	}
}

```

