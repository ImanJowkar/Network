# Port-Forwarding

![img](img/1.png)


# Mikrotik ISP1

```
system/identity/set name=ISP


ip dhcp-client/add interface=ether3 add-default-route=yes use-peer-ntp=yes use-peer-dns=yes


ip address/add interface=ether1 address=172.16.1.1/30



ip firewall/nat/add chain=srcnat action=masquerade
```



# R5

```
interface fastEthernet 1/1
no sh
ip addr 172.16.1.2 255.255.255.252

ip route 0.0.0.0 0.0.0.0 172.16.1.1



int fa 1/0
no sh
ip addr 192.168.86.1 255.255.255.0


int fa 0/0
no sh 
ip addr 192.168.85.1 255.255.255.0



int fa 1/1
ip nat outside


int range fa 0/0, fa 1/0
ip nat inside


ip access-list standard NAT-ACL
permit 192.168.85.0 0.0.0.255



ip nat inside source list NAT-ACL interface fastEthernet 1/1


! port forwarding
ip nat inside source static tcp 192.168.85.11 80 172.16.1.2 8080


do sh ip nat translations 
```