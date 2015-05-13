---
author: andrei
comments: true
date: 2014-08-27 17:35:43+00:00
layout: post
slug: set-up-your-system-for-wake-on-lan
title: Set up your system for Wake on LAN
excerpt: This is a quick tutorial on how to enable WOL on your your Linux machine.
image:
  feature: feature-image-filename.jpg
  thumb: thumbnail-image.jpg 
categories:
- administration
- linux
- networking
---

{% include _toc.html %}

This is a quick tutorial on how to enable WOL on your your Linux machine.I know that cloud has been out there for a while now, there are lots of cheap or even free processing providers, but if you ever need to use your own old PC as a remote server this is something you will be interested in. Why use your PC as a server? Because it doesn't cost you anything and you can configure it any way you want. Also there is no need to leave it ON, you can always start it remotely using WOL. **Please note that wol does not work with wireless, with some exceptions(very rare).**

<div style="text-align:center" markdown="1">
![wifi_icons-black2](/images/wifi-150x150.png)
</div>

##Bios setup
If you havent already, go to your BIOS, and turn on WakeOnLAN. Be aware, not all motherboards support WOL 

##Network setup
Find your network device that you will use. Most of the times it will be eth0.

{% highlight bash %}
ifconfig

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 192.168.0.5 netmask 255.255.255.0 broadcast 192.168.0.255
inet6 eb23::fec3:3e2a:da5e:321f prefixlen 64 scopeid 0x20 ether c5:d2:fc:a2:43:45 txqueuelen 1000 (Ethernet)
RX packets 81366 bytes 76053197 (72.5 MiB)
RX errors 0 dropped 2 overruns 0 frame 0
TX packets 61715 bytes 9544754 (9.1 MiB)
TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING> mtu 65536
inet 127.0.0.1 netmask 255.0.0.0
loop txqueuelen 0 (Local Loopback)
RX packets 13086 bytes 21831329 (20.8 MiB)
RX errors 0 dropped 0 overruns 0 frame 0
TX packets 13086 bytes 21831329 (20.8 MiB)
TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0
{% endhighlight %}

##Startup script
Create a new startup script. You need to be **root** or use **sudo**.

{% highlight bash %}
vi /etc/init.d/wakeonlan

/etc/init.d/wakeonlan

#!/bin/bash
ethtool -s eth0 wol g

exit
{% endhighlight %}

##Run at boot
Make the script executable and make sure it runs at startup. Depending on your distribution there are various ways to make it run at boot. I am using update-rc.d for this example, but it could be chkconfig ...

{% highlight bash %}
chmod a+x wakeonlan
update-rc.d -f wakeonlan defaults

Adding system startup for /etc/init.d/wakeonlan ...
/etc/rc0.d/K20wakeonlan -> ../init.d/wakeonlan
/etc/rc1.d/K20wakeonlan -> ../init.d/wakeonlan
/etc/rc6.d/K20wakeonlan -> ../init.d/wakeonlan
/etc/rc2.d/S20wakeonlan -> ../init.d/wakeonlan
/etc/rc3.d/S20wakeonlan -> ../init.d/wakeonlan
/etc/rc4.d/S20wakeonlan -> ../init.d/wakeonlan
/etc/rc5.d/S20wakeonlan -> ../init.d/wakeonlan
{% endhighlight %}

##Test the script
Next run the script and make sure you don't have any errors. Make sure you note down the mac address of the network device.
You cand see it in the output of ifconfig command or ping the server from another computer and check the arp table: **arp**

{% highlight bash %}
/etc/init.d/wakeonlan
{% endhighlight %}

##Wake computer
You can now shut down the server and wake it up from another computer using wakeonlan. You can find **wakeonlan **tool on almost any distribution repository(apt-get install wakeonlan -y ...)

{% highlight bash %}
wakeonlan 01:23:45:67:89:ab
{% endhighlight %}

Please replace 01:23:45:67:89:ab with your MAC addess you have from step 5.

You might want to wake your computer from internet, in that case you need to set up some settings on your home router.

	
  * First you need to enable port forwarding and forward port 9 to your server

	
  * Second make sure you set up DynamicDNS, so you will always know your router's address. Depending on your ISP plan you might get a different IP everytime your rooter disconnects . [No-IP](http://www.noip.com/) is a very good DynDNS provider and it's also free.



