---
layout: post
title: Howto Download Megaupload using command line
date: 2016-10-30 16:34:23
author: Renan Rocha
categories: Howto Download Megaupload wget command line files download megadl megatools megatool
short_description: This post will cover all the process of Downloading megaupload files using command line under linux
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is Megatools?

Megatools is a collection of programs for accessing Mega service from
a command line of your desktop or server.

Megatools allow you to copy individual files as well as entire directory
trees to and from the cloud. You can also perform streaming downloads for
example to preview videos and audio files, without needing to download
the entire file.

Megatools are robust and optimized for fast operation - as fast as Mega
servers allow. Memory requirements and CPU utilization are kept at minimum.

You can register account using a 'megareg' tool, with the benefit of having
true control of your encryption keys.

Mega website can be found at http://mega.nz.

Megatools can be downloaded at http://megatools.megous.com


Tools
=====

  megareg      Register and verify a new mega account
  megadf       Show your cloud storage space usage/quota
  megals       List all remote files
  megamkdir    Create remote directory
  megarm       Remove remote file or directory
  megaput      Upload individual files
  megaget      Download individual files
  megadl       Download file from a "public" Mega link
               (doesn't require login)
  megastream   Streaming download of a file
               (can be used to preview videos or music)
  megacopy     Upload or download a directory tree
  megafs       Mount remote filesystem locally.


All of these tools do:

- Local caching of remote session/filesystem information
  for faster execution. Cache is encrypted with your password
  key.
- Support loading login credentials from a configuration file

## Requirements needed to accomplish this task is the following:
**build-essential unzip libglib2.0-dev libssl-dev libcurl4-openssl-dev libgirepository1.0-dev asciidoc**

To install under Centos
{% highlight bash %}
yum update -y
yum install build-essential unzip libglib2.0-dev libssl-dev libcurl4-openssl-dev libgirepository1.0-dev asciidoc
{% endhighlight %}
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get update -y
apt-get -y install build-essential unzip libglib2.0-dev libssl-dev libcurl4-openssl-dev libgirepository1.0-dev asciidoc
{% endhighlight %}
<!--more-->
Next We Download megatools
{% highlight bash %}
wget https://github.com/megous/megatools/archive/master.zip
{% endhighlight %}
Extract our master.zip file with unzip
{% highlight bash %}
unzip master.zip
cd megatools-master/
{% endhighlight %}
Next We Generator our ./configure file
{% highlight bash %}
./autogen.sh
{% endhighlight %}
We Should now have our ./configure file generated
{% highlight bash %}
./configure
make
make install
{% endhighlight %}
We Should now have 
{% highlight bash %}
megacopy   megadf     megadl     megaget    megals     megamkdir  megaput    megareg    megarm
{% endhighlight %}
To Download Megaupload files use:
{% highlight bash %}
megadl 'https://mega.nz/FILE_extention'
{% endhighlight %}

## You can Now Download Megaupload Files using command line.

![alt text](http://i.imgur.com/FxaUMe2.jpg "Kim") 