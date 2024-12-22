## IPV6 static route


## R1
```
ipv6 unicast-routing

interface Ethernet0/1
 no ip address
 ipv6 address 2003::1/64
 ipv6 enable


interface Ethernet0/0
 ipv6 address 2001::1/64
 ipv6 enable
 no sh


ipv6 route 2002::/64 2003::2



```


## R2
```
ipv6 unicast-routing

interface Ethernet0/1
 no ip address
 ipv6 address 2003::2/64
 ipv6 enable

interface Ethernet0/0
 ipv6 address 2002::1/64
 ipv6 enable
 no sh


ipv6 route 2001::/64 2003::1




```



## clients:
```
auto ens4
iface ens4 inet6 static
        address 2001::11
        netmask 64
        gateway 2001::1

```

