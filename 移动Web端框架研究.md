# 移动WEB端框架研究



[Javascript MVC框架技术选型](https://segmentfault.com/a/1190000000379723)


## 单页面应用开发需求

- HTML和客户端JavaScript对象模型的双向绑定
- 视图模板
- 数据存储（本地存储或者通过服务器存储到数据库）
- URL路由（确保后退按钮和搜索引擎正常工作）
- 语言层面的服务，通用的Pub/Sub


> WEB端框架=MV* 框架+UI库


## 已发现框架
- framework7 [framework7.io](http://framework7.io)
- Ionic 跟phonegap、corodva很像的框架，准确说是做hybrid app的，不太适合做单页面应用
- Backbonejs 双向绑定框架 、路由
- React View层框架 ,借助backbone可以实现angular的全部功能
- ember.js 各方面都弱于angular，无论性能、文件大小、社区活跃度都弱于angular
- AMAZEUI 单纯的V层框架，依赖于react.js 
- Material-UI 单纯的V层框架，与React.js结合使用
