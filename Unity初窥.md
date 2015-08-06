- Unity 使用的mono运行时是以ECMA C#为标准来实现的，所以某些MS c#标准语法特性并未实现。
- Mono组成
  - C# Compiler
  - MONO Runtime:A JIT Compile；a AOT compiler ，a Library loader,垃圾收集齐器
  线程系统、内置的其他协作性的方法
  - Base Class Library： 提供了众多基础性的解决方案，能够与微软的.net framework兼容并存
  - Mono Class Library：
