# SNMP


### version 1
```
# read-only
snmp-server community iman ro


# if you want to restrict the ip 
ip access-list standard snmp
permit 192.168.40.10
exit
snmp-server community iman ro snmp



# -------------------

# you can define multiple community-string , one of them is readonly and another is read-write
snmp-server community iman-readonly ro
snmp-server community iman-readwrite rw

# -------------------

## trap
snmp-server host 192.168.40.10 iman


```


### version 2c
```

# read-only
snmp-server community iman ro


# if you want to restrict the ip 
ip access-list standard snmp
permit 192.168.40.10
exit
snmp-server community iman ro snmp



# -------------------

# you can define multiple community-string , one of them is readonly and another is read-write
snmp-server community iman-readonly ro
snmp-server community iman-readwrite rw

# -------------------

## trap
snmp-server host 192.168.40.10 version 2c iman

### trap inform
 snmp-server host 192.168.40.10 informs version 2c iman


```



## snmp version 3

```

snmp-server group A v3 noauth read
snmp-server group B v3 auth read
snmp-server group C v3 priv read


snmp-server user A1 A v3
snmp-server user B1 B v3 auth sha iman
snmp-server user C1 C v3 auth md5 iman priv aes 256 iman



ip access-list standard snmp
permit 192.168.40.10
exit
nmp-server user C1 C v3 auth md5 iman priv aes 256 iman access snmp


# trap 
snmp-server host 192.168.40.10 informs version 3 priv C1



```