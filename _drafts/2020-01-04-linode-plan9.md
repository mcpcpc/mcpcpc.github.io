## Prepare the Linode VM


## Installation
*   Start Rescue Mode.
*   Once in Rescue Mode, download your installation media and copy it to your Installer disk.

    ```
    wget http://9front.org/iso/9front-8013.d9e940a768d1.amd64.iso.gz -q -O -| funzip | dd of=/dev/sda
    ```
    
*   Empty the cache so that you have enough space to unpack and install the image.

    ```
    sync; echo 3 > /proc/sys/vm/drop_caches
    ```

*   Close the Lish console and Power Off the VM.
*   Start *installer* configuration.
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
