# screen (GNU Screen)

## Serial port setup

```Bash
screen /dev/ttyUSB0 115200,-crtscts,-ixoff,-ixon

# Options:
#
# 115200: Baud rate.
# -crtscts: Disable RTS/CTS handshaking.
# -ixoff: Disable sending of start/stop characters.
# -ixon: Disable XON/XOFF flow control.
```

Kill the window with `Ctrl+a k`.

## Filter the output through a command

```
: exec !.. sed -E "/(error_ctrl_loop::process)|(error_ctrl::loop_run)/d"
```

Remove the filter with the `kill` command, i.e. `Ctrl+a k`.
