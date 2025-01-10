

### PBR

```






```




### set route-map on router itself


```

ip access-list extended PBR-ACL
permit ip 10.10.10.0 0.0.0.255 10.10.50.0 0.0.0.255




route-map PBR-RP permit 10
match ip address PBR-ACL
set ip next-hop verify-availability 10.10.39.3 1 track 1
exit


ip local policy route-map PBR-RP

```