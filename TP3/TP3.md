#  TP3

Les IPS des machines

- m1 : 192.168.1.1 sur h1
- m2 : 192.168.1.2 sur h1
- m3 : 192.168.1.254 sur h1 et 10.10.255.254 sur h2 
- m4 : 10.10.0.4 sur h2

##### sur m1 et m2

route add-net 10.10.0.0/16  netmask gw  192.168.1.254 

##### sur m4#####

route add-net 192.168.1.0/24 gw 10.10.255.254

##### sur m3####

autoriser faire passerelle 

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```



route add default gw 10.10.255.254



route add default gw 192.168.1.254

