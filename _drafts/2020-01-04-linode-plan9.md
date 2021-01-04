---
layout: post
title: 9front and Linode
description: Installing and configuring 9front on Linode virtual machine.
---

## Why 9front?

Because we can.

## Preparing the Linode VM

*   Create a new Linode. I would recommend the Shared CPU "Nanode 1GB" plan, which is 1GB of RAM, 
    25GB of Storage and 1 CPU for $5 USD/month.
*   Click the **Storage** tab and press *Add a Disk*.
*   Specify a Label name, partition size (25600 MB recommended) and press *Create*.
*   Click the **Configurations** tab and press *Add a Configuration*.
*   Specify a Label name and the following recommended parameters and press *Submit*.

    |parameter              |value                                                              |
    |-----------------------|-------------------------------------------------------------------|
    |VM Mode                |Paravirtualization                                                 |
    |Boot Settings          |Direct Disk                                                        |
    |Run Level              |Run Default Level                                                  |
    |Memory Limit           |Do not set any limits on memory usage                              |
    |Block Device Assignment|`/dev/sda` should mach the Label name created in the previous step.|
    |Root Device            |/dev/sda                                                           |
    |Filesystem/Boot Helpers|All Disabled                                                       |

*   Click the *Settings* tab, and disable the Shutdown Watchdog.

## Installation and First Boot
*   With the VM powered off, start Rescue Mode.
*   Once in Rescue Mode, download your installation media and copy it to your Installer disk. Refer 
    to one of the 9front mirrors for the latest image [^2].

    ```
    wget http://9front.org/iso/9front-8013.d9e940a768d1.amd64.iso.gz -q -O -| funzip | dd of=/dev/sda
    ```
    
*   Empty the cache so that you have enough space to unpack and install the image.

    ```
    sync; echo 3 > /proc/sys/vm/drop_caches
    ```

*   Close the Lish console and press the *Power Off* button.
*   Press the **Configurations** tab and press the *Boot* button.
*   Start a new LISH console using **Glish**.
*   At this point, you should be able to follow the general "9front Installation Guide" [^3] with 
    little motification. At the conclusion of the installation the VM should automatically be 
    restarted.
*   Close the current LISH window. Upon refreshing your browser window, you may
    see that the VM is powered off. At this point, you can *Power On* your VM and launch a new LISH
    console. 

[^1]: https://www.linode.com/docs/guides/install-a-custom-distribution-on-a-linode
[^2]: http://9front.org/iso/
[^3]: http://fqa.9front.org/fqa4.html#4.3
