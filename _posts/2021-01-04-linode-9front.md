---
layout: post
title: Installing 9front OS on a Linode VM
description: Installing and configuring 9front operating system on Linode virtual machine.
---

![glenda](/assets/glenda_space_medium.jpg)

Why install 9front on a Linode virtual machine? Because we can!

*Note that if you are new to Linode and are looking to sign up, then please 
consider doing so using my referral link
[here](https://www.linode.com/?r=0c625ecd8478eb827df57d2e2ffa095759d089ab)
(which helps support me and my many projects).*

## Preparing the Linode VM

*   Create a new Linode virtual machine. I would recommend starting with the 
    Shared CPU "Nanode 1GB" plan (which is 1GB of RAM, 25GB of Storage and 1 CPU 
    for 5 USD per month).
*   Click the **Storage** tab and press *Add a Disk*. Specify a Label name,
    raw format type and the partition size (assuming you chose the "Nanode 1GB"
    plan, I would recommend using 25600MB) and press *Create*.
*   Click the **Configurations** tab and press *Add a Configuration*. Specify a
    Label name and the following recommended parameters and press *Submit*.

    |parameter              |value                                             |
    |-----------------------|--------------------------------------------------|
    |VM Mode                |Paravirtualization                                |
    |Boot Settings          |Direct Disk                                       |
    |Run Level              |Run Default Level                                 |
    |Memory Limit           |Do not set any limits on memory usage             |
    |Block Device Assignment|"/dev/sda" matches the *Storage* tab Label name.  |
    |Root Device            |/dev/sda                                          |
    |Filesystem/Boot Helpers|All options disabled                              |

*   Click the *Settings* tab, and disable the Shutdown Watchdog.

## Installation and First Boot

*   With the VM powered off, start Rescue mode.
*   Open a new LISH console window. Once in Rescue mode, download your
    installation media and copy it to your boot disk. Refer to one of the 9front 
    mirrors for the latest image[^1].

    ```shell
    wget http://9front.org/iso/9front-8013.d9e940a768d1.amd64.iso.gz -q -O -| funzip | dd of=/dev/sda
    ```
    
*   Empty the cache so that you have enough space to unpack and install the
    image.

    ```shell
    sync; echo 3 > /proc/sys/vm/drop_caches
    ```

*   Close the LISH console window and press the *Power Off* button.
*   Press the **Configurations** tab and press the *Boot* button.
*   Start a new LISH console (Glish). At this point, you should be able to 
    follow the general "9front Installation Guide"[^2] for installing 9front OS 
    to the main partition. At the conclusion of the installation the VM should 
    automatically be restarted.
*   Close the current LISH window. Upon refreshing your browser window, you may
    see that the VM is powered off. Press the *Power On* button and launch a new 
    LISH console window (glish). At this point, you should see the fully-
    functional rio window manger in a pseudoterminal.

## The Result

If all went well, then you should be seeing the rio window manager with a 
termimal window and process monitor in your LISH console (something like the 
screenshot below).

![9front in a pseudo-tty](/assets/9front-mothra.png)

## Next Steps

There are *many* resources at your disposal if you are looking to learn more 
about 9front or plan9. Here are some of the best that I have found: 

*   Official 9front FAQ, [9front.org](http://fqa.9front.org)
*   "Plan9 Desktop Guide", [pspodcasting.net](https://pspodcasting.net/dan/blog/2019/plan9_desktop.html)

---

[^1]: 9front ISO mirror, http://9front.org/iso/
[^2]: "9front Installation Guide", http://fqa.9front.org/fqa4.html#4.3
