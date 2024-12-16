
# R8-HQ

```

int fa 0/0
ip addr 10.10.38.8 255.255.255.0
no sh

ip route 0.0.0.0 0.0.0.0 10.10.38.3






int tun 1
ip address 172.16.1.8 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp map multicast dynamic
tunnel source 10.10.38.8
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360






int fa 1/0
no sh
ip addr 10.10.8.1 255.255.255.0




do sh dmvpn







router eig eig-dmvnp
address-family ipv4 unicast as 2
network 10.10.8.1 0.0.0.0
network 172.16.1.8 0.0.0.0
af-interface tunnel 1
no split-horizon
no next-hop-self

```


# R5-Spoke

```

int fa 0/0
ip addr 10.10.45.5 255.255.255.0
no sh

ip route 0.0.0.0 0.0.0.0 10.10.45.4


int tun 1
ip address 172.16.1.5 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp nhs 172.16.1.8
ip nhrp map 172.16.1.8 10.10.38.8
ip nhrp map multicast 10.10.38.8
tunnel source 10.10.45.5
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360


int fa 1/0
no sh
ip addr 10.10.5.1 255.255.255.0


do sh dmvpn




router eig eig-dmvnp
address-family ipv4 unicast as 2
network 10.10.5.1 0.0.0.0
network 172.16.1.5 0.0.0.0






```
