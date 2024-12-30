# EIGRP

## Setup Eigrp 

```

router eigrp 1
 eigrp router-id 2.2.2.2
 network 10.10.15.1 0.0.0.0
 network 192.168.4.1 0.0.0.0
 passive-interface Ethernet0/0




router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  network 10.10.10.1 0.0.0.0
  network 10.10.20.1 0.0.0.0
  network 10.10.15.1 0.0.0.0
  network 192.168.4.1 0.0.0.0

  af-interface Vlan10
   passive-interface
  exit-af-interface
  af-interface Vlan20
   passive-interface
  exit-af-interface




```

## Authentications
```
! Authentication
 ! classic only support md5(we have to use key chain)

key chain eigrp-password-md5
 key 1
  key-string secret

int eth 0/1
 ip authentication key-chain eigrp 1 eigrp-password-md5
 ip authentication mode eigrp 1 md5


 ! named support md5 and sha
    ! md5


key chain eigrp-password-md5
 key 1
  key-string secret

router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  af-interface Ethernet0/1
   authentication mode md5
   authentication key-chain eigrp-password-md5


    ! sha(don't need key chain)

router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  af-interface Ethernet0/1
   authentication mode hmac-sha-256 secret


sh ip eigrp interfaces detail ethernet 0/1




```
## timers in eigrp and bfd
```

! timer in eigrp 

interface Ethernet1/1
 ip hello-interval eigrp 1 2
 ip hold-time eigrp 1 6



router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  af-interface Ethernet0/1
   hello-interval 2
   hold-time 6


! BFD
# in classic mode

int eth 0/2
 bfd interval 200 min_rx 200 multiplier 3

router eigrp 1
 bfd interface Ethernet0/2


# in named mode
int eth 0/2 
 bfd interval 200 min_rx 200 multiplier 3


router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  af-interface Ethernet0/2
   bfd
  exit-af-interface

```

## 


## Stub router

```

router eigrp 1
 eigrp stub connected
 ! eigrp stub  # by default connected and summary



router eigrp my-eig
 address-family ipv4 unicast autonomous-system 1
  eigrp stub connected
  !eigrp stub connected summary


```


## Stub-Site-Function - only support on IOS-XE and in named mode configuration

```


```


## change bandwidth percentage
```

int eth 0/0
 ip bandwidth-percentage eigrp 1 30


router eig myeig
 address-family ipv4 unicast as 1
  af-interface 0/0
   bandwidth-percentage 30


```


## Route summerization

```

! summerization is per-interface
! classic configuration

int fa 1/0
 ip summary-address eigrp 1 10.10.8.0/22


router eigrp 1
 no auto-summary
 summery-metric 10.10.8.0 255.255.252.0 3000 20 255 0 1500



! named configuration
router eigrp myeig
 address-family ipv4 unicast as 1
  af-interface fast 1/0
   summary-address  10.10.8.0/22
    exit
  topology bash
   summery-metric 10.10.8.0 255.255.252.0 3000 20 255 0 1500
   no auto-summary
```


## Route Filtering

```



```





## IP prefix list

```





```