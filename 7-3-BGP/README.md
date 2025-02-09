# BGP (Border Gateway Protocols) 
BGP work with 179/tcp, and is an aplication layer protocol

* `Path Attributes`:
1. well-known mandatory ( AS-Path)
2. well-know discretionary
3. optional transitive
4. optional non-transitive

#### some path-attributes: 
* MED
* AS-Path
* origin
* local-pref
![img](1.png)

# Basic configuration

```
router bgp 100
 bgp router-id 1.1.1.1
 neighbor 10.10.0.0 remote-as 500
 neighbor 10.10.0.0 update-source loopback1 
 neighbor 10.10.0.0 ebgp-multihop 6
 neighbor 10.10.0.0 description this is provider-1
 neighbor 10.10.0.0 password bgpiman
 neighbor 10.10.0.0 timers keep_alive hold_time min_hold_time

 address-family ipv4 unicast 
  neighbor 10.10.0.0 activate

! keep-alive by default is : 60s
! hold time by default is : 180s

# monitoring
sh bgp ipv4 unicast neighbors | inc BGP neighbor is | BGP state =
alias exec mynei sh bgp ipv4 unicast neighbors | inc BGP neighbor is | BGP state =


```


# advertise a route using network command

```
ip rotue 10.22.10.0 255.255.255.0 null 0

router bgp 100
 address-family ipv4 unicast
  network 10.22.10.0 mask 255.255.255.0



# addvertise static route with redistribute and route-map

ip prefix-list bgpadvertise seq 5 permit 10.22.10.0/24
route-map bgpad permit 10
 match ip address prefix-list bgpadvertise
 exit

rotuer bgp 100
 address-family ipv4 unicast
  redistribute static route-map bgpad



```



# RR (Route Reflector)


```


router bgp 500
 neighbor 2.2.2.2 remote-as 500
 neighbor 2.2.2.2 update-source loopback1
 neighbor 2.2.2.2 next-hop-self

 neighbor 4.4.4.4 remote-as 500
 neighbor 4.4.4.4 update-source loopback1
 neighbor 4.4.4.4 next-hop-self
 neighbor 4.4.4.4 route-reflector-client


```

# Summerization

```




```


# Route filtering

```

# filtering with access-list standard

ip access-list standard bgp-filter
 permit 21.22.110.0 0.0.0.255

router bgp 200
 neighbor 10.10.4.7 distribute-list bgp-filter out


do sh bgp ipv4 unicast neighbors 10.10.4.7 advertised-routes



***************************************************************
# filtering with access-list extended

ip access-list extended bgp-filter
 permit ip host 21.22.110.0 host 255.255.255.0
                -----------       ------------
                   source          subnetmask


router bgp 200
 neighbor 10.10.4.7 distribute-list bgp-filter out


```


### filtering with prefix list

```

ip prefix-list bgp-filter seq 5 permit 21.22.110.0/24


router bgp 500
neighbor 10.4.4.4 prefix-list bgp-filter out 
neighbor 10.2.2.2 prefix-list bgp-filter out

```

#### filtering with Regex

```

ip as-path access-list 100 permit ^$


router bgp 500
 neighbor 10.2.2.2 filter-list 100 out
 neighbor 10.4.4.4 filter-list 100 out



sh bgp ipv4 unicast neighbors 10.2.2.2 advertised-routes 

```

## filtering with route-map
### with standard ACL
```
ip access-list standard bgp-filter
 permit 21.22.110.0 0.0.0.255

route-map bgp-filter permit 20
 match ip address bgp-filter

router bgp 500
  neighbor 10.4.4.4 route-map bgp-filter out
  neighbor 10.2.2.2 route-map bgp-filter out

```

### with extended ACL
```
ip access-list extended bgp-filter
 permit ip host 21.22.110.0 host 255.255.255.0

route-map bgp-filter permit 20
 match ip address bgp-filter

router bgp 500
  neighbor 10.4.4.4 route-map bgp-filter out
  neighbor 10.2.2.2 route-map bgp-filter out

```


### with prefix list
```
ip prefix-list bgp-filter seq 5 permit 21.22.110.0/24


route-map bgp-filter permit 20
 match ip address prefix bgp-filter

router bgp 500
  neighbor 10.2.2.2 route-map bgp-filter out
  neighbor 10.4.4.4 route-map bgp-filter out

```




#### with as-path
```
ip as-path access-list 100 permit ^$


route-map bgp-filter permit 20
 match as-path 100

router bgp 500
  neighbor 10.2.2.2 route-map bgp-filter out
  neighbor 10.4.4.4 route-map bgp-filter out


  

  

```


