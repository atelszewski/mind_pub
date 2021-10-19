# ADB (Android Debug Bridge)

## List packages

    $ adb shell pm list packages

## Disable package for particular user

In this example, disabled *GMail* package.

    $ adb shell pm disable-user --user 0 com.google.android.gm
