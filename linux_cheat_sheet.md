Linux cheat sheet
=================

# Filesystem permissions operations

## Set permissions to 0700 for dirs/execs and 0600 for regular files

    $ chmod -R u-s-t+r+w+X,go-s-t-r-w-x .

## Set permissions to 0755 for dirs/execs and 0644 for regular files

    $ chmod -R a-st,u+rwX,go-w+rX .

## Remove ACL-s recursively

    $ setfacl -R -b .

# Disk drive operations

## Re-scan SCSI for drives

    $ scsihost=1
    $ echo '- - -' > /sys/class/scsi_host/host${scsihost}/scan

## Eject drive, e.g. before hot-un-plug)

    $ dev=vda
    $ echo 1 > /sys/block/${dev}/device/delete
