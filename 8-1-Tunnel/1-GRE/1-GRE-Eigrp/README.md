## GRE-Eigrp




![img](img/1.png)

# R2

```

interface fastEthernet 0/0
ip address 10.10.23.2 255.255.255.0
no sh


interface fastEthernet 1/0
ip address 10.10.2.1 255.255.255.0
no sh


interface fastEthernet 1/1
ip address 10.10.22.1 255.255.255.0
no sh


router eigrp 1
network 10.10.23.2  0.0.0.0



int tunnel 1
tunnel source 10.10.23.2 
tunnel destin 10.10.34.4 
ip addr 10.10.10.1 255.255.255.252
ip mtu 1400
ip tcp adjust-mss 1360



router eigrp 2
network 10.10.10.1 0.0.0.0
network 10.10.2.1 0.0.0.0
network 10.10.22.1 0.0.0.0



```


# R3

```

interface fastEthernet 0/0
ip address 10.10.23.3 255.255.255.0
no sh


interface gig 2/0
ip address 10.10.34.3 255.255.255.0
no sh


router eigrp 1
network 10.10.23.3 0.0.0.0
network 10.10.34.3 0.0.0.0


```



# R4

```

interface gig 2/0
ip address 10.10.34.4 255.255.255.0
no sh


interface fastEthernet 1/0
ip address 10.10.4.1 255.255.255.0
no sh


interface fastEthernet 1/1
ip address 10.10.44.1 255.255.255.0
no sh

router eigrp 1
network 10.10.34.4 0.0.0.0



int tunnel 1
tunnel source 10.10.34.4 
tunnel destin 10.10.23.2 
ip addr 10.10.10.2 255.255.255.252
ip mtu 1400
ip tcp adjust-mss 1360



router eigrp 2
network 10.10.10.2 0.0.0.0
network 10.10.4.1 0.0.0.0
network 10.10.44.1 0.0.0.0


```