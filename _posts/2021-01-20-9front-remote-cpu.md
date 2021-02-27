---
layout: default
title: "9front OS: Remote CPU"
---

9front OS: Remote CPU
=====================

How to connect to your plan9 operating system on a Linode virtual machine using a cpu, auth and fs server.

Overview
--------

If you were following along with my previous 
[article]({% post_url 2021-01-04-linode-9front %}), then you probably have a working 
installation of 9front OS on a Linode virtual machine that you can access through a 
LISH pseudoterminal. In the following article, I will attempt to walk through the 
process of creating a cpu, auth and fs server, which will allow you to spawn a virtual 
desktop from any non-9front OS using drawterm.

For the purpose of this installation, I will assume that 9front was installed with
the device drive name of `sd00`, sysname of `cirno` and the `hjfs` filesystem.

Step 1: Gather System Information
---------------------------------

Invoke the DHCPCD server. Print the configured network database information, 
noting the values for `ip=`, `ipmask=` and `ipgw=` (these will be used later).
    
    term% ip/ipconfig
    term% cat /net/ndb
    ip=10.0.2.15 ipmask=255.255.255.0 ipgw=10.0.2.2
        sys=cirno
        dom=cirno.hsd1.wa.comcast.net

Step 2: Enable CPU Service
--------------------------

Mount `9fat` file.

    term% 9fs 9fat
    
Open the plan9.ini file using `sam /n/9fat/plan9.ini` or your preferred editor 
(i.e. acme, sam, etc). Add the `service=cpu` and `nobootprompt=` lines per the
example below.

    bootfile=9pc64
    bootargs=local!/dev/sd00/fs -m 147
    mouseport=ps2
    monitor=vesa
    vgasize=1024x768x16
    nobootprompt=local!/dev/sd00/fs -m 147 -a tcp!*!564
    service=cpu

Step 3: Auth Server
-------------------

Configure the auth server non-volitile ram host owner, name and password key [0].

    term% auth/wrkey
    authid: [glenda]
    authdom: [9front]
    secstore key: ↵
    password: [glenda’s password]

Start keyfs, which needs to be loaded every time you want to modify the users 
key, and modify the user key for glenda.
    
    term% auth/keyfs
    term% auth/changeuser [glenda]
    Password: [same as password used for nvram step]
    Confirm Password: [same as password used for nvram step]
    assign new Inferno/POP secret? (y/n): n
    Expiration date (YYYYMMDD or never)[never]: ↵
    Post id: ↵
    User's full name: ↵
    Department #: ↵
    User's email address: ↵
    Sponsor's email address: ↵
    user glenda installed for Plan 9

Enable the Plan 9 and Netkey keys for the host user.

    term% auth/enable [glenda]

Step 4: Network Database
------------------------

Open the network database using `sam /lib/ndb/local`. Near the bottom of 
the file, uncomment and modify the following lines using the values obtained
in **Step 1**. Take not of the `ip=` value which ends with `0`.
    
    auth=cirno authdom=9front
    ipnet=9front ip=10.0.2.0 ipmask=255.255.255.0
        ipgw=10.0.2.2
        dns=10.0.2.2
        auth=cirno
        dnsdom=9front
        cpu=cirno
        fs=cirno

Now it's time to reboot your system.

    term% fshalt -r

Step 5: Profit
--------------

Now comes the fun part.  From a non-plan9 OS, download and install the cpu client 
application, [drawterm](http://drawterm.9front.org). Note that the version linked is 
a fork of Russ CoX's drawterm. Once installed, launch the application, specify the 
server cpu IP address, user (glenda) and password.

Once connected, mount the web file system and start the rio window manager.

    webfs
    rio -i riostart

Optionally, we can edit the host user's profile via `sam $home/lib/profile` and add
those lines right below `fn cpu% { $* }`.

Credit
------

Special thanks to Youtuber C0tl43 and his video [Setting up a 9front cpu+auth+fs 
standalone server](https://www.youtube.com/watch?v=PjVpB3SpAfQ), which inspired and
helped create this article.

[0]: The `secstore key` and `password` are secret passwords of eight characters
      or more in length. The `password` is the password belonging to the authid 
      user on the auth server responsible for the authdom entered above. The  
      `secstore key` is the password of the user on the secure-store server 
      (Read: [FQA 7.4.3 - secstored](http://fqa.9front.org/fqa8.html#7.4.3)). If 
      the secstore client (Read: [FQA 8.4.7 - secstore](http://fqa.9front.org/
      fqa7.html#8.4.7)) is not being used on this machine (for example, if this 
      is the auth server where secstored will run), just hit enter at the 
      *secstore key:* prompt.
