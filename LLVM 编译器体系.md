# LLVM 编译器体系
总体说来，LLVM的功能主要集中在整个编译工具链的后半程，类似经典编译器中的编译后端。

- llc LLVM的静态编译器 ，它针对特定的平台编译LLVM的bytecode代码为一种汇编代码，而这种汇编代码在稍后可以传入本地的汇编器和链接器来产生本地的机器代码。
- llvm-as LLVM assembler主要作用就是将可供人阅读的LLVM汇编代码转换为LLVM的字节码（byte code）
- llvm-dis LLVM disassembler主要作用与上面相反，将LLVM的字节码转换可供人阅读的LLVM汇编代码
- lli 这个是LLVM的解释器，可直接运行LLVM的bytecode；默认状况下，lli会以JIT编译器的形式运行bytecode，这种模式要比解释器模式快很多
- 基本流程就是如下:
	- clang/gcc-llvm 等编译器前端将源码转换为可供人阅读的LLVM汇编代码(LLVM IR)
	- llvm-as LLVM汇编代码(LLVM IR)编译成LLVM字节码
		- lli JIT/解释运行 LLVM字节码
		- llc 编译LLVM字节码为目标平台的汇编码。 
			- 汇编码经汇编器链接器后转换成目标平台的ELF目标文件/可执行文件

## 非常棒的参考资料
- [LLVM作者编写的介绍文章](http://www.aosabook.org/en/llvm.html)
- [所有C语言程序员应该知道的关于LLVM的知识](http://blog.llvm.org/2011/05/what-every-c-programmer-should-know.html)


