#模块加载器比较：Webpack VS RequireJS VS Browserify

### 简而言之，使用Webpack是没错的。
以下阐述理由

### 名称映射

aliase 对于整个项目维护、开发、组织都是十分关键的，Webpack和RequireJS在客户端和服务端都有aliase。然而Browserify没有，因为其原理(运行于nodejs环境下)不方便支持强名称绑定的依赖。

### 速度

这里如果说开发时的速度(构建时的速度)，RequireJS无需构建期，它是运行期的依赖分析和加载，但是对于browserify和webpack则需要构建动作。如果考虑到运行期的时间消耗，更倾向于把时间耗费在构建期


### 内存使用

requirejs也是有优势的，他也是根据需要将模块文件动态加载，而另外两个则需要将所有文件源码一次性加载进入。



