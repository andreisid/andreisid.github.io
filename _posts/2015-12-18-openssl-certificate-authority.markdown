---
author: andrei
comments: true
date: 2015-12-18 15:01:00+00:00
layout: post
slug: openssl-certificate-authority 
title: OpenSSL Certificate Authority
excerpt: "OpenSSL-certificate-authority"
categories:
- ssl
- linux
- security
- certificates
---

{% include _toc.html %}
Ever wonder how to set up a Certificate Authority and how to propperly generate/revoke certificates? Openssl is an open source library that can help you accomplish that.

Certificate Authorities are entities that sign virtual certificates. Verisign or Digicert are some known public CA. They are most useful for public domains and certificates signed by them are not for free.

You can act as your own Certificate Authority on some cases and create your own CA for certificate management. This can be be done easily by using OpenSSL and it is best to implement on intranet systems.

<div style="text-align:center" markdown="1">
![poodle](/images/certificate-authority-590x250.jpg)
</div>


* Note:  Must read [Jamie's blog](https://jamielinux.com/docs/openssl-certificate-authority/index.html) 
* You can download and install a preconfigured CA [here](https://github.com/andreisid/dummyCA)

# Create the RootCA PK and certificate

###1. Set up directory structure 

{% highlight bash %}
mkdir /root/ca
cd /root/ca
mkdir certs crl newcerts private
chmod 700 private
touch index.txt
echo 1000 > serial
{% endhighlight %}

* cert dir will contain certificates
* crl will contain certification revocation lists
* private will contain the private keys

###2. Set up config file 

You can find [here](https://github.com/andreisid/dummyCA/blob/master/opensslRootCA.cnf) a sample configuration file. Save it as /root/ca/openssl.cnf, it will be used later

###3. Create RootCA private key

{% highlight bash %}
cd /root/ca
openssl genrsa -aes256 -out private/ca.key.pem 4096

Enter pass phrase for ca.key.pem: mypassword
Verifying - Enter pass phrase for ca.key.pem: mypassword

chmod 400 private/ca.key.pem
{% endhighlight %}

* omitting aes256 will not set a password on your PK. It is NOT recommended on RootCA or IntermediateCA PK

###4. Create the RootCA certificate
{% highlight bash %}
cd /root/ca

openssl req -config openssl.cnf \
      -key private/ca.key.pem \
      -new -x509 -days 7300 -sha256 -extensions v3_ca \
      -out certs/ca.cert.pem

Enter pass phrase for ca.key.pem: mypassword
You are about to be asked to enter information that will be incorporated
into your certificate request.
-----
Country Name (2 letter code) [XX]:GB
State or Province Name []:England
Locality Name []:
Organization Name []:Alice Ltd
Organizational Unit Name []:Alice Ltd Certificate Authority
Common Name []:Alice Ltd Root CA
Email Address []:

chmod 444 certs/ca.cert.pem

{% endhighlight %}

* extensions v3_ca specifies the extension from openssl.conf to be used
* set to expire after 20 years. CAs usually have a long expiry period

###5. Verify the RootCA certificate
{% highlight bash %}
openssl x509 -noout -text -in certs/ca.cert.pem
{% endhighlight %}

* Issuer and Subject will be the same as this is a self-signed certificate
* Subject CN section specifies the Common Name of the certificate and it is used as an identity field.

# Create Intermediate PK and certificate

An intermediate certificate is signed by the root certificate and it expires faster than the RootCA.

###1. Setting up dir structure

{% highlight bash %}
mkdir /root/ca/intermediate
cd /root/ca/intermediate
mkdir certs crl csr newcerts private
chmod 700 private
touch index.txt
echo 1000 > serial
echo 1000 > /root/ca/intermediate/crlnumber

{% endhighlight %}

* crlnumber is used for tracking certificate revocation lists

###2. Set up config file 

You can find [here](https://github.com/andreisid/dummyCA/blob/master/opensslRootCA.cnf) a sample configuration file. Save it as /root/ca/intermediate/openssl.cnf, it will be used later

###3. Create the IntermediateCA private key

{% highlight bash %}
cd /root/ca
openssl genrsa -aes256 \
      -out intermediate/private/intermediate.key.pem 4096

Enter pass phrase for intermediate.key.pem: mypassword
Verifying - Enter pass phrase for intermediate.key.pem: mypassword

chmod 400 intermediate/private/intermediate.key.pem
{% endhighlight %}


###4. Create the IntermediateCA certificate

Creating an intermediate certificate consists in 2 steps:

- create a certificate signing request using the IntermidiateCA openssl.cnf config file

- sing the intermediate request by using the RootCA openssl.cnf config file. It will result the intermediate certificare


##### 4.a Create the signing request
{% highlight bash %}
cd /root/ca
openssl req -config intermediate/openssl.cnf -new -sha256 \
      -key intermediate/private/intermediate.key.pem \
      -out intermediate/csr/intermediate.csr.pem

Enter pass phrase for intermediate.key.pem: mypassword
You are about to be asked to enter information that will be incorporated
into your certificate request.
-----
Country Name (2 letter code) [XX]:GB
State or Province Name []:England
Locality Name []:
Organization Name []:Alice Ltd
Organizational Unit Name []:Alice Ltd Certificate Authority
Common Name []:Alice Ltd Intermediate CA
Email Address []:
{% endhighlight %}

##### 4.a Create the certificate

{% highlight bash %}
cd /root/ca
openssl ca -config openssl.cnf -extensions v3_intermediate_ca \
      -days 3650 -notext -md sha256 \
      -in intermediate/csr/intermediate.csr.pem \
      -out intermediate/certs/intermediate.cert.pem

Enter pass phrase for ca.key.pem: mypassword
Sign the certificate? [y/n]: y

chmod 444 intermediate/certs/intermediate.cert.pem
{% endhighlight %}

###5. Verify the Intermediate certificate

{% highlight bash %}
openssl x509 -noout -text \
      -in intermediate/certs/intermediate.cert.pem
{% endhighlight %}
* this outputs the content of the certificate

{% highlight bash %}
openssl verify -CAfile certs/ca.cert.pem \
      intermediate/certs/intermediate.cert.pem

intermediate.cert.pem: OK
{% endhighlight %}
* this verifies IntermediateCA against the RootCA

###6. Create the certificate chain

{% highlight bash %}
cat intermediate/certs/intermediate.cert.pem \
      certs/ca.cert.pem > intermediate/certs/ca-chain.cert.pem
chmod 444 intermediate/certs/ca-chain.cert.pem
{% endhighlight %}


#Create a new certificate signed by the IntermediateCA

###1. Create a certificate private key
      
{% highlight bash %}
cd /root/ca
openssl genrsa -aes256 \
      -out intermediate/private/www.example.com.key.pem 2048
chmod 400 intermediate/private/www.example.com.key.pem
{% endhighlight %}

###2. Create a cert request and sign it

{% highlight bash %}
cd /root/ca
openssl req -config intermediate/openssl.cnf \
      -key intermediate/private/www.example.com.key.pem \
      -new -sha256 -out intermediate/csr/www.example.com.csr.pem

openssl ca -config intermediate/openssl.cnf \
      -extensions server_cert -days 375 -notext -md sha256 \
      -in intermediate/csr/www.example.com.csr.pem \
      -out intermediate/certs/www.example.com.cert.pem
chmod 444 intermediate/certs/www.example.com.cert.pem
{% endhighlight %}

* Note: new server/client certificates will be signed by the IntermediateCA. 
* "extensions server_cert" is used for creating a server certificate, you can use "extensions usr_cert" for user certificates.

###3. Verify the certificate

{% highlight bash %}
openssl verify -CAfile intermediate/certs/ca-chain.cert.pem \
      intermediate/certs/www.example.com.cert.pem

www.example.com.cert.pem: OK
{% endhighlight %}
*Note: this will verify the certificate against the certificate chain we've created before



