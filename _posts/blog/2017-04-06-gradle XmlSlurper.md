---
layout: post
title: "gradle XmlSlurper"
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
gradle task

	task deployApks(type:Copy){
	    description ="Copies APKs and Proguard mappings to the deploy directory"
	    def appName ="posture"
	    def versionDir =android.defaultConfig.versionName+"_"+android.defaultConfig.versionCode
	
	
	    println("copies APK and Proguard 2 " + versionDir)
	
	
	    from 'build/outputs/mapping/release'
	    include '**/mapping.txt'
	    into '../.admin/deploy/'+versionDir
	    rename ('mapping.txt',"${versionDir}-mapping.txt")
	
	    from ('.'){
	        exclude '**/build','**/src'
	    }
	
	    include '*.apk'
	    into '../.admin/deploy/'+versionDir
	    rename('app-release.apk',"${appName}-${versionDir}.apk")
	}



得到androidmainFest.xml 里面的属性：

	
	def getVersionName(){
	    def fileManifest = file("src/main/AndroidManifest.xml")
	    def androidManifest = new XmlSlurper().parse(fileManifest)
	    return androidManifest.@'android:versionName'
	}
	
	def getVersionCode(){
	    def fileManifest = file("src/main/AndroidManifest.xml")
	    def androidManifest = new XmlSlurper().parse(fileManifest)
	    return androidManifest.'@android:versionCode'
	}

> 注意：其实androidManifest.@'android:versionName' 和androidManifest.'@android:versionName'是一样的。也可以androidManifest.getProperty('@android:versionCode')。都可以正确获取，原理可以看源码：

example:

	def getVersionCode(){
	    //读取xml
	    def fileManifest = file("src/main/AndroidManifest.xml")
	    //解析
	    def androidManifest = new XmlSlurper().parse(fileManifest)
	
	//    <manifest xmlns:android="http://schemas.android.com/apk/res/android"
	//    package="com.chaozh.iReaderFree"
	//    android:installLocation="auto"
	//    android:versionCode="10001"
	//    android:versionName="1.0.1">
	
	    //要想得到非命名空间的属性，必须加上设置命名空间的属性
	    androidManifest.declareNamespace('android':'http://schemas.android.com/apk/res/android')
	    println androidManifest.getProperty('@package')
	
	    // 节点的名字
	    println androidManifest.name()
	    //  节点的长度
	    println androidManifest.size()
	    println androidManifest.getProperty('@android:installLocation')
	    println androidManifest.children().getProperty('@android:minSdkVersion')
	    /**
	     * Returns the specified Property of this GPathResult.
	     * <p>
	     * Realizes the follow shortcuts:
	     * <ul>
	     * <li><code>'..'</code> for <code>parent()</code>
	     * <li><code>'*'</code> for <code>children()</code>
	     * <li><code>'**'</code> for <code>depthFirst()</code>
	     * <li><code>'@'</code> for attribute access
	     * </ul>
	     * @param property the Property to fetch
	     */
	//    public Object getProperty(final String property) {
	
	    println androidManifest.getProperty('*').getProperty('@android:minSdkVersion')
		//会得到所有的直接子节点的所有带name的属性的name的值
	    println androidManifest.getProperty('*').getProperty('@android:name')
	
	    //androidManifest 下面的application 节点 的 getProperty
	    println androidManifest.application.getProperty('@android:largeHeap')
	
	    //便利当前子节点的所有节点名字
	    Iterator iterator=androidManifest.childNodes()
	    while(iterator.hasNext()){
	        def it=iterator.next();
	        println it.name
	    }
	
	}
	
	
	task getVersion{
	    getVersionCode()
	}






gradle 问题：
> 1.为什么可以androidManifest.'@android:versionName',为什么可以不用写方法名？androidManifest.getProperty('@android:versionCode')


> 2.why get packae failed

	def getVersionCode(){
	    def fileManifest = file("src/main/AndroidManifest.xml")
	    def androidManifest = new XmlSlurper().parse(fileManifest)
	    return androidManifest.getProperty('package=')
	}

解：

	//要想得到非命名空间的属性，必须加上设置命名空间的属性
	androidManifest.declareNamespace('android':'http://schemas.android.com/apk/res/android')
	println androidManifest.getProperty('@package')



>3.why 一定要加@
	
	println androidManifest.getProperty('@android:installLocation')
解：

	    /**
	     * Returns the specified Property of this GPathResult.
	     * <p>
	     * Realizes the follow shortcuts:
	     * <ul>
	     * <li><code>'..'</code> for <code>parent()</code>
	     * <li><code>'*'</code> for <code>children()</code>
	     * <li><code>'**'</code> for <code>depthFirst()</code>
	     * <li><code>'@'</code> for attribute access
	     * </ul>
	     * @param property the Property to fetch
	     */
	//    public Object getProperty(final String property) {












Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs