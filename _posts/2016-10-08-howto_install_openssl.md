---
layout: post
title: Howto Compile OpenSSL To the latest version
date: 2016-10-08 00:18:23
author: Renan Rocha
categories: openssl latest version compile make gcc extract tar gz howto 
short_description: This post will cover all the process of compiling and installing the latest version of openSSL
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
I have Debian 8 standard server and still running with OpenSSL 1.0.1t that is vulnerable to an remote attacker who can access parts of memory on system using vulnerable versions of OpenSSL. OpenSSL is a library that provides cryptographic functionality, specifically SSL/TLS for popular applications such as secure web servers (nginx web server, Apache web server) and MySQL database server.

OpenSSL is a library that provides cryptographic functionality, specifically SSL/TLS for popular applications such as secure web servers, MySQL databases and email applications.

I have tried to perform command “apt-get update openssl” but I receive “No Packages marked for Update” even though the latest version of tar version has been published.

The following steps describe how to install and update OpenSSL on Debian 8, CentOS 6 and CentOS 7.

## Requirements needed to accomplish this task is the following:
**wget gcc make tar unzip bzip2 nano**

To install under Centos
{% highlight bash %}
yum update -y
yum install wget gcc make tar unzip bzip2 nano
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get update -y
apt-get install wget gcc make tar unzip bzip2 nano
{% endhighlight %}
<!--more-->

1. Lets get the current version of openssl:
{% highlight bash %}
root@anon:~# openssl version
OpenSSL 1.0.1t  3 May 2016
{% endhighlight %}

2. To download the latest version of OpenSSL:
{% highlight bash %}
cd /usr/src
wget https://www.openssl.org/source/openssl-1.0.2j.tar.gz
tar -zxf openssl-1.0.2j.tar.gz
{% endhighlight %}
Before we start compiling this lets add an extra line of code inside our cryto

3. To manually compile OpenSSL and install/upgrade OpenSSL:
{% highlight bash %}
cd openssl-1.0.2j
./config
make
make test
make install
{% endhighlight %}
4. Check and see if the older version is still being displayed.
{% highlight bash %}
root@anon:/usr/src/openssl-1.0.2j# openssl version
OpenSSL 1.0.1t  3 May 2016
{% endhighlight %}
5. If the older version is still displaying, please make a copy of openssl in your bin folder to your root directory then link the new compiled version to your bin openssl folder:
{% highlight bash %}
mv /usr/bin/openssl /root/
ln -s /usr/local/ssl/bin/openssl /usr/bin/openssl
{% endhighlight %}
6. Check the Version again:
{% highlight bash %}
root@anon:/usr/src/openssl-1.0.2j# openssl version
OpenSSL 1.0.2j  26 Sep 2016
{% endhighlight %}
We are now running the latest version of OpenSSL.
Enjoy!



