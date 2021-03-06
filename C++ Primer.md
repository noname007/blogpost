# C++ Primer Plus-CH8函数探幽
1. C语言只允许按照值传递，为了避开值传递的限制，采用按指针传递的方式；前面说过，应在定义引用变量的时候对其进行初始化，函数调用使用实参初始化形参，因此函数的引用参数被初始化为函数调用传递的实参。
2. 什么时候创建临时变量呢，如果引用参数是const，则编译器将在下面两种情况下生成临时变量：
	- 实参的类型正确，但不是左值
		> 左值参数是可被引用的数据对象，例如变量、数组元素、结构成员、引用和解除引用的指针都是左值
		> 非左值包含字面常量和包含多项的表达式
	- 实参的类型不正确，但可以转换为正确的类型
3. 如果接受引用参数的函数的意图是修改作为参数传递的变量，则创建临时变量将阻止这种意图的实现。解决方法是禁止创建临时变量。如果函数调用的的参数不是左值或是相应的const引用参数的类型不正确，则C++将创建类型正确的匿名变量，将函数调用的参数的值传递给该匿名变量，并让参数引用该变量。
4. 应尽可能使用const，将引用参数声明为常量数据的引用的理由有三个
	1. 使用const可以避免无意中修改数据得编程错误
	2. 使用const使得函数能够正确处理const和非const实参，否则将只能接受非const数据
	3. 使用const引用使函数能够正确生成并使用临时变量
5. 何时使用引用参数
6. 默认参数并非编程方面的重大的突破，只是提供了一个便捷的方式。在设计类时您将发现，通过使用默认参数，可以减少要定义的析构函数、方法以及方法重载的数量。 实参按从左至右的顺序依次被赋予给相应的形参，而不能跳过任何参数。
7. 编译器选择使用哪个函数版本
	1. 创建候选函数列表 ，其中包含与被调用函数的名称相同的函数和模板函数。
	2. 使用候选函数列表创建可行函数列表，这些都是参数数目正确的函数，为此有一个隐式转换序列，其中包括实参类型与相应的形参类型完全匹配的情况。
	3. 确定是否有最佳的可行函数。
		- 完全匹配
		- 提升转化，char和shorts 自动转换为int，float转换为double
		- 标准转换， int 转换为char，long 转换为double
		- 用户定义的转换

	> 在最佳匹配中const和非const是一样的，除了指针和引用指向的数据外。
8. decltype和后置返回类型->	C++11标准

	~~~
	template<class T1, class T2>
	auto gt(T1 x,T2 y)->decltype（x+y）
	{
		return x+y； 
	}
	~~~
9. :octocat: