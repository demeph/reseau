*Jamet Felix - PHALAVANDISHVILI* Demetre

# TP 3 

## Mise en place de la configuration  

Après avoir tout brancher sur marionnet, on configure les machines m1,m2,m3 et  m4. 

Les adresses ip sont 

- m1 : 192.168.1.1 

- m2 : 192.168.1.2

- m3 : 2 adresses : sur h1 192.168.1.254 (derniere adresse disponible)

  ​			       sur h2 10.10.0.254 (derniere adresse disponible)	

Les commandes sont suivantes :

- machine m1

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
```

- machine m2

```
ifconfig eth0 192.168.1.2 netmask 255.255.255.0
```

- machine m3

  Comme elle est connectée aux des hub, nous sommes obligé d'attribuer 2 fois l'adresse.

```
ifconfig eth0 192.168.1.254 netmask 255.255.255.0 sur h1
ifconfig eth1 10.1O.255.254 netmask 255.255.0.0 sur h2
```

- machine m4

```
ifconfig eth0 10.10.0.4 netmask 255.255.0.0
```



## Configuration d'un connexion avec la passerelle pour chaque machine

​	Pour établir une connexion avec les machines qui sont connecté au hub h2, on doit configurer la passerelle sur la machine 3 car c'est une seule machine qui est relié a la fois à h1 et h2.

​	On utilise la commande *route* pour etablir la connexion avec les machines connectées au h1 et h2.

- sur la machine  1 et 2 , on tape la commande suivante:

````
route add -net 10.10.0.0/16 gw 192.168.1.254
````

- sur la machine 3, on n'a pas besoin cette commande, car par default elle est deja connectés à 2 hubs, mais on autorise de faire la passerelle en tapant la commande suivante :

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

- sur la machine 4 on tape la commande 

````
route add -net 192.168.1.0/24 gw 10.10.255.254
````

### Teste de la connexion

de la machine 1 vers la machine 4 :

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

On voit que la passerelle est bien configurer.

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

La différence en utilisant default est que m3 est maintenant la passerelle pour tous les réseaux et pas seulement pour les réseaux que l'on a créé. De plus, la commande route met beaucoup plus de temps à afficher la ligne correspondant à la passerelle lorsqu'elle est configurée par défaut.

Pour observer cette différence, il faudrait chercher à joindre un autre réseau et utiliser un outil comme wireshark pour analyser les trames.

## Le rôle de ICMP dans le routage IP : un cas de figure

en tentant un ping sur la machine m4, on obtient le résultat indiqué dans le sujet.

### configuration de l'IP de l'interface eth0 sur m1

Rien ne se passe car la passerrelle n'est pas configurée sur m1.

### configuration de m3 comme passerelle par défault sur m1

on observe des requêtes du protocole ARP, demandant la machine correspondant à l'addresse IP de la passerelle. Comme celle ci n'est pas configurée, les requêtes restent sans réponse.

### configuration des IPs des interfaces eth0 et eth1 sur m3

Une fois machione 3 configuré, on observe maintenant des requêtes du protocole ICMP envoyé par m1, mais commme la ip_forwarding n'est pas activé, on n'a pas de reponse.

### activation routage sur m3

- Une fois ip_forwading activer on voit que m3 repond a m1 en disant que m4 n'est pas atteignable en utilisant le protocole ICMP. Il ne s'agit ni d'un message de type REPLY ni d'un message de type ECHO mais d'un message de type HOST UNREACHABLE. Sur m4, on voit une requête ARP originant de m3, demandant à quelle machine correspond l'adresse 10.10.0.4 .

### configuration l'interface eth0 sur M4

- La situation est amelioré dans le sens que m1 envoie des messages a m4(ICMP de type ECHO) mais comme la passerelle n'est pas configuré sur m4, m4 ne reponds pas.
- Sur les deux reseaux on observe meme type des trames du protocole ICMP de type ECHO. 

### configuration de m3 comme passerelle par défault sur m4

  Une fois passerelle configurer le ping $m1 \rightarrow m4$ finalement fonctionne.



