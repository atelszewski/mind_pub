# Media Transfer Protocol (MTP), GVFS

**NOTE:** The following *gvfs-mount* mount method does not allow to use Krusader nor
Konqueror to copy files. Plain `cp` in the terminal works fine, though.

## Find MTP device

    $ lsusb
    (..)
    Bus 001 Device 071: ID 2717:ff40
    (..)

## Mount MTP device

The MTP device will be mounted under *~/.gvfs* directory.

    $ gvfs-mount 'mtp://[usb:001,071]'

## Unmount MTP device

    $ gvfs-mount -u 'mtp://[usb:001,071]'

**NOTE:** After unmounting, mobile phone disables MTP.
To mount again, MTP has to be re-enabled on the mobile phone.
Pay attenetion to the fact that **USB device number will change** on the host.

## Sync music using *rsync*

    $ rsync -v --progress --delete-before -c -r -l ~/music/ \
          ~/.gvfs/mtp\:host\=%5Busb%3A001%2C080%5D/Internal\ shared\ storage/Music/
