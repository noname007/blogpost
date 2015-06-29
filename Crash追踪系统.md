### Crash追踪系统

- **客户端部分**

  结合现有的主流游戏开发技术，根据不同平台，需要制作对应2.5套SDK。
  - Java 捕捉虚拟机可以捕获的Java语言层面的异常错误，这套已经单独实现过。
  - Cocos系列 捕捉使用Native Code开发的产生的不可恢复的异常。
  - Unity 捕捉使用C#开发产生的异常。
  > 解释一下，为什么是2.5套SDK？这已经是在复用代码、精简SDK代码的前提下做出的设计，我初步规划这套SDK使用Java来进行
  基本的数据采集、上报功能的开发，这是所有SDK共用的部分，通过JNI/Unity Plugin将这部分基础功能暴露给目标2/3对应的SDK代码，
  前者JNI修改幅度并不算大，所以算是0.5套；而Unity Plugin则修改的会比较多，算是1套，总计1+0.5+1套。

  再来看下客户端部分其中的实现难点和解决办法：
  - ***Native Code侧的错误捕捉***。通过对UNIX系统的认识和研究，需要在native侧注册异常处理函数，由于异常处理函数在系统中是按照
  异常表进行映射处理，我们需要筛选待捕捉的异常信号并注册对应信号的handler，通过捕获core dump/tombstone文件内容再转交给java侧的数据上报功能。
    - Android与UNIX系统不同的是其使用的标准C库是bionic，里面的异常信号还算比较少，信号值不同，主要有以下几种
      - SIGILL(非法指令异常)
      - SIGABRT(abort退出异常)
      - SIGBUS(硬件访问异常)
      - SIGFPE(浮点运算异常)
      - SIGSEGV(内存访问异常)
      - SIGSTKFLT(协处理器栈异常)
      - SIGPIPE(管道异常)
    - 这部分代码必须而且只能使用C语言来写，最后编译连接为so库，以供Java层Application初始化后载入。
  - ***Unity侧的错误捕捉***。【这部分内容的开发还需要继续了解Unity的底层运行原理，这部分是我目前掌握甚少的，还需要去研究，所以以下内容会存在偏差】
  具体实现原理跟Native Code类似，只不过这个需要多者混合，除了Java层的捕捉，还需要对Unity代码层（C#）的捕捉和Unity Runtime-Mono的捕捉。

- **服务端部分**

  > ***注意*** 这里并不只有服务端开发的内容，还有要借助我们这边开发的工具。

  服务端的数据展示、上传文件、内容管理等等这种基本的功能是由服务端开发人员开发。服务端人员在处理收集到的异常信息时，都是些表面上看去
  无意义的二进制码，需要借助我们开发的工具来还原异常信息。这套工具主要由3件组成。
  先展示一段异常信息：
  ```
  pid: 153, tid: 161  >>> system_server <<<
signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr 43bf3000
 r0 003dc4a0  r1 43bf3000  r2 00000400  r3 00000000
 r4 002cbc98  r5 002cbc98  r6 00000000  r7 00000000
 r8 00000001  r9 00000140  10 00000019  fp 00301e04
 ip 8090a1e0  sp 43f1eb68  lr 80c92cbb  pc afd0cdfc  cpsr 20000010
 d0  003b3a700033c9f8  d1  00301280002eb23b
 d2  000000000000003b  d3  0000000000000000
 d4  43bbc00043bb8000  d5  43d4800043bb8000
 d6  3f80000000000000  d7  000001e03f000000
 d8  0000000000000000  d9  0000000000000000
 d10 0000000000000000  d11 0000000000000000
 d12 0000000000000000  d13 0000000000000000
 d14 0000000000000000  d15 0000000000000000
 d16 3effff003effff00  d17 3f80000041808889
 d18 3f80000041c4cccd  d19 0701070100700798
 d20 0000000000000c27  d21 0000043f00890000
 d22 0000000000000000  d23 0000000000000008
 d24 3fc74721cad6b0ed  d25 3fc39a09d078c69f
 d26 0000000000000000  d27 0000000000000000
 d28 0000000000000000  d29 0000000000000000
 d30 0000000000000000  d31 0000000000000000
 scr 20000010

 #00  pc 0000cdfc  /system/lib/libc.so
#01  pc 00092cb8  /system/lib/egl/libGLESv2_adreno200.so
#02  pc 00093814  /system/lib/egl/libGLESv2_adreno200.so
#03  pc 00093890  /system/lib/egl/libGLESv2_adreno200.so
#04  pc 000938bc  /system/lib/egl/libGLESv2_adreno200.so
#05  pc 00095cce  /system/lib/egl/libGLESv2_adreno200.so
#06  pc 0006526a  /system/lib/egl/libGLESv2_adreno200.so
#07  pc 000655cc  /system/lib/egl/libGLESv2_adreno200.so
#08  pc 000188c4  /system/lib/egl/libGLESv1_CM_adreno200.so
#09  pc 000265ca  /system/lib/libsurfaceflinger.so
#10  pc 0001b04c  /system/lib/libsurfaceflinger.so
#11  pc 0001bda8  /system/lib/libsurfaceflinger.so
#12  pc 0001bf52  /system/lib/libsurfaceflinger.so
#13  pc 00020f3c  /system/lib/libsurfaceflinger.so
#14  pc 00023df6  /system/lib/libsurfaceflinger.so
#15  pc 000259de  /system/lib/libsurfaceflinger.so
#16  pc 0001c52c  /system/lib/libutils.so
#17  pc 0001ca8a  /system/lib/libutils.so
#18  pc 00011bc4  /system/lib/libc.so
#19  pc 00011790  /system/lib/libc.so
  ```
  这样的异常信息捕获后直接对开发者来看毫无意义,需要借助add2line外加调试表符号才能还原出来正确的调用函数栈，前者
  属于GNU binutils的工具，而后者则是我们要开发的调试符号表提取工具。

  这个符号表工具进行的工作就是需要接入者在开发者本地对自己以debug模式编译出来的so文件使用该工具提取调试符号信息。
  获取到符号信息后在借助addr2line还原成对应的文件以及行数。

  第3个工具便是将处理整个错误栈信息文件，将整个文件内容进行还原。

  另外，还需要开发一个java混淆还原工具，根据用户提供的mapping文件对混淆后的代码进行还原。

  综上所述，服务端这边的功能还需要使用我们提供的4个工具
，其中3个需要自行开发。我上周主要是进行了符号表信息提取工具的尝试开发，还没有开发完全，目前进度为可以提取部分EIF文件的DWARF调试符号信息。
