---
layout: post
title: "android apk瘦身之图片压缩-tinypng"
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

## 参考地址：  ##
http://blog.csdn.net/jy692405180/article/details/52409369

http://www.tuicool.com/articles/BraI3qV

https://github.com/saitjr/STTinyPNG-Python/issues/3

tinypng官网

Android 的图片压缩其实压缩比很小。tinypng 大概可以压缩20%左右，我们工程的所有图片，之前是860k,压缩之后620k，少了200k。

# 使用：  #
1。安装python

2.使用pip进行安装tinypng的api：pip install –-upgrade tinify

3。执行脚本,脚本如下：

    import tinify
	import os
	import os.path
	# reload(sys)
	# sys.setdefaultencoding("utf-8")
	
	tinify.key = "s8s--eMb8bFVe4Z-9fHEL9xUfehY6sKC" # AppKey
	# src
	fromFilePath = "D:/svn/bak2//src/main/res/drawable-xxhdpi" # src
	toFilePath = "F:/pytest" # out


	for root, dirs, files in os.walk(fromFilePath):
	    for name in files:
	        fileName, fileSuffix = os.path.splitext(name)
	        if fileSuffix == '.png' or fileSuffix == '.jpg':
	            toFullPath = toFilePath + root[len(fromFilePath):]
	            toFullName = toFullPath + '/' + name
	            fromFullPath = fromFilePath + root[len(fromFilePath):]
	            fromFullName = fromFullPath + '/' + name
	
	            if os.path.isdir(toFullPath):
	                pass
	            else:
	                os.mkdir(toFullPath)
	
	            source = tinify.from_file(fromFullName)
	            source.to_file(toFullName)




其中：


tinify.key = “s8s–eMb8bFVe4Z-9fHEL9xUfehY6sKC” # AppKey 是你的APPkey,去tinypng申请 
fromFilePath = “D:/svn/bak2/src/main/res/drawable-hdpi” # 是你要压缩的图片目录 
toFilePath = “F:/pytest” # out 是压缩完之后的目录

备注： 
申请tinypng api地址

注意：
如果你的图片中含有.9.png那么最好不要传到这个网站上去压缩，可能会导致你的图片变得不可以用，然后你的Android stadio 会一直告诉你图片有问题，别问我怎么知道的。





Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs
