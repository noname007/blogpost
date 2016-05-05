## 渲染引擎
- HTML解释器
- CSS解释器
- 布局
- JS引擎
- 绘图


## 流程
- DOM树构建
- CSS、布局计算和渲染
	- CSS计算后 RenderObject生成
	- 布局计算后 RenderLayer生成
	- 渲染

- Android系统的局限性，Renderer进程的数目会被严格限制，“影子”(PHANTOM)标签就是浏览器会将后台的网页所使用的渲染设施都清除，只是原来的一个影子，当用户再次切换的时候，网页需要重新加载和渲染。
- 在Android的WebView中，Single Process模式会被采用。


## 资源加载和网络栈
- 资源缓存
	- 利用HTTP请求头:If-Modified-SInce 或者 If-None-Match
- chrome://net-internals

## HTML解释器和DOM模型

- Web开发者在监听者的代码中应该调用时间的preventDefault()函数来阻止浏览器触发它的默认处理行为。
- 事件默认行为是不冒泡
- 影子DOM

## CSS

## 布局计算
- 样式变化，重新计算布局
- 可视区域发生变化，需要重新计算布局
- 网页的动画在显示结束后，动画可能改变样式属性，那么Webkit就需要重新计算。

## 安全机制
- 域 Origin 	