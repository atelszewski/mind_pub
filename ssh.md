# SSH (Secure Shell)

## Key management

### Add remote host key to the known_hosts file

Get the remote key with:

    $ ssh-keyscan [-t rsa] github.com [-p 22]

Verify the key by piping it to `ssh-keygen`:

    $ cat << EOF | ssh-keygen -l -f -
    <KEY_GOES_HERE>
    EOF

Paste the key into `~/.ssh/known_hosts`.

## Disconnect a locked-up session

To disconnect a locked-up ssh session, type: `enter ~ .`
