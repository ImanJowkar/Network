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
--------------------------------------
ruleset(name="remote"){
  action(type="omfwd" Target="192.168.229.167" Port="1514" Protocol="tcp" Template="RSYSLOG_SyslogProtocol23Format" TCP_Framing="octet-counted")
}


module(load="imudp")
input(type="imudp" port="514" ruleset="remote")

module(load="imtcp")
input(type="imtcp" port="514" ruleset="remote")

---------------------------------------------------

```



## run grafana-loki-promtail


```
docker compose up -d

```