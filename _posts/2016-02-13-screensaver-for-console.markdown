---
author: andrei
comments: true
date: 2016-02-13 17:00:00+00:00
layout: post
slug: screensaver-for-console
title: Screensaver for Console
excerpt: "Set up a nice looking screensaver for your Linux Console"
categories:
- linux
- bash
- fun
---

{% include _toc.html %}

Having a screensaver on my Linux console souded like a fun ideea. After some investigation I found an easy way to have a matrix-like screensaver, and it looks pretty awesome.
You just need to setup screen utility and the cmatrix screensaver. See below details for installation steps.


<div style="text-align:center" markdown="1">
![matrix teminal screensaver](/images/matrix-500x257.png)
</div>

# 1. Install screen utility and screensavers

Depending on you distributin check and install the following packages: screen, cmatrix. I am installing them on an ArchLinux instance, but the packages can be found on most Linux distributions.

{% highlight bash %}
yaourt -S screen cmatrix
{% endhighlight %}

# 2. Test your cmatrix screensaver in console

- By using the 's' option you specify to run the utility as a screensaver. It will end when pressing a key
- 'b' option tells cmatrix to use Bold characters
- There are more options available, you can check them in the man pages. 'C' option for example  sets the color.

{% highlight bash %}
cmatrix -sb
{% endhighlight %}

# 3. Start screen when opening a console

Append the following to the end of your bashrc file

{% highlight bash %}
vi /etc/bash.bashrc
...

[[ $TERM != "screen" ]] && exec screen -q
{% endhighlight %}

# 4. Set up screensaver to start after IDLE time

After setting up screen utility /etc/screenrc has been created for you. Add the following options to /etc/screenrc or ~/.screenrc :

{% highlight bash %}
blankerprg cmatrix -ab -u2
idle 60 blanker

{% endhighlight %}

- The first line starts cmatrix when blanker is called
- The second line calls blanker after 60 seconds of idle time. You can use other value for idle time
- You can use other screensavers aswell. You can find some examples [here](http://termsaver.brunobraga.net/) and [here](http://www.robobunny.com/projects/asciiquarium/html/)
