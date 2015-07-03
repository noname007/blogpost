## ndk编程
1. NDK提供的组件
  - ARM,X86,MIPS 交叉编译器
  - 构建系统
  - JNI接口头文件
  - C库
  - POSIX线程库
  - 精简版C++库
  - 动态链接库
  - android log库
  - Android pixel buffer库
  - Android native应用API
  - OpenGL ES 3D图像库
  - OpenSL ES native Audio库
2. NDK Android应用工程
  - jni； 这个目录下面包含了native部分的源码，Android.mk描述了native源码如何被build，Android NDK构建系统将此目录设置为NDK工程的主目录并要求Application.mk应该处在工程根目录下
  - libs：这个目录是由ndk build系统在build时创建的，它包含着多个不同机器架构的子目录，这个目录会在apk打包的过程中包入APK中
  - obj 这个目录是在编译源码的中间环节产物，开发者不应在这里涉足。
3. NDK的构建系统依赖于GNU Make，初衷就是帮助开发者在仅编写少量构建文件代码就可以构建整个不同系统架构、平台下的native应用。各种mk文件处在ndk目录下的/build/core/下。
4. 这套构建系统还依赖着用户提供两个make file文件，一个是Android.mk,另外一个便是Application.mk
  - **Android.mk** 这个是用来告诉Android NDK build系统整个NDK工程样子的
    下面以hello-jni工程的jni目录下的android.mk文件为例，来解释一下
    ```
    LOCAL_PATH := $(call my-dir)
include $(CLEAR_VARS)
LOCAL_MODULE    := hello-jni
LOCAL_SRC_FILES := hello-jni.c
include $(BUILD_SHARED_LIBRARY)
    ```
      - 根据约定，变量名应该大写
      - Android.mk应该要以LOCAL_PATH作为起始行，并且提供了my-dir这个宏函数，它可以返回准确的当前目录地址
      。CLEAN_VARS的含义是将使用clear_var.mk中的文件内容，这个文件的作用是按照模块清除该模块使用的环境变量
      像什么LOCAL_MODULE,LOCAL_SRC_FILES等，但惟独LOCAL_PATH不处理。每一个native组件都应该被认作是一个模块
      - LOCAL_MODULE 是用来命名编译产生的模块名，通常还会加上特定的前缀，例如本例中就是libhello-jni.so
      - BUILD_SHARED_LIBRARY作用就是按照build-shared-library.mk文件预先设定的规则来编译源文件成为一个shared library
      - 更多的请参考[Android.mk file syntax specification](http://www.kandroid.org/ndk/docs/ANDROID-MK.html)
  - **Application.mk**
    - 对于NDK build system来说，这个文件是一个可选文件，他描述了应用到底需要那个模块，以及一些针对所有模块的设置信息
      - APP_MODULES:默认会编译Android.mk下的所有模块，修改此选项可以改变此行为，以空格分隔
      - APP_OPTIM:这个变量设置到底是release还是debug模式下编译native库，
      - APP_CLAGS:这个选项设置在编译时传入编译器的参数
      - APP_CPPFLAGS：这个选项设置编译C++源文件时输入编译器的参数
      - APP_BUILD_SCRIPT：决定NDK build system寻找android.mk文件还是其他文件
      - APP_ABI：默认NDK只产生armeabi架构的文件,你可以如下修改产生其他架构的
        ```
        APP_ABI := armeabi mips
        #APP_ABI := all
        ```
