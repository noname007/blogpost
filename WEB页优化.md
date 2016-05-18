# WEB页优化

## DOM构建
![](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/images/full-process.png)

## render-tree 构建、布局、绘制

- DOM和CSSOM树组装成render树
- render树只包含需要在页面生成的节点
- 布局阶段会准确计算每个元素的位置大小
- 绘制是render树最后要做的事情:将每一像素绘制到屏幕上

## Blocking CSS

- 默认情况下，CSS被认定为一种渲染阻塞型的资源，
- Media类型可以允许某些CSS作为非渲染阻塞性
- 所有CSS资源无论阻塞非阻塞，都需要由浏览器下载

## JS优化
最好使你的Script改成async类型，并且限制那些无关紧要的JS影响你的关键渲染路径（critical rendering path）
- JS执行阻塞CSSOM构建
- 除非JS脚本被声明为async，JS会阻塞DOM构建
- 执行内联的脚本代码会阻塞DOM树构建，并同时延后初始化渲染
- CSSOM构建会阻塞JS执行
