# GRE over IPsec ( IKE version-1 & IPsec Profile)
![img](./1.png)


## R11
```
interface Tunnel0
 tunnel source 1.1.1.2
 tunnel destination 1.1.2.2
 ip addr 172.16.1.11 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360


interface Tunnel1
 tunnel source 1.1.1.2
 tunnel destination 1.1.4.3
 ip addr 172.17.1.11 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360





crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
crypto isakmp key secret address 0.0.0.0 


crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode transport

crypto ipsec profile IPSEC-PRO
 set transform-set T-SET


interface range tunnel 0-1
 tunnel protection ipsec profile IPSEC-PRO



router eig 1
 network 172.16.1.11 0.0.0.0
 network 172.17.1.11 0.0.0.0
 network 10.10.10.1 0.0.0.0
 network 10.10.20.1 0.0.0.0

```



## R17
```

interface Tunnel1
 tunnel source 1.1.4.3
 tunnel destination 1.1.1.2
 ip addr 172.17.1.17 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360



crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
crypto isakmp key secret address 0.0.0.0 


crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode transport


crypto ipsec profile IPSEC-PRO
 set transform-set T-SET


interface range tunnel 1
 tunnel protection ipsec profile IPSEC-PRO
 

router eig 1
 network 172.17.1.17 0.0.0.0
 network 172.16.100.1 0.0.0.0
 network 172.16.150.1 0.0.0.0




```




## R5
```

interface Tunnel0
 tunnel source 1.1.2.2
 tunnel destination 1.1.1.2
 ip addr 172.16.1.5 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360



crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
crypto isakmp key secret address 0.0.0.0 


crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode transport


crypto ipsec profile IPSEC-PRO
 set transform-set T-SET


interface range tunnel 0
 tunnel protection ipsec profile IPSEC-PRO



router eig 1
 network 172.16.1.5 0.0.0.0
 network 10.10.50.1 0.0.0.0

```