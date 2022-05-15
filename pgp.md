Pretty Good Privacy (PGP) / GnuPG (GPG)
=======================================

## Primary (aka master) key and subkeys

It is possible to create private keys in a way so that they have a particular
relationship.

> **TODO**
>
> Statement: _Subkey derived from primary key_ is used a couple of times below.
> _Most probably_ this is not correct, that is, the _subkey_ can be _certified_
> by a _primary_ key, and not _derived_ from it.
> See [here](https://superuser.com/questions/1113308/what-is-the-relationship-between-an-openpgp-key-and-its-subkey).

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

## Signing vs certification

_Signing_ is an action against arbitrary data. _Certification_ is the signing
of another key. Ironically, the act of certifying a key is universally called
_key signing_.

References:

- [Anatomy of a GPG Key](https://davesteele.github.io/gpg/2014/09/20/anatomy-of-a-gpg-key/)

## Capabilities of a key pair

It is possible to set custom capabilities to the public/private key pair.

The following capabilities are available:

- `[C]ertify` (only for primary keys) - allows the key to create subkeys,
mandatory for primary keys.

- `[S]ign` - allows the key to create cryptographic signatures that others
can verify with the public key.

- `[E]ncrypt` - allows anyone to encrypt data with the public key, that only
the private key can decrypt.

- `[A]uthenticate` - allows the key to authenticate with various non-GnuPG
programs. The key can be used as e.g. an SSH key.

In the output of `gpg --list-keys` and elsewhere, these capabilities are shown
abbreviated to the first letter and in square brackets, e.g.:

- `[SC]` - meaning sign and certify capabilities,
- `[E]` - meaning encrypt capability.

References:

- [Arch Linux Wiki: GnuPG](https://wiki.archlinux.org/title/GnuPG)

## RSA-2048, 3072, 4096

NIST states that RSA-2048 gives roughly 112 bits of security and RSA-3072 gives
roughly 128. There is no formal recommendation on where RSA-4096 lies,
but the general consensus is that it would come in somewhere around 140 bits -
28 bits of improvement over RSA-2048. This is an improvement so marginal that
it's really not worth mentioning.

If you need more security than RSA-2048 offers, the way to go would be to switch
to elliptical curve cryptography - not to continue using RSA.

References:

- [GnuPG FAQ: 11.5 Why do people advise against using RSA-4096?](https://www.gnupg.org/faq/gnupg-faq.html#please_use_ecc)

## Per-device private subkeys

Having per-device private subkeys _would_ allow, in a case of a key compromise,
to revoke only the key used for the particular machine -- the one on which
the key has been compromised. All other keys _could_ be kept without revoking.

Due to the nature of implementation, the following good practices hold true:

- use a _per-device_ _signing_ subkey,
- use a _single_ _encryption_ subkey, _common_ to all devices.

It is _not_ a good practice to have a _per-device_ _encryption_ subkey.
This is because the _default enceryption key selection algorithm_ is to use
the newest key available. _Senders_ will simply use the newest key available
and there is not much that can be done about that.

> **TODO**
>
> Write note about signing key selection algo.

References:

- [Reddit: Good idea? Multiple encryption subkeys for different devices?](https://www.reddit.com/r/GnuPG/comments/2tvwn1/good_idea_multiple_encryption_subkeys_for/)
- [superuser: Why does GPG not decrypt with all subkeys?](https://superuser.com/questions/1054220/why-does-gpg-not-decrypt-with-all-subkeys)

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
