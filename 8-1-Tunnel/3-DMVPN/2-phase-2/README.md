# Phase2 dmvpn



## HUB 

```

int tun 1
ip address 172.16.1.11 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp map multicast dynamic
tunnel source 10.10.38.8
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360




```

## Spokes

```

int tun 1
ip address 172.16.1.17 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.1.2
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360


```