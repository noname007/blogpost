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