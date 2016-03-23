---
author: andrei
comments: true
date: 2016-03-23 17:00:00 +0200
layout: post
slug: sudo-insults
title: SUDO insults
excerpt: "Get insulted if you type the sudo password wrong :)"
categories:
- linux
- bash
- fun

---

{% include _toc.html %}


<div style="text-align:center" markdown="1">
![matrix](/images/insults-225x225.jpg)
</div>

There is a list of insults preinstalled on any linux system. You can get the os to insult you when misstyping the sudo password.
In order to enable the feature edit the sudoers file as below 

# 1. sudo visudo 

{% highlight bash %}

...
Default    insults
...

{% endhighlight %}

# 2. sudo su 
Now, open a new terminal window and  try "sudo su ", followed by a wrong password.
You will see something like this:

{% highlight bash %}

[me:/tmp]$ sudo su 
[sudo] password for me: 
You silly, twisted boy you.
[sudo] password for me: 
No soap, honkie-lips.
[sudo] password for me: 
You type like I drive.
sudo: 3 incorrect password attempts

{% endhighlight %}

have fun :)
