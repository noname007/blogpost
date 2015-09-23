# iOS Framework Programming Guide 学习笔记

> 什么是Framework?

顾名思义，它应该是框架。这个框架一个带有层次结构的目录，它封装包含了许多共享的资源，例如动态库dylib、nib文件、图片文件，本地化语言文件、头文件以及相关的文档等。许多程序可以同时使用，系统加载它到内存中并在不同程序之间共用一份拷贝。

> 框架与普通的静态库、动态库的区别

Framework与静态动态库的有着共同点，它们提供了一堆方法并且可以被程序调用用来做指定的任务，与此同时，framework提供了其他优势之处。

- framework把那些有联系但是却分离的文件聚集在一起，这种方式可以方便的安装卸载和重定位资源
- framework可以包含更多不同类型的资源，例如一个framework可以包含更多的相关的头文件或者文档
- 一个bundle中可以包含同一个框架的多个版本
- 在同一时间，只读性的资源在内存中只保留一份拷贝

------

- framework的bundle结构不同于现在主流的bundle结构，它使用的是早期的bundle结构，这种结构包含的是不同版本的代码，可以方便的在低版本系统中降级使用。
- 基本结构如下:

```
MyFramework.framework/
    MyFramework  -> Versions/Current/MyFramework
    Resources    -> Versions/Current/Resources
    Versions/
        A/
            MyFramework
            Resources/
                English.lproj/
                    InfoPlist.strings
                Info.plist
        Current  -> A
```

你可能会发现有两层软链接，为什么不直接一层软连接就好呢？原因额外的一层软连接可以在更新版本选择时，只需要更新Versions/Current这层的软连接，而不需要直接各个资源的链接。

---------

### The Umbrella Framework 
umbrella framework与一般的framework区别在于两点：

- umbrella framework包含子框架
- umbrella framework包含头文件

下面是一个Core Services的umbrella framework，其中headers只有一个，只能包含主干版本的header文件

```
CoreServices.framework/
    CoreServices           -> Versions/Current/CoreServices
    CoreServices_debug     -> Versions/Current/CoreServices_debug
    CoreServices_profile   -> Versions/Current/CoreServices_profile
    Frameworks             -> Versions/Current/Frameworks
    Headers                -> Versions/Current/Headers
    Resources              -> Versions/Current/Resources
    Versions/
        A/
            CoreServices
            CoreServices_debug
            CoreServices_profile
            Frameworks/
                CarbonCore.framework
                CFNetwork.framework
                OSServices.framework
                SearchKit.framework
                WebServicesCore.framework
            Headers/
                Components.k.h
                CoreServices-gcc3.p
                CoreServices-gcc3.pp
                CoreServices.h
                CoreServices.p
                CoreServices.pp
                CoreServices.r
            Resources/
                Info-macos.plist
                version.plist
        Current             -> A
```

苹果官方并不建议开发者使用Umbrella framework来构建自己的程序。

