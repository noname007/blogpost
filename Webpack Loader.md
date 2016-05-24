# Webpack Loader

一个Loder满足一个node module的定义，并export 一个function。

一般情况下，一个loader只会被传入一个参数2，那就是待处理的文件内容的字符串。
一个同步式的loader只需要return一个value，而异步式的loader就可以传入更多的数据。如this.callback(err,values）函数。在loader运行期间发生的错误就会被抛入this.callback或者直接在同步式loader中抛出异常。

在复杂的例子中，当多个loader链式处理，只有最后的loader会获得resource file并且第一个loader只需要一个活着了两个参数，其他loader的返回将会把返回传给前一个loader。


### loader 加载顺序
按照以下顺序处理
- config文件中的preloaders
- config文件中的loaders
- 源码中的require("loader")
- config文件中的postloaders

但是在使用第三种request时，可以使用一些字面量语法：
- 在require中加入！，如require("!A!./aaa.js") ,这种会使config中的preloaders失效
- 在require中加入！！，如require("!!A!./aaa.js"),这种会使config中的所有loaders失效
- 在require中加入-！，如require("-!A!./aaa.js"),这种会使config中的preloaders 和loaders失效


