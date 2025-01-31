# GRE over IPsec ( IKE version-2 & IPsec Profile)

![img](./1.png)

## R11
```

int tun 1
 tunnel source 1.1.1.2
 tunnel destin 1.1.4.3
 ip mtu 1400
 ip tcp adjust-mss 1360
 ip addr 172.17.1.11 255.255.255.0



int tun 0
 tunnel source 1.1.1.2
 tunnel destin 1.1.2.2
 ip mtu 1400
 ip tcp adjust-mss 1360
 ip addr 172.16.1.11 255.255.255.0


! phase-1
crypto ikev2 keyring MY_KEY
 peer ALL
  address 0.0.0.0 0.0.0.0
  pre-shared-key secret

  
crypto ikev2 profile IKE-PROF
 match identity remote address 0.0.0.0
 authentication remote pre-share
 authentication local pre-share 
 keyring local MY_KEY



crypto ikev2 proposal default
 encryption aes-cbc-256 aes-cbc-192 aes-cbc-128
 integrity sha512 sha384 sha256
 group 24 21 20

! phase-2
crypto ipsec transform-set T-SET esp-aes esp-sha-hmac
 mode transport



crypto ipsec profile IPSEC-PROFILE
 set transform-set T-SET
 set ikev2-profile IKE-PROF
 set pfs group14


crypto ipsec security-association replay window-size 1024


int range tun 0-1
 tunnel protection ipsec profile IPSEC-PROFILE




router eig eig-dmvnp
address-family ipv4 unicast as 1
network 10.10.20.1 0.0.0.0
network 10.10.10.1 0.0.0.0
network 172.16.1.11 0.0.0.0
network 172.17.1.11 0.0.0.0


```



## R17
```


int tun 1
 tunnel source 1.1.4.3
 tunnel destin 1.1.1.2 
 ip mtu 1400
 ip tcp adjust-mss 1360
 ip addr 172.17.1.17 255.255.255.0



crypto ikev2 keyring MY_KEY
 peer ALL
  address 0.0.0.0 0.0.0.0
  pre-shared-key secret


crypto ikev2 profile IKE-PROF
 match identity remote address 0.0.0.0
 authentication remote pre-share 
 authentication local pre-share 
 keyring local MY_KEY


crypto ikev2 proposal default
 encryption aes-cbc-256 aes-cbc-192 aes-cbc-128
 integrity sha512 sha384 sha256
 group 24 21 20


crypto ipsec transform-set T-SET esp-aes esp-sha-hmac
 mode transport


crypto ipsec profile IPSEC-PROFILE
 set transform-set T-SET
 set ikev2-profile IKE-PROF
 set pfs group14

crypto ipsec security-association replay window-size 1024



int tun 0
 tunnel protection ipsec profile IPSEC-PROFILE








router eig eig-dmvnp
address-family ipv4 unicast as 1
network 172.16.100.1 0.0.0.0
network 172.16.150.1 0.0.0.0
network 172.17.1.17 0.0.0.0





```




## R5
```

int tun 0
 tunnel source 1.1.2.2
 tunnel destin 1.1.1.2
 ip mtu 1400
 ip tcp adjust-mss 1360
 ip addr 172.16.1.5 255.255.255.0




crypto ikev2 keyring MY_KEY
 peer ALL
  address 0.0.0.0 0.0.0.0
  pre-shared-key secret


crypto ikev2 profile IKE-PROF
 match identity remote address 0.0.0.0
 authentication remote pre-share 
 authentication local pre-share 
 keyring local MY_KEY


crypto ikev2 proposal default
 encryption aes-cbc-256 aes-cbc-192 aes-cbc-128
 integrity sha512 sha384 sha256
 group 24 21 20


crypto ipsec transform-set T-SET esp-aes esp-sha-hmac
 mode transport


crypto ipsec profile IPSEC-PROFILE
 set transform-set T-SET
 set ikev2-profile IKE-PROF
 set pfs group14

crypto ipsec security-association replay window-size 1024



int tun 1
 tunnel protection ipsec profile IPSEC-PROFILE





router eig eig-dmvnp
address-family ipv4 unicast as 1
network 10.10.50.1 0.0.0.0
network 172.16.1.5 0.0.0.0





```