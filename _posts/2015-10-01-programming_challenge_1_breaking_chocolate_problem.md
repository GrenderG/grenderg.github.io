---
layout: post
title: "Programming challenge #1. Breaking chocolate problem"
date: 2015-10-01 18:20:00
description: Will you be able to help Bill breaking his chocolate bar?
categories: 
  - programming-challenge-1
  - java
permalink: "breaking-chocolate-problem"
published: true
---

I have been having a lot of fun with [Codewars](http://www.codewars.com/r/sXy0Vg) so I've decided to create a **"Programming challenge"** section to publish some coding challenges and their solutions (of course in a spoiler, don't be naughty!) in order to check if you're right when you are done. Usually I will solve them using Java or Python, but you can use what you want. Let's start!

##The problem
Bill is a fat and a lazy guy who loves eating chocolate, but due to his lazyness he wants to break the chocolate bar with the minimum number of breaks needed.

**This is what he wants:**

> Your task is to split the chocolate bar of given dimension n x m into small squares. Each square is of size 1x1 and unbreakable. Implement a function that will return minimum number of breaks needed.
> 
> For example if you are given a chocolate bar of size 2 x 1 you can split it to single squares in just one break, but for size 3 x 1 you must do two breaks.
> 
> If input data is invalid you should return 0 (as in no breaks are needed if we do not have any chocolate to split). Input will always be a non-negative integer.

##The solution
[spoiler]
{% highlight java %}
public class Chocolate {
  public static int breakChocolate(int n, int m) {
    return (n == 0 || m == 0)?0:(n * m - 1);
  }
}
{% endhighlight %}
[/spoiler]

Are you ready to help Bill?
