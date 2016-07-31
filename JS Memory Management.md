# JS Memory Management

JS的垃圾回收机制并不意味着JS程序员可以完全无需考虑内存分配问题。


## JS中的内存分配

在声明变量的同时也完成了内存的分配:

```
function f(a){
  return a + 2;
} // allocates a function (which is a callable object)

// function expressions also allocate an object
someElement.addEventListener('click', function(){
  someElement.style.backgroundColor = 'blue';
}, false);
```

## 垃圾回收

事实上并没有合适的算法来决定何时变量才永远不会被使用，所以垃圾回收算法在实现上存在诸多限制。

### 基于引用计数的垃圾回收

#### 引用计数统计

当一个对象的任何属性没有被引用或者没有对象的原型是它的话，那么这个对象就可被垃圾回收。

#### 引用循环

当有两个对象进行互相引用时，此时会进入引用循环，这种情况下，垃圾回收算法会无法将其回收。


或者对象引用其本身的时候

### 基于Mark-Sweep的垃圾回收算法

前一个算法是没有其他对象引用他，那么这个就是一个对象不可达。
它会从一个根对象上去寻找所有可达和不可达的对象，不可达的对象就会被回收。


