#WEB前端框架架构解析

## 前言


经过一段时间的研究和开发，这套Web框架日趋成型。这套框架的设计初衷有如下三点：

- **组件式的源码架构** 提高代码的复用性，可以实现快速开发，较为清晰的源码结构方便开发者快速接手，并且方便团队协作
- **高效的页面加载和执行速度** 动态的模块加载方式可以按需加载模块，有效提高首屏加载速率，这对于一个Web SPA应用来说非常重要。
- **快速灵活的打包发布方式** 方便我们使用更多更先进的前端技术，不会受限于框架本身所提供。


在设计整个前端框架时，也是基于上述三点的考虑，通过研究比对现有的主流Web框架方案Angular、React、Vue等、未来代表技术流行趋势的Web框架方案Polymer等以及当下热点的技术框架等等，再结合我们实际的需求，设计出我们自己的前端框架X框架。


## 整体结构

- X框架
	- 路由和页面状态管理 X.Router 
	- HTML模板 Jade
	- CSS预处理器 SASS
	- 模块加载和管理 Webpack
	- CSS Module CSS-loader
	- 模块通讯中心 X.Mediator
	- 压缩混淆工具 uglify2
	- ES6预处理器 Babel
	- UI库 Webix
	- 函数化工具 lodash

## 技术点分析

首先说明的是，这个框架并没有像其他成熟的Web框架Angular、React、Vue等提供自定义组件(元素)、指令、数据绑定这几个常见MVVM框架中的必备功能，目前必须承认的是这几个功能对于开发者来说是极其便利的，但对于整体运行速度存在一定影响，具体要不要后续补到框架中，也是需要再考虑的。


### 路由和状态管理

具体使用方法如下：

```
var AppRouter = X.Router.extend({
            routes: {
                "posts/:id" : "getPost",
                "download/*path": "downloadFile",  //对应的链接为<a href="#/download/user/images/hey.gif">download gif</a>
                ":route/:action": "loadView",      //对应的链接为<a href="#/dashboard/graph">Load Route/Action View</a>
                "*actions" : "defaultRoute"
            },
            getPost: function(id) {
                alert(id);
            },
            defaultRoute : function(actions){
                alert(actions);
            },
            downloadFile: function( path ){
                alert(path); // user/images/hey.gif
            },
            loadView: function( route, action ){
                alert(route + "_" + action); // dashboard_graph
            }
        });

        var app_router = new AppRouter;

        X.history.start();

```
### 模块通信中心 X.Mediator

使用设计模式中的中介者模式是最适合多模块通信的一种模式。

首先要实例化一个X.Mediator 负责全局事件的监听和通知，模块之间的通信都需要借助Mediator来完成。

![](http://ww3.sinaimg.cn/large/4483e99ejw1f5kbfmp1d1j20am09xwff.jpg)

ModuleA 想要做什么事，publish 了一个event，Mediator获得此消息后，然后启动能处理此事件的ModuleB，如果ModuleB还没有加载，此时可以动态加载，处理完此event后，ModuleB再将完成的消息发送给Mediator，最后Mediator再将Event完成的消息下发给ModuleA。

### HTML模板

使用jade

### CSS预处理和CSS模块化

使用sass和CSS-loader

### Webpack

webpack不止是充当了我们模块加载的加载器，它还担当了整个打包流程中各个预处理阶段事务、编译事务、合并事务、压缩混淆等后期事务的指挥者。具体原理和技术细节不再赘述了。





	