ADB (Android Debug Bridge)
==========================

## List packages

    $ adb shell pm list packages

## Disable package for a particular user

In this example, disabled *GMail* package.

    $ adb shell pm disable-user --user 0 com.google.android.gm

## Enable package for a particular user

    $ adb shell pm enable com.google.android.gm
