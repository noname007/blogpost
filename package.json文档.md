# package.json 中关于各种dependencies

官方文档在这里[https://docs.npmjs.com/files/package.json](https://docs.npmjs.com/files/package.json)

- dependencies
顾名思义，用来描述一个package所依赖的库的版本信息。
另外，请不要把各类代码转换工具、测试工具作为你的依赖库放入到列表中来
- devDependencies
如果你想下载并使用某个模块对的话，并且他们不需要额外下载测试文件、文档等文件，那么就把它加入devDependencies里面，在构建阶段在scripts里面使用prepublish目标来描述你需要做的事情。
- peerDependencies
需要优先配置好的依赖，算是绝对依赖项。
- bundleDependencies 
需要合并在一起的依赖库
- optionalDependencies 
跟dependencies类似，唯一区别是安装失败不会报错



