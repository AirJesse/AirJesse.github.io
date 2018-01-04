---
title: 解决jenkins git timeout的问题
date: 2018-01-04 14:25:04
tags:
	- 零碎手札
---

最近工作中遇到jenkins构造项目报错 ```ERROR: Timeout after 10 minutes``` 原因在于：项目过大且网速过慢，git fetch 默认时限是10分钟，超时导致构造失败。

那么解决方法自然是调整git超时时间，遂百度之，广泛得文如下：
![git超时解决方案-网络.jpg](http://upload-images.jianshu.io/upload_images/1336536-cda1ac9883e4a186.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



一派胡言......真正合适的解决方法应该是:
<!-- more -->

1. 进入项目配置(project configure)
1. "源码管理"选项卡中，找到 ```Additional Behaviours``` 点击旁边的 add
![image.png](http://upload-images.jianshu.io/upload_images/1336536-5686a283e54fb6d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
1. 点击 ```advanced clone behavious``` 
1. 在 ```Timeout (in minutes) for clone and fetch operations``` 一栏中填入你需要的超时时间（比如 20）。

最终保存，以上操作即完成了对git fetch超时时间的设置。

网上历史遗留博文害人不浅，望自思考，勤探索。

