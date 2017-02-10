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

La différence en utilisant default est que m3 est maintenant la passerelle pour tous les réseaux et pas seulement pour les réseaux que l'on a créé. De plus, la commande route met beaucoup plus de temps à afficher la ligne correspondant à la passerelle lorsqu'elle est configurée par défaut.

Pour observer cette différence, il faudrait chercher à joindre un autre réseau et utiliser un outil comme wireshark pour analyser les trames.

## Le rôle de ICMP dans le routage IP : un cas de figure ##

en tentant un ping sur la machine m4, on obtient le résultat indiqué dans le sujet.

### configuration de l'IP de l'interface eth0 sur m1 ###

Rien ne se passe car la passerrelle n'est pas configurée sur m1.

### configuration de m3 comme passerelle par défault sur m1 ###

on observe des requêtes du protocole ARP, demandant la machine correspondant à l'addresse IP de la passerelle. Comme celle ci n'est pas configurée, les requêtes restent sans réponse.

### configuration des IPs des interfaces eth0 et eth1 sur m3 ###

Une fois machione 3 configuré, on observe maintenant des requêtes du protocole ICMP envoyé par m1, mais commme la ip_forwarding n'est pas activé, on n'a pas de reponse.

### activation routage sur m3 ###
 - Une fois ip_forwading activer on voit que m3 repond a m1 en disant que m4 n'est pas atteignable en utilisant le protocole ICMP. Il ne s'agit ni d'un message de type REPLY ni d'un message de type ECHO mais d'un message de type HOST UNREACHABLE. Sur m4, on voit une requête ARP originant de m3, demandant à quelle machine correspond l'adresse 10.10.0.4 .

### configuration l'interface eth0 sur M4 ###
 - La situation est amelioré dans le sens que m1 envoie des messages a m4(ICMP de type ECHO) mais comme la passerelle n'est pas configuré sur m4, m4 ne reponds pas.
 - Sur les deux reseaux on observe meme type des trames du protocole ICMP de type ECHO. 
 

### configuration de m3 comme passerelle par défault sur m4 ###
  Une fois passerelle configurer le ping $m1 \rightarrow m4$ finalement fonctionne.
