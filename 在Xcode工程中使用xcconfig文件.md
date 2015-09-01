# 在Xcode工程中使用xcconfig文件


如果你经常苦恼于解决与其他开发者协作开发引发的冲突问题，那么你需要调整xcconfig文件。我的经验是将building的设置项移到分离出来的xcconfig文件中，这些文件可被版本管理系统独立地追踪。

xcconfig 文件是Xcode用来配置project、target等属性的文件，并且cocospod工具也是使用xcconfig来完成依赖库的构建工作的。

新建xcconfig文件可以从新建文件的一下位置处建立
![](http://ww3.sinaimg.cn/large/4483e99egw1evmxorgh51j20kk0c5wg9.jpg)
新建立的xcconfig文件除了注释的版权信息外，并没有其他内容，你需要往其中添加内容，除此之外，这个文件并没有跟project文件建立联系，你需要手动指定这其中的关系。

![](http://ww1.sinaimg.cn/large/4483e99egw1evmxwqua49j20b70933z9.jpg)
在右侧project的info中找到如下内容
![](http://ww2.sinaimg.cn/large/4483e99egw1evmxx6utxlj20e203qq35.jpg)

点击展开指示器，在对应的Target下选择不同的xcconfig文件，这样便算是建立了联系。

xcconfig文件本质上是个Key-Value文件，其中的有效键名key是从build seeting这个选项卡中选择的。
