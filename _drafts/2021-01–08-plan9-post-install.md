---
type: post
title: plan9 and Linode: Post-Install
description:
---

## Cpu+auth Server Configuration

*   Mount `9fat` and make a copy of your plan9.ini file.
```
9fs 9fat
cd /n/9fat
cp plan9.ini plan9.ini.old
```

* Invoke the dhcpcd server and **record the IP address at setup**.

```
ip/ipconfig
cat /net/ndb
# should print several lines, but record the ip=XX.X.X.XX
```

* Open the plan9.ini file in your preferred editor (i.e. sam, acme, ed).

```
sam plan9.ini
```

* Set the bootargs as a default using nobootprompt

```
bootfile=9pc
bootargs=local!/dev/sdXX/fs -n 832
mouseport=ps2
monitor=vesa
vgasize=1024x768x16
nobootprompt=local!/dev/sdXX/fs -
user=glenda
auth=XX.X.X.XX
cpu=XX.X.X.XX
authdom=9plan
service=cpu
```



