# GRUB bootloader

```bash
grub-install                   \
    --target=x86_64-efi        \
    --efi-directory=/boot/efi  \
    --bootloader-id=grub       \
    --boot-directory=/boot/efi \
    --removable
```
