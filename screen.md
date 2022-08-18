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
