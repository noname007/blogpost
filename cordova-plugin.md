# Cordova custom plugin 

## Parse Plugin.xml

- plugin  [top element]
- engine 描述可支持的平台版本

```
<engines>
  <engine name="my_custom_framework" version="1.0.0" platform="android" scriptSrc="path_to_my_custom_framework_version"/>
  <engine name="another_framework" version="&gt;0.2.0" platform="ios|android" scriptSrc="path_to_another_framework_version"/>
  <engine name="even_more_framework" version="&gt;=2.2.0" platform="*" scriptSrc="path_to_even_more_framework_version"/>
</engines>
```
- name 
- description
- author
- keywords
- license
- asset 这个是用来列出文件或者目录需要拷贝到cordova中的www目录下，当然这个元素可以内嵌入<platform>标签下，成为平台特定的资源
- js-module 主要是将js-module中的js文件可以作为动态加载，并且由于plugin本身的特性，所以plugin中的js文件将会在整个应用启动前率先加载进来。

假设现在有个plugin，其plugin-id为B，那么这个js—module所对应的文件将会在打包阶段拷贝到/www/plugins/B/A.js目录中，并且添加一个入口到/www/cordova_plugin.js,在加载阶段，cordova.js会使用XHR技术加载每一个js文件到html中

```
<js-module src="A.js" name="A">
</js-module>
```
- info 提供给开发者的额外信息
- preference 允许开发者设定自定义变量