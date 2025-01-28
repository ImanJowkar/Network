# NAT (Network Address Translation)

![img](1.png)

```


ip route 0.0.0.0 0.0.0.0 192.168.1.1

interface Ethernet1/1
 ip address 192.168.1.2 255.255.255.252
 ip nat outside



interface Ethernet0/0.10
 encapsulation dot1Q 10
 ip address 10.10.10.1 255.255.255.0
 ip nat inside

interface Ethernet0/0.20
 encapsulation dot1Q 20
 ip address 10.10.20.1 255.255.255.0
 ip nat inside


ip access-list standard NAT-ACL
 permit 10.10.10.0 0.0.0.255






ip nat inside source list NAT-ACL interface ethernet 1/1 overload		# inside = source NAT











```