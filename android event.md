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