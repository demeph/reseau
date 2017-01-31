**Phalavandishvili Demetre - Felix Jamet**

# TP1 - Réseaux & Télécoms

## BIlan de Travaux pratiques  1

### Modele OSI

Le modèle OSI est un modèle théorique permettant de décrire le fonctionnement d'un réseau. Ils'agit de sept couches empilées de sorte à ce que chaque couche fournisse un service à la couche du dessus en s'appuyant sur le service rendu par la couche du dessous. Parmi ces 7 couches, on en distingue deux types : les couches hautes et les couches matérielles. 

| **Couche**                | **Description**                                              |
| ------------------------- | ---------------------------------------- |
| **Couches Hautes**        |                                                                            |
| 7. Application            | Point d'accès aux	services réseaux       |
| 6. Présentation           | Permet de convertir les données machine en données qui permet aux autres machines	d'utiliser |
| 5. Session                |                                          |
| 4. Transport              | Permet de transporter les données et se charge que les données sont bien				reçu |
| **Couches	Matérielles**   |                                          |
| 3. Réseau                 |                                          |
| 2. Liaison                |                                          |
| 1. Physique               |                                          |
# finir le tableau #


Pour permettre à deux "entités" de communiquer, chaque couche ajoute un entête aux données fournies par la couche du dessus. Une fois arrivées à la couche physique, les données sont transmises au destinataire et les entêtes sont interprétés par les couches successives, fournissant à la couche supérieure, les données envoyées par la couche équivalente de l'émetteur.

Ce mécanisme permet donc de créer un lien virtuel entre les couches. 



## Modèle TCP/IP

Le modèle OSI n'étant qu'un concept, les protocoles de communication ne suivent pas strictement les règles établies par OSI.
Le protocole nous intéressant, TCP/IP n'utilise que quatre couches : application, tpc, ip et physique.

TCP est le protocole de transport. Le rôle principal du protocole IP est d'assurer le routage des paquets.

Le routage des paquets est la procédure permettant à deux ordinateurs distants d'échanger des paquets s'ils ne font pas parti du même réseau local. Pour pouvoir communiquer en dehors du réseau local, les paquets doivent transiter par une passerelle qui est chargée de transmettre les paquets vers l'extérieur.



### Adresses IP  & adresses MAC

L'adresse IP est une adresse logique permettant d'identifier une machine dans un réseau. Il existe plusieurs formats d'adresse ip, chacune ayant un certain nombre de bits destiné à identifier le réseau et un certain nombre de bits identifiant la machine. On identifie 5 différentes classes d'adresses IP :
| **Classe**								| **Description** 											| **nombre de postes** | **notes** |
|-|-|-|
| A | 0RRR.MMMM.MMMM.MMMM | 16 777 214 | |
| B | 10RR.RRRR.MMMM.MMMM | 65 534 | |
| C | 110R.RRRR.RRRR.MMMM | 254 | |
| D | 1110.XXXX.XXXX.XXXX | | utilisé pour les communications multicast |
| E | 1111.XXXX.XXXX.XXXX | | réservé par l'IANA mais non utilisé |


Une adresse MAC permet d'identifier de manière unique une carte réseau (en théorie). Une adresse MAC est constituée de six octets, généralement représentés de la manière suivante : XX:XX:XX:YY:YY:YY.
Les X permettent d'identifier de manière unique le fabriquant du matériel. On appelle cette partie Organizationally Unique Identifier (OUI).
Les Y sont spécifiques à la carte produite. Cette partie est désignée par Network interface controller (NIC).

## Manipulations réalisées sur machine

Résultat de la commande **ifconfig** avant la configuration :

```
lo       Link encap:Boucle locale
          inetadr:127.0.0.1  Masque:255.0.0.0 
          adrinet6: ::1/128 Scope:Hôte 
          UPLOOPBACK RUNNING  MTU:16436  Metric:1 
          RXpackets:192 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:192 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:0lg file transmission:0 
          RXbytes:52605 (20.3 KiB)  TX bytes:52605 (20.3 KiB) 
```
On configure le réseau à l'aide de la commande `ifconfig eth0 192.168.0.2 netmask 255.255.255.0`.

