# Pretty Good Privacy (PGP) / GnuPG

## Working with _NOT IMPORTED_ key files

### Brief peek at an OpenPGP key file

    $ gpg -vv keyfile.asc

### Verify and list the fingerprint of the key

    $ gpg --with-fingerprint --with-subkey-fingerprint keyfile.asc

## Working with imported keys

### Listing keys

    $ gpg2 --list-keys

### Change the passphrase of the secret key

    $ gpg2 --edit-key your-key-id-here
    gpg> passwd
    gpg> save
    gpg> quit
