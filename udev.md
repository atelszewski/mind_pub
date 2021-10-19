udev - Linux devices dynamic management
=======================================

# Watch udev events

    $ udevadm monitor

# Reload rules

    $ udevadm control --reload

# Apply rules without re-connecting the device and for particular subsystem

    $ udevadm trigger --subsystem-match=usb
    $ udevadm trigger --subsystem-match=block /dev/sda

# Test rule's syntax

    $ udevadm test /dev/bus/usb/001/011

# Find out device properties

```bash
$ udevadm info --query=all --name=/dev/sda
P: /devices/pci0000:00/0000:00:17.0/ata3/host2/target2:0:0/2:0:0:0/block/sda
N: sda
S: disk/by-id/ata-HITACHI_HTS725050A9A364_110302PCK404GLH11YRJ
S: disk/by-id/wwn-0x5000cca67fce933a
E: DEVLINKS=/dev/disk/by-id/ata-HITACHI_HTS725050A9A364_110302PCK404GLH11YRJ /dev/disk/by-id/wwn-0x5000cca67fce933a
E: DEVNAME=/dev/sda
(..)
E: ID_SERIAL_SHORT=110302PCK404GLH11YRJ
(..)
E: SUBSYSTEM=block
(..)
```
