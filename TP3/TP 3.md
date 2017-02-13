*Jamet Félix - PHALAVANDISHVILI Demetre*

# TP 3 

## Mise en place de la configuration

Après avoir tout branché sur marionnet, on configure les machines m1, m2, m3 et m4 avec les adresses suivantes :
- m1 : 192.168.1.1 
- m2 : 192.168.1.2
- m3 : 192.168.1.254 sur LAN1 et 10.10.0.254 sur LAN2

Voici les commandes utilisées pour configurer les machines :

- machine m1 :

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
```

- machine m2 :

```
ifconfig eth0 192.168.1.2 netmask 255.255.255.0
```

- machine m3 :

Cette machine étant connectée aux deux réseaux, nous sommes obligés de lui attribuer deux adresses

```
ifconfig eth0 192.168.1.254 netmask 255.255.255.0
ifconfig eth1 10.1O.255.254 netmask 255.255.0.0
```

- machine m4 :

```
ifconfig eth0 10.10.0.4 netmask 255.255.0.0
```



## Configuration d'un connexion avec la passerelle pour chaque machine

Pour établir une connexion entre deux machines appartenant à des réseaux différents, on doit configurer la passerelle sur la machine 3 car c'est la seule machine qui est reliée à la fois à LAN1 et à LAN2.

On utilise la commande *route* pour définir une route avec un autre réseau.

- sur les machine m1 et m2, on tape la commande suivante:

```
route add -net 10.10.0.0/16 gw 192.168.1.254
```

- sur la machine m3, on n'as pas besoin cette commande, car elle est déjà connectée aux deux réseaux, mais on doit cependant activer l'ip forwarding avec la commande suivante :

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

- sur la machine 4 on tape la commande 

```
route add -net 192.168.1.0/24 gw 10.10.255.254
```

### Test de la connexion

De la machine 1 vers la machine 4 :

```
ping 10.10.04
PING 10.10.04 (10.10.0.4) 56(84) bytes of data.
64 bytes from 10.10.0.4: icmp_seq=1 ttl=63 time=41.1 ms
64 bytes from 10.10.0.4: icmp_seq=2 ttl=63 time=1.46 ms
64 bytes from 10.10.0.4: icmp_seq=3 ttl=63 time=1.18 ms

--- 10.10.04 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2014ms
rtt min/avg/max/mdev = 1.181/14.583/41.102/18.752 ms
```

On constate que la passerelle est bien configurée.

### Configuration de passerelle par défaut

On supprime les routes précédemment rajoutées et on configure m3 en tant que passerelle par défaut :

```
m1:~# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.1.0     *               255.255.255.0   U     0      0        0 eth0
10.10.0.0       192.168.1.254   255.255.0.0     UG    0      0        0 eth0

m1:~# route del -net 10.10.0.0/16 gw 192.168.1.254

m1:~# route add default gw 192.168.1.254

m1:~# route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.1.0     *               255.255.255.0   U     0      0        0 eth0
default         192.168.1.254   0.0.0.0         UG    0      0        0 eth0
```

La différence en utilisant la configuration par défaut est que la machine m3 fait maintenant office de passerelle pour tous les réseaux et plus seulement entre les réseaux LAN1 et LAN2 que l'on a créé.
De plus, la commande route met beaucoup plus de temps à afficher la ligne correspondant à la passerelle lorsqu'elle est configurée par défaut.

Pour observer cette différence, il faudrait chercher à joindre un autre réseau et utiliser un outil comme wireshark pour analyser les trames.

## Le rôle de ICMP dans le routage IP : un cas de figure

En tentant un ping sur la machine m4, on obtient le résultat indiqué dans le sujet ( ```connect: Network is unreachable``` ).

### Configuration de l'IP de l'interface eth0 sur m1

Rien ne se passe car la passerelle n'est pas configurée sur m1.

### Configuration de m3 comme passerelle par défaut sur m1

On observe des requêtes du protocole ARP, demandant quelle est la machine correspondant à l'addresse IP de la passerelle. Comme celle ci n'est pas configurée, les requêtes restent sans réponse.

### Configuration des IPs des interfaces eth0 et eth1 sur m3

Une fois machine 3 configurée, on observe maintenant des requêtes du protocole ICMP envoyé par m1, mais commme l'ip forwarding n'est pas activé, celles-ci restent sans réponse.

### Activation du routage sur m3

Une fois l'ip forwarding activé, on voit que m3 réponds à m1 en disant que m4 n'est pas atteignable en utilisant le protocole ICMP. Il ne s'agit ni d'un message de type REPLY ni d'un message de type ECHO mais d'un message de type HOST UNREACHABLE. Sur m4, on voit une requête ARP originant de m3, demandant à quelle machine correspond l'adresse 10.10.0.4.

### Configuration de l'interface eth0 sur M4

La situation est ameliorée dans le sens que m1 envoie des messages a m4(ICMP de type ECHO). Cependant, comme la passerelle n'est pas configurée sur m4, m4 ne réponds pas.
- Sur les deux réseaux, on observe des trames du protocole ICMP de type ECHO. 

### Configuration de m3 comme passerelle par défault sur m4

Une fois la passerelle configurée, le ping $m1 \rightarrow m4$ fonctionne finalement.



