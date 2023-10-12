# SW1 config
```
hostname sw1
interface fastEthernet 0/1
switchport mode trunk


vlan 10
vlan 11
exit


interface range fastEthernet 0/2-3
switchport mode access
switchport access vlan 10
exit


interface range fastEthernet 0/4-5
switchport mode access
switchport access vlan 11
exit



```


# R1 config
```
hostname R1


interface fastEthernet 0/0
no sh
exit

interface fastEthernet 0/0.10
encapsulation dot1Q 10
ip address 172.16.10.1 255.255.255.224

exit

interface fastEthernet 0/0.11
encapsulation dot1Q 11
ip address 172.16.11.1 255.255.255.224



ip dhcp pool vlan10
network 172.16.10.0 255.255.255.224
dns-server 192.168.80.2
default-router 172.16.10.1


ip dhcp pool vlan11
network 172.16.11.0 255.255.255.224
dns-server 192.168.80.2
default-router 172.16.11.1

exit

ip dhcp excluded-address 172.16.11.1 172.16.11.2
ip dhcp excluded-address 172.16.10.1 172.16.10.2


interface fastEthernet 0/1
no sh
ip address 214.65.87.5 255.255.255.252



interface fastEthernet 1/0
no sh
ip address 54.1.85.1 255.255.255.252


interface fastEthernet 1/1
no sh
ip address 9.4.8.1 255.255.255.252



router rip
 version 2
 network 9.0.0.0
 network 54.0.0.0
 network 172.16.0.0
 network 214.65.87.0
 no auto-summary



```



# R2

```
interface fastEthernet 0/0
no sh
ip address 214.65.87.6 255.255.255.252
exit

interface fastEthernet 0/1
no sh
ip address 154.65.21.5 255.255.255.252



router rip
 version 2
 network 154.65.0.0
 network 214.65.87.0
 no auto-summary



```



# R3

```

hostname R3


interface fastEthernet 0/0
no sh
ip address 154.65.21.6 255.255.255.252


interface fastEthernet 0/1
no sh
ip address 54.1.85.2 255.255.255.252


interface fastEthernet 1/1
no sh
ip address 5.2.2.2 255.255.255.252



interface fastEthernet 1/0
no sh
ip address 192.168.80.1 255.255.255.248



router rip
 version 2
 network 5.0.0.0
 network 54.0.0.0
 network 154.65.0.0
 network 192.168.80.0
 no auto-summary


```



# R4

```
hostname R4


interface fastEthernet 0/1
no sh
ip address 10.10.10.1 255.255.255.240


interface fastEthernet 0/0
no sh
ip address 5.2.2.1 255.255.255.252



interface fastEthernet 1/0
no sh
ip address 9.4.8.2 255.255.255.252




router rip
 version 2
 network 5.0.0.0
 network 9.0.0.0
 network 10.0.0.0
 no auto-summary






```
