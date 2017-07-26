---
layout: post
title: "Service Intent must be explicit"
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

    public static Intent getExplicitIntent(Context context, Intent implicitIntent) {  
        // Retrieve all services that can match the given intent  
        PackageManager pm = context.getPackageManager();  
        List<ResolveInfo> resolveInfo = pm.queryIntentServices(implicitIntent, 0);  
        // Make sure only one match was found  
        if (resolveInfo == null || resolveInfo.size() != 1) {  
            return null;  
        }  
        // Get component info and create ComponentName  
        ResolveInfo serviceInfo = resolveInfo.get(0);  
        String packageName = serviceInfo.serviceInfo.packageName;  
        String className = serviceInfo.serviceInfo.name;  
        ComponentName component = new ComponentName(packageName, className);  
        // Create a new intent. Use the old one for extras and such reuse  
        Intent explicitIntent = new Intent(implicitIntent);  
        // Set the component to be explicit  
        explicitIntent.setComponent(component);  
        return explicitIntent;  
}  














Check out on the github [Fork me on github][Tomas' Yu] for more info on how to get the most out of Jekyll. That's all,thanks !

[Tomas' Yu]: https://github.com/TomasYu/blogs
[Tomas' Yu]: https://github.com/TomasYu/blogs