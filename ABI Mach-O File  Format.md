# ABI Mach-O File  Format

> The Mach-O file format provides both intermediate (during the build process) and final (after linking the final product) storage of machine code and data. It was designed as a flexible replacement for the BSD a.out format, to be used by the compiler and the static linker and to contain statically linked executable code at runtime. Features for dynamic linking were added as the goals of OS X evolved, resulting in a single file format for both statically linked and dynamically linked code.

这里说明了Mach-O文件与BSD系统的二进制执行文件a.out的差异在于后者需要静态连接器进行静态连接可执行代码。而Mach-O设计初衷寻找解决动态链接的方案，使得单一文件格式既可以满足动态连接，也能静态连接。

> 这里单独提下a.out文件格式。这种格式实际上是BSD系统中旧版的可执行文件、目标文件、共享库的格式，其原名为"assembler output",也有很多不同的格式标准，例如PDP-7、PDP-11(出现于Unix)，后来在Unix SystemV中被COFF取代，再后来在SystemV Release4版本中由ELF取代，基本上现代BSD系统都转向了ELF格式了。

>> 再插入ELF的说明:[ELF文件格式说明](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format) 比较重要的一点就是segment和section的差别 segment table中包含的是运行时相关信息，而section table包含的是在连接和重定位中的重要信息


-------

### Mach-O文件结构 

![](https://developer.apple.com/library/mac/documentation/DeveloperTools/Conceptual/MachORuntime/art/mach_o_segments.gif)

一个Mach-O文件通常包含三大部分

- Header 在每个Mach-O文件中都有的结构，会包含一些基础信息，包括目标架构、以及文件中剩余内容的成分等等，相当于文件头，用以描述文件本身的属性。
- Header接下来的部分是Segment的引用表【虽然叫做load command】，会指明以下东西:
	-  文件在虚拟内存空间中的初始化布局
	-  符号表在文件的位置[为了动态连接使用]
	-  主线程程序的入口点
	-  共享库中符号信息
- 在接下来就是由不同section组成的segment，每个segment对应着虚拟内存中某个区域，在动态链接时会被定位到对应的进程内存空间中去
- 在完整连接后，最后一个segent会包含一些可修改的连接信息，包含这个符号表、字符串表位置等等，这部分信息会被动态加载器在连接时修改
- 当使用Stabs这种调试格式时，符号表也会保存可供调试信息；当你使用DWARF时，调试信息会保存在与此文件关联的dSYM文件。

> DWARF和STAB的关系，