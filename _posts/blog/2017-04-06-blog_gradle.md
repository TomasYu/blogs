---
layout: post
title: "电脑多屏显示分辨率问题 "
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
# gradle 常用列子： #

## 遍历文件 ##
	task loadfile {
	    doLast {
	        def files = file('src/main/java').listFiles().sort()
	        listFile(files)
	    }
	
	}
	
	def listFile(Object files){
	    files.each { File file ->
	        if (file.isFile()) {
	//            ant.loadfile(srcFile: file, property: file.name)
	            println " *** $file.name ***"
	//                println "${ant.properties[file.name]}"
	        }else{
	            listFile(file.listFiles())
	        }
	    }
	}



## 文件排序 ##
	
	task loadfile {
	    doLast {
	        def files = file('test').listFiles()
	        Arrays.sort(files,new CompratorByLastModified())
	        listFile(files)
	    }
	
	}
	
	//根据文件修改时间进行比较  最晚修改的放在前面
	class CompratorByLastModified implements Comparator<File> {
	
	    public int compare(File f1, File f2) {
	        long diff = f1.lastModified() - f2.lastModified();
	        if (diff > 0) {
	            return -1;
	        } else if (diff == 0) {
	            return 0;
	        } else {
	            return 1;
	        }
	    }
	}
	
	
	def listFile(Object files){
	    files.each { File file ->
	        if (file.isFile()) {
	//            ant.loadfile(srcFile: file, property: file.name)
	            println " *** $file.name ***"
	//                println "${ant.properties[file.name]}"
	        }else{
	            listFile(file.listFiles())
	        }
	    }
	}



## copy ##

	task copyApkAndMapping(type: Copy){
	//    from 'build/outputs/apk'
	//    into '../apkBackUp'
	//    exclude '**/*-unsigned.apk'
	//    rename 'app-debug.apk', 'yuge.apk'
	
	    def logger=project.getLogger()
	//    project.logging.setLevel(LogLevel.INFO)
	    logger.info('caonima')
	    ant.lifecycleLogLevel = "INFO"
	    ant.echo(level: "info", message: "hello from info priority!")
	    String string = "abcedfg";
	    string=string.substring(1);
	    System.out.print(string)
	
	}

## zip ##
	task testZip(type:Zip){
	//    from 'build'
	//    into 'plug.zip'
	//    rename 'plug.zip','xinyu.zip'
			//压缩文件存放的目录
	        destinationDir = file('hehe')
			//压缩文件的名字
	        archiveName =  'abc.zip'
	
	        from(files('build')) {
	//            into( 'hehe' )
	        }
	//        from('misc'){
	//            include('config.json')
	//            into('.')
	//        }
	}


## 备份厂商sdk ##

	task backUpSdk(type: Copy){
	    //厂商名字
	    def changshang ='vivo'
	
	    def files = file('../signedApk').listFiles()
	    //排序，取最后生成的
	    Arrays.sort(files,new CompratorByLastModified())
	    println files.getAt(0).name  //plug.zip
	    println files.getAt(1).name  //mapping.txt
	    println files.getAt(2).name  //apk
	
	    from('../signedApk'){
	        include files.getAt(0).name
	        include files.getAt(1).name
	        include files.getAt(2).name
	    }
	
	    def backUpPath ='F:/ireader_work_changshang/backUpSdk/'+changshang+'/'+ getVersion()
	
	    println backUpPath
	    into(backUpPath)
	
	}
	
	
	//根据文件修改时间进行比较  最晚修改的放在前面
	class CompratorByLastModified implements Comparator<File> {
	
	    public int compare(File f1, File f2) {
	        long diff = f1.lastModified() - f2.lastModified();
	        if (diff > 0) {
	            return -1;
	        } else if (diff == 0) {
	            return 0;
	        } else {
	            return 1;
	        }
	    }
	}
	
	def getVersion(){
	    def mainfest =new XmlSlurper().parse(file('src/main/AndroidManifest.xml'))
	    return mainfest.getProperty('@android:versionName')
	}








Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs