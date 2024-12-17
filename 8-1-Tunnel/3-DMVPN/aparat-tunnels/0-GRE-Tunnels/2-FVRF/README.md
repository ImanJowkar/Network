# Multi WAN , FVRF + GRE 

![img](./1.png)


# R11

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




interface Tunnel0
 tunnel vrf ISP1
 ip address 172.16.1.11 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360
 tunnel source 1.1.1.2
 tunnel destination 1.1.4.3
 


router eigrp my-eigrp
address-family ipv4 unicast  autonomous-system 2
network 172.16.1.11 0.0.0.0
network 10.10.10.1 0.0.0.0
network 10.10.20.1 0.0.0.0


```

# R17

```

vrf definition ISP1
 !
 address-family ipv4
 exit-address-family
!

interface Serial2/0
 vrf forwarding ISP1
 no sh
 ip address 1.1.4.3 255.255.255.0

        

ip route vrf ISP1 0.0.0.0 0.0.0.0 1.1.4.1


interface Tunnel0
 tunnel vrf ISP1
 ip address 172.16.1.17 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360
 tunnel source 1.1.4.3
 tunnel destination 1.1.1.2




router eigrp my-eigrp
address-family ipv4 unicast  autonomous-system 2
network 172.16.1.17 0.0.0.0
network 172.16.150.1 0.0.0.0
network 172.16.100.1 0.0.0.0


```