---
layout: post
title: "Programming challenge #2. Pizza pieces"
date: 2015-10-05 19:00:03
description: Receiving unexpected guests.
categories: [programming, challenges]
permalink: "blog/pizza-pieces"
published: true
---

Today I'll continue this series with a problem if you are astute you will solve it in less than 5 minutes. *Don't forget triangles!*

## The problem
In her trip to Italy, Elizabeth Gilbert made it her duty to eat perfect pizza. One day, she ordered one for dinner. And then some Italian friends appeared at her room. The problem is that there were many people who ask for a piece of pizza at that moment. And she had a knife that only cuts straight.

**This is what she wants:**

> Given a number K (K <= 45000), help her get the maximum of pieces possible (not necessarily of equal size) with K cuts. 
> 
> If K is a negative number, the result must be -1.

## Examples
{% highlight java %}
Pizza.maxPizza(0) == 1
{% endhighlight %}
{% highlight java %}
Pizza.maxPizza(1) == 2
{% endhighlight %}
{% highlight java %}
Pizza.maxPizza(3) == 7
{% endhighlight %}

## The solution
[spoiler]
{% highlight java %}
public class Pizza {
  public static int maxPizza(int k) {
    return k < 0 || k >= 45000 ? -1 : k * (k + 1) / 2 + 1;
  }
}
{% endhighlight %}
[/spoiler]

Good luck and have fun!
