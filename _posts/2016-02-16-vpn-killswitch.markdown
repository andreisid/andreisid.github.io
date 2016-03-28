---
author: andrei
comments: true
date: 2016-02-16 17:00:00 +0200
layout: post
slug: vpn-killswitch
title: VPN Killswitch
excerpt: "Stop all internet trafiic if VPN connection fails"
categories:
- linux
- bash
- security
- vpn
---

{% include _toc.html %}

VPN is a powerful tool that provides security and encryption for as long as it stays connected. As soon as the VPN connection is dropped, you become vulnerable against all kinds of cyber criminals and automated threats. In most cases, VPN takes a few seconds to reconnect but these few seconds may risk your online identity or data. The Internet Kill Switch is designed to remove this risk. Some VPN providers offer this feature, but not all of them.
You can set up your own killswitch system on a Linux machine by following the below steps: 




<div style="text-align:center" markdown="1">
![vpn killswitch](/images/killswitch-300x225.png)
</div>

# 1. Make sure you have ufw and iptables installed
These are usually installed by default on Debian/Redhat based systems, but if they are not please installed them.
UFW - uncomplicated firewall is actually a wrapper over iptables, making it easier to add firewall rules without knowing iptables syntax

{% highlight bash %}
apt-get install iptables
apt-get install ufw
{% endhighlight %}

# 2. Connect to your VPN

Please follow your VPN provider's intructions on connecting to the VPN. Note down the ip address for the VPN gateway as you will use it later. You can use either the command line or the Network-Manager applet for connecting to your vpn. 

**Please also make sure you use an IP for the VPN gateway when saving your OpenVPN configuration file. DNS resolution will not be allowed through the regular interface to avoid DNS leakung.** 


# 3. Set up your firewall

### check if firewall is running

{% highlight bash %}
ufw status
{% endhighlight %}

### start your firewall

{% highlight bash %}
ufw enable
{% endhighlight %}

### set default policy to deny all

{% highlight bash %}
ufw default deny outgoing
ufw default deny incoming
{% endhighlight %}

### allow traffic to your local network

The example below is for a C-class private network, that most home routers use. If you are using a different Network class please adjust it.

{% highlight bash %}
ufw allow out to 192.168.0.0/16
ufw allow in to 192.168.0.0/16
{% endhighlight %}

### allow traffic to your VPN gateway

Please replace <vpn_ip> with the ip you noted down in step 2. 

{% highlight bash %}
ufw allow out to <vpn_ip>
{% endhighlight %}

### allow traffic through your tun/tap VPN interface

Please replace <vpn_if> with the VPN interface you are using. For OpenVPN this is usually tun0, and it is created after you establish the VPN connection

{% highlight bash %}
ufw allow out on <vpn_if>
{% endhighlight %}

If you want to find out the name of the interface run ifconfig command.

# 4. Automatic script

- You can use [this script](https://github.com/andreisid/bash/blob/master/killswitch.sh) to run a killswitch with the push of a button.
