---
layout: post
title: "android button settextcolor 无效"
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

## android button settextcolor 无效 ##

坑死我了，今天花了半个小时，一直在调试，为什么刚才有颜色，现在设置的颜色都不生效，都是灰色的。我明明在代码里面设置了红色，但是就是灰色。

后来，发现问题的关键了，
	
	button.setTextColor(R.color.mColorRight); 不生效，还不报错。但是你的
	颜色一直都是灰色的，因为R.color.mColorRight也是一个int值，好坑。
	
	必须要通过resource得到你的颜色，再设置才行。	
	button.setTextColor(mcontext.getResources().getColor(mDefaultColor));





Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs
