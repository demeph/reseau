root

## Câblage et configuration de base

ifconfig eth0 194.85.44.2/22 donne une erreur lorsque tapé une fois. comme l'adresse commence par 194, ifconfig s'attends à une adresse de classe C avec un masque de sous réseau d'au moins 24 bits

on configure les machines du réseau LAN1 comme suit :
```
# ifconfig eth0 194.85.40.x/22
```
et les machines du réseau LAN2 comme suit :
```
# ifconfig eth0 194.85.44.x/22
```

où x est le numéro de la machine

### Utilisation des alias de carte

ajoutons m5 au réseau LAN3 :
```
# ifconfig eth0:lan3 10.10.10.5/24
```

même chose pour m6 :
```
# ifconfig eth0:lan3 10.10.10.6/24
```

On teste les connexions :

$m5 \rightarrow m1$ (sur LAN1)
```
m5 -> m1
 ping -c 5 194.85.40.1
PING 194.85.40.1 (194.85.40.1) 56(84) bytes of data.
64 bytes from 194.85.40.1: icmp_seq=1 ttl=64 time=9.02 ms
64 bytes from 194.85.40.1: icmp_seq=2 ttl=64 time=2.86 ms
64 bytes from 194.85.40.1: icmp_seq=3 ttl=64 time=2.27 ms
64 bytes from 194.85.40.1: icmp_seq=4 ttl=64 time=7.20 ms
64 bytes from 194.85.40.1: icmp_seq=5 ttl=64 time=4.17 ms

--- 194.85.40.1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4029ms
rtt min/avg/max/mdev = 2.273/5.108/9.026/2.596 ms
```

$m6 \rightarrow m5$ (sur LAN3)
```
 ping -c 5 10.10.0.5
PING 10.10.0.5 (10.10.0.5) 56(84) bytes of data.
64 bytes from 10.10.0.5: icmp_seq=1 ttl=64 time=3.77 ms
64 bytes from 10.10.0.5: icmp_seq=2 ttl=64 time=1.39 ms
64 bytes from 10.10.0.5: icmp_seq=3 ttl=64 time=2.82 ms
64 bytes from 10.10.0.5: icmp_seq=4 ttl=64 time=1.52 ms
64 bytes from 10.10.0.5: icmp_seq=5 ttl=64 time=1.27 ms

--- 10.10.0.5 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4044ms
rtt min/avg/max/mdev = 1.273/2.157/3.775/0.983 ms
```

$m1 \rightarrow m2$ (respectivement sur LAN1 et LAN2)
```
m1 -> m2
 ping 194.85.44.2
connect: Network is unreachable
```

On constate que les deux premiers pings sont un succès tandis que le dernier ping ne fonctionne pas. La raison derrière ce comportement est que les machines m1 et m2 ne sont pas sur le même réseau et qu'aucune passerelle entre ces réseaux n'est pas configurée.

## Polarité MDI/MDI-X

- $m1 \rightarrow m6$

```
 ping 194.85.40.6
From 194.85.40.6 icmp_seq=29 Destination Host Unreachable
From 194.85.40.6 icmp_seq=30 Destination Host Unreachable
From 194.85.40.6 icmp_seq=31 Destination Host Unreachable
From 194.85.40.6 icmp_seq=33 Destination Host Unreachable
From 194.85.40.6 icmp_seq=34 Destination Host Unreachable
From 194.85.40.6 icmp_seq=35 Destination Host Unreachable
From 194.85.40.6 icmp_seq=36 Destination Host Unreachable
From 194.85.40.6 icmp_seq=37 Destination Host Unreachable
From 194.85.40.6 icmp_seq=38 Destination Host Unreachable
64 bytes from 194.85.40.1: icmp_seq=39 ttl=64 time=1025 ms
64 bytes from 194.85.40.1: icmp_seq=40 ttl=64 time=19.7 ms
64 bytes from 194.85.40.1: icmp_seq=41 ttl=64 time=1.82 ms
64 bytes from 194.85.40.1: icmp_seq=42 ttl=64 time=2.16 ms
64 bytes from 194.85.40.1: icmp_seq=43 ttl=64 time=2.34 ms
64 bytes from 194.85.40.1: icmp_seq=44 ttl=64 time=2.92 ms
64 bytes from 194.85.40.1: icmp_seq=45 ttl=64 time=7.55 ms
64 bytes from 194.85.40.1: icmp_seq=46 ttl=64 time=2.24 ms
64 bytes from 194.85.40.1: icmp_seq=47 ttl=64 time=1.98 ms
64 bytes from 194.85.40.1: icmp_seq=48 ttl=64 time=1.92 ms
```

On constate que quand on remplace un câble croisé  par un cable droit entre le switch 1 et 2, on voit que on  n'arrive pas joindre la machine 6 (m6). 

## non Etanchéité

