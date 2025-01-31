# DMVPN FVRF




# R11-HQ
```

vrf definition ISP1
 !
 address-family ipv4
 exit-address-family
!


interface Serial2/0
 vrf forwarding ISP1
 ip address 1.1.1.2 255.255.255.252
 no sh

      
        
ip route vrf ISP1 0.0.0.0 0.0.0.0 1.1.1.1





int tun 1
tunnel vrf ISP1
ip address 172.16.1.11 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp map multicast dynamic
tunnel source 1.1.1.2
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360






router eig eig-dmvnp
address-family ipv4 unicast as 2
network 10.10.10.1 0.0.0.0
network 10.10.20.1 0.0.0.0
network 172.16.1.11 0.0.0.0
af-interface tunnel 1
no split-horizon
no next-hop-self
exit
af-interface ethernet 0/0.10
passive-interface
exit
af-interface ethernet 0/0.20
passive-interface
exit





```

# R17-Spoke

```

vrf definition ISP1
 !
 address-family ipv4
 exit-address-family
!

interface Serial2/0
 vrf forwarding ISP1
 ip address 1.1.4.3 255.255.255.0
 no sh

      
        
ip route vrf ISP1 0.0.0.0 0.0.0.0 1.1.4.1



int tun 1
tunnel vrf ISP1
ip address 172.16.1.17 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.4.3
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360




router eig eig-dmvnp
address-family ipv4 unicast as 2
network 172.16.100.1 0.0.0.0
network 172.16.150.1 0.0.0.0
network 172.16.1.17 0.0.0.0
af-interface ethernet 0/0
passive-interface
exit



```





# R5-Spoke

```

vrf definition ISP1
 !
 address-family ipv4
 exit-address-family
!

interface Serial2/0
 vrf forwarding ISP1
 ip address 1.1.2.2 255.255.255.252
 no sh

      
        
ip route vrf ISP1 0.0.0.0 0.0.0.0 1.1.2.1



int tun 1
tunnel vrf ISP1
ip address 172.16.1.5 255.255.255.0
ip nhrp authentication secret
ip nhrp network-id 1
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.2.2
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360




router eig eig-dmvnp
address-family ipv4 unicast as 2
network 10.10.50.1 0.0.0.0
network 172.16.1.5 0.0.0.0
af-interface ethernet 0/0
passive-interface
exit



```
