---
author: andrei
comments: true
date: 2014-09-07 16:21:26+00:00
layout: post
slug: mosh-an-alternative-to-ssh
title: Mosh, an alternative to ssh
excerpt: "This article presents Mosh, a great alternative to ssh for mobile clients, that supports intermittent connectivity."
categories:
- administration
- linux
---

{% include _toc.html %}

This article presents Mosh, a great alternative to ssh for mobile clients, that supports intermittent connectivity.
Mosh takes advantege of ssh functionality but provides better user experience in situations when clients move a lot, change ips or have a low badwidth internet connection. When the connection to the remote server is lost SSH will freeze, mosh will not!

<div style="text-align:center" markdown="1">
![mosh](/images/mosh.jpg)
</div>

Mosh is a product of MIT research and uses SSP(State Synchronization Protocol), a protocol based on UDP. In comparrison to SSH which uses TCP, this is what makes it faster.

Transmission Control Protocol - used by SSH - works under the assumption that the two endpoints it connects are fixed, and that the information exchanged must be received in the same order it was sent.  
Obviously, when it comes to mobile connections, at least one of the endpoints will be moving around, shifting between Wi-Fi, computer and cellular networks, and this is something that TCP isn't equipped to deal with effectively. Consequently, SSH sessions are easily lost.
User Datagram Protocol's stateless nature - perfect for servers answering small queries from huge numbers of clients - and its transmission model that is not concerned about receiving bytes in the right order but about synchronizing objects / receiving latest screens, makes it suitable for mobile networking.


## Why Mosh?

	
  * It stays connected even when the ip changes.

	
  * You don't need to be root to install Mosh.

	
  * If you lose connectivity the session will resume once the conectivity is restablished.

	
  * If you put your computer into sleep mode, the connection wil resume when the computer wakes up.

	
  * Mosh does not openup a new port and will not install any daemons

	
  * Mosh does not fill up network buffers, so Ctrl+C always work on runaway processes.

	
  * Mosh does not have network lag. If you connection is slow typing and editing will be instant.




##Install Mosh


 > Mosh will need to be installed on both the client and the remote server.


#### > Centos 6/RHEL


Enable epel repository first:

{% highlight bash %}
wget http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
rpm -Uvh epel-release-6-8.noarch.rpm
{% endhighlight %}

{% highlight bash %}
yum install mosh
{% endhighlight %}


#### > Ubuntu


{% highlight bash %}
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:keithw/mosh
sudo apt-get update
sudo apt-get install mosh
{% endhighlight %}

#### > Archlinux

{% highlight bash %}
yaourt -S mosh
{% endhighlight %}

##How to use Mosh

  * mosh user@ip_address . The basic sintax is the same as ssh. Example:

{% highlight bash %}
mosh root@192.168.0.100
{% endhighlight %}

	
  * if you need to change the port


{% highlight bash %}
mosh root@192.169.0.100 --ssh="ssh -p 2222"
{% endhighlight %}

For more details you can visit the MIT [official page](https://mosh.mit.edu/) of the Mosh project. Also, below you can see a presentation of Keith Winstein, the author of mosh project.

<iframe width="560" height="315" src="https://www.youtube.com/embed/XsIxNYl0oyU" frameborder="0" allowfullscreen></iframe>
