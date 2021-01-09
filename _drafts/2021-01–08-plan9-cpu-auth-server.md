---
layout: post
title: "9front OS: cpu+auth Server Setup"
description: How to connect to your plan9 OS on a Linode virtual machine using a cpu+auth server.
---

If you were following along with my previous 
[article]({% post_url 2021-01-04-linode-9front %}), then you probably have a working 
installation of 9front OS on a Linode virtual machine that you can access through a 
LISH pseudoterminal. In the following article, I will attempt to walk through the 
process of creating a cpu+auth server, which will allow you to spawn a virtual 
desktop from any non-9front OS[^1].

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
    bootargs=local!/dev/sdC0/fs -m 832
    mouseport=ps2
    monitor=vesa
    vgasize=1024x768x16
    nobootprompt=local!/dev/sdC0/fscache -a tcp!*!564
    user=glenda
    auth=XX.X.X.XX
    cpu=XX.X.X.XX
    authdom=9plan
    service=cpu
    ```
    
*   Configure the auth server non-volitile ram host owner, name and password key.

    ```
    term% auth/wrkey
    bad nvram des key
    bad authentication id
    bad authenication domain
    authid: glenda
    authdom: 9plan
    secstore key: <glenda sectore password>
    secstore key: <repeat glenda secstore password>
    password: <actual glenda password>
    password: <repeat actual glenda password>
    ```

*   Start keyfs, which needs to be loaded every time you want to modify the users 
    key.

    ```
    term% auth/keyfs
    ```

*   Modify the user key for glenda:

    ```
    term% auth/changeuser glenda
    Password: <same as password used for nvram step>
    Password: <same as password used for nvram step>
    Confirm Password: <same as password used for nvram step>
    assign new Inferno/POP secret? (y/n): n
    make it the same as Plan 9 password? (y/n): y
    Expiration date (YYYYMMDD or never)[never]:
    Post id: glenda
    User's full name:
    Department #:
    User's email address:
    Sponsor's email address:
    user glenda installed for Plan 9
    ```

*   Invoke `auth/enable` on glenda.

    ```
    term% auth/enable glenda
    ```

*   Open the network database using `sam /lib/ndb/local`. Scroll to the bottom of 
    the file and add/modify the following lines. 

    ```
    sys=plan9 ether=000027ad3b9a authdom=plan9 auth=10.0.2.15 ip=10.0.2.15

    ipnet=Home ip=10.0.2.0 ipmask=255.255.255.0
      ipgw=10.0.2.2
      auth=10.0.2.15
      authdom=plan9
      fs=10.0.2.15
      cpu=10.0.2.15
      dns=75.75.75.75

    ```

*   Reboot the system.

    ```
    term% fshalt -r
    ```

## Connecting

tbd

[^1]: Special thanks to Youtube user C0tl43 and his video [Setting up a 9front 
      cpu+auth+fs standalone server](https://www.youtube.com/watch?v=PjVpB3SpAfQ),    
      which inspired and helped create this article.
