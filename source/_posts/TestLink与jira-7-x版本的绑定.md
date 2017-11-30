---
title: TestLink与jira 7.x版本的绑定
date: 2017-11-12 15:57:19
tags:
	- 零碎手札
---

近期帮测试安装TestLink并配置与jira的绑定。搜索到的文章基本都是说在```issue Tracker Management```中设置```jira(interface:soap)```。
但如此设置在实际使用中会出现无法连接的提示。
随后又有文章中说要在jira的通用设置中打开```remote api calls```,然而在公司所安装的jira(7.3)中并无此设置。

翻阅Jira官方文档的时候我看到了这个:
![image.png](http://upload-images.jianshu.io/upload_images/1336536-efe0a6a166894c19.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

所以实际上soap的方式已经在7.x版本中被移除了.....如果恰巧安装的是jira7以上版本，那么在这件事上互联网上大部分博文都是在误导你（论看官方文档的重要性）

### 解决方案
采用rest方式即可，不需在jira中进行任何配置。
![image.png](http://upload-images.jianshu.io/upload_images/1336536-6fb6bc79ed8eba8f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

替换上述中账号密码url以及projectKey。

