# WEB前端框架 -X框架
> 根据之前对Angular、Angular2、React、Vue、Polymer框架的研究，综合比较来看，当下[2016年5月31日]最适合的拿来做基础部分的是React和Vue，我整个框架思路也将是建立在这两个框架之上，然后再根据我们实际的需求添加新的特性。以下把这个框架名称称为X。


## 总体技术

核心部分: Webpack、ES6、Module-loader(自硏)、X框架、X-CLI（自硏）、

- Webpack ：项目构建工具，负责ES6语法转化、模块依赖分析、模块合并、优化、混淆、压缩和其他静态资源调整步骤
- ES6 ：使用由babel支持的ES6语法特性
- Module-loader：主要是模块化语法转换
- X框架： 框架本身
- X-CLI:创建样例工程、编译组件

## 工程结构预览

- Demo_Project
	- build 
		- component 组件编译目录 
	- res 
		- css
		- image
		- font
		- ...
	- src
		- components
			- componentA 组件A
				- A.js
				- A.css
				- A.json 
				- A.html(并不是标准的html文件，所以这里的后缀值得商榷)
			- componentB
		- utils 工具集合
		- filter
		- store
		- app.js  应用入口
	- lib 第三方库，这里主要存放是不适合用component结构来编写或者改写的库，如jquery等
	- index.html 首页

## 底层特性

- 将virtual dom融入Vue中，这也是Vue2.0在做的事情(借鉴React)
- 支持组件、过滤器、双向绑定(借鉴Vue)
- 支持更多钩子函数(借鉴React)
	- getDefaultProps
	- getInitialState
	- componentWillMount
	- render
	- componentDidMount
	- componentWillUpdate
	- componentShouldUpdate
	- componentDidUpdate
	- componentWillUnmount
- 支持配置式组件的开发，将组件逻辑和运行参数分离，可能方便将来可视化工具开发
- 剩下的特性基本与Vue一致


## 组件component定义

- 特征基本与Vue中的component中的一致，不过我们是拆分成具体的js、html、css文件，优点可能有1条，就是源码文件看起来整洁。
- 在编译组件环节，html、css、js三者合并进入同一js文件。


## 开发流程

- X-CLI 创建样例工程
- 开发各个组件
- 编译组件
- 配置webpack中module-loader
- 运行webpack完成模块合并、压缩、混淆





 