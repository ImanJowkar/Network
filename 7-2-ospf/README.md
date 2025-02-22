# OSPF

#### Setup OSPF

```
! setup ospf 
router ospf 1
 router-id 1.1.1.1
 network 192.168.1.1 0.0.0.0 area 0


int eth 0/0
 ip ospf 1 area 0



! metric   = 10 ^ 8 / interface-bandwidth

int eth 0/0
 Bandwidth 1000

int eth 0/0
 ip ospf cost 20
```



#### change timer
============================================================================
```
! change ospf timer
interface ethernet 1/1
 ip ospf hello-interval 2
 ip ospf dead-interval 6


! BFD
int eth 0/0
 ip ospf bfd
 bfd interval 300 min_rx 300 multiplier 3
```
============================================================================





#### Authentication
```
============================================================================
!!!!!! method - 1

interface fastEthernet  0/0
ip ospf authentication message-digest
ip ospf message-digest-key 1 md5 <password>


!!!!! method - 2

router ospf 1
 area 1 authentication message-digest

interface fastEthernet  0/0
 ip ospf message-digest-key 1 md5 <password>

============================================================================
```


#### default route advertisement
```
router ospf 1
 default-information originate
 default-information originate always
 default-information originate always metric 12
 default-information originate always metric 12 metric-type 1
 


```

#### DR and BDR
`all router send update to 224.0.0.6`
`DR and BDR send update to 224.0.0.5`




#### GRE tunnel and DMVPN



! Network Type
	# loopback: advertise all route in /32 format 
	# point-to-point       --> not use DR/BDR
	# Broadcast            --> Use DR/BDR
	# point-to-multipoint  --> not use DR/BDR

int eth 0/0
 ip ospf network point-to-point



### OSPF LSA Types and Area types
#### LSA-Types
* LSA type-1: Router LSA (all router)
* LSA type-2: Network LSA (DR router)
* LSA type-3: Summary LSA (ABR router)
* LSA type 4: Summary ASBR LSA. (ABR router)
* LSA type 5: Autonomous system external LSA.(ASBR router)
* LSA type 7: Not-so-stubby area LSA.(ASBR router)


#### Area Types
* Stub Area, (don't allow LSA type 4,5)
* Totally Stubby Area, (don't allow LSA type 3,4,5)
* Not So Stubby Area(NSSA), (don't allow LSA type 4,5 but allow 7)
* Totally NSSA , (don't allow LSA type 3,4,5, but allow 7)











#### Redistribute 
```
------------------------------
route-map RMAP permit 10
 match interface Ethernet0/0

router ospf 1
 redistribute connected subnets route-map RMAP
------------------------------

-------------------------------
router ospf 1
 redistribute eigrp 1 metric 10 subnets

--------------------------------
router eigrp 1
 redistribute ospf 1 metric 100 10 255 1 1500


```


#### Route Summerization
note that , summerization only set in ABR router, or ASBR router

```
### summary only apply on ABR
router ospf 1
 area 17 range 192.168.120.0 255.255.252.0
 area 5 range 172.17.0.0 255.255.248.0 cost 11





### in ASBR run below 
router ospf 1
 summary-address 10.255.0.0 255.255.252.0




```



#### ip prefix list


```
Ip prefix-list 192.168.1.0/24
Ip prefix-list 192.168.3.0/24
Ip prefix-list 172.16.0.0/16


Ip prefix-list 10.10.10.0/24 ge 24       subnet: /24, /25, /26, /27, /28, /29, /30, /31, /32

Ip prefix-list 10.10.10.0/24 ge 24 le 27     ip address: 10.10.10.x             subnet: /24, /25, /26, /27

Ip prefix-list 10.10.0.0/16 ge 24 le 27     ip address: 10.10.x.x             subnet: /24, /25, /26, /27


Ip prefix-list 10.10.0.0/16   le 20     ip address: 10.10.x.x             subnet: /20, /19, /18, /17, /16

Ip prefix-list 10.10.0.0/16  ge 16 le 16     ip address: 10.10.x.x             subnet: /16

Ip prefix-list 0.0.0.0/0 ge 30 le 30              ip address: x.x.x.x            subnet: /30                     # select all /30 network


Ip prefix-list 0.0.0.0/0  le 32     # any ip address

Ip prefix-list 0.0.0.0/0             # default route



### select all private ip address

ip prefix-list 10.0.0.0/8 le 32
ip prefix-list 172.16.0.0/12 le 32
ip prefix-list 192.168.0.0/16 le 32




```



#### Route Filtering

```

# filtering with summerization

router ospf 1
 area 1 range 10.15.1.0 255.255.255.0 not-advertise





## Area - filtering ( use ip prefix list)

ip prefix-list ospf-filter seq 5 deny 10.15.2.0/24
ip prefix-list ospf-filter seq 6 deny 10.15.3.0/24
ip prefix-list ospf-filter seq 20 permit 0.0.0.0/0 le 32


router ospf 1
 area 4 filter-list prefix ospf-filter in




```


#### Virtual-link

```

router ospf 1
 router-id 1.1.1.1
 area 1 virtual-link 15.15.15.15

```





### OSPFv3 configuration

```
ipv6 unicast-routing

router ospfv3 1
 router-id 1.1.1.1
 address-family ipv4 unicast
  exit-address-family
 address-family ipv6 unicast
  exit-address-family
 
 





interface range ethernet 0/0-2
 ipv6 enable
 ospfv3 1 ipv4 area 0
 ospfv3 1 ipv6 area 0
 

interface ethernet 0/3
 ipv6 enable
 ospfv3 1 ipv4 area 4
 ospfv3 network point-to-point
 




```


### Mikrotik
##### route filtering

```

if (dst in 10.10.54.0/24 && dst-len in 24) {reject;}
if (dst in 10.10.205.0/24 && dst-len in 24) {reject;}else{accept}




```