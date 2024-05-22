
![img](img/1.png)



# R5
```
interface fa 1/0
ip address 10.10.5.1 255.255.255.0


interface fastEthernet 0/0
no sh
ip address 10.10.57.5 255.255.255.0



interface serial 5/0
no sh
ip address 10.10.58.5 255.255.255.0




router eigrp 1
network 10.10.5.1 0.0.0.0
network 10.10.57.5 0.0.0.0
network 10.10.58.5 0.0.0.0
passive-interface fastEthernet 1/0




```


# R7
```
interface fastEthernet 0/0
no sh
ip address 10.10.57.7 255.255.255.0


int fa 1/0
no sh
ip address 10.10.79.7 255.255.255.0




router eigrp 1
network 10.10.57.7 0.0.0.0
network 10.10.79.7 0.0.0.0

do sh ip eigrp interfaces
do sh ip protocol
do sh ip eigrp neighbors
do sh ip eigrp topology
do sh ip eigrp topology all-links







```


# R8

```
interface serial 5/1
no sh
ip address 10.10.89.8 255.255.255.0



interface serial 5/0
no sh
ip address 10.10.58.8 255.255.255.0




router eigrp myeig-1
address-family ipv4 unicast autonomous-system 1
network 10.10.58.8 0.0.0.0
network 10.10.89.8 0.0.0.0










```

# R9
```

int fa 1/0
no sh
ip address 10.10.79.9 255.255.255.0

interface serial 5/1
no sh
ip address 10.10.89.9 255.255.255.0


int fastEthernet 0/0
ip addr	10.10.9.1 255.255.255.0





router eigrp eig-1
address-family ipv4 unicast autonomous-system 1
network 10.10.79.9 0.0.0.0
network 10.10.89.9 0.0.0.0
network 10.10.9.1 0.0.0.0
af-interface fastEthernet 0/0
passive-interface
exit-af-interface


```