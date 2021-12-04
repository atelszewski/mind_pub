rsync (a fast, versatile, remote and local file-copying tool)
=============================================================

## Transfer local file to remote site over SSH

    $ rsync -P -e ssh <src_file> <dest_user>@<dest_host>:<dest_file>

      -P:  show progress during transfer

## Sync local directory contents to remote site over SSH

> **WARNING**
>
> If a file doesn't exisit locally, but exists remotely, the remote file will
> be removed (implied by `--delete` option).

```
$ rsync -Pv -a --delete -e ssh <src_dir> <dest_user>@<dest_host>:<dest_dir>

  -P:        show progress during transfer
  -a:        archive mode
  --delete:  delete extraneous files from dest dirs
  -v:        increase verbosity
```
