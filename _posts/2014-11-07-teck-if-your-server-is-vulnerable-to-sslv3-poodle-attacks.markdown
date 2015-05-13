---
author: andrei
comments: true
date: 2014-11-07 09:21:14+00:00
layout: post
slug: teck-if-your-server-is-vulnerable-to-sslv3-poodle-attacks
title: Is your server vulnerable to SSLv3 Poodle attacks?
excerpt: "POODLE stands for Padding Oracle On Downgraded Legacy Encryption. This vulnerability allows a man-in-the-middle attacker to decrypt ciphertext using a padding oracle side-channel attack. More details are available in the upstream OpenSSL advisory."
categories:
- hack
- linux
---

{% include _toc.html %}
POODLE stands for Padding Oracle On Downgraded Legacy Encryption. This vulnerability allows a man-in-the-middle attacker to decrypt ciphertext using a padding oracle side-channel attack. More details are available in the upstream OpenSSL advisory.
POODLE affects older standards of encryption, specifically Secure Socket Layer (SSL) version 3. It does not affect the newer encryption mechanism known as Transport Layer Security (TLS).

<div style="text-align:center" markdown="1">
![poodle](/images/poodle-300x286.jpg)
</div>


In order to test if your servers are vulnerable to SSLv3 Poodle attacks please see the below commands:


##1-way-ssl


{% highlight bash %}
curl -v3 -X HEAD https://yourserver.domain
....
{% endhighlight %}

OR

{% highlight bash %}
openssl s_client -connect yourserver.domain:443 -ssl3
{% endhighlight %}


You should se some relevant output like: "SSL peer handshake failed" if you cannot negociate a connection with your server by using SSLv3 protocol. In this case, congratulations! you are not vulnerable!
On the other hand, if you see huge chuck of data on the output, or something like: "SSL handshake has read 8349 bytes and written 2375 bytes" that means that you are vulnerable.


##2-way-ssl


{% highlight bash %}
openssl s_client -connect yourserver.domain:443 -ssl3 -cert cert.pem -key cert.key
{% endhighlight %}

Again, you should see some handshake faliure messages if your server is not vulnerable. In order to make sure your server is working fine using TLSv1.X use the following

{% highlight bash %}
openssl s_client -connect yourserver.domain:443 -tls1 -cert cert.pem -key cert.key
{% endhighlight %}

You should see some big output containg certificate exchange and a handshake success



##How to fix?


Depending on what webserver you ar running, you need to disable the use of SSLv3.
Please follow the RedHat reccomended solution [here](https://access.redhat.com/solutions/1232233)
