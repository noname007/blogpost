# name mangling
Name mangling技术提供的是一种为函数、结构体、类等数据类型的命名“装饰”的方案，这种装饰
能够帮助编译器向链接器 链接时提供更多的有效信息。
## c language name managing in Microsoft
尽管name mangling有的时候会被用在那些不支持函数重载的语言的上面，例如C语言和经典Pascal
语言，斌一起在某些场合会使用这些技术提供更多的关于此函数的信息。像以下C语言的例子

```
int _cdecl f (int x) {return 0;}
int _stdcall g (int y) {return 0;}
int _fastcall h (int z) {return 0;}
```

经过编译器编译后，其函数签名变为如下

```
_f
_g@4
@h@4
```

在stdcall和fastcall的mangling中，函数被编码为_name@x和@name@x的形式，其中X是参数的位数
（以32位编译器为例）

## C++ name mangling
C++编译器应该是使用name mangling技术最多的语言编译器。
这里有篇资料[c++ mangling and demangling](http://www.kegel.com/mangle.html)

最开始的时候，C++编译器只是相当于一个翻译器，将C++源码转化为C代码并由C编译器来编译成目标代码
正因为如此，所以符号名称必须遵照C语言的规则。而之后出现了可以直接将C++编译成机器代码或者汇编
的编译器。

因为C++并没有制定标准的名称修饰规则，所以每一个编译器实际上使用的是自己的规则，C++通常也包含
复杂的语言特性，例如classes、templates、namespaces 和operator overloading的特点，
几乎没有编译器可以连接由不同的编译器编译的各种代码。

## 如何处理C++代码和C代码连接

```
#ifdef _cplisplus
extern "C"{
#endif
/*...*/
#ifdef _cplusplus
}
#endif
```

如果不使用extern “C”的话，那么标准库中的代码在连接时会被mangling 导致连接失败。

举个栗子

```
#ifdef __cplusplus
extern "C" {
#endif

void *memset (void *, int, size_t);
char *strcat (char *, const char *);
int   strcmp (const char *, const char *);
char *strcpy (char *, const char *);

#ifdef __cplusplus
}
#endif
```

这段代码是正常的，并且在连接时的代码是这样的

```
if (strcmp(argv[1], "-x") == 0)
    strcpy(a, argv[2]);
else
    memset (a, 0, sizeof(a));

```

如果没有使用extern包围，那么会被C++编译器处理成这样

```
if (__1cGstrcmp6Fpkc1_i_(argv[1], "-x") == 0)
    __1cGstrcpy6Fpcpkc_0_(a, argv[2]);
else
    __1cGmemset6FpviI_0_ (a, 0, sizeof(a));
```

这样在连接时，就无法从标准库中连接memset和strcpy代码了。


