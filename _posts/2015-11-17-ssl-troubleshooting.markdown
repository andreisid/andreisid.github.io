---
author: andrei
comments: true
date: 2015-11-17 16:17:00+00:00
layout: post
slug: ssl-troubleshooting 
title: SSL troubleshooting
excerpt: "ssl-troubleshooting"
categories:
- ssl
- linux
- security
- certificates
---

{% include _toc.html %}
See below a list of commands, commonly used when working with certificates and troubleshooting SSL.

<div style="text-align:center" markdown="1">
![poodle](/images/digital-certificate-300x250.png)
</div>


# Read certificates

### 1. Read a PEM certificate

{% highlight bash %}
openssl x509 -in certificate.pem -text -noout
{% endhighlight %}

### 2. Read a PFX/P12 certificate

{% highlight bash %}
keytool -list -v -keystore <keystore.pfx> -storetype PKCS12 -storepass <pass>
openssl pkcs12 -info -in <keyStore.pfx>
{% endhighlight %}


### 3. Read a JKS Keystore

{% highlight bash %}
keytool -list -v -keystore <keystore.jks> -storetype JKS -storepass <pass>
{% endhighlight %}

Note: depending on the "Entry type" field of each entry (PrivateKeyEntry or trustedCertEntry) you can deduce if your JKS is a keystore or truststore. 
A truststore would only contain trustedCertEntry entries


# Convert certificates

### 4.Convert a JKS into a PKCS12 (all aliases)

{% highlight bash %}
keytool -importkeystore -srckeystore <keystore.jks> -srcstoretype JKS -deststoretype PKCS12 -destkeystore <keystore.p12>
{% endhighlight %}

### 5.Converting a JKS into a PKCS12 (only one alias)

{% highlight bash %}
keytool -importkeystore -srckeystore <keystore.jks> -destkeystore <keystore.p12> -srcstoretype JKS -deststoretype PKCS12 -srcstorepass 
<pass> -deststorepass <pass> -srcalias <alias> -destalias <alias> -srckeypass <keypass> -destkeypass <keypass> -noprompt
{% endhighlight %}

### 6.Convert a PKCS12 into a PEM (with password)

{% highlight bash %}
openssl pkcs12 -in <cert.pfx> -out <cert.pem>
{% endhighlight %}

Note: You can add -nocerts to only output the private key or add -nokeys to only output the certificates.

### 7.Convert a PEM certificate and private key into a PKCS12

{% highlight bash %}
openssl pkcs12 -export -out <certificate.pfx> -inkey <privateKey.key> -in <certificate.crt> -certfile <CACert.crt>
{% endhighlight %}


### 8.Convert PEM to DER
{% highlight bash %}
openssl x509 -in <cert.pem> -inform PEM -out <cert.der> -outform DER
{% endhighlight %}

### 9.Convert DER to DER
{% highlight bash %}
openssl x509 -inform der -in <certificate.cer> -out certificate.pem
{% endhighlight %}

# Troubleshooting

### 10.Read a cert from a remote host

{% highlight bash %}
echo QUIT | openssl s_client -connect <domain.com:443>
{% endhighlight %}

### 11.Simulate a client

{% highlight bash %}
openssl s_client -connect <domain.com:443> -showcerts -state -msg
openssl s_client -connect <domain.com:443> -showcerts -state -msg -CAfile <truststore.pem>
{% endhighlight %}

### 12.Simulate a server clientAuth=False

{% highlight bash %}
openssl s_server -accept 443 -cert <server-cert.pem> -pass pass:<pass> -WWW -state -msg -tlsextdebug
{% endhighlight %}

### 13.Simulate a server clientAuth=False
{% highlight bash %}
openssl s_server -accept 443 -cert <server-cert>.pem -pass pass:<pass> -WWW -state -msg -tlsextdebug -CAfile <truststore.pem> -Verify 1
{% endhighlight %}

### 14.Import a .pem certificate to a JKS truststore
{% highlight bash %}
openssl x509 -outform der -in cert.pem -out cert.der
keytool -import -alias cert.alias -keystore truststore -file cert.der
{% endhighlight %}

