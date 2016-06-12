# Export 的哲学

## Exports a Namespace

```
var fs = exports;
fs.xxx={};
```


## Exports a Function

```
module.exports = function(){}
```
## Exports a Higher Order Function

```
var connect = require('connect'),
    query = require('connect/lib/middleware/query');

var app = connect();
app.use(query({maxKeys: 100}));


var qs = require('qs')
  , parse = require('../utils').parseUrl;

module.exports = function query(options){
  return function query(req, res, next){
    if (!req.query) {
      req.query = ~req.url.indexOf('?')
        ? qs.parse(parse(req).query, options)
        : {};
    }

    next();
  };
};


```

## Exports a Constructor

```
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return "Hi, I'm " + this.name;
};

module.exports = Person;
```
## Exports a Singleton 

Require Cache

## Extends a Global Object

```
var should = function(obj) {
  return new Assertion(util.isWrapperType(obj) ? obj.valueOf(): obj);
};

//...

exports = module.exports = should;

//...

Object.defineProperty(Object.prototype, 'should', {
  set: function(){},
  get: function(){
    return should(this);
  },
  configurable: true
});
```

## Applies a Monkey Patch
 
 