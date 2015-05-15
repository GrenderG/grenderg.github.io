---
layout: post
title: "Snippet .1 Overlapping circles positions"
date: 2015-05-15 19:12:00
description: Get the overlapping circles positions the easy-way.
categories: 
  - android
  - java
  - snippet
permalink: "overlapping-circles"
published: true
---

Let our snippet section begun with some fresh Java (Android focused) code here! If you want to get the position of n-overlapping circles position like so:

![snippet1](/assets/image/snippet1.png)

Check this:
{% highlight java %}
public int[] getCirclePositions(int radius, int viewWidth, int items){
	int[] positions = new int[items];
	int portionSize = viewWidth / (items + 1);
 
	for (int i = 0; i < positions.length; i++){
		positions[i] = (portionSize*(i+1)) - radius;
	}
 
	return positions;
}
{% endhighlight %}

**radius:** Radius of each circle.
**viewWidth:** Total width of the view where circles will be placed.
**items:** Total of circles.

###What does it returns?
An int array containing the starting position where each circle should be placed.
