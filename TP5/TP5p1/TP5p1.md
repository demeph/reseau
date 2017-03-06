***PHALAVANDISHVILI Demetre - JAMET Félix - Groupe 601B***

# TP5 Partie 1#

## Câblage et configuration de base

Pour segmenter la plage réseau en deux parties, on ajoute un bit à la partie réseau de l'adresse, celle ci passant sur 22 bits. On créé de cette manière la plage 194.85.44.2/22 et la plage 194.85.40.2/22.

```ifconfig eth0 194.85.44.2/22``` donne une erreur lorsque tapé une fois. En effet, l'adresse commençant par 194, ifconfig s'attend à une adresse de classe C avec un masque de sous réseau d'au moins 24 bits. En retapant la commande, elle est acceptée

On configure les machines du réseau LAN1 comme suit :
```
# ifconfig eth0 194.85.40.x/22
```
On configure les machines du réseau LAN2 comme suit :
```
# ifconfig eth0 194.85.44.x/22
```

Où x est le numéro de la machine

### Utilisation des alias de carte

Ajoutons m5 au réseau LAN3 :
```
# ifconfig eth0:lan3 10.10.10.5/24
```

Même chose pour m6 :
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

On constate que les deux premiers pings sont un succès tandis que le dernier ping ne fonctionne pas. La raison de ce comportement est que les machines m1 et m2 ne sont pas sur le même réseau et qu'aucune passerelle entre ces réseaux n'est configurée.

## Polarité MDI/MDI-X

- $m1 \rightarrow m6$

```
 ping 194.85.40.6
 [...]
64 bytes from 194.85.40.1: icmp_seq=14 ttl=64 time=1.92 ms
64 bytes from 194.85.40.1: icmp_seq=15 ttl=64 time=1.87 ms
64 bytes from 194.85.40.1: icmp_seq=16 ttl=64 time=1.82 ms
64 bytes from 194.85.40.1: icmp_seq=17 ttl=64 time=2.16 ms
64 bytes from 194.85.40.1: icmp_seq=18 ttl=64 time=2.04 ms
64 bytes from 194.85.40.1: icmp_seq=19 ttl=64 time=2.92 ms
64 bytes from 194.85.40.1: icmp_seq=20 ttl=64 time=7.55 ms
64 bytes from 194.85.40.1: icmp_seq=21 ttl=64 time=2.24 ms
64 bytes from 194.85.40.1: icmp_seq=22 ttl=64 time=1.98 ms
64 bytes from 194.85.40.1: icmp_seq=23 ttl=64 time=1.92 ms
From 194.85.40.6 icmp_seq=24 Destination Host Unreachable
From 194.85.40.6 icmp_seq=25 Destination Host Unreachable
From 194.85.40.6 icmp_seq=26 Destination Host Unreachable
From 194.85.40.6 icmp_seq=27 Destination Host Unreachable
From 194.85.40.6 icmp_seq=28 Destination Host Unreachable
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
64 bytes from 194.85.40.1: icmp_seq=41 ttl=64 time=2.02 ms
64 bytes from 194.85.40.1: icmp_seq=42 ttl=64 time=2.17 ms
64 bytes from 194.85.40.1: icmp_seq=43 ttl=64 time=1.80 ms
64 bytes from 194.85.40.1: icmp_seq=44 ttl=64 time=1.92 ms
64 bytes from 194.85.40.1: icmp_seq=45 ttl=64 time=2.55 ms
64 bytes from 194.85.40.1: icmp_seq=46 ttl=64 time=7.11 ms
64 bytes from 194.85.40.1: icmp_seq=47 ttl=64 time=3.51 ms
64 bytes from 194.85.40.1: icmp_seq=48 ttl=64 time=2.55 ms
```

On constate que quand on remplace un câble croisé par un cable droit entre le switch 1 et 2, on n'arrive pas à joindre la machine 6 (m6) depuis m1. Le ping refonctionne normalement en rebranchant le câble croisé



## Non Etanchéité

### Broadcast *ARP*

Quand on lance la commande de ping de m1 $\rightarrow$ m5, on voit sur le ***tcpdump*** de la machine 4 une trame ARP demandant à qui correspond l'adresse de la machine 5 :

```
12:57:07.818536 arp who-has 194.85.40.5 tell 194.85.40.1
```
### Broadcast DHCP

En suivant les etapes décrites dans la feuille de TP, nous avons défini la plage des adresses IP sur m1 & m2 :

- m1 :

  ```
  subnet 194.85.40.0 netmask 255.255.252.0
  {
    194.85.40.51 192.85.40.99
  }
  ddns-update-style none;
  ```

- m2

  ```
  subnet 194.85.44.0 netmask 255.255.252.0
  {
    194.85.44.51 192.85.44.99
  }
  ddns-update-style none;
  ```

  ​

Ensuite, nous avons ajouté les machines m7, m8 et m9. La machine m7 est branchée sur le switch 1, m8 sur le switch 3 et m9 sur le switch 2.
Puis nous avons lancé une demande d'affectation d'adresse ip avec la commande suivante :

```
dhclient eth0
```

On obtient comme résultats :

- m7

```
Internet Systems Consortium DHCP Client V3.0.5
Copyright 2004-2006 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/sw/dhcp/

Listening on LPF/eth0/02:04:06:e6:f6:28
Sending on   LPF/eth0/02:04:06:e6:f6:28
Sending on   Socket/fallback
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 7
DHCPOFFER from 194.85.44.2
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.40.1
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 5
receive_packet failed on eth0: Network is down
DHCPOFFER from 194.85.44.2
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.40.1
DHCPACK from 194.85.44.2
SIOCADDRT: Network is unreachable
bound to 194.85.44.98 -- renewal in 263 seconds.
```

- m8

```
Internet Systems Consortium DHCP Client V3.0.5
Copyright 2004-2006 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/sw/dhcp/

Listening on LPF/eth0/02:04:06:02:07:90
Sending on   LPF/eth0/02:04:06:02:07:90
Sending on   Socket/fallback
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 7
DHCPOFFER from 194.85.40.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.44.2
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 6
receive_packet failed on eth0: Network is down
DHCPOFFER from 194.85.40.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.44.2
DHCPACK from 194.85.40.1
SIOCADDRT: Network is unreachable
bound to 194.85.40.98 -- renewal in 267 seconds.
```

- m9

```
Internet Systems Consortium DHCP Client V3.0.5
Copyright 2004-2006 Internet Systems Consortium.
All rights reserved.
For info, please visit http://www.isc.org/sw/dhcp/

Listening on LPF/eth0/02:04:06:f0:af:a7
Sending on   LPF/eth0/02:04:06:f0:af:a7
Sending on   Socket/fallback
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 3
DHCPOFFER from 194.85.40.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.44.2
DHCPDISCOVER on eth0 to 255.255.255.255 port 67 interval 4
receive_packet failed on eth0: Network is down
DHCPOFFER from 194.85.40.1
DHCPREQUEST on eth0 to 255.255.255.255 port 67
DHCPNAK from 194.85.44.2
DHCPACK from 194.85.40.1
SIOCADDRT: Network is unreachable
bound to 194.85.40.96 -- renewal in 260 seconds.
```

On voit que ces adresses IP vont être renouvelées dans un certain temps(ici en moyenne 260 secondes). De plus on voit que la machine m7 et m9 appartient au $LAN_{1}$ et la machine m8 appartient au $LAN_{2}$.​
