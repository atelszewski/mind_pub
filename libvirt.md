Libvirt
=======

## Create VM from XML

## Enable Virtio disk in LILO

```
boot = /dev/vda
disk = /dev/vda bios=0x80 max-partitions=7
```

## Clone machine without cloning disk images

> **WARNING:**
>
> Remember to update the _clone_ with appropriate disk files.
>
> This warning applies to _EFI NVRAM_ files as well.
> For example:
>
>     $ cp /usr/share/ovmf-x64/OVMF_VARS-pure-efi.fd \
>           ~/.config/libvirt/qemu/nvram/<clone_machine_name>_VARS.fd

```
$ virt-clone --check disk_size=off --auto-clone --print-xml        \
      --original=<source_machine_name> --name=<clone_machine_name> \
  | virsh define /dev/stdin --validate
```

## Use UEFI instead of BIOS

```
<os>
  ...
  <loader readonly='yes' type='pflash'>/usr/share/ovmf-x64/OVMF_CODE-pure-efi.fd</loader>
  <nvram>/home/username/.config/libvirt/qemu/nvram/machine_name_VARS.fd</nvram>
  ...
</os>
```

## Enable bi-directional audio (using PulseAudio on the host side)

1. Ensure host and guest are using the same sampling rate.

   - On Linux host verify _/etc/pulse/daemon.conf_ to contain the following line:

         default-sample-rate = 44100
         alternate-sample-rate = 48000

   - On Windows 10 guest:

       _[Windows Settings] -> System -> Sound -> [Output] -> Device properties -> [Related Settings] ->_
       _Additional device properties -> Advanced -> [16 bit, 44100 Hz (CD Quality)]_

       Repeat the same procedure for _[Input]_ as well.

2. Libvirt XML.

> **WARNING:**
> 
> Make sure to use the correct domain XML schema, otherwise _qemu:commandline_
> will not work as expected.

```
<domain type='kvm' xmlns:qemu='http://libvirt.org/schemas/domain/qemu/1.0'>
  ...
  <qemu:commandline>
    <qemu:arg value='-device'/>
    <qemu:arg value='ich9-intel-hda,bus=pcie.0,addr=0x1b'/>
    <qemu:arg value='-device'/>
    <qemu:arg value='hda-micro,audiodev=hda'/>
    <qemu:arg value='-audiodev'/>
    <qemu:arg value='pa,id=hda,server=unix:/run/user/1010/pulse/native'/>
  </qemu:commandline>
</domain>
```

> **TODO:**
> 
> The above snippet is not optimal, because it uses deprecated QEMU command line
> arguments for setting up the device and/or properties.
> Find the modern way to do the thing.

## Convert _libvirt_ XML to QEMU command line

> **WARNING:**
> 
> Due to a bug, the below command will not work in _libvirt_ before version 4.6.
> 
> `$ virsh domxml-to-native qemu-argv --domain domain_name`

## Commands

### Balloon lower and then increase guest memory

```
$ virsh setmem buildbot 4GiB --live
$ virsh setmem buildbot 5GiB --live
```
