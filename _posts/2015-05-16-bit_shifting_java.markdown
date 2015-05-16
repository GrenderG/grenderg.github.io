---
layout: post
title: "Let's talk about bit shifting in Java"
date: 2015-05-16 12:56:00
description: Today you will learn what is bit shifting focused in Java programming language.
categories: 
  - bitshifting
  - java
permalink: "bit-shifting-java"
published: true
---
>In digital computer programming, a bitwise operation operates on one or more bit patterns or binary numerals at the level of their individual bits. It is a fast, primitive action directly supported by the processor, and is used to manipulate values for comparisons and calculations.
>
>On simple low-cost processors, typically, bitwise operations are substantially faster than division, several times faster than multiplication, and sometimes significantly faster than addition.

Bit shifting operations are, indeed, bitwise operations because they treat every value as a series of bits instead of a numerical quantity. With these operations you can "move" bits to the reft or right.

##What the f*** are you talking about?
Well, it is said that in software, exists 10% of code that is running 90% of the time. So, what if in that 10% of code you are doing huge operations repeteadly? Maybe you want to consume less resources, so instead of doing operations with common "/, *" I recommend you to use bit shifting operations. I will tell you basic usages and how to implement it in Java.

##Usages and explanation
Imagine that you want to divide 128 by 32. You usually will do it like so:
{% highlight java %}
int div = 128 / 32;
{% endhighlight %}
It's working, but if you want to optimize it, just use bit shifting:
{% highlight java %}
int bShiftDiv = 128 >> 5;
{% endhighlight %}

Magic? Nah, you can try it, both operations will return the same: 4.

###What just happened?
Okay, 128 in binary is 100000000.
<table>
    <tr>
        <td>128</td>
        <td>64</td>
        <td>32</td>
        <td>16</td>
        <td>8</td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>0</td>
    </tr>
        <tr>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
    </tr>
</table>
If you bit shift it to the right (division, >>) 5 positions... What number do you get in binary? 1000, and 1000 is... 4!
<table>
    <tr>
        <td>0 -></td>
        <td>1 -></td>
        <td>2 -></td>
        <td>3 -></td>
        <td>4 -></td>
        <td>5</td>
    </tr>
    <tr>
        <td>128</td>
        <td>64</td>
        <td>32</td>
        <td>16</td>
        <td>8</td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>0</td>
    </tr>
    <tr>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
    </tr>
</table>

As you see, the basics are so easy to understand. You can do the same if you want to multiply values, instead of shifting bits to the right, you just have to shift them to the left (<<).
{% highlight java %}
int bShiftDiv = 4 << 5;
{% endhighlight %}
That operation will return 128.
<table>
    <tr>
        <td>5</td>
        <td><- 4</td>
        <td><- 3</td>
        <td><- 2</td>
        <td><- 1</td>
        <td><- 0</td>
    </tr>
    <tr>
        <td>128</td>
        <td>64</td>
        <td>32</td>
        <td>16</td>
        <td>8</td>
        <td>4</td>
        <td>2</td>
        <td>1</td>
        <td>0</td>
    </tr>
    <tr>
        <td>1</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
        <td>0</td>
    </tr>
</table>

###Conclusion
Hope you have learn a lot reading this and I encourage you to use bit shifting (you can do it in almost all languages and it's the same!) in order to decrease resource consumption in your software.

