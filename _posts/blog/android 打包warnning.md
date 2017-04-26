---
layout: post
title: "android 打包warnning "
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
	
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Proguard returned with error code 1. See console
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Note: there were 372 duplicate class definitions.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Warning: com.alipay.android.phone.mrpc.core.d: can't find referenced method 'org.apache.http.auth.AuthSchemeRegistry getAuthSchemes()' in class com.alipay.android.phone.mrpc.core.d
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Warning: com.alipay.android.phone.mrpc.core.d: can't find referenced method 'org.apache.http.cookie.CookieSpecRegistry getCookieSpecs()' in class com.alipay.android.phone.mrpc.core.d
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Warning: com.alipay.android.phone.mrpc.core.d: can't find referenced method 'org.apache.http.client.CredentialsProvider getCredentialsProvider()' in class com.alipay.android.phone.mrpc.core.d
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1]       You should check if you need to specify additional program jars.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] Warning: there were 3 unresolved references to program class members.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1]          Your input classes appear to be inconsistent.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1]          You may need to recompile them and try again.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1]          Alternatively, you may have to specify the option 
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1]          '-dontskipnonpubliclibraryclassmembers'.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] java.io.IOException: Please correct the above warnings first.
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] 	at proguard.Initializer.execute(Initializer.java:321)
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] 	at proguard.ProGuard.initialize(ProGuard.java:211)
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] 	at proguard.ProGuard.execute(ProGuard.java:86)
	[2017-04-17 13:44:44 - vivo_3.0.1_plug1] 	at proguard.ProGuard.main(ProGuard.java:492)

解决方法：
在proguard里面，设置：

	-ignorewarnings












Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs