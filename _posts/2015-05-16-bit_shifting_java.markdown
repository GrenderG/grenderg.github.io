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