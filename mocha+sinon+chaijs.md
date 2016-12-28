# Javascript Unit Test Framework

这一块使用的JS测试框架和工具集主要如下：

- Mocha
- Chaijs
- Sinon

这之间的联系是Mocha作为测试驱动工具，Chaijs提供了断言相关的工具，Sinon提供了跟测试密切联系的spy、stub、mock的功能。

## mocha
 - 测试异步代码 callback or promise
 - 同步测试代码
 - Hook
  - before()
  - after()
  - beforeEach()
  - afterEach()
  - root-level hooks
 - Use.skip() instead of commenting tests out;
 - Don't do nothing ! A test should make an assertion or use this.skip()
 - mocha test --reporter nyan
## chai
- BDD expect or should ,TDD asse=
- Of the three style options, assert is the only one that is not chainable.

## sinon
- Spy
	- checking how many times a function was called
	- checking what arguments were passed to a function
- Stub
	- Stubs can be used to replace problematic code
	- Stubs can also be used to trigger different code paths. 
	- Thirdly, stubs can be used to simplify testing asynchronous code.