---
layout: post
title: Howto Install Latest I2P Anonymous Network On Linux
date: 2016-10-23 16:27:23
author: Renan Rocha
categories: Howto Install Latest I2P version under Linux Anonymous Network Darknet
short_description: This post will cover all the process of Installing the latest I2P router Anonymous Network
image_preview: https://avatars1.githubusercontent.com/u/5298501?v=3&s=466
---
## What is I2P?
The Invisible Internet Project (I2P)
I2P is an anonymous network, exposing a simple layer that applications can use to anonymously and securely send messages to each other. The network itself is strictly message based (a la IP), but there is a library available to allow reliable streaming communication on top of it (a la TCP). All communication is end to end encrypted (in total there are four layers of encryption used when sending a message), and even the end points ("destinations") are cryptographic identifiers 

## How does it work?

To anonymize the messages sent, each client application has their I2P "router" build a few inbound and outbound "tunnels" - a sequence of peers that pass messages in one direction (to and from the client, respectively). In turn, when a client wants to send a message to another client, the client passes that message out one of their outbound tunnels targeting one of the other client's inbound tunnels, eventually reaching the destination. Every participant in the network chooses the length of these tunnels, and in doing so, makes a tradeoff between anonymity, latency, and throughput according to their own needs. The result is that the number of peers relaying each end to end message is the absolute minimum necessary to meet both the sender's and the receiver's threat model.

The first time a client wants to contact another client, they make a query against the fully distributed "network database" - a custom structured distributed hash table (DHT) based off the Kademlia algorithm. This is done to find the other client's inbound tunnels efficiently, but subsequent messages between them usually includes that data so no further network database lookups are required.

## Command line (headless) install:
Let's get the i2p install file.
{% highlight bash %}
wget https://download.i2p2.de/releases/0.9.27/i2pinstall_0.9.27.jar
{% endhighlight %}
Next we install i2p using -console for our install since we are using ssh client to install i2p headless.
{% highlight bash %}
java -jar i2pinstall_0.9.27.jar -console
{% endhighlight %}
You will see the following questions use 1 to continue after you make your decision based on where you want to install i2p files.
{% highlight bash %}
Welcome to the installation of i2p 0.9.27!
 - I2P <https://geti2p.net/>
The homepage is at: https://geti2p.net/
press 1 to continue, 2 to quit, 3 to redisplay
1
Select target path [/home/user]
press 1 to continue, 2 to quit, 3 to redisplay
1
[ Starting to unpack ]
[ Processing package: Base (1/1) ]
[ Unpacking finished ]
[ Console installation done ]
{% endhighlight %}
Next we start i2prouter using the following command:
{% highlight bash %}
./i2prouter start
{% endhighlight %}
You will get the following display:
{% highlight bash %}
Starting I2P Service...
Waiting for I2P Service......
running: PID:4326
{% endhighlight %}
We now have i2p running

Here's an i2p cheatsheet
{% highlight bash %}
./i2prouter start - to start the i2p router
./i2prouter stop - to stop the i2p router 
./i2prouter restart - to restart the i2p router
{% endhighlight %}
Welcome to the Underground! 

![alt text](http://i.imgur.com/FwuqFSEl.jpg "Shhh")
