---
layout: post
title: "The beauty of Diffie-Hellman protocol"
date: 2015-12-02 23:59:00
description: From my point of view one of the most elegant protocols.
categories: 
  - diffie-hellman
  - protocol
permalink: "beauty-of-diffie-hellman-protocol"
published: true
---

Last day I was thinking with a friend of mine a simple way to encrypt credentials in a Rest API with Basic Auth without using SSL. We ended up studying this fascinating protocol (the way an algorithm should be used) called **"The Diffie-Hellman protocol"**.

>The Diffie-Hellman protocol (due to <a href="https://en.wikipedia.org/wiki/Whitfield_Diffie" target="_blank">Whitfield Diffie</a> and <a href="https://en.wikipedia.org/wiki/Martin_Hellman" target="_blank">Martin Hellman</a>) is a *key-agreement protocol* between two parts without previous contact, using an unsafe channel and without authentication.
>
>It's usually implemented as a way to obtain **symmetric keys** that will be used to encrypt some data (in our case the HTTP header). It's security lies in the difficulty of computing discrete logarithms in a finite body.
>
>This is a diagram showing the usage of that protocol:
>
><a href="/assets/image/diffie_hellman.png" target="_blank"><img style="display: block; margin-left: auto; margin-right: auto; background-color: white" src="/assets/image/diffie_hellman.png" width="100%" height="100%" /></a>
>***Note:** There is no need to pass p and g from A to B, it could be agreed before between the parts.*

### Explanation

For example, Alice thinks two numbers: **p** and **g**, being p a prime number and g a number usually between 2 and 5, after that she thinks a random number **a** (a < p) to do that:

A = g<sup>a</sup> mod p
{: style="font-weight:bold; font-size: 120%; text-align: center;"}

She sends **g**, **p** and **A** to Bob. *(View the note in the image footer)*.

When Bob receives the data he thinks a random number **b** (b < p) and computes that:

B = g<sup>b</sup> mod p
{: style="font-weight:bold; font-size: 120%; text-align: center;"}

Then, he sends B back to Alice.

When Alice receives the answer from Bob, she does that:

K = B<sup>a</sup> mod p
{: style="font-weight:bold; font-size: 120%; text-align: center;"}

and Bob does that:

J = A<sup>b</sup> mod p
{: style="font-weight:bold; font-size: 120%; text-align: center;"}

K and J will be equals, so there is the shared and symmetric private key.
{: style="color:red; font-weight:bold; text-align: center;"}
<hr>
I hope you've enjoyed this algorithm as much as I.



