---
layout: post
title: Howto Install Teamspeak 3 Server On Linux Server
date: 2016-10-23 13:39:23
author: Renan Rocha
categories: howto install teamspeak 3 server under linux freebsd debian centos 7
short_description: This post will cover all the process of installing a secure teamspeak server under Linux
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is TeamSpeak?

TeamSpeak is proprietary voice-over-Internet Protocol (VoIP) software for audio communication between users on a chat channel, much like a telephone conference call. Users typically use headphones with a microphone. The client software connects to a TeamSpeak server of the user's choice, from which the user may join chat channels.

The target audience for TeamSpeak is gamers hackers and team planning, who can use the software to communicate with other users on the same team of a multiplayer game. Communicating by voice gives a competitive advantage by enabling players to keep their hands on the controls.

## Requirements needed to accomplish this task is the following:
**Putty, SSH, Centos or any other linux distribution**

To install under Centos
{% highlight bash %}
yum update -y
yum install nano wget perl net-tools -y
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get update -y
apt-get install nano wget perl net-tools -y
{% endhighlight %}
<!--more-->
This will update Centos/Debian and install some needed packages. For some crazy reason they decided not to ship Centos with ifconfig so the net-tools takes care of that.

1. Now we need to add a user for installing and running Teamspeak 3 server as doing it with root is not a good idea. For this guide I will be creating the user "teamspeak". If you go with another name make sure to change the name in all your paths such as cronjob.

{% highlight bash %}
adduser
passwd teamspeak
{% endhighlight %}

2. Now switch to the new account using su.
{% highlight bash %}
su teamspeak

cd
{% endhighlight %}

3. Download the server files, unpack them, and copy them back to the teamspeak home directory for making things a bit cleaner and easyer to find later on.
If you're using Freebsd look for the server files under http://dl.4players.de/ts/releases/3.0.13/ and download the right server files based on the OS you're operating.
{% highlight bash %}
wget http://dl.4players.de/ts/releases/3.0.13/teamspeak3-server_linux_amd64-3.0.13.tar.bz2
tar xvfz teamspeak3-server_linux_amd64-3.0.13.tar.bz2
cd teamspeak3-server_linux_amd64-3.0.13
cp * -R /home/teamspeak
cd ..
rm teamspeak3-server_linux_amd64-3.0.13 -r
rm teamspeak3-server_linux_amd64-3.0.13.tar.bz2
{% endhighlight %}

4. Now we will setup a crontab so if the server reboots Teamspeak will automatically start itself:
{% highlight bash %}
crontab -e
{% endhighlight %}

5. This opens the crontab file for your user with vi which can be a little tricky. hit SHIFT + I to put it insert mode and paste in this:

{% highlight bash %}
@reboot /teamspeak/ts3server_startscript.sh start
{% endhighlight %}

6. Hit Esc than type:
{% highlight bash %}
:wq
{% endhighlight %}
7. This will save and exit the editor. Now you can check and make sure it is there by doing:

{% highlight bash %}
crontab -l
{% endhighlight %}

![alt text](http://i.imgur.com/ebKwP33.jpg "Like This")

You can now start your new server.
{% highlight bash %}
./ts3server_startscript.sh start
{% endhighlight %}

## Make sure to copy and save the security token that is listed when the server starts.

