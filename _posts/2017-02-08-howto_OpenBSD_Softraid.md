---
layout: post
title: Howto Configure OpenBSD With Softraid Encryption
date: 2017-02-08 09:53:23
author: Renan Rocha
categories: Howto Configure OpenBSD With Softraid Encryption bioctl 8192 PBKDF2 algorithm CYRPTO discipline raid 
short_description: This post will cover all the process of configuring OpenBSD with total disk encryption
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is OpenBSD?

OpenBSD is a free and open source Unix-like computer operating system descended from Berkeley Software Distribution (BSD)
a Research Unix derivative developed at the University of California, Berkeley. 
In late 1995, Theo de Raadt forked it from NetBSD.

## What is PBKDF2?
At its most basic, PBKDF2 is a “password-strengthening algorithm” that makes it difficult for a computer to check that any one password is the correct master password during a brute-force attack. The standard implementation of PBKDF2 uses SHA-1, a secure hashing algorithm.

## What is SoftRAID?
SoftRAID is disk driver software that allows you to create, monitor, and maintain a software implementation of RAID. ... striped (RAID level 0), mirrored (RAID level 1), or standard. HFS volumes on the same set of disks.


## Our VM Has the following setup:
100GB HD
2Core

First We boot into our ISO and we begin our fresh install.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part1.png "Part 1") 

We select "(S) for shell."
<!--more-->

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part2.png "Part 2")

"fdisk -iy wd0" -i initializes a new MBR bootcode and -y avoids asking questions.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part3.png "Part 3")

Next we enter the disklabel editor with "disklabel -E wd0"

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part4.png "Part 4")

We Will now do a few disklabeling where:
a=root b=swap 
We start by creating a root partition with "a a" and giving it only 256M. 
This is because we only need a small amount of space to host the OpenBSD boot information and kernel. 
This will provide us the general information needed to unencrypted on boot.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part5.png "Part 5")

You notice that I wrote "RAID" rather than 4.2BSD at the end!
If you try to create the softraid on a FS labeled 4.2BSD it will fail. 
then i "w" and "q" w - write and q - quit.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part6.png "Part 6")

bioctl is the command we use to manage RAID interfaces in OpenBSD. 
There are a few options we pass to it -c C which stipulates the RAID will be a CYRPTO discipline. -r 8192 is the number of iterations of the PBKDF2 algorithm to run. -l simply specifics the hosting disk label. Enter the command: "bioctl -c C -r 8192 -l /dev/wd0d softraid0" Here you will enter your passphrase that will allow you to mount on boot. I recommend something very difficult to brute-force or a yubikey.
You notice that i miss spelled my passcode a few times because its massive.
Then write "/install" to get back to our install progress.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part7.png "Part 7")

Go through the install process as you normally would, but when presented with the Available Disks HOLD TIGHT! First we will select wd0 which if you remember is the main drive hosting our root, swap, and RAID. 
For wd0 we are going to use the "(W)hole disk"
The OpenBSD installer will present a default auto-layout that otherwise would be great, but since we are encrypting we are going to create a "(C)ustom Layout"

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part8.png "Part 8")

The disklabel editor will come up that looks vaguely like the one we started with earlier. We are going to label the partitions and mount points.
We issue "m a" and set the A label to mount on / – remember this is the 256M partition we created to host our boot specific information. This is what the computer will start with prior to dumping us to a rescue shell to mount our crypto RAID. Issue w q and we will move forward with the install.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part9.png "Part 9")

The Install process will now show that there is a single remaining drive "sd0" and we will initialize it.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part10.png "Part 10")

Now we need to configure the important parts of our crypto volume. 
Our first step is to create a replica of our 256M root partition. 
Create a 256M partition with the only different being it is mounted on /altroot

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part11.png "Part 11")

Now we will create the additional partitions needed. 
The sizing of the partitions is dependent on the environment, but for the example here the Virtual Machine had a 10GB drive. You will need at a minimum /tmp /var /usr /home After you are done with those partitions you can w q and move on.

![alt text](https://raw.githubusercontent.com/valinux/blog/gh-pages/images/part12.png "Part 12")

After you customized your partition setup w q - write and quit. 
chose cd 
{% highlight bash %}
{% endhighlight %}
{% highlight bash %}
{% endhighlight %}
{% highlight bash %}
{% endhighlight %}