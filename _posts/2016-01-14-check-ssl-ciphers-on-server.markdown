---
author: andrei
comments: true
date: 2016-01-14 15:01:00+00:00
layout: post
slug: check-ssl-ciphers-on-server 
title: Check SSL ciphers on server
excerpt: "Check SSL ciphers on server"
categories:
- ssl
- linux
- security
- bash
---

{% include _toc.html %}

 When a TLS connection is established, a handshaking, known as the TLS Handshake Protocol, occurs. Within this handshake, a client hello (ClientHello) and a server hello (ServerHello) message are passed. First, the client sends a cipher suite list, a list of the cipher suites that it supports, in order of preference. Then the server replies with the cipher suite that it has selected from the client cipher suite list. In order to test which TLS ciphers that a server supports an SSL/TLS Scanner may be used. - Wiki

 This post shows how to check installed SSL ciphers on a remote server by taking advatage of OpenSSL library.
<div style="text-align:center" markdown="1">
![cipher](/images/cipher-275x183.jpg)
</div>

# 1. Check against Client ciphers

 The below one-line command checks the list of ciphers that are installed both on the server and the client. 
The client is where you run the command from. 

- First create a list of all SSL ciphers supported by the client 
- For every cipher found, check if it is installed on the server
- Please replace www.example.com:443 with the address and port of your server

{% highlight bash %}
declare -a a=$(openssl ciphers 'ALL:eNULL' | sed -e 's/:/\n /g') && for i in ${a}; do \
result=$(echo -n | openssl s_client -cipher "$i" -connect www.example.com:443 2>&1); \
if [[ "$result" =~ ":error:" ]] ; then echo "NO - $i"; else echo "YES - $i"; fi; done;
{% endhighlight %}

- Output semnification: NO means that the cipher is not found on the server, YES means the cipher is supported by the server

# 2. Check against ciphers read from file

The below command will read file.txt and will check which of the SSL ciphers from that file are installed on the server.

- First create a file.txt coontaining all the ciphers you would like to check against the server.
- Please enter each cipher on a separate line in the file, like below:

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

- The script will output YES if the cipher is found on the server, and NO if not
   
{% highlight bash %}
declare -a a=$(cat file.txt) && for i in ${a}; do \
result=$(echo -n | openssl s_client -cipher "$i" -connect www.example.com:443:443 2>&1); \
if [[ "$result" =~ ":error:" ]] ; then echo "NO - $i"; else echo "YES - $i"; fi; done; 
{% endhighlight %}


You can download a shell script [here](https://github.com/andreisid/bash/blob/master/check_cipher.sh) that checks ciphers and it is very easy to use.

