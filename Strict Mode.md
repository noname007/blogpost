# Strict Mode

## \#WARN\# 
非strict模式和strict模式的文件在"use strict"处于全局时的表现是不一致的，所以要求我们在使用strict模式时要注意strict文件和非strict文件在相互引用时可能会造成不可理解的异常。


## 差异变化

### 抛出异常
原先可能被接受的错误现在直接抛出。

- 避免错误地创建全局变量，否则会抛出referenceError
- 函数参数列表变量名要唯一
- ES5禁止使用八进制，而ES6是允许的，0
- ES6禁止对私有属性赋值，非strict模式下，这个操作会被忽略，而在strict模式下，直接抛出异常

### 部分函数无效
- 出于安全的考虑，部分函数调用如fun.caller\fun.arguments在strict模式下无效

### 为未来ES语法铺路

Strict 迁移 <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode> 

