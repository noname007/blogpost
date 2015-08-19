### Xcode Project
一个标准的Xcode工程文件会包含些什么呢？

- 源文件的引用
	- 源代码，包含头文件和实现文件
	- 库library和框架framework文件
	- 资源文件
	- 图像文件
	- Interface Builder文件
- 可以将源文件分组组织
- 工程级别的构建设置，你可以指定多个不同的构建配置
- 构建目标target，每个构建目标包含如下
	-  一个由工程build出来的product
	-  引用那些在构建product时所需的源码文件
	-  build配置选项，可以依赖其他构建目标，并且target的build配置选项可以覆盖整个工程级别的配置选项
- 可以用来调试程序的可执行环境，每一个可执行环境会指明
	- 需要启动哪个可执行文件来运行或者调试
	- 命令行参数将会被传入到可执行文件
	- 在程序运行需要环境变量时进行配置

**一个工程文件既可以单独存在也可以和多个工程组成一个workspace**

### Xcode Schema
schema，顾名思义，模式。 模式一般反映的是不同对象类型之间的的内部结构。

>> An Xcode schema defines a collection of targets to build,a configuration to use when building , and a collection of tests to execute.

同一时间只能有一个schema是活跃的，你可以指定一个schema是针对某个工程的（并可以随工程包含进入workspace），也可以指定一个适用于workspace的schema

### Xcode Setttings
一个xcode setting包含的信息应该能够充分描述一个product的构建过程，这些信息其中部分会在编译阶段传入到编译器中

你可以指定target级别的xcconfig，也可以指定project级别的。并且工程级别的setting会被其下所有的target接受除非target它本身的xcconfig设置覆盖了它。


综合以上内容总结如下：

根据大小及其包含关系来看：

```                                             
                ┌────────┐      ┌───────────┐     ┌──────────┐
                │ Target │─────▶│ Projetct  │────▶│Workspace │
                └────────┘      └───────────┘     └──────────┘
                     │                │                 │     
                     │ ┌────────┐     │                 │     
                     │ │xcconfig│     │                 │     
                     │ └────────┘     │                 │     
                     ▼                │                 │     
                ┌────────┐            │                 │     
                │Product │            │                 │     
                └────────┘            │                 │     
                     │                ▼                 │     
                     │           ┌─────────┐            │     
                     └──────────▶│ Schema  │◀───────────┘     
                                 └─────────┘                  
``` 	