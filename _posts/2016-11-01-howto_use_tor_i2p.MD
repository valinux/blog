---
layout: post
title: Howto Tor + I2p with privoxy tunnel ports via SSH Putty
date: 2016-11-01 13:27:23
author: Renan Rocha
categories: Howto TOR + I2P privoxy onion i2p darknet sites
short_description: This post will cover all the process of creating an anoymous proxy server for darknet usage
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is privoxy?
Privoxy is a non-caching web proxy with filtering capabilities for enhancing privacy, manipulating cookies and modifying web page data and HTTP headers before the page is rendered by the browser. Privoxy is a "privacy enhancing proxy", filtering Web pages and removing advertisements. Privoxy can be customized by users, for both stand-alone systems and multi-user networks. Privoxy can be chained to other proxies and is frequently used in combination with Squid and can be used to bypass Internet censorship.

## Requirements needed to accomplish this task is the following:
**tor, i2p, privoxy, nano**

## Warning this Turtorial is for people who have already had tor compiled and i2p installed.
To install under Centos
{% highlight bash %}
yum update -y
yum install privoxy
{% endhighlight %}
To install under Debian: 
{% highlight bash %}
apt-get update -y
apt-get -y install privoxy
{% endhighlight %}
<!--more-->
After privoxy is installed we need to configure for our custom needs.
{% highlight bash %}
nano /etc/privoxy/config
{% endhighlight %}
Use your pg down button to scroll all the way to the bottom of this config file and add the following lines:
{% highlight bash %}
forward .i2p 127.0.0.1:4444
forward-socks5 .onion 127.0.0.1:9050 .
{% endhighlight %}
After you have done this save exit and restart privoxy
{% highlight bash %}
service privoxy restart
[ ok ] Restarting filtering proxy server: privoxy.
{% endhighlight %}
## Now that Privoxy has restarted we need to forward port 8118 with putty to be able to use our private proxy.
On Putty Type in your server ip address and port.
![alt text](http://i.imgur.com/kUbGKUg.png "Putty Tunnel") 
Next Under Your connection tab click Tunnel:
![alt text](http://i.imgur.com/pmSQYIi.png "Putty Tunnel") 
Next we add our Tunnel config
![alt text](http://i.imgur.com/NXiv1oE.png "Putty Tunnel") 
Source port: 8118
Destination: localhost:8118
Click Open Button type in your username and password for your SSH session and the port should be open.
{% highlight bash %}
Our tunnel is basically like this:
SSH Client <8118:localhost:8118> <22:8118> Remote SSH Server <8118: Local Privoxy Server <8118 
{% endhighlight %}
## Firefox Proxy Setting
On Your Option tab> then Advenced tab> and Network Tab> Click on the [Settings button] and add the following:
![alt text](http://i.imgur.com/BYQeiy0.png "FireFox Proxy") 
## !!! REMEMBER IF YOU VISIT A REGULAR WEBSITE YOU ARE USING YOUR REAL IP ADDRESS AND NOT UNDER TOR !!! 
LATER I WILL SHOW YOU HOW TO CONNECT TO TOR AND USE OPENVPN PROXY CLIENT TO CONNECT TO A SECURE LINE TOR > OPENVPN > CLEARNET
Go to your i2p control panel by visiting the following address:
{% highlight bash %}
http://127.0.0.1:7657/home
^ This is your router control panel for i2p Privoxy will allow you to access local ports under your remote server cheers! 
https://thehiddenwiki.org/
^ This link is for all the .onion sites my fav is the hiddenwiki! 
{% endhighlight %}
## REMEMBER THIS!!!
{% highlight bash %}
When you request to access an .onion site on the tor network you will be able to access that site.
When you request to access an .i2p site on the i2p network you will be able to access that site.
When you request to access an local port on your server you will be able to access that.
When you request to access THE CLEARNET SITES YOU WILL BE ACCESSING USING YOUR SERVERS IP ADDRESSS!!!!! AAAAAAAAAAAAHHHHHHHHHHHH!!! READ THIS!
{% endhighlight %}

## LATER I WILL SHOW YOU HOW TO CREATE THE ULTIMATE ANON BLACKHOLE WITH OPENVPN tails and ssh tunnels with tor and i2p