Cette commande permet de mettre en place le reseau local, en attribuant `192.168.0.2` comme adresse IP à la première interface physique.

Résultat de la commande **ifconfig** après la configuration:

```
eth0     Link encap:Ethernet  HWaddr 00:23:ae:a6:7f:f6
          inetadr:192.168.0.2  Bcast:192.168.0.255  Masque:255.255.255.0 
          adrinet6: fe80::223:aeff:fea6:7ff6/64 Scope:Lien 
          UPBROADCAST MULTICAST  MTU:1500  Metric:1 
          RXpackets:247 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:123 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:10lg file transmission:1000 
          RXbytes:37369 (36.4 KiB)  TX bytes:16466 (16.0 KiB) 
          Interruption:16
          
lo       Link encap:Boucle locale
          inetadr:127.0.0.1  Masque:255.0.0.0 
          adrinet6: ::1/128 Scope:Hôte 
          UPLOOPBACK RUNNING  MTU:16436  Metric:1 
          RXpackets:192 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:192 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:0lg file transmission:0 
          RXbytes:52605 (51.3 KiB)  TX bytes:52605 (51.3 KiB) 
```

### Routage

Pour avoir la table de routage IP, on utilise la commande Unix **route** et on obtient

```
Table de routage IP du noyau 
Destination    Passerelle      Genmask         Indic Metric Ref    Use  Iface 
192.168.0.0    *               255.255.255.0   U     0      0        0  eth0 
```

La commande suivante permet d’établir une connexion avec une autre machine, dans notre cas on a établi la connexion avec la passerelle (bob) :

```
route add -net 10.0.0.0 netmask 255.255.255.0 gw 192.168.0.254
```

Après cette manipulation, la commande route donne les lignes suivantes :
```
Destination		Passerelle 		Genmask 		Indic	Metric	Ref	Use Iface
192.168.0.0  	*   			255.255.255.0 	U 		0 		0 	0	eth0
10.0.0.0		none-5.local	255.255.255.0	UG		0		0	0	eth0
```

Après avoir établi toutes les connexions, on vérifie qu’on peut se connecter avec les autres machines. Pour cela on utilise la commande ping suivi de l'adresse IP à tester.
Voici quelques tests réalisés lors des TP :

```
- ping 10.0.0.7 
PING 10.0.0.7 (10.0.0.7) 56(84) bytes of data. 
64 bytes from 10.0.0.7: icmp_req=1 ttl=63 time=0.699 ms 
64 bytes from 10.0.0.7: icmp_req=2 ttl=63 time=0.690 ms 
64 bytes from 10.0.0.7: icmp_req=3 ttl=63 time=0.688 ms 
^C 
--- 10.0.0.7 ping statistics --- 
3 packets transmitted, 3 received, 0% packet loss, time 2000ms 
rtt min/avg/max/mdev = 0.688/0.692/0.699/0.022 ms 


- ping 192.168.0.3 
PING 192.168.0.3 (192.168.0.3) 56(84) bytes of data. 
64 bytes from 192.168.0.3: icmp_req=1 ttl=64 time=1.38 ms 
64 bytes from 192.168.0.3: icmp_req=2 ttl=64 time=0.758 ms 
64 bytes from 192.168.0.3: icmp_req=3 ttl=64 time=0.748 ms 
64 bytes from 192.168.0.3: icmp_req=4 ttl=64 time=0.754 ms 
^C 
--- 192.168.0.3 ping statistics --- 
4 packets transmitted, 4 received, 0% packet loss, time 3000ms 
rtt min/avg/max/mdev = 0.748/0.910/1.380/0.271 ms
```

La commande arp -a  permet de voir l’histoirique de la connexion avec les autres machines :

```
arp -a 
none-5.local (192.168.0.254) at 00:12:3f:64:6c:dc [ether] on eth0 
? (192.168.0.1) at <incomplete> on eth0 
none-2.local (192.168.0.3) at 00:23:ae:a6:80:40 [ether] on eth0 
? (192.168.0.4) at <incomplete> on eth0 
? (192.168.0.5) at <incomplete> on eth0 
none-6.local (192.168.0.6) at 00:23:ae:a6:7c:8a [ether] on eth0
```