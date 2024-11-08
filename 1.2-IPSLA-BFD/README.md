# IPSLA

### icmp-echo

```
ip sla 1
icmp-echo 8.8.8.8 source-interface gigabitEthernet 3/0
frequency 60 
ip sla schedule 1 start-time now life forever
do sh ip sla statistics

track 1 ip sla 1
delay down 70 up 70

```


### http-sla

```
ip sla 2  
http get http://10.10.90.10
frequency 60 
ip sla schedule 2 life forever start-time now

track 2 ip sla 2
delay down 70 up 70



```

### tcp connect sla
```
ip sla 3  
tcp-connect 10.10.90.12 21 control disable
frequency 60 
ip sla schedule 3 life forever start-time now


track 3 ip sla 3
delay down 70 up 70

```


# Track

### The track can monitor the following items and generate a syslog whenever an event occurs
1) layer 2 interface
2) layer3 interface
3) ip route
4) ip sla


#### layer-2 interface
If the interface goes up or down, the track will be triggered.
```
track 7 interface fastEthernet 0/0 line-protocol 
delay down 10 up 10

```

#### layer-3 interface
If the interface goes up or down, or no ip address on the interface , the track will be triggered.
```
track 8 interface fastEthernet 0/0 ip routing
delay down 10 up 10

```


#### routing table
If the route was not in the routing table , the track will be triggered.
```
ip route 90.90.90.0 255.255.255.0 192.168.229.2
track 9 ip route 90.90.90.0/24 reachability
delay down 10 up 10

```


#### IPSLA 

```
ip sla 1
icmp-echo 8.8.8.8 source-interface gigabitEthernet 3/0
frequency 60 
ip sla schedule 1 start-time now life forever
do sh ip sla statistics

track 1 ip sla 1
delay down 70 up 70

```

# binray track

```
track 30 interface fastEthernet 0/0 line-protocol 
delay down 10 up 10

track 31 interface fastEthernet 1/0 line-protocol 
delay down 10 up 10

track 32 interface fastEthernet 1/1 line-protocol 
delay down 10 up 10

track 33 interface gig 2/0 line-protocol 
delay down 10 up 10


# AND 
track 40 list boolean and
object 30
object 31
object 32
object 33



# OR
track 41 list boolean or
object 30
object 31
object 32
object 33


# threshold
track 43 list threshold percentage
threshold percentage up 50  
threshold percentage down 40 
object 30
object 31
object 32
object 33

```