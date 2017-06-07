---
layout: post
title: "android log "
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
anroid 打印一些东西，在你的测试包的时候，会很有用。比如说，你打出去包，给测试测试，然后有问题，你可以直接获取日志。


下面我给大家看下我的log工具类，它会打印堆栈信息，并且java 代码的连接也会打印出来，在logcat里面你可以直接点过去。

    package com.zhangyue.iReader.tools;

	import android.text.TextUtils;
	import android.util.Log;
	
	import com.chaozh.iReaderFree.BuildConfig;
	import com.zhangyue.iReader.app.PATH;
	
	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.IOException;
	import java.io.PrintStream;
	
	/**
	 * 日志类，用于统一关闭日志，或文件输出等
	 */
	public class LOG {
		private static boolean IS_SHOW_LOG = BuildConfig.isDebug;
	
		public static final String DEFAULT_MESSAGE = "execute";
		private static final String TAG_DEFAULT = "LOG";
		private static final int STACK_TRACE_INDEX = 5;
		public static final String SUFFIX = ".java";
		public static final String NULL_TIPS = "Log with null object";
		public static final String PARAM = "Param";
		public static final String NULL = "null";
		public static final int V = 0x1;
		public static final int D = 0x2;
		public static final int I = 0x3;
		public static final int W = 0x4;
		public static final int E = 0x5;
		public static final int A = 0x6;
	
		public static void D(String tag, String msg) {
		}
	
		public static void e(String tag, Throwable msg) {
			if(msg == null){
				return;
			}
			e(tag, msg.getMessage());
		}
	
		public static void e(String tag, String msg) {
			if (!IS_SHOW_LOG) {
				return;
			}
			Log.e(tag, msg);
		}
	
		public static void e(String msg) {
			e("", msg);
		}
	
		public static void d(String tag, String msg) {
			if (!IS_SHOW_LOG) {
				return;
			}
			Log.d(tag, msg);
		}
	
		public static void d(String tag) {
			d("", tag);
		}
	
		public static void I(String tag, String msg) {
			if (!IS_SHOW_LOG) {
				return;
			}
			if (tag.equalsIgnoreCase("http")) {
				I2File(msg);
			}
			Log.i(tag, msg);
		}
	
		public static void E(String tag, String msg) {
			if (!IS_SHOW_LOG) {
				return;
			}
			Log.e(tag, msg);
		}
	
		public static void setSystemOutToFile() {
			if (!IS_SHOW_LOG) {
				return;
			}
			File logFile = new File(PATH.getCacheDir() + "log.txt");
			try {
	
				if (!logFile.exists()) {
					logFile.createNewFile();
				}
				System.setOut(new PrintStream(new FileOutputStream(logFile, true)));
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	
		public static void I2File(String msg) {
			if (!IS_SHOW_LOG) {
				return;
			}
			System.out.println(msg);
		}
	
		public static void E(String tag, String msg, Throwable tr) {
			if (!IS_SHOW_LOG) {
				return;
			}
			Log.e(tag, msg, tr);
		}
	
		public static void printStackTrace() {
			if (!IS_SHOW_LOG) {
				return;
			}
			Appendable out = System.err;
			StackTraceElement[] stack = Thread.currentThread().getStackTrace();
			try {
				if (stack != null) {
					for (int i = 0; i < stack.length; i++) {
						out.append("");
						out.append("\tat ");
						out.append(stack[i].toString());
						out.append("\n");
					}
				}
			} catch (Exception e) {
				// TODO: handle exception
			}
		}
	
	
		public static void i() {
			printLog(I, null, DEFAULT_MESSAGE);
		}
	
		public static void i(Object msg) {
			printLog(I, null, msg);
		}
	
		public static void i(String tag, Object... objects) {
			printLog(I, tag, objects);
		}
	
		private static void printLog(int type, String tagStr, Object... objects) {
			if (!IS_SHOW_LOG) {
				return;
			}
			String[] contents = wrapperContent(tagStr, objects);
			String tag = contents[0];
			String msg = contents[1];
			String headString = contents[2];
			switch (type) {
				case V:
				case D:
				case I:
				case W:
				case E:
				case A:
					printDefault(type, tag, headString + msg);
					break;
			}
		}
	
		private static String[] wrapperContent(String tagStr, Object... objects) {
			StackTraceElement[] stackTrace = Thread.currentThread().getStackTrace();
			StackTraceElement targetElement = stackTrace[STACK_TRACE_INDEX];
			String className = targetElement.getClassName();
			String[] classNameInfo = className.split("\\.");
			if (classNameInfo.length > 0) {
				className = classNameInfo[classNameInfo.length - 1] + SUFFIX;
			}
			String methodName = targetElement.getMethodName();
			int lineNumber = targetElement.getLineNumber();
			if (lineNumber < 0) {
				lineNumber = 0;
			}
			String methodNameShort = methodName.substring(0, 1).toUpperCase() + methodName.substring(1);
			String tag = (tagStr == null ? className : tagStr);
			if (TextUtils.isEmpty(tag)) {
				tag = TAG_DEFAULT;
			}
			String msg = (objects == null) ? NULL_TIPS : getObjectsString(objects);
			String headString = "[ (" + className + ":" + lineNumber + ")#" + methodNameShort + " ] ";
	
			return new String[]{tag, msg, headString};
		}
	
		private static String getObjectsString(Object... objects) {
			if (objects.length > 1) {
				StringBuilder stringBuilder = new StringBuilder();
				stringBuilder.append("\n");
				for (int i = 0; i < objects.length; i++) {
					Object object = objects[i];
					if (object == null) {
						stringBuilder.append(PARAM).append("[").append(i).append("]").append(" = ").append(NULL).append("\n");
					} else {
						stringBuilder.append(PARAM).append("[").append(i).append("]").append(" = ").append(object.toString()).append("\n");
					}
				}
				return stringBuilder.toString();
			} else {
				Object object = objects[0];
				return object == null ? NULL : object.toString();
			}
		}
	
		public static void printDefault(int type, String tag, String msg) {
			int index = 0;
			int maxLength = 4000;
			int countOfSub = msg.length() / maxLength;
			if (countOfSub > 0) {
				for (int i = 0; i < countOfSub; i++) {
					String sub = msg.substring(index, index + maxLength);
					printSub(type, tag, sub);
					index += maxLength;
				}
				printSub(type, tag, msg.substring(index, msg.length()));
			} else {
				printSub(type, tag, msg);
			}
		}
	
		private static void printSub(int type, String tag, String sub) {
			switch (type) {
				case V:
					Log.v(tag, sub);
					break;
				case D:
					Log.d(tag, sub);
					break;
				case I:
					Log.i(tag, sub);
					break;
				case W:
					Log.w(tag, sub);
					break;
				case E:
					Log.e(tag, sub);
					break;
				case A:
					Log.wtf(tag, sub);
					break;
			}
		}
	}


## LOG.i("initAPP",startTime);  ##
这样，就会把类的链接打印在logcat里面，可以直接点到java类里面。
原理是：
## 只要你的log是 Log.d("APP", "(APP.java:5)"); ## 

只要你的log里面有"(APP.java:4)" 小括号，类名，行号，打印出来都是可以点进去的连接。














Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs