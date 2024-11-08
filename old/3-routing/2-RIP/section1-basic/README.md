# Example

![img](img/1.PNG)

### config static route

```

# config on R1
hostname R1
interface FastEthernet0/0
ip address 15.2.3.6 255.255.255.252

interface FastEthernet0/1
ip address 5.6.2.1 255.255.255.252


interface FastEthernet1/0
ip address 172.16.24.1 255.255.255.0


ip route 192.168.25.0 255.255.255.0 5.6.2.2 
ip route 10.10.10.0 255.255.255.0 15.2.3.5 


# config on R2
hostname R2
interface FastEthernet0/0
ip address 192.168.25.1 255.255.255.0

interface FastEthernet0/1
ip address 8.4.6.5 255.255.255.252

interface FastEthernet1/0
ip address 5.6.2.2 255.255.255.252

ip route 172.16.24.0 255.255.255.0 5.6.2.1 
ip route 10.10.10.0 255.255.255.0 8.4.6.6 



# config on R3
hostname R3
interface FastEthernet0/0
ip address 8.4.6.6 255.255.255.25

interface FastEthernet0/1
ip address 10.10.10.1 255.255.255.0

interface FastEthernet1/0
ip address 15.2.3.5 255.255.255.252


ip route 172.16.24.0 255.255.255.0 15.2.3.6
ip route 192.168.25.0 255.255.255.0 8.4.6.5 


```


### RIPv1 config
```

# config on R1
hostname R1
interface FastEthernet0/0
ip address 15.2.3.6 255.255.255.252

interface FastEthernet0/1
ip address 5.6.2.1 255.255.255.252


interface FastEthernet1/0
ip address 172.16.24.1 255.255.255.0


router rip
network 5.6.2.0
network 15.2.3.4
network 172.16.24.0


# config on R2
hostname R2
interface FastEthernet0/0
ip address 192.168.25.1 255.255.255.0

interface FastEthernet0/1
ip address 8.4.6.5 255.255.255.252

interface FastEthernet1/0
ip address 5.6.2.2 255.255.255.252


router rip
network  192.168.25.0
network 5.6.2.0
network 8.4.6.4




# config on R3
hostname R3
interface FastEthernet0/0
ip address 8.4.6.6 255.255.255.25

interface FastEthernet0/1
ip address 10.10.10.1 255.255.255.0

interface FastEthernet1/0
ip address 15.2.3.5 255.255.255.252


router rip
network 8.4.6.4
network 15.2.3.4
network 10.10.10.0



```


### RIPv2 config

```

# config on R1
hostname R1
interface FastEthernet0/0
ip address 15.2.3.6 255.255.255.252

interface FastEthernet0/1
ip address 5.6.2.1 255.255.255.252


interface FastEthernet1/0
ip address 172.16.24.1 255.255.255.0

router rip
network 5.6.2.0
network 15.2.3.4
network 172.16.24.0
version 2
no auto-summary




# config on R2
hostname R2
interface FastEthernet0/0
ip address 192.168.25.1 255.255.255.0

interface FastEthernet0/1
ip address 8.4.6.5 255.255.255.252

interface FastEthernet1/0
ip address 5.6.2.2 255.255.255.252



network  192.168.25.0
network 5.6.2.0
network 8.4.6.4
version 2
no auto-summary



# config on R3
hostname R3
interface FastEthernet0/0
ip address 8.4.6.6 255.255.255.25

interface FastEthernet0/1
ip address 10.10.10.1 255.255.255.0

interface FastEthernet1/0
ip address 15.2.3.5 255.255.255.252


network 8.4.6.4
network 15.2.3.4
network 10.10.10.0
version 2
no auto-summary



```

![img](img/2.PNG)