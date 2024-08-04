# BFD

![img](img/1.png)

# R1

```
int fa 1/0
no sh
ip addr 10.10.40.1 255.255.255.252

int fa 1/1
no sh
ip addr 10.10.50.1 255.255.255.252

interface fastEthernet 0/0
no sh

interface fastEthernet 0/0.10
encapsulation dot1Q 10
ip addr 10.10.10.1 255.255.255.0


interface fastEthernet 0/0.20
encapsulation dot1Q 20
ip addr 10.10.20.1 255.255.255.0




ip route 10.10.90.0 255.255.255.0 fastEthernet 1/0 10.10.40.2
ip route static bfd fastEthernet 1/0 10.10.40.2
int fast 1/0
bfd interval 333 min_rx 333 multiplier 3


ip route 10.10.90.0 255.255.255.0 fastEthernet 1/1 10.10.50.2
ip route static bfd fastEthernet 1/1 10.10.50.2
int fast 1/1
bfd interval 333 min_rx 333 multiplier 3









```

# R2

```

int fa 0/0
no sh
ip addr 10.10.40.2 255.255.255.252

int fa 1/0
no sh
ip addr 10.10.50.2 255.255.255.252

int fa 1/1
no sh
ip addr 10.10.90.1 255.255.255.0


ip route 0.0.0.0 0.0.0.0 fast 0/0 10.10.40.1
ip route static bfd fastEthernet 0/0 10.10.40.1
int fast 0/0
bfd interval 333 min_rx 333 multiplier 3


ip route 0.0.0.0 0.0.0.0 fast 1/0 10.10.50.1
ip route static bfd fastEthernet 1/0 10.10.50.1
int fast 1/0
bfd interval 333 min_rx 333 multiplier 3




```



# IOU1

```

int eth 0/0
switchport trunk encapsulation dot1q 
switchport mode trunk 


vlan 10,20
exit

int eth 0/1
switchport mode access 
switchport access vlan 10


int eth 0/2
switchport mode access 
switchport access vlan 20


```