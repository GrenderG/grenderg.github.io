---
layout: post
title: "Snippet #2. Know if a service is running"
date: 2015-05-16 17:31:00
description: Simple way to know if a service is running in Android.
categories: [programming, snippets, android]
permalink: "blog/is-service-running"
published: true
---

The second snippet is... -drum roll- How to know if a service is running in Android!

Check this:
{% highlight java %}
public boolean isMyServiceRunning(Class<?> serviceClass) {
    ActivityManager manager = (ActivityManager) 
                            getSystemService(Context.ACTIVITY_SERVICE);
    for (ActivityManager.RunningServiceInfo service : 
        manager.getRunningServices(Integer.MAX_VALUE)) {
        if (serviceClass.getName()
            .equals(service.service.getClassName())) {
            return true;
        }
    }
    return false;
}
{% endhighlight %}

- **serviceClass:** The class name of the service that you want to check.

### What does it returns?
true if the service is running, false if not.
