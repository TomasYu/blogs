---
layout: post
title: "android ?attr/的使用"
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

## ?attr的使用  ##

## 在res/values/attrs.xml ##

	<?xml version="1.0" encoding="utf-8"?>
	<resources>
	    <attr name="welcombg" format="reference"></attr>
	</resources>


## 使用 ##
	<?xml version="1.0" encoding="utf-8"?>
	<resources xmlns:android="http://schemas.android.com/apk/res/android" xmlns:tools="http://schemas.android.com/tools">
	    <style name="demo" parent="Theme.AppCompat">
	        <item name="welcombg">@mipmap/welcome_bg</item>
	    </style>
	    <style name="demo2" parent="Theme.AppCompat">
	        <item name="welcombg">@mipmap/ic_launcher</item>
	    </style>
	    <style name="Theme.Application" parent="android:style/Theme.Light">
	        <item name="android:windowNoTitle">true</item>
	        <item name="android:windowIsTranslucent">false</item>
	    </style>
	    <style name="Theme.windowIsTranslucent" parent="@style/Theme.AppCompat.Light">
	        <item name="android:windowNoTitle">true</item>
	        <item name="android:windowIsTranslucent">false</item>
	        <item name="android:background">@color/white</item>
	    </style>
	    <style name="IreaderTheme" parent="demo">
	        <item name="android:windowNoTitle">true</item>
	        <item name="android:windowIsTranslucent">false</item>
	
	        <item name="android:windowBackground">?attr/welcombg</item>
	    </style>
	
	    <style name="Theme.Author" parent="@android:style/Theme.Translucent">
	        <item name="android:windowNoTitle">true</item>
	        <item name="android:windowIsTranslucent">true</item>
	    </style>
	
	    <style name="Theme.Common" parent="@android:style/Theme.Translucent.NoTitleBar"/>
	
	    <style name="Theme.noTranslucent" parent="@style/Theme.Application">
	        <item name="android:windowIsTranslucent">false</item>
	    </style>
	
	    <style name="btnStyle">
	        <item name="android:layout_width">match_parent</item>
	        <item name="android:layout_height">50dp</item>
	        <item name="android:layout_marginTop">10dp</item>
	        <item name="android:layout_marginLeft">30dp</item>
	        <item name="android:layout_marginRight">30dp</item>
	    </style>
	
	    <style name="BrowserBtnStyle">
	        <item name="android:layout_width">0dp</item>
	        <item name="android:layout_height">50dp</item>
	        <item name="android:textSize">13sp</item>
	        <item name="android:layout_weight">1</item>
	        <item name="android:layout_marginLeft">10dp</item>
	    </style>
	
	    <style name="bootom_text_style">
	        <item name="android:layout_width">0dp</item>
	        <item name="android:layout_weight">1</item>
	        <item name="android:layout_height">match_parent</item>
	        <item name="android:gravity">center</item>
	        <item name="android:background">@drawable/bt_shape</item>
	    </style>
	</resources>

比如你有两套theme,那么他就会根据你当前的theme去取welcombg的值显示出来。






Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs
