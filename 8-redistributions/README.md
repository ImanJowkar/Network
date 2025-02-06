# Redistrbute eigrp into ospf

```

router ospf 1
 redistribute eigrp 1 metric 21 subnets metric-type 2


```


# Redistribute ospf into eigrp

```

router eigrp 1
 redistribute ospf 1 metric 10000 10 255 1 1500


```

# redistribte static route into ospf 

```
ip route 1.1.1.1 255.255.255.255 null 0
router ospf 1 
 redistribute static subnets metric 33 metric-type 1

```