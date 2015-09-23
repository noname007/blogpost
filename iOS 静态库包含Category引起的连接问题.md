# iOS 静态库包含Category引起的连接问题

iOS所使用的编译器LLVM Clang在编译C/C++这种静态强类型语言时必须严格遵守引用的规则，而Objective-C作为一门动态强类型语言，很多语言特性都是运行时特性（即只有在运行的时候才能体现其作用），比如Category。这种差异可能会导致连接错误的问题，原因在于Category如果没有直接引用的话，是无法在编译时建立起符号连接，单纯的Category实现文件编译形成的目标文件是无法合并入静态库文件中，所以我们在打包静态库后，在其他工程饮用时，会出现找不到Category的连接问题。

有人问包含Category的头文件可以么？

如果该Category实现文件是单纯的Category文件的话，即并没有包含其他诸如类的实现的话，那么这个文件也不会被连接。而且头文件只是在静态分析时使用，它并不影响运行时Category的查找和运行。

网上也有很多解决办法，例如Stackoverflow上面就有详细的解释，我觉得这个问题和答案都非常棒连接在下 

[http://stackoverflow.com/questions/2567498/objective-c-categories-in-static-library](http://stackoverflow.com/questions/2567498/objective-c-categories-in-static-library)

里面Mecki的第五种方法已经非常棒了，但是我们还可以做到更好！

在上面我也提到了单纯的Category在无引用时无法被连接入静态库内的，但是如果在Category中加入其他代码就不一样了。此思路来源于iOS指明开源框架NimbusKit。代码如下


首先你要定义一个宏

```
#ifndef FIX_CATEGORY_BUG
#define FIX_CATEGORY_BUG(name) @interface FIX_CATEGORY_BUG##name :NSObject @end\
@implementation FIX_CATEGORY_BUG##name @end
#endif
```

然后在你Category的实现文件中使用该宏命令就可以了，次宏命令的功能也很简单，实际上就是定义了一个空类，这样Category便会被静态库连接了

