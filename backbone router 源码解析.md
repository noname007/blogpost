# backbone router 源码解析

跟路由功能相关的有两个，一个是router，一个是history，其中router负责的就是触发对应的路由事件，history的功能有点类似window.history对象(实际上是window.historyd的wrapper对象)用来记录路由历史的。

## Router部分
先是对参数初始化