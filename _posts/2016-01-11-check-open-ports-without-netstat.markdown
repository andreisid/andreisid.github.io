---
author: andrei
comments: true
date: 2016-01-11 15:01:00+00:00
layout: post
slug: check-open-ports-without-netstat 
title: Check open ports without netstat
excerpt: "Cool command to verify open ports without netstat"
categories:
- ssl
- linux
- security
- certificates
---

{% include _toc.html %}

## Command

Note: The below command shows ALL open ports on a Linux machine, not only ports that are awaiting connections(LISTENING).
This includes random high-number souce ports assigned locally when a conection is established with a remote server(ESTABLISHED). 

{% highlight bash %}
declare -a array=($(tail -n +2 /proc/net/tcp|cut -d":" -f"3"|cut -d" " -f"1"))\
&& for port in ${array[@]}; do echo $((0x$port)); done
{% endhighlight %}



