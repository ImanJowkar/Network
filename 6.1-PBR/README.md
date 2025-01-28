

### PBR - select all - protocol

# SW5
! for use in switch change sdm template 


```
ip access-list extended my-pbr-acl
 permit ip host 10.10.150.50 host 192.168.44.10

ip access-list extended my-pbr-acl-vlan-20
 permit tcp 10.10.20.0 0.0.0.255 host 192.168.45.10 eq www


route-map rm-PBR-vlan-20 permit 50
 match ip address my-pbr-acl-vlan-20
 set ip next-hop 10.10.45.4


route-map rm-PBR permit 50
 match ip address my-pbr-acl
 set ip next-hop 10.10.45.4



interface Vlan20
 ip policy route-map rm-PBR-vlan-20


     
interface Vlan150
 ip policy route-map rm-PBR

```


# R3
```

ip access-list extended my-pbr-acl
 permit ip host 192.168.44.10 host 10.10.150.50


ip access-list extended my-pbr-acl-vlan-20
 permit tcp host 192.168.45.10 eq www 10.10.20.0 0.0.0.255



route-map rm-PBR-vlan-20 permit 50
 match ip address my-pbr-acl-vlan-20
 set ip next-hop 10.10.34.4


route-map rm-PBR permit 50
 match ip address my-pbr-acl
 set ip next-hop 10.10.34.4



interface Ethernet0/0.44
 ip policy route-map rm-PBR
  
interface Ethernet0/0.45
 ip policy route-map rm-PBR-vlan-20




```


# PBR with ip sla track



##### SW5
```


ip access-list extended my-pbr-acl
 permit ip host 10.10.150.50 host 192.168.44.10

ip access-list extended my-pbr-acl-vlan-20
 permit tcp 10.10.20.0 0.0.0.255 host 192.168.45.10 eq www








int loopback 100
 ip addr 192.168.5.5 255.255.255.255

ip route 192.168.3.3 255.255.255.255 10.10.45.4



ip sla 1  
 icmp-echo 192.168.3.3 source-interface Loopback100
  frequency 5

ip sla schedule 1 start-time now life forever

track  1 ip sla 1
 delay down 10 up 10






route-map rm-PBR-vlan-20 permit 50
 match ip address my-pbr-acl-vlan-20
 set ip next-hop verify-availability 10.10.45.4 1 track 1


route-map rm-PBR permit 50
 match ip address my-pbr-acl
 set ip next-hop verify-availability 10.10.45.4 1 track 1



interface Vlan20
 ip policy route-map rm-PBR-vlan-20


     
interface Vlan150
 ip policy route-map rm-PBR




```



##### R4

```
ip route 192.168.3.3 255.255.255.255 10.10.34.3
ip route 192.168.5.5 255.255.255.255 10.10.45.5


```



##### R3

```

ip access-list extended my-pbr-acl
 permit ip host 192.168.44.10 host 10.10.150.50


ip access-list extended my-pbr-acl-vlan-20
 permit tcp host 192.168.45.10 eq www 10.10.20.0 0.0.0.255





int loopback 100
 ip addr 192.168.3.3 255.255.255.255


ip route 192.168.5.5 255.255.255.255 10.10.34.4



ip sla 1  
 icmp-echo 192.168.5.5 source-interface Loopback100
  frequency 5

ip sla schedule 1 start-time now life forever

track  1 ip sla 1
 delay down 10 up 10



route-map rm-PBR-vlan-20 permit 50
 match ip address my-pbr-acl-vlan-20
 set ip next-hop verify-availability 10.10.34.4 1 track 1


route-map rm-PBR permit 50
 match ip address my-pbr-acl
 set ip next-hop verify-availability 10.10.34.4 1 track 1



interface Ethernet0/0.44
 ip policy route-map rm-PBR
  
interface Ethernet0/0.45
 ip policy route-map rm-PBR-vlan-20





```




### set route-map on router itself


```

ip access-list extended PBR-ACL
permit ip 10.10.10.0 0.0.0.255 10.10.50.0 0.0.0.255




route-map PBR-RP permit 10
match ip address PBR-ACL
set ip next-hop verify-availability 10.10.39.3 1 track 1
exit


ip local policy route-map PBR-RP

```