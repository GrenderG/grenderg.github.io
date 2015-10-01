---
layout: post
title: "Snippet 3. Know if a device is connected to the internet"
date: 2015-07-31 17:38:00
description: Simple way to know if a device is connected to the internet (Wifi or mobile data).
categories: 
  - android
  - internet
  - snippet
permalink: "is-internet-available"
published: true
---

[spoiler]Sometimes you need or want to know if a device is connected to the internet to prevent (or to do) some action. Maybe the device is connected to some Wifi or maybe it's to mobile data.[/spoiler]
If you don't mind what type of connection it has, and you only want to check if it's connected to any type of internet you can do it easily with this code:

[spoiler]
{% highlight java %}
public static boolean isConnectedToTheInternet(Context context) {
    ConnectivityManager cm = (ConnectivityManager) 
                           context.getSystemService
                           (Context.CONNECTIVITY_SERVICE);
    NetworkInfo ni = cm.getActiveNetworkInfo();

    return ni != null && ni.isConnected() && ni.isAvailable();
}
{% endhighlight %}
[/spoiler]
- **context:** A valid context.

###What does it returns?
true if the the device is connected to the internet, false if not.
