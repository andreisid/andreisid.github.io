---
author: andrei
comments: true
date: 2016-01-14 15:01:00+00:00
layout: post
slug: check-ssl-cyphers-on-server 
title: Check SSL cyphers on server
excerpt: "Check SSL cyphers on server"
categories:
- ssl
- linux
- security
- bash
---

{% include _toc.html %}

<div style="text-align:center" markdown="1">
![cypher](/images/cypher-275*183.jpg)
</div>


#
{% highlight bash %}
declare -a array=($(tail -n +2 /proc/net/tcp | cut -d":" -f"3"|cut -d" " -f"1")) && \ 
for port in ${array[@]}; do echo $((0x$port)); done
{% endhighlight %}



