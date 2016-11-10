# AppContainer

App容器是一种Hybrid开发的方式


# 可能出现的问题
## JSBridge
- 桥接协议设计
- NativeHandler
- 异步回调
- 多线程

## 版本更迭问题
Native本身已经十分稳定了，很少新增功能了，否则在直连情况下就会面临一个尴尬，因为web站点永远保持最新的，就会在一些低版本容器中调用了没有提供的Native能力而报错。

## 跳转
跳转是Hybrid必用API之一，对前端来说有以下跳转：

- 页面内跳转，与Hybrid无关
- H5跳转Native界面
- H5新开Webview跳转H5页面，一般为做页面动画切换

## 跨域问题

Native代理转发可以解决


## 资源缓存和离线更新问题
- 静态资源按版本缓存
- 优先本地资源加载
- 增量/全量更新

## 用户系统
- 持久化用户登录态信息
- 登入时机策略

## NativeUI
- 常用通用组件：提示、弹窗、Modal、导航栏、界面栈
- 低效DOM元素在渲染时转换为Native侧UI实现，如\<ul/>\<ol/>【类似React Native、NativeScript、Weex实现】