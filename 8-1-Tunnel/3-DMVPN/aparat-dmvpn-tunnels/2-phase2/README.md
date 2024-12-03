# R11-HUB

```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp map multicast dynamic
tunnel source 1.1.1.2
tunnel mode gre multipoint
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.11 255.255.255.0





ip route 10.10.51.0 255.255.255.0 172.16.1.14
ip route 10.10.50.0 255.255.255.0 172.16.1.5
ip route 192.168.88.0 255.255.255.0 172.16.1.17



```



# R5-Branch

```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.2.2
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.5 255.255.255.0




ip route 10.10.51.0 255.255.255.0 172.16.1.14
ip route 10.10.11.0 255.255.255.0 172.16.1.11
ip route 192.168.88.0 255.255.255.0 172.16.1.17

```

# R14-Branch

```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.3.2
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.14 255.255.255.0




ip route 10.10.50.0 255.255.255.0 172.16.1.5
ip route 10.10.11.0 255.255.255.0 172.16.1.11
ip route 192.168.88.0 255.255.255.0 172.16.1.17

```



# command

```
sh ip nhrp 
sh dmvpn


```


## R17-Branch

```
int tun 0
ip nhrp network-id 1
ip nhrp authentication AdEs124
ip nhrp nhs 172.16.1.11 nbma 1.1.1.2 multicast
tunnel source 1.1.4.3
tunnel mode gre multipoint
ip nhrp holdtime 600
ip nhrp registration no-unique
ip mtu 1400
ip tcp adjust-mss 1360
ip addr 172.16.1.17 255.255.255.0



ip route 10.10.50.0 255.255.255.0 172.16.1.5
ip route 10.10.11.0 255.255.255.0 172.16.1.11
ip route 10.10.51.0 255.255.255.0 172.16.1.14


```