---
author: andrei
comments: true
date: 2015-11-13 09:21:14+00:00
layout: post
slug: add-a-certificate-chain-and-private-key-to-a-jks-keystore 
title: Add a certificate chain and private key to a jks keystore
excerpt: "Add a certificate chain and private key to a jks keystore"
categories:
- ssl
- linux
---

{% include _toc.html %}
Not long time ago i needed to change a certificate that expired on a tomcat webserver that used a 2-way-ssl connection type to communicate to another server. I received the new certificate from my privider in a .pem form but i needed to add it to my java keystore. The problem was that I would only add the certificate and the chain (but no private key) to my keystore. By doing so I have created a truststore so my webserver did not serve a propper certificare. After some digging, I found a way to make my truststore a keystore.


<div style="text-align:center" markdown="1">
![ssl certificate](/images/ssl-certificate-220x220.png)
</div>


I will describe below the steps to create a valid java keystore.


## 1. Split your .pem file so you have a different file for the certificate, PK, Root certificate and intermidiate certificates
In my case this resulted in 5 files:

{% highlight bash %}
-leaf.pem -> leaf certificate
-leaf.key -> Private key of my server certificare 
-root.pem -> Root entry in the certificate chain
-inter1.pem -> First intermidiate certificate in the chain
-inter2.pem -> Second intermidiate certificate in the chain
{% endhighlight %}

You might not have the root and intermidiate certificates, as they might be specified in a separate trustore. If thats the case please skip steps 2/3/4

## 2. Import Root and intermidiate certificates to your keystore:
You will be asked for a passkey to protect your new keystore. Please enter twice your desired key.Also confirm  you want to add the cert to your keystore by typing "yes" and ENTER:
{% highlight bash %}
keytool -import -trustcacerts -alias root -file root.pem -keystore keystore.jks

    Enter keystore password:  
    Re-enter new password:
    
    Trust this certificate? [no]:

{% endhighlight %}

Follow the same steps for adding the intermidiate certificates(if needed):

{% highlight bash %}
keytool -import -trustcacerts -alias intermidiate1 -file inter1.pem -keystore keystore.jks
    -Enter keystore password:  
    -Trust this certificate? [no]:

keytool -import -trustcacerts -alias intermidiate2 -file inter2.pem -keystore keystore.jks
    -Enter keystore password:
    -Trust this certificate? [no]:

{% endhighlight %}


## 3. Create a .p12 keystore containing your leaf certificate and private key
You will need to specify your PK password. this is usually provided by your certificate provider and might not be set.
Also you will need to enter and confirm your .p12 keystore password. 

{% highlight bash %}

openssl pkcs12 -export -name <server alias name> -in leaf.pem -inkey leaf.key -out keystore.p12

    -Enter pass phrase for leaf.key:
    
    -Enter Export Password:
    -Verifying - Enter Export Password:
{% endhighlight %}

Replace <server alias name> with the name that your certificate will be used inside your keystore. Usualy the name of the certificate is set to be the domain name of your server.
To verify that your .p12 keystore contains your certificate and PK run the below commands. You will be prompted for your keystore and privatekey passwords.

{% highlight bash %}
openssl pkcs12 -info -in keystore.p12

    -Enter Import Password:
    
    -Enter PEM pass phrase:
    -Verifying - Enter PEM pass phrase:
{% endhighlight %}

## 4. Import your .p12 content to your .jks keystore

You will be propted for the .p12 and .jks passwords.

{% highlight bash %}

keytool -importkeystore -destkeystore keystore.jks -srckeystore keystore.p12 -srcstoretype pkcs12 -alias <server alias name>
    -Enter destination keystore password:  
    -Enter source keystore password:  
{% endhighlight %}

## 5. Verify the content of yout jks keystore

{% highlight bash %}

keytool -list -v -keystore keystore.jks

{% endhighlight %}

In case of everything worked well you should see 4 entries in your truststore.
3 of the woud be of trustedCertEntry type and one will be PrivateKeyEntry.

{% highlight bash %}
...
Entry type: PrivateKeyEntry
...
Entry type: trustedCertEntry
...
Entry type: trustedCertEntry
...
Entry type: trustedCertEntry
{% endhighlight %}

