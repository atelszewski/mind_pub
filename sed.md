sed - stream editor for filtering and transforming text
=======================================================

## Use submatch (aka capture group)

### To replace

Replace all `*VIRTIO*=m` with `*VIRTIO*=y`:

    $ sed -E -e 's/(.*VIRTIO.*)=m/\1=y/g' .config

### To print only the submatch portion

    $ sed -E -n -e 's/^Downstream port [1-3] is (ON|OFF)$/\1/p'
