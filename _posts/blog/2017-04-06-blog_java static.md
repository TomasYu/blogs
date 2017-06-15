---
layout: post
title: "java static "
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
java static 使用陷阱

今天解决了一个bug，这个bug真的是不应该。但是后来还是有这个bug.
书架上很多书，然后进入了编辑态之后，我点了其中一本，其他的书全都选中了。
开始的时候，我跟着点击事件去跟。当然我必须让自己养成不调试的习惯，因为调试太费时间了。
我尽量让代码在自己脑子里执行，我尽量读懂代码。

后来跟了半天也没有发现什么异常。妈的，后来我还是去找那个会影响选中状态的东西，也就是一个变量，
我看谁会改变这个变量。当我再看这个变量的时候，我一看，我把它改成static的了。
我懂了。瞬间知道问题在哪了。

static的字段，所有的类的实例共享。也就是说，很多书籍的实例，都共享这个变量。所以，一本书变了，其他的
都变了。我应该想到的。还是年轻。经验少。这些书都是一个类的实例，一个改变，其他也都改变，肯定是共享了一个
静态的成员变量。


不过好开心，自己对java的理解，又近了一步。以后这种错误，再也不会犯了。真的，少用静态的好。














Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs