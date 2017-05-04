---
layout: post
title: "gradle copy 指定的文件 "
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

copy 指定的文件：

	task copyTaskWithPatterns(type: Copy) {
	    from 'src/main/webapp'
	    into 'build/explodedWar'
	    include '**/*.html'
	    include '**/*.jsp'
	    exclude { details -> details.file.name.endsWith('.html') &&
	                         details.file.text.contains('staging') }
	}



只copy .apk

	task TestOne{
	    copy{
	        from 'build/outputs'
	        into 'yuge'
	//        exclude {
	//            details -> details.file.name.endsWith('.apk')
	////                &&                details.file.text.contains('staging')
	//        }
	
	        include{
	            details -> details.file.name.endsWith('.apk') || fileNotEmpty(details.file)
	        }
	
	    }
	
	
	}
	def fileNotEmpty(Object file){
	    if (file.isDirectory()) {
	        String[] files = file.list();
	        if (files.length > 0) {
	            System.out.println("目录 " + file.getPath() + " 不为空！");
	            return true
	        }
	    }else{
	        return false
	    }
	}

只不过上面的这个有问题，会copy空的文件夹。




> 问题1：

	exclude { details -> details.file.name.endsWith('.html') &&
		                         details.file.text.contains('staging') }

这种闭包的写法，里面的参数是方法吗？到底是什么？里面到底可以写什么？
哪里可以找到答案？















Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs