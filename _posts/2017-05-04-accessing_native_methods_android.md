---
layout: post
title: "Accessing the native methods of a decompiled Android app"
date: 2017-05-04 01:45:00
description: How to access the native methods of a decompiled Android application.
category: [programming, android, pentesting]
permalink: "blog/accessing_native_methods_android"
published: true
---

Using native code through JNI is a very common practice in Android development, in fact it's common to store secret keys inside a native library in order
to keep them a bit more safe. As I said that practice just difficults the process of getting access to those secrets. Here you will learn how to reverse engineer an
APK and mimic the original project structure in order to call your victim's app native methods.

## Getting the apk

I'm assuming you already have the apk, but if not you can use online services like [APKPure](https://apkpure.com/).

Alternatively you can download and install the app in your device, then get the location of the apk through adb.

First of all you need to know where the apk is stored.

```
adb shell pm path com.niceguys.someapp
```

Then just use adb again to pull the apk to your computer.

```
adb pull /data/app/org.niceguys.repost-1/base.apk /destination/folder
```

## Decompiling the apk

You need to decompile the apk for two main reasons. First you wanna get `.so` files in order to use them; second you wanna find where are native funcion calls taking
place in order to know methods names and mimic later the project structure.

### Online

A very easy way to decompile an apk is by using [this web](http://www.javadecompilers.com/apk). Just upload the apk, wait and you will be able to download a zip file
containing the decompiled apk.

### Using some tools

If you don't want to use that web or you don't have access to Internet there is a tool called **JADX** which you can download from [here](https://github.com/skylot/jadx)
and follow the instructions on its README file in order to view the decompiled code. I'm not going to explain how to use it here since it's very good explained in it's
GitHub repo and I usually use the online way just for convenience.

### Getting the native libraries

Once you have the decompiled apk you will find a folder called **lib** in the root folder, rename it to **jniLibs** and place it anywhere, you will use it later.

### Finding native method calls

I usually use grep in order to find where the calls are taking place, for example you can search for `System.loadLibrary` calls.

```
grep -rnw /path/to/decompiled/apk -e "System.loadLibrary"
```

or finding directly the methods by searching for `native` keyword.

```
grep -rnw /path/to/decompiled/apk -e "native"
```

### Mimicking project structure

Okay, so you already know where the method calls are taking place, take a look to the project structure.

```
org
└── niceguys
    └── repost
        ├── apackage
        │   └── CoolClass.java
        └── MainActivity.java
```

Imagine the method call is taking place inside `org.niceguys.repost.apackage.CoolClass.java`.

{% highlight java %}
public class CoolClass {
    static {
        System.loadLibrary("native-lib");
    }

    public static native String getSuperSecureKey();
}
{% endhighlight %}

You don't need to know this, but the native method would be something like this.

{% highlight c %}
#include <jni.h>
#include <string>

extern "C"
JNIEXPORT jstring JNICALL
Java_org_niceguys_repost_apackage_CoolClass_getSuperSecureKey(
        JNIEnv *env,
        jobject) {
    std::string super_secure_key = "1234ABCD";
    return env->NewStringUTF(super_secure_key.c_str());
}
{% endhighlight %}

You need to create (for example) an Android Studio project maintaining that structure. So the package name would be
`org.niceguys.repost`. 

Copy the folder containg the `.so` files under your `/src/main` directory.

```
app
└── src
    └── main
        └── jniLibs
```

After that, create a package named `apackage` and inside, a class called `CoolClass.java`.

### Calling the native methods

At this point you have mimicked the project structure and added your victim's libraries inside your fake project.

Load the native library inside `CoolClass.java` and then copy the native methods as in the original file (take a look to the code
above).

Congratulations, now you are free to use `CoolClass.getSuperSecureKey()` wherever you want (for example, in your MainActivity class)
and print the result to the LogCat.

{% highlight java %}
Log.d("API_KEY", CoolClass.getSuperSecureKey());
{% endhighlight %}

---

Keeping keys securely in an application is an almost impossible task, because anyone with sufficient knowledge and time will be able to find them. 
Therefore, it is not uncommon for developers to try to hide them in very diverse and curious ways.
