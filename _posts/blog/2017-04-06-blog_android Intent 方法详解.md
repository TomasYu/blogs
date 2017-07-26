---
layout: post
title: "android Intent 方法详解"
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

Intent intent = new Intent("com.yunos.sdk.account.ssoservice");
intent.setPackage("com.aliyun.ams.tyid");

注意：com.yunos.sdk.account.ssoservice 这里面的这个，是action 的名字。action 的名字，可不等同于真正的service的类名。

	
	 Intent intent = new Intent();
	intent.setClassName(context.getPackageName),"com.yunos.sdk.account.ssoservice");



    /**
     * Create an intent with a given action.  All other fields (data, type,
     * class) are null.  Note that the action <em>must</em> be in a
     * namespace because Intents are used globally in the system -- for
     * example the system VIEW action is android.intent.action.VIEW; an
     * application's custom action would be something like
     * com.google.app.myapp.CUSTOM_ACTION.
     *
     * @param action The Intent action, such as ACTION_VIEW.
     */
    public Intent(String action) {
        setAction(action);
    }



这样写是不行的。因为

    /**
     * Convenience for calling {@link #setComponent} with an
     * explicit application package name and class name.
     *
     * @param packageName The name of the package implementing the desired
     * component.
     * @param className The name of a class inside of the application package
     * that will be used as the component for this Intent.
     *
     * @return Returns the same Intent object, for chaining multiple calls
     * into a single statement.
     *
     * @see #setComponent
     * @see #setClass
     */
    public Intent setClassName(String packageName, String className) {
        mComponent = new ComponentName(packageName, className);
        return this;
    }

setClassName 设置的是直接的启动的类名。可以是ACitivy，也可以是service的类名。

总之，所有的东西，都要看源码。不是自己觉得。

Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs