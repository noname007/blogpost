# Marionette VS Chaplin

## Backbone App的核心关键

- 事件驱动的机制
	- Pub/Sub事件
	- 清理监听器
- 应用架构
	- 单纯Router是无法完成的复杂的架构设计
	- controller和a manage layer
- 强页面约束
	- Backbone的View是一种比较抽象的模式，并没有提供绘制到界面上的方法，你需要按照自己的实际需求去重写render函数
	- M和C都提供了View的封装，并具备默认的render方法，你只需要选择模板语言
	- 安全的嵌套View和设置Region

## M实现的关键点
- 你可以拆分的使用M，M是一个足够模块化的框架
- Application Modules
 - 可以包含多种Routers 、Controllers、Models和Views。
 - Module可以装载也可以被卸载，并且模块当Route匹配后可以被Lazy-Loded
 - M.Application 也是个Module
- View Management
 - Layout holds several named Regions 
 - Region 可以插入view ，常见的有 header、navigation、 main、sidebar 、footer
 - 一个Region同一时间只有一个View，一个被打开了，另外一个就被安全的关闭


## M中不好的点
- 过于薄弱的抽象设计
- 不清晰的最佳实践思路
	- 过多的全局变量
	- Routing 和Controler不大
	
## N实现的关键点
- 使用OOP思想开发
- 支持CommonJS/AMD规范
- 明确的App架构
- 变量清理和Controller之间共享变量
- Mediator设计
- 