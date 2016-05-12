# WEB端框架设计


## 模块化

 - 模块打包	
	- 模块定义 一个具有公共接口、内部具有绝对DOM控制权、自包含CSS、JS、data.json（配置文件）的文件集合，形式也要固定
	- 模块引用 使用怎样的语法规则引入
		- RequireJS
	- 所有模块文件合并为一个文件
		- JS语法分析
			- 获取AST 
				- Babel => Babylon => acron
					- Plugin 
			- 获取所有require or import 所依赖的模块
		- 寻找模块文件所存放的地址
			- 提前配好配置 
		- 模块内文件合并
			- JS、CSS、JSON、HTML结合 
				- Vue
			- 依赖分析 
		- 库文件，非模块化定义JS脚本     
	- 模块加载 
		- AMD && CommonJS
			- requirejs 
			- browserfy 
	- 模块生命周期管理
		- requirejs

## 任务流
 
- 流式任务链
	- 编译
		- es6 =》es5
		- less=》css
		- 非ecma script编译es
	- 库管理
		- bower 
		- npm 
	- 静态资源整合和流控制
		- webpack
	- 优化
		- jslint
	- 压缩
		- compress
	- 混淆
		- uglify2
	- 单元测试

## UI控件库

- 模块化封装
	- jQueryMobile
	- SenchaTouch
	- Webix
	- XXXXUI 等UI库

## 封装接口

- 统一命名接口
- 命名空间nireus

## CLI工具
- 操作简化成命令行
- 任务配置化
	