# Network 


## common configuration of cisco devices:

![Cisco device modes](./image/1.png)
```
# switch between modes
---> enable ----> en
     disable

---> configure terminal ---> conf t

?  # help


```




# change hostname

```
hostname sw1   #change device name
no hostname    #reset hostname

```

 for exit when request send to the dns

```
ctrl+shift+6 

```

you can disable this feature by typing 

```
no ip domain-lookup

```

# for enable password 

```
enable password test
enable secret test
enable secret 5 $1$mERr$126VWMuSfhXn9GAlqkjPo/


```



# set password for console 
```
line console 0
password test
login


```


# how to create a user

```
username admin privilege 15 secret admin
username user1 privilege 1 secret user1

```





# save configs

```

do write
# or 
copy running-config startup-config
reload

```





# delete configs
```
erase startup-config
reload
show flash
delete vlan.dat
show flash
reload

```



```

show  running-config
do show run
show flash
```

# inspect the detail of a switch status
```
do show int fa0/1 switchport
```






# how to set IP address on router ports

```

interface gigabitEthernet 0/0/0
ip address 192.168.1.1 255.255.255.0
no sh
do show ip int bri
do show run

```




# cdp protocol, LLDP protocol
tip: cdp only works on cisco devices, but lldp works on all standard devices.


```
show cdp neighbors

```

# for using lldp, first we have to enable it
```

lldp run
show lldp neighbors

```



# how to set IP on layer3 switches
```
int fa 0/1
no switchport
ip addr 192.168.1.1 255.255.255.0

```



# how to enable telnet: 
```
username admin privilege 15 secret admin
line vty 0 2
login local

```


# how to enable ssh 
```

hostname device1
ip domain-name test
crypto key generate rsa
line vty 0 2
transport input ssh


# for show publickey
do show crypto key mypubkey rse
```




## Enable dhcp on Cisco switchs and routers 

```
# how to enable dhcp on cisco router
ip dhcp pool pool-name
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1
dns-server 192.168.1.1


exit

ip dhcp excluded-address 192.168.1.1 192.168.1.10



# for showing which IP assgin to client
do show ip dhcp binding
do show ip dhcp pool

# for seeing the ip confilict in dhcp
do show ip dhcp confilict
```

# how to run dhcp on a multi-layer switch
```

ip dhcp pool <name>
network 192.168.2.0 255.255.255.0
default-router 192.168.2.1
dns-server 8.8.8.8
exit
ip dhcp exclude-address 192.168.2.1 192.168.2.30
```

# Port Security
```
show int fa 0/1
conf t
int fa 0/1
switchport mode access
switchport port-security

do show port-security
do show port-security int fa 0/1


# change the maximum default device
switchport port-security maximum 3


switchport port-security violation restrict




# clear port-security
do clear port-security all



```





# vlan

```
vlan 10
name IT
vlan 20
name ACCOUNT


int range fa 0/1-2
switchport access vlan 10


int range fa 0/3-4
switchport access vlan 20



# choosing multiple range
int range fa 0/1-3 , fa 0/5

```

![Alt text](./image/vlan.png)



### delete vlan

```
no vlan 10

```



# set ip on layer2 switches 
```
int vlan1 
ip add 192.168.1.1 255.255.255.0
no sh
exit
ip default-gateway 192.168.1.254


```