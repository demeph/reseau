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



### Adresse IP  & adresse MAC

L'adresse IP est une adresse logique permettant d'identifier une machine dans un réseau. Il existe plusieurs formats d'adresse ip, chacune ayant un certain nombre de bits destiné à identifier le réseau et un certain nombre de bits identifiant la machine.

Une adresse MAC permet d'identifier de manière unique une carte réseau (en théorie). Une adresse MAC est constituée de six octets, généralement représentés de la manière suivante : XX:XX:XX:YY:YY:YY. Les X permettent d'identifier le fabriquant du matériel. Et les Y sont spécifiques à la carte produite

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

Pour avoir la table de routage IP, on utilise la commande Unix **route** et on obtient

```
Table de routage IP du noyau 
Destination    Passerelle      Genmask         Indic Metric Ref    Use  Iface 
192.168.0.0    *               255.255.255.0   U     0      0        0  eth0 
```
