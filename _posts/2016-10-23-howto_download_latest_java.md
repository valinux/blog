---
layout: post
title: Howto Manually Install Oracle Java on Debian Linux
date: 2016-10-23 14:57:23
author: Renan Rocha
categories: Howto Manually Install Oracle Java on a Debian Linux OS
short_description: This post will cover all the process of Installing the latest Java under Debian
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---

## Introduction

Java is a programming technology originally developed by Sun Microsystems and later acquired by Oracle. Oracle Java is a proprietary implementation for Java that is free to download and use for commercial use, but not to redistribute, therefore it is not included in a officially maintained repository.

There are many reasons why you would want to install Oracle Java.

You will need to know whether you are running a 32 bit or a 64 bit OS:
{% highlight bash %}
uname -m
{% endhighlight %}


    x86_64: 64 bit kernel

    i686: 32 bit kernel

## Downloading Oracle Java JDK

Using your web browser, go to the Oracle Java SE (Standard Edition) website and decide which version you want to install:
{% highlight bash %}
http://www.oracle.com/technetwork/java/javase/downloads/index.html
{% endhighlight %}
JDK: Java Development Kit. Includes a complete JRE plus tools for developing, debugging, and monitoring Java applications.

Server JRE: Java Runtime Environment. For deploying Java applications on servers. Includes tools for JVM monitoring and tools commonly required for server applications.

In this tutorial we will be installing the JDK Java SE Development Kit 8 x64 bits. Accept the license and copy the download link into your clipboard. Remember to choose the right tar.gz (64 or 32 bits). Use wget to download the archive into your server:


{% highlight bash %}
wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u111-b14/jdk-8u111-linux-x64.tar.gz
{% endhighlight %}
Oracle does not allow downloads without accepting their license, therefore we needed to modify the header of our request. Alternatively, you can just download the compressed file using your browser and manually upload it using a SFTP/FTP client.

Always get the latest version from Oracle's website and modify the commands from this tutorial accordingly to your downloaded file.

## Installing Oracle JDK
In this section, you will need sudo privileges:
{% highlight bash %}
sudo su
{% endhighlight %}
The /opt directory is reserved for all the software and add-on packages that are not part of the default installation. Create a directory for your JDK installation:
{% highlight bash %}
 mkdir /opt/jdk
{% endhighlight %}
and extract java into the /opt/jdk directory:
{% highlight bash %}
tar -zxf jdk-8u111-linux-x64.tar.gz -C /opt/jdk
{% endhighlight %}
Verify that the file has been extracted into the /opt/jdk directory.
{% highlight bash %}
 ls /opt/jdk
{% endhighlight %}
## Setting Oracle JDK as the default JVM
In our case, the java executable is located under /opt/jdk/jdk1.8.0_111/bin/java . To set it as the default JVM in your machine run:
{% highlight bash %}
update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_111/bin/java 100
{% endhighlight %}
and
{% highlight bash %}
update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_111/bin/javac 100
{% endhighlight %}
## Verify your installation
Verify that java has been successfully configured by running:
{% highlight bash %}
update-alternatives --display java
{% endhighlight %}
and
{% highlight bash %}
update-alternatives --display javac
{% endhighlight %}
The output should look like this:
{% highlight bash %}
java - auto mode
  link currently points to /opt/jdk/jdk1.8.0_111/bin/java
/opt/jdk/jdk1.8.0_111/bin/java - priority 100
Current 'best' version is '/opt/jdk/jdk1.8.0_111/bin/java'.

javac - auto mode
  link currently points to /opt/jdk/jdk1.8.0_111/bin/javac
/opt/jdk/jdk1.8.0_111/bin/javac - priority 100
Current 'best' version is '/opt/jdk/jdk1.8.0_111/bin/javac'.
{% endhighlight %}
Another easy way to check your installation is:
{% highlight bash %}
java -version
{% endhighlight %}
The output should look like this:

{% highlight bash %}
Java(TM) SE Runtime Environment (build 1.8.0_111-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.111-b14, mixed mode)
{% endhighlight %}
## (Optional) Updating Java
To update Java, simply download an updated version from Oracle's website and extract it under the /opt/jdk directory, then set it up as the default JVM with a higher priority number (in this case 110):
{% highlight bash %}
update-alternatives --install /usr/bin/java java /opt/jdk/jdk.new.version/bin/java 110
update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk.new.version/bin/javac 110
{% endhighlight %}
You can keep the old version or delete it:

{% highlight bash %}
update-alternatives --remove java /opt/jdk/jdk.old.version/bin/java
update-alternatives --remove javac /opt/jdk/jdk.old.version/bin/javac

rm -rf /opt/jdk/jdk.old.version
{% endhighlight %}
Enjoy!

![alt text](http://i.imgur.com/iqLX7mC.gif "Impressive") 


