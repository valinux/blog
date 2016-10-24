---
layout: post
title: Howto Logout user / Logoff User Under Linux Command Line
date: 2016-10-23 15:37:27
author: Renan Rocha
categories: Howto logout user logoff user under linux SSH Command line putty
short_description: This post will cover all the process of logging off a linux user off your server.
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---

## How can I forcefully kill any user using bash shell on Linux?

A root user can kill any user session forcefully.

1. pkill – Kill processes by name.

2. kill – terminate or signal a process.

3. logout – Logout of a login shell. This command can be used by normal users to end their own session.

## Next you need to check and see what user is logged in, The syntax is:
{% highlight bash %}
root@: users
nobody nobody
{% endhighlight %}
you can also use who the syntax is:
{% highlight bash %}
root@: who
nobody     pts/2        Oct 23 23:55 (172.XX.XX.XXX)
nobody     pts/3        Oct 23 23:57 (173.XX.XX.XXX)
{% endhighlight %}

You can also use w the syntax is:

{% highlight bash %}
root@: w
 00:00:12 up 18 days, 20:13,  2 users,  load average: 0.96, 1.10, 1.04
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
nobody     pts/2    172.xx.xx.xxx    23:55    3:22   0.04s  0.04s -bash
nobody     pts/3    173.xx.xx.xxx    23:57    0.00s  0.04s  0.00s -bash

{% endhighlight %}

We know that there is 2 users name nobody logged in using 2 sessions and from 2 IPs very odd. Lets kill them.
{% highlight bash %}
pkill -KILL -u nobody
{% endhighlight %}
Now You need to investigate your system for possible exploit that gave them access into your system. Check your logs files under:
{% highlight bash %}
cd /var/logs/
{% endhighlight %}

Enjoy! Keep your eyes open and always monitor your server and kill unwanted users:

![alt text](http://i.imgur.com/IiGEycM.gif "Fuck my Sessions")