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

