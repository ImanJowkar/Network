# SNMP

### version 2c
```

# read-only
snmp-server community iman ro


# if you want to restrict the ip
ip access-list standard snmp-acl
permit 192.168.40.10
exit
snmp-server community iman ro snmp-acl



# -------------------

# you can define multiple community-string , one of them is readonly and another is read-write
snmp-server community iman-readonly ro
snmp-server community iman-readwrite rw

# -------------------

## trap
snmp-server host 192.168.40.10 version 2c iman
snmp-server enable trap


### trap inform
 snmp-server host 192.168.40.10 informs version 2c iman


```



## snmp version 3

```

# noauth   --> No Authentication  / No encription
# auth     --> Authentication     / No encription
# priv     -->  Authentication  / Encriyption




snmp-server group group-A v3 noauth
snmp-server group gruop-B v3 auth
snmp-server group gruop-C v3 priv


snmp-server user myuserA1 group-A v3
snmp-server user myuserB1 gruop-B v3 auth sha iman
snmp-server user myuserC1 gruop-C v3 auth md5 iman priv aes 256 iman



ip access-list standard snmp
permit 192.168.40.10
exit
nmp-server user myuserC1 gruop-C v3 auth md5 iman priv aes 256 iman access snmp


# trap 
snmp-server host 192.168.40.10 informs version 3 priv C1



```


# snmp-v3-finall


```
snmp-server group mygroup v3 priv
ip access-list standard snmp
permit 192.168.40.10
exit
snmp-server user iman mygroup v3 auth md5 iman55555555 priv aes 256 iman55555555 access snmp


```