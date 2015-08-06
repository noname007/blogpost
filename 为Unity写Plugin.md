# Unity3D-Plugin
在Unity中如果想使用Unity之外开发的功能，那么你就需要用到Plugin，
Unity3D提供了两种Plugin，分别是Managed plugins和Native plugins。

- Managed plugin是管理那些由Visual Studio或者MonoDevelop开发的.net assemble文件
它们只包含那些不能直接由库文件提供功能的.net 代码，它们跟原生的Unity Script差别不大。
- Native plugin是特定平台编写的native code提供的功能，他们可以使用那些普通unity脚本无法直接使用的
系统调用或者第三方库的功能

由于ManagedPlugins并不存在非常难的地方所以就把它省略了。这里主要讲述开发Native plugin

以拿为Android开发Plugin为例。

如果你使用C++开发plugin，那么你需要注意避免name mangling问题的发生。

目前有3种plugin开发场景，分别是:
- 在Unity c# script中调用native code
- 在Unity C# script中调用java code
- 在Unity C# script中调用javacode，并且这部分java code调用了native code

其中第一种比较简单就不用说了。主要说下另外两种。

这两种的解决方案其实是一种，都是将转化为native code的调用，只不过是过程变成了unity->native->java
,其中native->java 需要JNI技术，JNI技术使用起来比较复杂，所以Unity提供了Helper Class
来提高JNI使用效率。

举个栗子
```
AndroidJavaClass jc = new AndroidJavaClass("com.unity3d.player.UnityPlayer");
// jni.FindClass("com.unity3d.player.UnityPlayer");
AndroidJavaObject jo = jc.GetStatic<AndroidJavaObject>("currentActivity");
// jni.GetStaticFieldID(classID, "Ljava/lang/Object;");
// jni.GetStaticObjectField(classID, fieldID);
// jni.FindClass("java.lang.Object");

Debug.Log(jo.Call<AndroidJavaObject>("getCacheDir").Call<string>("getCanonicalPath"));
// jni.GetMethodID(classID, "getCacheDir", "()Ljava/io/File;"); // or any baseclass thereof!
// jni.CallObjectMethod(objectID, methodID);
// jni.FindClass("java.io.File");
// jni.GetMethodID(classID, "getCanonicalPath", "()Ljava/lang/String;");
// jni.CallObjectMethod(objectID, methodID);
// jni.GetStringUTFChars(javaString);
```
注释的地方便是使用标准JNI接口的调用方法，而AndroidJavaClass和AndroidJavaObject则可以快捷使用的简洁方法来实现这些功能。

## 使用Unity Plugin的最佳实践
- 尽可能少的使用这种技术，毕竟存在性能损耗
- 如果使用JNI技术的话，建议使用using{}来保证其生命周期在using结束之后会被立即销毁
否则你也不知道Mono的Garbage Collector会在什么时候销毁这种对象。
