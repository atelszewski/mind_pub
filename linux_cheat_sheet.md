# Linux cheat sheet

# Filesystem permissions operations

## Set permissions to 0700 for dirs/execs and 0600 for regular files

    $ chmod -R u-s-t+r+w+X,go-s-t-r-w-x .

## Set permissions to 0755 for dirs/execs and 0644 for regular files

    $ chmod -R a-st,u+rwX,go-w+rX .

## Remove ACL-s recursively

    $ setfacl -R -b .

# Disk drive operations

## Re-scan SCSI for drives

    $ scsihost=1
    $ echo '- - -' > /sys/class/scsi_host/host${scsihost}/scan

## Eject drive, e.g. before hot-un-plug)

    $ dev=vda
    $ echo 1 > /sys/block/${dev}/device/delete

## MIME and file types

### Prevent wine from adding file associations:

http://askubuntu.com/questions/323437/how-to-prevent-wine-from-adding-file-associations/400430#400430

### Global MIME association

```
/usr/share/applications/mimeapps.list
```

## Download from YouTube and convert to audio

```
$ youtube-dl -F https://www.youtube.com/watch?v=Y1_VsyLAGuk
$ youtube-dl -f 171 https://www.youtube.com/watch?v=Y1_VsyLAGuk
$ ffmpeg -i "Burak Yeter - Tuesday ft. Danelle Sandoval-Y1_VsyLAGuk.webm" \
  -vn -acodec copy "Burak Yeter feat. Danelle Sandoval - Tuesday.ogg"
```

## Convert AAC to OGG

```
$ ffmpeg                                                                  \
      -i Shakira\ -\ Addicted\ To\ You.aac -codec:a libvorbis -qscale:a 6 \
      Shakira\ -\ Addicted\ To\ You.ogg
```
