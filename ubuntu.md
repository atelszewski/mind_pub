Ubuntu tips
===========

# Network

## Firewall

1. Enable _ufw_ (Uncomplicated Firewall)

       $ ufw enable

2. Check status / applied rules

       $ ufw status
       Status: active
       
       To                         Action      From
       --                         ------      ----
       22/tcp                     ALLOW       Anywhere
       22/tcp (v6)                ALLOW       Anywhere (v6)

3. Allow connections

       $ ufw allow ssh
       $ ufw allow 53825/udp

4. Detele rules

       $ ufw delete allow ssh
       $ ufw status numbered
       $ ufw delete [number]

5. Allow routing

       $ ufw route allow in on eth0 out on eth1 to 12.34.45.67 port 80 proto tcp
       $ ufw route allow in on eth1 out on eth2
       $ sysctl -w net/ipv4/ip_forward=1
       $ sysctl -w net/ipv6/conf/default/forwarding=1
       $ sysctl -w net/ipv6/conf/all/forwarding=1

## Enable SSH

    $ systemctl enable ssh
