Wireguard secure network tunnel
===============================

# Server

```
$ umask 077
$ cd /etc/wireguard
$ wg genkey | tee wg0key | wg pubkey > wg0key.pub

$ cat << EOF > /etc/wireguard/wg0.conf
[Interface]
Address = 192.168.200.1/32
ListenPort = 53825
PrivateKey = private_key_from[server wg0key file]

[Peer]
AllowedIPs = 192.168.200.2/32
PublicKey = public_key_from[client wg0key.pub file]
EOF
```

# Client

```
$ umask 077
$ cd /etc/wireguard
$ wg genkey | tee wg0key | wg pubkey > wg0key.pub

$ cat << EOF > /etc/wireguard/wg0.conf
[Interface]
Address = 192.168.200.2/32
PrivateKey = private_key_from[client wg0key file]

[Peer]
Endpoint = server_address:server_port
AllowedIPs = 192.168.200.1/32
PublicKey = public_key_from[server wg0key.pub file]
PersistentKeepalive = 12
EOF
```
