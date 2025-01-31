# DMVPN - Phase 3


# R11 - HUB - R11
```

int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp map multicast dynamic
tunnel source 1.1.1.2
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.11 255.255.255.0
ip nhrp redirect


ip route 10.10.50.0 255.255.255.0 172.16.1.5
ip route 10.10.51.0 255.255.255.0 172.16.1.14
ip route 172.16.100.0 255.255.255.0 172.16.1.17
ip route 172.16.150.0 255.255.255.0 172.16.1.17




```

## Spoke-R17
```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source serial 2/0
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.17 255.255.255.0
ip nhrp shortcut



ip route 10.10.50.0 255.255.255.0 172.16.1.11
ip route 10.10.51.0 255.255.255.0 172.16.1.11
ip route 10.10.10.0 255.255.255.0 172.16.1.11
ip route 10.10.20.0 255.255.255.0 172.16.1.11




```




## Spoke-R5
```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source serial 2/0
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.5 255.255.255.0
ip nhrp shortcut



ip route 10.10.51.0 255.255.255.0 172.16.1.11
ip route 10.10.10.0 255.255.255.0 172.16.1.11
ip route 10.10.20.0 255.255.255.0 172.16.1.11
ip route 172.16.100.0 255.255.255.0 172.16.1.11
ip route 172.16.150.0 255.255.255.0 172.16.1.11


```


## Spoke-R14
```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source serial 2/0
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.14 255.255.255.0
ip nhrp shortcut



ip route 10.10.50.0 255.255.255.0 172.16.1.11
ip route 10.10.10.0 255.255.255.0 172.16.1.11
ip route 10.10.20.0 255.255.255.0 172.16.1.11
ip route 172.16.100.0 255.255.255.0 172.16.1.11
ip route 172.16.150.0 255.255.255.0 172.16.1.11



```


