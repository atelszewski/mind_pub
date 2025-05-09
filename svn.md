Subversion (svn) VCS
====================

## Change working copy's remote directory location

Point local working copy's to a different remote directory:

    $ svn ls ^/
    $ svn switch ^/1.0.1


## Show log for a period of time

    $ svn log ^/                                     \
          -r "{2020-01-25 23:59}:{2019-12-26 00:00}" \
          --search <USERNAME>

## Show log limited by number of commits

    $ svn log -l 32

## Perform shallow checkout

    $ svn checkout --depth empty svn://<address>/<repo> <repo>
    $ svn update --set-depth infinity <repo>/<dir>

## Resolve conflict using text from file in working copy

    $ svn resolve --accept working \
          buildroot/package/ap_pairing/main.c
