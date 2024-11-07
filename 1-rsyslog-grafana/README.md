# How to manage your log with loki and grafana 

first of all install rsyslog in your linux server(like debian, ubuntu, rockey, ...)
I use ubuntu

## install rsyslog
```
sudo apt update
sudo apt install rsyslog
```


### add rsyslog config for reciving the log and send to promtail 

```
vim /etc/rsyslog.d/00-promtail-relay.conf

ruleset(name="remote"){
  action(type="omfwd" Target="192.168.229.167" Port="1514" Protocol="tcp" Template="RSYSLOG_SyslogProtocol23Format" TCP_Framing="octet-counted")
}


module(load="imudp")
input(type="imudp" port="514" ruleset="remote")

module(load="imtcp")
input(type="imtcp" port="514" ruleset="remote")


```



## run grafana-loki-promtail


```
docker compose up -d

```



## syslog command on cisco ios

```
logging on
logging host <syslog-server-ip-address>

logging host 192.168.229.100 transport tcp port 514

logging host 192.168.229.100 transport tcp port 514 session-id string R111
logging host 192.168.229.100 transport tcp port 514 session-id hostname

logging source-interface loopback 0

logging trap 5          # send from level 5 to lower

show logging


no logging console      # don't show any log on console



int fa 0/0
no logging event link-status     # on interface which connected to the end user



service timestamps log datetime localtime    # use this if all your network devices located in the same timezone
service timestamps log datetime show-timezone localtime

service timestamps log datetime msec    # use this if all your network devices located in different timezone
```

# ssh-log

```
ip domain-name iman.local
crypto key generate rsa modulus 2048
ip ssh version 2
ip ssh logging events
ip ssh authentication-retries 5


username iman secret iman
enable secret iman
line vty 0 2
transport input ssh
login local

```

## IP SLA logs

```






```


## logQL
```
{hostname="10.10.1.1"}

{hostname=~".+", hostname!="192.168.229.170"}   # all logs but not for "192.168.229.170"

{hostname=~".+", hostname!="192.168.229.170"} |= "down"
{hostname=~"10.10.1.100|10.11.1.2"} |= "down"

{hostname=~".+"} |~ "[Dd]own"   # search for down or Down
{hostname=~".+"} |~ "down|Down"  # same as above


{hostname=~".+"} |~ "ssh|SSH"

{hostname=~".+"} |~ "ssh|SSH" |~ "Failed" |~ "(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)"

{hostname=~".+"} |~ "ssh|SSH" !~ "Failed" |~ "(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)"

{job="syslog"} |= "Failed" 



# annotation
{hostname=~".+"} |~ "ssh|SSH"  |~ "Failed"
```