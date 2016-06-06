# Parse Module ES6

## Module Record
一个Module Record(以下简称MR)封装了关于这个模块imports和exports的记录，被用于连接（import和export）其他模块，当解析一个Module时，会使用MR中4个字段。

因为某些特殊的用途，MR的格式也是特定的Record格式，就好比面向对象中一个抽象类的子类。本规范只制定了一个Record格式， 名称叫做Source Text Module Record。其他规范和实现可能会根据自己的实际需求来定义Module Record。

Module Record Field

Field Name|Value Type | Meanning|
-----|-----|-----|
realm|||说明module在哪里创建的|
environment|词法环境lexical environment|词法环境包含所有在顶层包含此模块的绑定关系，这个字段会在<br>模块实例化时设定|
namespace|object|模块的命名空间对象会伴随模块的诞生而设置|
evaluated|boolean| 初始值为false，当开始解析这个模块的时候被设置为true，true的状态会一直保持在解析结束|

Module Record Nethod

Method|Purpose|
-----|-----|
GetExportedNames(exportStarSet)|返回一个列表，其中包含这个模块所有直接或间接的的export名称|
ResolveExport（exportName，resolveSet，exportStarSet）|返回这个模块export出来的binding，binding是以下这种关系{[[module]]:module record,[[bindingName]]：String} |
ModuleDeclarationInstantiation()|解决模块的所有依赖关系|
ModuleEvaluation()|如果Module已经被解析过，那么将不会有任何动作；否则将会解析所有依赖的模块并再处理当前模块。ModuleDeclarationInstantiation(）必须要在此函数执行前执行 |


## Source Text Module Record

Additional Fields of Source Text Module Records

Field Name| Value Type| Meaning|
---------|----------|---------|
ECMAScriptCode| 解析结果|解析mmodule源码结果|
RequestedModules|字符串列表| 此模块中所有需要import的模块名称|
ImportEntries| ImportEntry 列表记录| 所有引入模块点|
ExportEntries|        |所有导出点|

- ImportEntry
	- ModuleRequest  import的模块名称
	- ImportName     导入的名称
	- LocalName 		导入之后使用的名称
- ExportEntry
	- ExportName     
	- ModuleRequest
	- ImportName
	- LocalName 

## ParseModule

1. 分析文件，语法、句法错误
2. 如果有错误就抛出，没错误就构建AST
3. 