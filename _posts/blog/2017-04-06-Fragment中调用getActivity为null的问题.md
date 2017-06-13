---
layout: post
title: "Fragment中调用getActivity为null的问题 "
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
Fragment中调用getActivity为null的问题

> 参考博客：[http://blog.csdn.net/tablle/article/details/50420767](http://blog.csdn.net/tablle/article/details/50420767)

场景：
我们做的浏览器插件，在meizu手机上面，如果用户home返回。我们在后台运行，然后用户很长时间都没有去点击小说，当手机的内存不够用的时候，就会销毁我们的activity。但是会保存activity的Fragment。当我们从最近任务里面去点击进去的时候，activity重新创建，Fragment恢复。但是Fragment里面的getactivity 就会返回null.程序直接挂掉。

解决方法上面的博客已经说了。其实就是在你的activity里面重写：

    @Override
    protected void onSaveInstanceState(Bundle outState) {
        //重写onSaveInstanceState  不保存Fragment 防止getActivity = null
    }

这样，不调用super.onSaveInstanceState 就不会保存。

原理是什么呢？它是怎么保存Fragment的呢？
我们可以看下Fragmentactivity的源码：

    /**
     * Save all appropriate fragment state.
     */
    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        Parcelable p = mFragments.saveAllState();
        if (p != null) {
            outState.putParcelable(FRAGMENTS_TAG, p);
        }
    }

有一个关键的，FRAGMENTS_TAG。既然put的时候这个tag 去put 的，那么什么时候恢复？怎么恢复的呢？
在当前ｊａｖａ里面搜索：

可以看到Ｆｒａｇｍｅｎｔａｃｔｖｉｔｙ的onCreate里面：

    /**
     * Perform initialization of all fragments and loaders.
     */
    @SuppressWarnings("deprecation")
    @Override
    protected void onCreate(@Nullable Bundle savedInstanceState) {
        mFragments.attachHost(null /*parent*/);

        super.onCreate(savedInstanceState);

        NonConfigurationInstances nc =
                (NonConfigurationInstances) getLastNonConfigurationInstance();
        if (nc != null) {
            mFragments.restoreLoaderNonConfig(nc.loaders);
        }
        if (savedInstanceState != null) {
            Parcelable p = savedInstanceState.getParcelable(FRAGMENTS_TAG);
            mFragments.restoreAllState(p, nc != null ? nc.fragments : null);
        }
        mFragments.dispatchCreate();
    }

里面mFragments.restoreAllState(p, nc != null ? nc.fragments : null);

好了，先说到这里吧。














Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs