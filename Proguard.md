# proguard简单介绍和常用配置

## proguard简单介绍 

proguard是一个对java class文件进行压缩、优化、混淆和预校验的工具。

你可以使用proguard来作如下事情：

- 创建更紧凑的代码归档文件(jar)，更快的网络传输速率、更快的加载速度和更小的内存占用
- 使得程序更难被逆向工程破解
- 列出无用的代码，以便于将其从源码中移除
- 预校验现有的class文件是否符合Java 6以上的更迅速的类加载机制

<table class="diagram" align="center">

<tbody><tr>
<td rowspan="4" class="lightblock">Input jars</td>
<td colspan="8" class="transparentblock"></td>
</tr>

<tr>
<td rowspan="2" class="transparentblock"></td>
<td rowspan="3" class="lightblock">Shrunk code</td>
<td colspan="6" class="transparentblock"></td>
</tr>

<tr>
<td class="transparentblock"></td>
<td rowspan="2" class="lightblock">Optim. code</td>
<td colspan="3" class="transparentblock"></td>
<td rowspan="2" class="lightblock">Output jars</td>
</tr>

<tr>
<td class="transparentblock">- shrink →</td>
<td class="transparentblock">- optimize →</td>
<td class="transparentblock">- obfuscate →</td>
<td class="lightblock">Obfusc. code</td>
<td class="transparentblock">- preverify →</td>
</tr>


<tr>
<td class="darkblock">Library jars</td>
<td colspan="7" class="transparentblock">------------------------------- (unchanged) -------------------------------→</td>
<td class="darkblock">Library jars</td>
</tr>

</tbody></table>

以上所有步骤均可以省略，为了决定哪些代码是需要保护的哪些代码是需要混淆的，你需要指出你代码中的Entry points，这些入口类大多具有main函数或activities或applets或midlets。
	
- 在shrinking的环节，proguard从这些entry point开始递归的分析哪些类使用过的哪些是没有用过的
- 在optimization环节，proguard可能会调整部分代码。那些不能成为entry point的class会被变成私有函数、static、无用的参数将会被移除，甚至某些函数将会转换为inline的形式
- 在obfuscation环节，proguard会重新命名class和class member那些不会是entry point的。在整个过程中，这些entry point依然会用其原始名称访问到
- 预校验环节是唯一不涉及entry point的过程

需要注意的是反射的使用，当代码中大量使用反射技术，可能会出现异常情况，最好进行测试，

## proguard 常用配置
[proguard usage](http://proguard.sourceforge.net/)

proguard 进行各项操作依据的是便是其配置文件XXX.pro

### keep option
- keep option 
	- 用来描述某些类和类成员作为entry point从而被保护起来
- keepclassmenmbers
	- 保护某些成员变量和函数 如果其所属的类也被保护的话
- printseeds
	- 列出所有被keep option保护的类和类成员

用图表示如下
![](http://ww1.sinaimg.cn/large/4483e99egw1euzvaicpgrj20mj03r750.jpg)
### obfuscation options
- printmapping 打印出混淆后的新名称和之前的旧名称之间的映射

### class specification
一些通配符和匹配规则

通配符|规则|
---|----|
？| 在类名中匹配任意单个字符|
*| 匹配类名中的任何部分，但不包含额外的包名|
`**`|匹配类名中的任何部分，并且可以包含额外的包名|
%| 匹配任何基础类型的类型名|
`***`|匹配任意类型名 ,包含基础类型/非基础类型|
`...`|匹配任意数量、任意类型的参数|
`<init>`| 匹配任何构造器|
`<field>`|匹配任何字段名|
`<method>`| 匹配任何方法|
*(当用在类内部时)|匹配任何字段和方法|