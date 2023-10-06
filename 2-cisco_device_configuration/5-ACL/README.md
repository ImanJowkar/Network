
## configurations

```
# R1
hostname R1
int gig 0/0/0 
ip addr 192.168.1.254 255.255.255.0
no sh
exit

username iman privilege 15 secret iman

ip domain-name iman.local
crypto key generate rsa

line vty 0 1
login local
transport input ssh
exit


ip access-list extended 100
exit


int gig 0/0/0
ip access-group 100 in
exit
do sh run





```