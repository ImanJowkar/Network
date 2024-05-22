# most used eigrp command


## classic eigrp
```

router eigrp 1
network 10.10.5.1 0.0.0.0
network 10.10.57.5 0.0.0.0
network 10.10.58.5 0.0.0.0
passive-interface fastEthernet 1/0




```


# Named eigrp
```

router eigrp myeig-1
address-family ipv4 unicast autonomous-system 1
network 10.10.58.8 0.0.0.0
network 10.10.89.8 0.0.0.0
af-interface <default|interface>
passive-interface




```