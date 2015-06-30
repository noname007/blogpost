2. 编写JNI方法有两种：
  - **静态方法**
    1. 在java层声明带有native关键字的方法
    2. 在native层，按照_命名规范_来命名native方法（可以借助javah工具），并实现
    >如何加载呢？虚拟机寻找JNI库，如果找到后就建立一个联系（保存JNI层函数的函数指针）
    以后在调用直接使用函数指针。

  - **动态注册**
    1. 有一个结构体
      ```
        typedef struct{
          const char* name;
          const char* signature;//函数签名
          void* fnPtr; //函数指针，void*类型
        }JNINativeMethod
      ```
    2. 注册函数
      ```
      AndroidRuntime::registerNativeMethods(env,"包名路径",JNINativeMethod结构体数组,前一个参数的数量);

      在AndroidRuntime类中，这个函数是如下实现的
      int AndroidRuntime::registerNativeMethods(JNIEnv *env,const char* classname,const JNINativeMethod* gMethods, int numMethods){
        return jniRegisterNativeMethods(env,classname,gMethods,numMethods);
      }
      jniRegisterNativeMethods的实现在JNIHelper中实现的，主要实现如下
      {
        jClass clazz;
        clazz=(*env)->FindClass(env,className);
        if((*env)->RegisterNatives(env,clazz,gMethods,numMethods)<0){
          return -1;
        }
        return 0;
      }
      ```
      >当Java层通过System.loadLibrary加载完JNI动态库后，紧接着会查找库中一个叫做
      JNI_onLoad函数，动态注册的工作就在这里完成。

2. JNI native和java数据类型
  ![](http://ww4.sinaimg.cn/large/4483e99egw1etm3kj6bayj20wr0bfwgp.jpg)
  ![](/Users/dongjiawei/.atom/evnd/tmp/clipboard_20150630_142445.png "Optional title")
3. JNIEnv 是一个与线程相关的代表JNI环境的结构体，提供了一些JNI系统函数，通过这些函数可以调用Jva对象，操作jobject对象
4. 垃圾回收
  - 一般Java中创建的对象由垃圾器管理回收和释放内存，而且现在的JVM基本上采取的mark-sweap
  的方式回收内存
  - JNI侧的对象需要手动管理，有两种本地引用Local Reference和全局引用Global Reference
，前者存在于JNI函数中一旦返回，这些对象就可能会被垃圾回收；而后者如果不主动释放，永远不会被垃圾回收。
注意要销毁这些全局引用。
5. JNI异常处理，通常有两种方法：
  - native方法选择立即返回，并抛回本地异常到所调用native方法的java代码
  - native代码使用ExceptionClear（）清楚异常并调用其他JNI函数
    - ExceptionOccurred
    - ExceptionClear
    - ExceptionCheck
    - ExceptionDescribe
    - ReleaseStringChars
    - ReleaseStringUTFChars
    - DeleteLocalRef
    - DeleteGlobalRef
    - PushLocalFrame
    - PopLocalFrame
