---
author: andrei
comments: true
date: 2014-08-27 08:01:54+00:00
layout: post
slug: using-ssh-proxycommand
title: 'Using  Ssh ProxyCommand '
excerpt: "shh ProxyCommand for tunneling all ssh connections"
categories:
- administration
- linux
tags:
- linux
- proxy
- ssh
---

{% include _toc.html %}

Sometimes I needed to login to servers that are not directly accesible from internet. So i needed to first login to a bastion server and from that bastion server to ssh into the target server. The solution described in this article takes advantage of shh ProxyCommand option and ControlMaster for keeping one tunnel for all ssh connections.

<div style="text-align:center" markdown="1">
![ssh](/images/ssh-150x150.png)
</div>

{% highlight bash %}
ssh user@bastion
ssh user@server
{% endhighlight %}

## Problem
After a while i got sick of running 2 commands every time and enter my password twice.As a security best practice bastion servers usually use a 2-way-authentication method. That was my case also, so imagine every time i had  to generate a one-time password on my phone, ssh to the bastion server using that+PIN and from there ssh to the target server using my user's password. Doesn't sound much work, but when you have to do this simultaneously to 20 servers it becomes very annoying.

## Solution

**How It works:**

{% highlight bash %}
+---------+                +--------+
| bastion | ----netcat---> | server |
+---------+                +--------+
{% endhighlight %}
   
{% highlight bash %} 
+-------+                  +--------------+                +--------+
|  PC   |                  | bastion      |                | server |
|       | =============ssh=over=netcat=tunnel============> |        |
+-------+                  +--------------+                +--------+
{% endhighlight %}
 

So this is what happens behind the scenes:

1)ssc connection is established between the **PC** and the **bastion**
2) A netcat tunnel is created between the **bastion** and the** server**
3)ssh will use the already created tunnel to login to the **server**

In order to use the bastion server as a proxy you need to do the following changes on the **PC**:

{% highlight bash %}
PC$ vi ~/.ssh/config

#~/.ssh/config

Host server.mydomain.com
User myusername
ForwardAgent yes
ProxyCommand ssh bastion.mydomain.com nc %h %p

Host bastion.mydomain.com
ControlMaster auto
ControlPath /tmp/%r@%h:%p
{% endhighlight %}



	
  * In the first Host declaration you specify the ssh username, set the ForwardAgent to yes and then the ProxyCommand.The ProxyCommand statement means: connect to the bastion server and from there start a connection to **%h** (host) on port **%p **(port). %h and %p are parameters supplied to ssh command, in this case %h will be server.mydomain.com and port will be the implicit value of 22.

	
  *  The second Host declaration help using the same **PC to bastion** connection for all ssh sessions to server.mydomain.com. This is from the manual of ssh**_ "Control Master: Enables the sharing of multiple sessions over a single network connection."_**_ _ Control path is the path of the opened socket for the shared connections. The above settings will create a socket file /tmp/myusername@bastion.mydomain.com:22, and all ssh sessions to server1.mydomain.com will use this socket to connect to the tunnel.


So if you open up a ssh session to the bastion server, all the following sessions to the server will go throught the allready set up tunnel, and you will only be prompted for the server's password



[Here](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man5/ssh_config.5) you can find the manual page for a complet set of ssh config options.

