---
layout: post
title: Howto Download Wikileaks Files under Linux
date: 2016-10-10 12:02:23
author: Renan Rocha
categories: wikileaks leak email under linux using bash download files
short_description: This post will cover all the process of downloading and backing up wikileaks email leaks
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is Curl?
A command line tool for getting or sending files using URL syntax.

Since cURL uses libcurl, it supports a range of common Internet protocols, currently including HTTP, HTTPS, FTP, FTPS, SCP, SFTP, TFTP, LDAP, DAP, DICT, TELNET, FILE, IMAP, POP3, SMTP and RTSP (the last four only in versions newer than 7.20.0 or 9 February 2010).

cURL supports HTTPS and performs SSL certificate verification by default when a secure protocol is specified such as HTTPS. When cURL connects to a remote server via HTTPS, it will first obtain the remote server certificate and check against its CA certificate store the validity of the remote server to ensure the remote server is the one it claims to be. Some cURL packages have bundled with CA certificate store file. There are few options to specify CA certificate such as --cacert and --capath. --cacert option can be used to specify the location of the CA certificate store file. In the Windows platform, if a CA certificate file is not specified, cURL will look for a CA certificate file name “curl-ca-bundle.crt” in the following order:

    1. Directory where the cURL program is located.
    2. Current working directory.
    3. Windows system directory.
    4. Windows directory.
    5. Directories specified in the %PATH% environment variables.[6]

## What is Wget?

GNU Wget (or just Wget, formerly Geturl) is a computer program that retrieves content from web servers. It is part of the GNU Project.

Its name is derived from World Wide Web and get. It supports downloading via the HTTP, HTTPS, and FTP protocols.

Its features include recursive download, conversion of links for offline viewing of local HTML, and support for proxies. It appeared in 1996, coinciding with the boom of popularity of the Web, causing its wide use among Unix users and distribution with most major Linux distributions. Written in portable C, Wget can be easily installed on any Unix-like system and has been ported to many environments, including Microsoft Windows, Mac OS X, OpenVMS, HP-UX, MorphOS and AmigaOS. Since version 1.14 Wget has been able to save its output in the web archiving standard WARC format.[3]

It has been used as the basis for graphical programs such as GWget for the GNOME Desktop.

## Requirements needed to accomplish this task is the following:
**curl, wget**

To install under Centos: 
{% highlight bash %}
yum install -y curl wget
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get install -y curl wget
{% endhighlight %}
<!--more-->

1. Lets begin by using curl to download latest leaks
protip make sure to create a directory by using the following command:
{% highlight bash %}
mkdir wikileaks_emails
cd wikileaks_emails
curl -O https://wikileaks.org/podesta-emails/get/[1-4160]
{% endhighlight %}

2. Let's use wget if you don't like curl
{% highlight bash %}
mkdir wikileaks_emails
cd wikileaks_emails
for i in `seq 2061 4047`; do wget https://wikileaks.org/podesta-emails/get/$i; done
{% endhighlight %}

You should now have all the latest wikileaks leaks
if a new publication happens we can change the seq id from 2061 4047 to the latest release.
Under curl change the url [2061-4047] and the link "/podesta-emails/get/"

## Search all emails for key words by using the following command:
{% highlight bash %}
grep -rnw '/home/yourusername/wikileaks' -e "UFO"
{% endhighlight %}

**-r or -R is recursive,**
**-n is line number, and**
**-w stands match the whole word.**
**-l (lower-case L) can be added to just give the file name of matching files.**

## Results should show this:
{% highlight bash %}
/home/username/wikileaks/2505:24:> quoted you as trying to get to the bottom of UFO reports but that theCIA
/home/username/wikileaks/2505:50:vorite programs on 116 - quoted you as trying to get to the bottom of UFO r=
/home/username/wikileaks/3289:65:>> about UFO disclosure. I have been researching this phenomenon for a little
/home/username/wikileaks/3289:105:Gabe at Murch, and recently saw your twitter post about UFO disclosure. I h=
/home/username/wikileaks/3319:48968:DAjgfzL1cexyvD6/6N9Yz7zEWpXJfrc4cR/UFO+JPn+HTnrfh6qxt7+5uzheuNO2PpdiuF6knw39
{% endhighlight %}

## Studying this result is simple:

2505 is the name of the file inside our directory
24 is the line inside the file where the keyword was found
Enjoy! 