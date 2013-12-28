---
layout: post
title: "new post"
description: ""
category: 
tags: []
---
{% include JB/setup %}
## Hot to Setup Node.js with Forever proxied through Nginx on Ubuntu 12.04

#Introduction, and why to use Nginx and Forever

Node.js (herafter referred to as node) is fantastic tool for creating scalable websites, however running node as server by
 itself has several drawbacks.

 1. Node is slow and inefficient at serving static content. (We will address this by serving static content with Nginx).
 2. If the node application crashes the server goes away (Addressed by running our node application through forever).
 3. To run a server at port 80 the node application has to be running as root. (Addressed by proxying through Ngnix).
 4. A node application takes over an entire port thus if it is running on port 80, only one http application can run.  (Also addressed by proxying through Nginx).

#Hardening

We will start by assuming you have already hardened your Ubuntu VPS.  This will include installing
[fail2ban](https://help.ubuntu.com/community/Fail2ban), [ufw](https://help.ubuntu.com/community/UFW), disabling
root login if it already isn't disabled and [changing the SSH port](https://help.ubuntu.com/lts/serverguide/openssh-server.html).
A good guide for securing Ubuntu 12.04 can be found [here](http://www.thefanclub.co.za/how-to/how-secure-ubuntu-1204-lts-server-part-1-basics).

Also as good housekeeping, you should update and upgrade

    sudo apt-get update

#Install Nodejs

If you are willing to work with an old version (0.6.x) of node you could

    sudo apt-get install nodejs

However, to install the latest version of node

    sudo apt-get install python-software-properties python g++ make
    sudo add-apt-repository ppa:chris-lea/node.js
    sudo apt-get update
    sudo apt-get install nodejs

To make sure it works type

    node -v

#Installing Nginx

Install Nginx with apt-get:

    sudo apt-get install nginx

Check to make sure it working:

    sudo /etc/init.d/nginx restart
    sudo apt-get install curl
    curl localhost

You should see:

    <html>
    <head>
    <title>Welcome to nginx!</title>
    </head>
    <body bgcolor="white" text="black">
    <center><h1>Welcome to nginx!</h1></center>
    </body>
    </html>




