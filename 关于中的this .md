# 关于中的this 

```
var a = Function('return this')();
console.log(a===this);

function M(){
  return this;
}
function N(){
  return Function('return this')();
}
console.log(M()===this);
var b ={};
console.log((M.bind(b))()===this);
console.log((N.bind(b))()===b);
console.log((N.bind(b))()===this);

```

正确答案是 true、true、false、false、 true

this的指向跟句法作用域没关系，跟调用者有关系