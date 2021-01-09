---
type: post
title: plan9 and Linode: Post-Install
description:
---

## Cpu and Auth Server Configuration

*   Mount `9fat` and make a copy of your plan9.ini file.
```
9fs 9fat
cd /n/9fat
cp plan9.ini plan9.ini.old
```

*   Invoke the dhcpcd server and print the configured network database information.  
    Note the values for `ip=`, `ipmask=`, `ipgw=` as these will be used later.

    ```
    term% ip/ipconfig
    term% cat /net/ndb
    ip=10.0.2.15 ipmask=255.255.255.0 ipgw=10.0.2.2
      sys=cirno
      dom=cirno.hsd1.wa.comcast.net
    ```

*   Open the plan9.ini file in your preferred editor (i.e. sam, acme, ed).

  ```
  sam plan9.ini
  ```

*   Set the bootargs, default hostowner, auth, cpu, authdom and service to cpu server.

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
* Configure the auth server non-volitile ram host owner, name and password key.

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

* Start keyfs, which needs to be loaded every time you want to modify the users key.

```
term% auth/keyfs
```

* Modify the user key for glenda:

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

* Invoke `auth/enable` on glenda.

```
term% auth/enable glenda
```

* Open the network database.

```
sam /lib/ndb/local
```

* Scroll to the bottom of the file and add the authdom, 

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

