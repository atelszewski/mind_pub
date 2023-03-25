# ADB (Android Debug Bridge)

> **NOTE**
>
> If `adb` complains about no `plugdev` group, first make sure that the phone
> USB connection is set to _File transfer_.

## Package management (pm)

### List packages

```
$ adb shell pm list packages
```

### Disable package for a particular user

In this example, disabled *GMail* package.

```
$ adb shell pm disable-user --user 0 com.google.android.gm
```

### Enable package for a particular user

```
$ adb shell pm enable com.google.android.gm
```

### Uninstall a package (root required)

> **WARNING**
>
> All **data** and cached will be removed as well. Pass `-k` option
> to keep the data and cache directories around after package removal.
>
> One might need to pass `--user X` argument if uninstalling fails
> with the following error: `Failure [DELETE_FAILED_INTERNAL_ERROR]`.

```
$ adb shell pm uninstall foundation.e.calendar
```
