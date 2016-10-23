---
layout: post
title: Howto Secure Your Linux Server with CSF - ConfigServer Security & Firewall
date: 2016-10-23 14:57:23
author: Renan Rocha
categories: Howto Secure your Linux OS DDOS protection SYN flood with CSF ConfigServer Security Firewall ssh sshd
short_description: This post will cover all the process of securing your linux server to prevent cyber attacks
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---

## What is CSF (ConfigServer Security & Firewall)?
ConfigServe Firewall, also known as CSF, is a firewall configuration script created to provide better security for your server while giving you an easy to use, advanced interface for managing your firewall settings. CSF configures your server’s firewall to lock down public access to services and only allow certain connections, such as logging in to FTP, checking your email, or loading your websites.

ConfigServe Firewall also comes with a service called Login Failure Daemon, or LFD. LFD watches your user activity for excessive login failures which are commonly seen during brute force attacks. If a large amount of login failures are seen coming from the same IP address, that IP will immediately be temporarily blocked from all services on your server. These IP blocks will automatically expire, however they can be removed manually through the ConfigServer interface in WebHost Manager. In addition to removing IPs, CSF also allows you to manually whitelist or blacklist IPs in your firewall, as well as real time monitoring for automatic IP blocks in LFD.

## Requirements needed to accomplish this task is the following:
**wget, gcc, make, perl, nano, net-tools**

To install under Centos
{% highlight bash %}
yum update -y
yum install nano wget perl net-tools gcc make -y
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get update -y
apt-get install nano wget perl net-tools gcc make -y
{% endhighlight %}
<!--more-->

## Now lets Begin our journey:

We will change to the root user for adding some security to the server:

{% highlight bash %}
su

cd
{% endhighlight %}
We will change the default SSH port as this is the most common attack point.
{% highlight bash %}
nano /etc/ssh/sshd_config
{% endhighlight %}
Find the line by pressing ctrl + w
{% highlight bash %}
#Port 22
{% endhighlight %}
Uncomment it and change the port. For this guide I change the port to 6677.
{% highlight bash %}
Port 6677
{% endhighlight %}
Now save Ctrl o and exit Ctrl x and do:
{% highlight bash %}
service sshd restart
{% endhighlight %}
Remember to change the port in Putty/ssh client or you won't be able to connect into your session,  Centos 7 shipped with a new Iptables management system called firewalld. We are going to get rid of that as we will be using CSF (Config Server Firewall) instead.
{% highlight bash %}
systemctl stop firewalld
systemctl mask firewalld
yum install iptables-services -y
systemctl enable iptables
systemctl start iptables
{% endhighlight %}
Now install CSF and test it:
{% highlight bash %}
wget https://download.configserver.com/csf.tgz
tar -xzf csf.tgz
cd csf
sh install.sh
perl /usr/local/csf/bin/csftest.pl
{% endhighlight %}
Now we need to change the settings in the firewall. You can find the settings below by doing a search with Ctrl w. Change the settings so they are like this:
{% highlight bash %}
nano /etc/csf/csf.conf
{% endhighlight %}
Ctrl W to find the lines you want to edit.
This configuration is for our Teamspeak server as you can see these are the only ports i want open for my teamspeak server you may add the ports you want open for your server or custom settings.
## I recommend reading /etc/csf/csf.conf so that you can understand the firewall Policies.
{% highlight bash %}
TESTING = 0
RESTRICT_SYSLOG = 3
RESTRICT_UI = 2
TCP_IN = 2008,5454,10011,30033,41144
TCP_OUT = 2008,5454,10011,30033,41144
UDP_IN = 9987
UDP_OUT = 2011:2110
LF_DIRWATCH = 0
PT_LIMIT = 0
PT-------_ALL_USERS = 0
PT_USERPROC = 0
PT_USERMEM = 0
PT_USERTIME = 0
{% endhighlight %}

Now save, exit and restart CSF:
{% highlight bash %}
csf -r
{% endhighlight %}


## How to use CSF once its installed:
This we will cover some useful CSF SSH Command Line Commands in a “cheat sheet” format.
{% highlight bash %}
Command 	Description 
csf -s 	Start the firewall rules
csf -f 	Flush/Stop firewall rules
csf -r 	Restart the firewall rules
csf -a [IP.add.re.ss] [comment] 	Allow an IP and add to /etc/csf/csf.allow
csf -tr [IP.add.re.ss] 	Remove an IP from the temporary IP ban or allow list.
csf -tf 	Flush all IPs from the temporary IP entries
csf -d [IP.add.re.ss] [comment] 	Deny an IP and add to /etc/csf/csf.deny
csf -dr [IP.add.re.ss] 	Unblock an IP and remove from /etc/csf/csf.deny
csf -df 	Remove and unblock all entries in /etc/csf/csf.deny
csf -g [IP.add.re.ss] 	Search the iptables and ip6tables rules for a match (e.g. IP, CIDR, Port Number)
csf -t 	 Displays the current list of temporary allow and deny IP entries with their TTL and comment 
{% endhighlight %}

Enjoy! 