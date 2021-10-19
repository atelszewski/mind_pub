# Device Mapper (DM) notes

## Logical Volume Manager (LVM)

### Create Physical Volume (PV):

    $ pvcreate /dev/vda
    $ pvdisplay /dev/vda
    $ pvs /dev/vda

### Create Volume Group (VG):

    $ vgcreate vg0 /dev/vda
    $ vgdisplay /dev/mapper/vg0
    $ vgs /dev/mapper/vg0

### Create Logical Volume (LV):

    $ lvcreate -L 8G -n lv0 vg0
    $ lvdisplay /dev/mapper/vg0-lv0
    $ lvs /dev/mapper/vg0-lv0

### Remove LV:

    $ lvremove /dev/mapper/vg0-lv0

### Remove VG:

    $ ...

### Remove PV:

    $ ...

### Rename VG

    $ vgrename /dev/vg_old /dev/vg_new

### Rename LV

    $ lvrename /dev/vg02/lv_old /dev/vg02/lv_new

### Create LV snapshot:

With 3 GiB worth of COW capacity.
`-s` stands for *snapshot*.
`-n` is the snapshot name.

    $ lvcreate -L 3G -s -n snap0 /dev/mapper/vg0-lv0

### Make LV read-only:

    $ lvchange -p r /dev/mapper/vg0-lv0

### Create thin LV pool:

Thin LV pool in required for thinly provisioned logical volume (LV).
`-T` stands for *thin*.

    $ lvcreate -L 8G -T vg0/pool0

### Create thin LV:

**Thin** LV requires thin pool.

Note that in this case you are specifying virtual size, and that you are specifying
a virtual size for the volume that is greater than the pool that contains it.

    $ lvcreate -V 128G -T vg0/pool0 -n tv0

### Create snapshot of thinly provisioned LV:

    $ lvcreate -s --name snap0 vg0/tv0

## Linux Unified Key Setup (LUKS)

### Create LUKS device:

Default encryption parameters depend on what is compiled-in.

    $ cryptsetup luksFormat /dev/vda1

### Activate LUKS device:

    $ cryptsetup luksOpen /dev/vda1 vda1plain

### List active LUKS devices:

    $ dmsetup ls --target crypt

## Virtual Data Optimizer (VDO)

Main features:

- block layer compression,
- block layer deduplication.

### Create VDO volume:

    $ vdo create --name=vdo0 --device=/dev/vda1 --vdoLogicalSize=128G

### VDO tuning:

[VDO performance tuning](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/storage_administration_guide/vdo-ig-tuning-vdo)
