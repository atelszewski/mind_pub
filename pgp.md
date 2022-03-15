Pretty Good Privacy (PGP) / GnuPG (GPG)
=======================================

## Primary key and subkey

It is possible to create private keys in a way so that they have a particular
relationship.

Namely, it is possible to create first private key, called _primary key_,
and then a second private key, called _subkey_, that is derived from
the _primary key_.

The benefit of this scheme is that:

- subkey is like a normal key in that it can be used for signing or encryption,
- primary key can reside on an isolated machine and is only used for deriving
  subkey(s),
- if a subkey is lost or compromised, it is only the subkey that needs
  to be revoked -- and a new subkey can be again derived from the _safe_
  primary key.

One can think of the above as of a _Certification Authority_, where _root_ key
is (should be) only used to sign _intermediate_ keys, which in turn are used
to sign _end entities_ keys.

GnuPG actually uses a signing-only key as the _primary_ key, and creates
an encryption _subkey_ automatically. Without a subkey for _encryption_,
you can't have encrypted e-mails with GnuPG at all.

References:

- [Using OpenPGP subkeys in Debian development](https://wiki.debian.org/Subkeys)

## Certification vs signing

_Signing_ is an action against arbitrary data. _Certification_ is the signing
of another key. Ironically, the act of certifying a key is universally called
_key signing_.

References:

- [Anatomy of a GPG Key](https://davesteele.github.io/gpg/2014/09/20/anatomy-of-a-gpg-key/)

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
