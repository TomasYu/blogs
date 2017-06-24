---
layout: post
title: "Android 布局错乱 Android花屏"
modified:
categories: blog
excerpt:
tags: []
image:
  feature: so-simple-sample-image-7.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/

date: 2014-08-08T15:39:55-04:00
modified: 2016-06-01T14:19:19-04:00
---

 最近做项目，妈的，有个一个很难受的bug.
 这个bug ,自己这里没有手机，没有办法复现，找到了手机之后。解决了。
 我先给大家看下什么叫布局错乱，花屏：
来张正常的图片：
![这里写图片描述](http://img.blog.csdn.net/20170624172408265?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzI3MDQ0NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

正常情况下是这样的。然后，错误的情况下：
![这里写图片描述](http://img.blog.csdn.net/20170624172438021?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdTAxMzI3MDQ0NA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

全乱了。有的图片都没有显示出来。

## 我说一下复现步骤： ##
1。打开应用
2。最近任务，一键杀死所有进程。
3。点击应用
4。home 键会桌面。
5。点击应用或者最近任务启动程序。

就出现了。

----------


还好有log输出，不然真的不知道哪里的问题。开始我自己也乱了，妈的，这是哪里的问题？不就是到了后台？

后来我就盯着logcat 看，我发现，只要屏幕乱了，就会出现：
OpenGLRenderer: GL error: GL_INVALID_VALUE

sb 都能看懂，GL 绘图错了。 但是不是每次都输出这个log 奥。有时候，会输出：E/libEGL: validate_display:255 error 3008 (EGL_BAD_DISPLAY)

然后我就百度。

[参考](http://vjson.com/wordpress/android-webview%E5%BC%80%E5%90%AF%E7%A1%AC%E4%BB%B6%E5%8A%A0%E9%80%9F%E5%AF%BC%E8%87%B4%E5%B1%8F%E5%B9%95%E8%8A%B1%E5%B1%8F.html)

然后就知道了，硬件加速导致的问题。关于硬件加速导致的问题，网上一堆。

[参考](http://blog.csdn.net/xu_fu/article/details/48208795)

怎么关闭呢？一般都不会让你在应用程序里面直接关闭，粒度太大。
我的是webview那么就在自己的webview里面不开启就可以了。最小粒度的去解决了问题。记住，一定要在构造函数里面关闭，别问怎么知道的。

```
	public CustomWebView(Context context) {
		super(context);
		webViewId = toString();
		setLayerType(View.LAYER_TYPE_SOFTWARE, null);
	}
```
setLayerType(View.LAYER_TYPE_SOFTWARE, null); 就可以了。















Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs