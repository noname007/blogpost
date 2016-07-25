# 企业内分发应用

苹果支持无线安装企业内分发的应用，应用必须以ipa的形式提供并且配有企业内分发的配置文件。需要以下三个:

- 一个xml.manifest 文件
- 一个可以让用户访问到itunes server的配置
- 使用https和7.1以上iOS版本


# 流程

- 使用你的企业证书来打包
- 生成的manifest的file格式
	- url : https url用来下载应用
	- title :你安装时应用的名称
	- display-image ：57*57像素安装时的应用图标
	- full-size-image :512*512像素Image代表应用在商店的图标
- 构建你的web应用
	- 用户点击下载

	```
	<a href="itms-services://?action=download-manifest&url=https://example.com/manifest.plist">Install App</a>
	```
- 正确设置MIME Type
	- application/octet-stream ipa
	- text/xml plist
- certificate 验证
	- 当应用第一次启动，发布认证会去苹果OCSP server上验证证书真伪