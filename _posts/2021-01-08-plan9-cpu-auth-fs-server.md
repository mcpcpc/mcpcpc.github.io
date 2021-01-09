---
layout: post
title: "9front OS: cpu, auth and fs Server Setup"
description: How to connect to your plan9 operating system on a Linode virtual machine using a cpu+auth server.
---

If you were following along with my previous 
[article]({% post_url 2021-01-04-linode-9front %}), then you probably have a working 
installation of 9front OS on a Linode virtual machine that you can access through a 
LISH pseudoterminal. In the following article, I will attempt to walk through the 
process of creating a cpu+auth server, which will allow you to spawn a virtual 
desktop from any non-9front OS using drawterm[^1]. 

For the purpose of this installation, I will assume that 9front was installed with
default configurations selected (e.g. cwfs) and the device drive name of *sd00*.

## Configuration

*   Mount `9fat` file.

    ```
    term% 9fs 9fat
    ```

*   Invoke the DHCPCD server. Print the configured network database information, 
    noting the values for `ip=`, `ipmask=` and `ipgw=` (these will be used later).

    ```
    term% ip/ipconfig
    term% cat /net/ndb
    ip=10.0.2.15 ipmask=255.255.255.0 ipgw=10.0.2.2
        sys=cirno
        dom=cirno.hsd1.wa.comcast.net
    ```

*   Open the plan9.ini file using `sam /n/9fat/plan9.ini` or your preferred editor 
    (i.e. acme, ed, etc). Set the bootargs, default hostowner, auth, cpu, authdom 
    and service to cpu server.

    ```
    bootfile=9pc
    bootargs=local!/dev/sd00/fscache
    mouseport=ps2
    monitor=vesa
    vgasize=1024x768x16
    nobootprompt=local!/dev/sd00/fscache -a tcp!*!564
    user=glenda
    auth=10.0.2.15
    cpu=10.0.2.15
    authdom=9front
    service=cpu
    ```
    
*   Configure the auth server non-volitile ram host owner, name and password key [^2].

    ```
    term% auth/wrkey
    bad nvram des key
    bad authentication id
    bad authenication domain
    authid: glenda
    authdom: 9front
    secstore key: [glenda’s secstore password]
    secstore key: [glenda’s secstore password repeated]
    password: [glenda’s password]
    password: [glenda’s password repeated]
    ```

*   Start keyfs, which needs to be loaded every time you want to modify the users 
    key, and modify the user key for glenda.

    ```
    term% auth/keyfs
    term% auth/changeuser glenda
    Password: <same as password used for nvram step>
    Password: <same as password used for nvram step>
    Confirm Password: <same as password used for nvram step>
    assign new Inferno/POP secret? (y/n): n
    Expiration date (YYYYMMDD or never)[never]:↵
    Post id:↵
    User's full name:↵
    Department #:↵
    User's email address:↵
    Sponsor's email address:↵
    user glenda installed for Plan 9
    ```

*   Invoke `auth/enable` on glenda.

    ```
    term% auth/enable glenda
    ```

*   Open the network database using `sam /lib/ndb/local`. Scroll to the bottom of 
    the file and add/modify the following lines. 

    ```
    sys=9front ether=000027ad3b9a authdom=9front auth=10.0.2.15 ip=10.0.2.15

    ipnet=9front ip=10.0.2.0 ipmask=255.255.255.0
        ipgw=10.0.2.2
        auth=10.0.2.15
        authdom=9front
        fs=10.0.2.15
        cpu=10.0.2.15
        dns=75.75.75.75

    ```

*   Reboot the system.

    ```
    term% fshalt -r
    ```

## Connecting

Now comes the fun part.  From a non-plan9 OS, download and install the cpu client 
application, [drawterm](http://drawterm.9front.org). Note that the version linked is 
a fork of Russ CoX's drawterm. Once installed, launch the application, specify the server cpu IP address, user (glenda) and password.

Once connected, start webfs and rio window manager.

```
webfs
bind -b '#S' /dev
rio -i riostart
```

## Tips And Tricks

*   You probably don't want to enter the above commands each and every time you want  
    to access your plan9 system remotely. Instead, we can edit the host users 
    profile via `sam /usr/glenda/lib/profile` and add those lines right below 
    `fn cpu% { $* }`.

[^1]: Special thanks to Youtuber C0tl43 and his video [Setting up a 9front cpu+auth+fs standalone server](https://www.youtube.com/watch?v=PjVpB3SpAfQ), which inspired and helped create this article.
[^2]:  The `secstore key` and `password` are secret passwords of eight characters
       or more in length. The `password` is the password belonging to the authid 
       user on the auth server responsible for the authdom entered above. The  
       `secstore key` is the password of the user on the secure-store server 
       (Read: [FQA 7.4.3 - secstored](http://fqa.9front.org/fqa8.html#7.4.3)). If 
       the secstore client (Read: [FQA 8.4.7 - secstore](http://fqa.9front.org/
       fqa7.html#8.4.7)) is not being used on this machine (for example, if this 
       is the auth server where secstored will run), just hit enter at the 
       *secstore key:* prompt.

