sed - stream editor for filtering and transforming text
=======================================================

# Use submatch (aka capture group)

Replace all `*VIRTIO*=m` with `*VIRTIO*=y`:

    $ sed -E -e 's/(.*VIRTIO.*)=m/\1=y/g' .config
