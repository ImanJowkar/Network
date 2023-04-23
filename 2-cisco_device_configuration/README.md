# Network 


## How to config cisco devices

![Cisco device modes](./image/1.png)
```
# switch between modes
---> enable ----> en
     disable


---> configure terminal ---> conf t

?  # help


# change hostname
hostname sw1   #change device name
no hostname    #reset hostname

ctrl+shift+6 # for exit when request send to the dns or you can disable this feature by typing 

no ip domain-lookup

# for enable password 
enable password test
enable secret test
enable secret 5 $1$mERr$126VWMuSfhXn9GAlqkjPo/



# set password for console 
line console 0
password test
login


# how to create a user
username admin privilege 15 secret admin
username user1 privilege 1 secret user1





# save configs
do write
# or 
copy running-config startup-config


reload



show  running-config
do show run
show flash


# do show arp

# how to set IP address on router ports
interface gigabitEthernet 0/0/0
ip address 192.168.1.1 255.255.255.0
no sh
do show run




# cdp protocol, lldp protocol
# tip: cdp only works on cisco devices, but lldp works on all standard devices.

show cdp neighbors

# for using lldp, first we have to enable it
lldp run
show lldp neighbors


# how to set IP on layer3 switches
int fa 0/1
no switchport
ip addr 192.168.1.1 255.255.255.0


# how to enable dhcp on cisco router
ip dhcp pool pool-name
network 192.168.1.0 255.255.255.0
default-router 192.168.1.1


# how to enable telnet: 
username admin privilege 15 secret admin
line vty 0 2
login local


# how to enable ssh 
hostname device1
ip domain-name test
crypto key generate rsa
line vty 0 2
transport input ssh















```