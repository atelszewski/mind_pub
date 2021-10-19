Linux Disk / Block device UUID manipulation
===========================================

# Change UUID of ext* filesystem

    $ tune2fs /dev/sdxY -U abcdefgh-abcd-1234-1234-123456789012

# Change UUID of LUKS device

    $ cryptsetup luksUUID /dev/sdxY --uuid abcdefgh-abcd-1234-1234-123456789012

# Change UUID of VFAT filesystem

> **NOTE:**
> 
> Volume ID must be a hexadecimal number, without a dash '-'.

    $ dosfslabel --volume-id /dev/sdxY 12345679
