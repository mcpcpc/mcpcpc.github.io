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

*   Close the Lish window and shutdown VM.
*   Start *installer* configuration.
*   Start a new Lish session, using Glish.

[^1]: https://www.linode.com/docs/guides/install-a-custom-distribution-on-a-linode
[^2]: http://9front.org/iso/
[^3]: http://fqa.9front.org/fqa4.html#4.3
