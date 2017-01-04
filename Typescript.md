# Typescript
## Basic Types
Enum members have numeric value associated with them and can be either constant or computed. 

- +1 or 0

- To avoid paying the cost of extra generated code and additional indirection when accessing enum values it is possible to use const enums

```
const enum Enum {
    A = 1,
    B = A * 2
}
```
## Classes 



## Enum 
Enum members have numeric value associated with them and can be either constant or computed. 

- +1 or 0

- To avoid paying the cost of extra generated code and additional indirection when accessing enum values it is possible to use const enums

```
const enum Enum {
    A = 1,
    B = A * 2
}
```
## Function 

- function type
```
let myAdd: (x: number, y: number)=>number =
    function(x: number, y: number): number { return x+y; };
```
- optional param XXX?:string
- default param XXX="ABCD"
- rest param ...XXX:string[]

## Generics
```
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);  // Now we know it has a .length property, so no more error
    return arg;
}
```

## module
 with ES6 Module,after typescript 1.5,namespace is simliar with "module"