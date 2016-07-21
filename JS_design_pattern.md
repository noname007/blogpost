# Javascript Design Pattern 

## The Structure of a design pattern

- Pattern name
- Context outline
- Problem statement
- Solution
- Design
- Implementation 
- ILLustrations
- Examples
- Corequisites
- Relations
- Known usage


## Anti-patterns in Javascript
- polluting the global namespace 
- 在setInterval或者setTimeout中设置触发器时并没有使用函数而是传递了字符串，这回导致其内部会调用eval()函数
- 修改Object对象的原型
- document.write这个函数在页面加载完毕后触发会引发页面重写等严重问题。