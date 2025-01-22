# Site-to-Site-IPsec(IKEv1 + cryptomap)
![img](./1.png)






## R11
```

! phase 1 tunnel
crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
 lifetime 86400
crypto isakmp key secret address 1.1.2.2


! phase 2 tunnel
crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode tunnel
crypto ipsec security-association lifetime seconds 3600 



ip access-list extended IPSEC-ACL
 10 permit ip 10.10.10.0 0.0.0.255 10.10.50.0 0.0.0.255
 20 permit ip 10.10.20.0 0.0.0.255 10.10.50.0 0.0.0.255


crypto map C-MAP 10 ipsec-isakmp 
 set peer 1.1.2.2
 set transform-set T-SET
 match address IPSEC-ACL
! set pfs group14




int eth 0/0
 crypto map  C-MAP


```


## R5
```


crypto isakmp policy 10
 encr aes 256
 hash sha512
 authentication pre-share
 group 14
 lifetime 86400
crypto isakmp key secret address 1.1.1.2

! phase 2 tunnel
crypto ipsec transform-set T-SET esp-aes 128 esp-sha-hmac 
 mode tunnel
crypto ipsec security-association lifetime seconds 3600 



ip access-list extended IPSEC-ACL
 10 permit ip 10.10.50.0 0.0.0.255 10.10.10.0 0.0.0.255 
 20 permit ip 10.10.50.0 0.0.0.255 10.10.20.0 0.0.0.255 


crypto map C-MAP 10 ipsec-isakmp 
 set peer 1.1.1.2
 set transform-set T-SET
 match address IPSEC-ACL
! set pfs group14




int eth 0/0
 crypto map  C-MAP



```