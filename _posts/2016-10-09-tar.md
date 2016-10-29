---
layout: post
title: Howto extract tar bz2 tar.gz
date: 2016-10-08 12:55:23
author: Renan Rocha
categories: howto extract tar bz2 tar.gz IredMail
short_description: This post will cover all the process of extracting tar bz2 files
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is Tar?
In computing, tar is a computer software utility for collecting many files into one archive file, often referred to as a tarball, for distribution or backup purposes. The name is derived from (t)ape (ar)chive, as it was originally developed to write data to sequential I/O devices with no file system of their own. The archive data sets created by tar contain various file system parameters, such as name, time stamps, ownership, file access permissions, and directory organization. The command line utility was first introduced in the seventh edition of unix (v7) in January 1979, replacing the tp program.[1] The file structure to store this information was later standardized in POSIX.1-1988[2] and later POSIX.1-2001.[3] and became a format supported by most modern file archiving systems.

## What is Bz2?

bzip2 is a free and open-source file compression program that uses the Burrows–Wheeler algorithm. It only compresses single files and is not a file archiver. It is developed and maintained by Julian Seward. Seward made the first public release of bzip2, version 0.15, in July 1996. The compressor's stability and popularity grew over the next several years, and Seward released version 1.0 in late 2000.


### What is .tar.gz
A .tar.gz (also .tgz) file is nothing but an archive. It is a file that acts as a container for other files. An archive can contain many files, folders, and subfolders, usually in compressed form using gzip or bzip2 program on Unix like operating systems.

## Requirements needed to accomplish this task is the following:
**bzip2, tar**

To install under Centos: 
{% highlight bash %}
yum install -y bzip2 tar
{% endhighlight %}

To install under Debian: 
{% highlight bash %}
apt-get install -y bzip2 tar
{% endhighlight %}
<!--more-->

1. We have IredMail .tar.bz2 that needs to be extracted
{% highlight bash %}
ls
iRedMail-0.9.5-1.tar.bz2
{% endhighlight %}

2. Lets Begin by using bzip2 to extract our tar file
{% highlight bash %}
bzip2 -d iRedMail-0.9.5-1.tar.bz2
ls
iRedMail-0.9.5-1.tar
{% endhighlight %}

3. Now we have iRedMail-0.9.5-1.tar let's extract this file
{% highlight bash %}
tar -xvf iRedMail-0.9.5-1.tar
ls
iRedMail-0.9.5-1  iRedMail-0.9.5-1.tar
{% endhighlight %}

We have our file extracted we can now check the directory by:
{% highlight bash %}
cd iRedMail-0.9.5-1
pwd
/root/zip/iRedMail-0.9.5-1
{% endhighlight %}

## To Extract a .tar.gz

Do the following command, remember to rename data.tar.gz with the file you're trying to extract.
{% highlight bash %}
tar -zxvf data.tar.gz
{% endhighlight %}

The Definition of this command is:

    **-z** : Uncompress the resulting archive with gzip command.
    **-x** : Extract to disk from the archive.
    **-v** : Produce verbose output i.e. show progress and file names while extracting files.
    **-f** data.tar.gz : Read the archive from the specified file called data.tar.gz.

By defaults files will be extracted into the current directory. To change the directory use -C option. In this example, extract files in /data/projects directory:

{% highlight bash %}
tar -zxvf data.tar.gz -C /data/projects
{% endhighlight %}