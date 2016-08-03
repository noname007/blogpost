## Webpack中常见loader处理

- url-loader: 主要承担的任务是在没有超过limit传入的参数限制时，是将引用的文档数据是以"Data URI"格式传入的，超过限制后就按照file-loader来处理了。
- file-loader: 将引用的文件复制到Outpath输出目录下
- css-loader： 
	- 可以css-module处理
	- CSS中的url转换
		- 添加root参数(root=.)后，可以将url(/XXX) 转换为require(./XXX)
		- CSS中的url() 转换为require()
- Autoprefixer 主要处理的是多浏览器环境下的CSS前缀问题，并可以参数设置支持的最低版本 ，还可以优化你所写的CSS
- style-loader 将所写的CSS\<style\>添加到DOM树上 可以使用url(也就是rel的方式)或者raw

## Webpack中常见plugin处理
- ExtractTextPlugin:将所接收样式文件规则合并入同一文件中
	- allChunks: 默认情况下是只从initial chunk中加载合并的CSS文件，加入true，会将所有CSS从所有的模块中加载进来
	