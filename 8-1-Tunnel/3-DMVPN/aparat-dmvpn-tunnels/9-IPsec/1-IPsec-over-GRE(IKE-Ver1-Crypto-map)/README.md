# IPsec over GRE ( IKE version-1 & Crypto Map)
![img](./1.png)
## R11
```

interface Tunnel0
 tunnel source 1.1.1.2
 tunnel destination 1.1.2.2
 ip addr 172.16.1.11 255.255.255.0
 ip mtu 1400
 ip tcp adjust-mss 1360

! phase 1 tunnel
crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
crypto isakmp key secret address 0.0.0.0 

! phase 2 tunnel
crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode transport


ip access-list extended IPSEC-ACL
 permit ip any any


crypto map C-MAP 10 ipsec-isakmp 
 set peer 172.16.1.5
 set transform-set T-SET
 match address IPSEC-ACL




int tun 0
 crypto map  C-MAP



router eig 1
 network 172.16.1.11 0.0.0.0
 network 10.10.10.1 0.0.0.0

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


ip access-list extended IPSEC-ACL
 permit ip any any


crypto map C-MAP 10 ipsec-isakmp 
 set peer 172.16.1.11
 set transform-set T-SET
 match address IPSEC-ACL




int tun 0
 crypto map  C-MAP


router eig 1
 network 172.16.1.5 0.0.0.0
 network 10.10.50.1 0.0.0.0

```