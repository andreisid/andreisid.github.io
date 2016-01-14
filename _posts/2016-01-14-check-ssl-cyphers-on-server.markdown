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

Check installed SSL cyphers on a remote server by taking advatage of OpenSSL library
<div style="text-align:center" markdown="1">
![cypher](/images/cypher-275*183.jpg)
</div>

##1. Check against Client cyphers

The below one-line command checks the list of cyphers that are installed both on the server and on the client. 
The client is where you run the command from. Please replace www.example.com:443 with the address and port of your server

{% highlight bash %}
declare -a a=$(openssl ciphers 'ALL:eNULL' | sed -e 's/:/\n /g') && for i in ${a}; do \
result=$(echo -n | openssl s_client -cipher "$i" -connect www.example.com:443 2>&1); \
if [[ "$result" =~ ":error:" ]] ; then echo "NO - $i"; else echo "YES - $i"; fi; done;
{% endhighlight %}

##2. Check against cyphers read from file

The below command will read file.txt and will check which of these SSL cyphers are installed on the server
{% highlight bash %}
declare -a a=$(cat file.txt) && for i in ${a}; do \
result=$(echo -n | openssl s_client -cipher "$i" -connect www.example.com:443:443 2>&1); \
if [[ "$result" =~ ":error:" ]] ; then echo "NO - $i"; else echo "YES - $i"; fi; done; 
{% endhighlight %}

Please enter each cypher on a separate line in the file, like below:
{% highlight bash %}
...
ECDHE-RSA-NULL-SHA
ECDHE-ECDSA-NULL-SHA
AECDH-NULL-SHA
ECDH-RSA-NULL-SHA
ECDH-ECDSA-NULL-SHA
NULL-SHA256
...
{% endhighlight %}

You can find a shell script [here](https://github.com/andreisid/bash/blob/master/check_cypher.sh) that checks cyphers and it is very easy to use.

