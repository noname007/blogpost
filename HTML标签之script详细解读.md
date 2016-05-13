# HTML标签之script解读
## 属性
除了global attributes以外，还有下面几个属性
- src 资源地址
- type 资源类型
- charset 字符串编码
- async 无阻塞，当可用时执行脚本
- defer 延后执行脚本
- crossorigin 如何处理跨域请求
- nonce 内容审查机制

## type
允许的格式

```
application/ecmascript
application/javascript
application/x-ecmascript
application/x-javascript
text/ecmascript
text/javascript
text/javascript1.0
text/javascript1.1
text/javascript1.2
text/javascript1.3
text/javascript1.4
text/javascript1.5
text/jscript
text/livescript
text/x-ecmascript
text/x-javascript

```
如果省略上述格式或者使用上述格式，将会默认使用script top-level，将会受到charset、async、defer影响。另外还有一汇总module top-level的script，它并不会被charset和defer影响。

## defer & async

对于classic scripts ，如果出现了async，那么它们会被并行请求并当script可用时，会被解析。如果没有async但是有defer的话，那么script将会被并行请求并且当页面解析完成后才会被解析。如果defer和async都没有出现，脚本将会被请求并立即执行，会阻塞页面解析知道这个脚本执行完成。
而对于module script，如果有async，那么这个脚本和它所依赖的脚本将会并行请求并执行，如果没有async，那么module script将会并行请求所有依赖脚本并且在页面解析完成后执行，【warn:module script 没有defer】

![](https://html.spec.whatwg.org/images/asyncdefer.svg)

