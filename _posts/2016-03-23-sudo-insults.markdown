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

There is a list of insults preinstalled on any linux system. You can get the os to insult you when misstyping the sudo password.
In order to enable the feature add the following in sudoers file

{% highlight bash %}
sudo visudo

...
Default    insults
...

{% endhighlight %}

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
