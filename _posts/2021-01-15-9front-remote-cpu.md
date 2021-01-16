---
layout: post
title: "9front OS: Remote CPU"
description: Configuring a cpu, auth and fs server on the 9front operating system using Linode virtual machine.
---

If you were following along with my previous 
[article]({% post_url 2021-01-04-linode-9front %}), then you probably have a working 
installation of 9front OS on a Linode virtual machine that you can access through a 
LISH pseudoterminal. In the following article, I will attempt to walk through the 
process of creating a cpu, auth and fs server, which will allow you to spawn a virtual 
desktop from any non-9front OS using [drawterm](http://drawterm.9front.org)[^1]. 

## Prerequisits

For the purpose of this guide, I will assume that you are installed 9front using the
`hjfs` filesystem and default sysname (`cirno`) and hostowner (`glenda`).

## Step 1: Gather Information

Invoke the dhcpcd server. Print the configured network database information, noting 
the values for `ip=`, `ipmask=` and `ipgw=` (these will be used later for network 
configuration and connecting remotely).

```
term% ip/ipconfig
term% cat /net/ndb
ip=10.0.2.15 ipmask=255.255.255.0 ipgw=10.0.2.2
	sys=cirno
	dom=cirno.hsd1.wa.comcast.net
```

## Step 2: CPU Server

Mount the 9fat partition, add `service=cpu` to the *plan9.ini* file and reboot.

```
% 9fs 9fat
% sam -d /n/9fat/plan9.ini
-. /n/9fat/plan9.ini
a
service=cpu
.
w
q
% fshalt -r
```

Upon reboot, you will be prompted to configure the nvram auth credentials[^2].

```
bad nvram key               # You may not see these errors.
bad authentication id       # You may not see these errors.
bad authentication domain   # You may not see these errors.
authid: <glenda>
authdom: <9front>
secstore key:
password: <glenda's password>
```

## Step 3: Listing Ports

Edit you *plan9.ini* file again, specify the listing port and reboot. Do **not**  
modify the `-m XXX` value of bootargs.

```
% 9fs 9fat
% sam -d /n/9fat/plan9.ini
-. /n/9fat/plan9.ini
2
bootargs=local!/dev/sdXX/fs
c
bootargs=local!/dev/sdF0/fs -m 192 -A -a tcp!*!564
.
w
q
% fshalt -r
```
	
## Step 4: Network Configuration

Configure your network according to the parameters obtained in *Step 1* and reboot. 
Note the last value in `ip=` was changed to `0`. Leave the `ether=` values as is.

```
% sam -d /lib/ndb/local
-. /lib/ndb/local
33
# example: adjust to fit your network
34,47 p
auth=cirno authdom=9front
ipnet=9front ip=10.0.2.0 ipmask=255.255.255.0
	ipgw=10.0.2.2
	dns=4.2.2.2
	auth=cirno
	dnsdom=9front
	cpu=cirno
	fs=cirno
#
#ip=192.168.0.99 sys=cirno dom=cirno.9front ether=112233445566 
sys=cirno ether=52540000ee03
% fshalt -r
```

## Step 5: Connecting Remotely

From a non-plan9 OS, download and install the cpu client
[drawterm](http://drawterm.9front.org). Once installed, start drawterm and 
specify the server cpu IP address, user (glenda) and password when prompted.

![drawterm client session](/assets/drawterm-mothra.png)

Once connected, start webfs and rio window manager.[^3] 

```
webfs
rio -i riostart
```

## Credit

Special thanks to the following blogs and developers:

*   [Nicolas Montanaro](https://nicolasmontanaro.com/blog/9front-guide/)
*   [Roy Niang](https://royniang.com/cpu_auth.html)

[^1]: Note that the version linked is a fork of Russ CoX's drawterm.
[^2]: The `secstore key` and `password` are secret passwords of eight characters
      or more in length. The `password` is the password belonging to the authid 
      user on the auth server responsible for the authdom entered above. The  
      `secstore key` is the password of the user on the secure-store server 
      (Read: [FQA 7.4.3 - secstored](http://fqa.9front.org/fqa8.html#7.4.3)). If 
      the secstore client (Read: [FQA 8.4.7 - secstore](http://fqa.9front.org/
      fqa7.html#8.4.7)) is not being used on this machine (for example, if this 
      is the auth server where secstored will run), just hit enter at the 
      *secstore key:* prompt.
[^3]: These commands can be added to the host users profile (e.g. 
	  /usr/glenda/lib/profile` below `fn cpu% { $* }`.
