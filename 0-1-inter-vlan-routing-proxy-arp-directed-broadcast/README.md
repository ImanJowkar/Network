# we have 2 method for intervlan routing 

* ROAS
* SVI



## routing-proxy-arp-directed-broadcast:
on the layer3 interface disable below 

```
# on normal router
int fa 0/0
no sh
ip addr 10.10.10.1 255.255.255.0
no ip directed-broadcast
no ip proxy-arp

# ROAS
int fa 0/0.10
encapsulation dotq1 10
no sh
ip addr 10.10.10.1 255.255.255.0
no ip directed-broadcast
no ip proxy-arp




on layer 3 switch (SVI)
int vlan 100
no ip directed-broadcast
no ip proxy-arp

```