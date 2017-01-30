# TP 2 reseaux #
##Cablage et configuration de base ##

Après avoir brancher tous les machines avec swithc, on attribue a chaque machine adrresse ip en utilisant les commande suivantes
- ifconfig eth0 192.168.1.1 netmask 255.255.255.0
- ifconfig eth0 192.168.1.2 netmask 255.255.255.0
- ifconfig eth0 192.168.1.3 netmask 255.255.255.0


Une fois configurer on utilise la commande *ping* pour verifier les liaisons
 - A partir de la machine m1
 ping 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=27.4 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.777 ms
64 bytes from 192.168.1.2: icmp_seq=3 ttl=64 time=0.791 ms
64 bytes from 192.168.1.2: icmp_seq=4 ttl=64 time=1.16 ms
64 bytes from 192.168.1.2: icmp_seq=5 ttl=64 time=0.928 ms
64 bytes from 192.168.1.2: icmp_seq=6 ttl=64 time=0.514 ms

--- 192.168.1.2 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5059ms
rtt min/avg/max/mdev = 0.514/5.271/27.456/9.923 ms

 ping 192.168.1.3
PING 192.168.1.3 (192.168.1.3) 56(84) bytes of data.
64 bytes from 192.168.1.3: icmp_seq=1 ttl=64 time=23.6 ms
64 bytes from 192.168.1.3: icmp_seq=2 ttl=64 time=0.832 ms
64 bytes from 192.168.1.3: icmp_seq=3 ttl=64 time=3.17 ms
64 bytes from 192.168.1.3: icmp_seq=4 ttl=64 time=1.59 ms
64 bytes from 192.168.1.3: icmp_seq=5 ttl=64 time=1.55 ms
64 bytes from 192.168.1.3: icmp_seq=6 ttl=64 time=0.791 ms


--- 192.168.1.3 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, times 6059ms
rtt min/avg/max/mdev = 0.791/4.680/23.621/7.768 ms


- ping realiser a partir la machine m2
ping -192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=12.7 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.742 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=2.72 ms
64 bytes from 192.168.1.1: icmp_seq=4 ttl=64 time=0.934 ms
64 bytes from 192.168.1.1: icmp_seq=5 ttl=64 time=0.775 ms
64 bytes from 192.168.1.1: icmp_seq=6 ttl=64 time=0.408 ms

--- 192.168.1.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5056ms
rtt min/avg/max/mdev = 0.408/3.057/12.764/4.405 ms

ping 192.168.1.3
PING 192.168.1.3 (192.168.1.3) 56(84) bytes of data.
64 bytes from 192.168.1.3: icmp_seq=1 ttl=64 time=21.0 ms
64 bytes from 192.168.1.3: icmp_seq=2 ttl=64 time=0.785 ms
64 bytes from 192.168.1.3: icmp_seq=3 ttl=64 time=0.541 ms
64 bytes from 192.168.1.3: icmp_seq=4 ttl=64 time=1.18 ms
64 bytes from 192.168.1.3: icmp_seq=5 ttl=64 time=0.880 ms
64 bytes from 192.168.1.3: icmp_seq=6 ttl=64 time=1.71 ms

--- 192.168.1.3 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5044ms
rtt min/avg/max/mdev = 0.541/4.354/21.030/7.466 ms

- ping realiser a partir la machine m3
ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=21.3 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.730 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.774 ms
64 bytes from 192.168.1.1: icmp_seq=4 ttl=64 time=1.09 ms
64 bytes from 192.168.1.1: icmp_seq=5 ttl=64 time=0.680 ms
64 bytes from 192.168.1.1: icmp_seq=6 ttl=64 time=1.05 ms

--- 192.168.1.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5043ms
rtt min/avg/max/mdev = 0.521/0.807/1.091/0.204 ms

 ping -c 6 192.168.1.2
PING 192.168.1.2 (192.168.1.2) 56(84) bytes of data.
64 bytes from 192.168.1.2: icmp_seq=1 ttl=64 time=21.2 ms
64 bytes from 192.168.1.2: icmp_seq=2 ttl=64 time=0.832 ms
64 bytes from 192.168.1.2: icmp_seq=3 ttl=64 time=0.530 ms
64 bytes from 192.168.1.2: icmp_seq=4 ttl=64 time=0.826 ms
64 bytes from 192.168.1.2: icmp_seq=5 ttl=64 time=1.24 ms
64 bytes from 192.168.1.2: icmp_seq=6 ttl=64 time=0.582 ms

--- 192.168.1.2 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5039ms
rtt min/avg/max/mdev = 0.530/0.803/1.242/0.230 ms

Pour chaque requête  ping on voit que la premiere requête prend beaucoup plus de temps que les requets suivants, la raison de cette phenomene est que au debut quand on a juste confieguré notre réseau arp est vide donc il sait pas les adresses ip des autres machines; pour connaitre leurs adresses ils envoient la demande a chaque machine en demandant a qui appartient l'adresse donnée, une fois la machine ayant cet adresse reponds,  on etablie la connection avec cette machine.

### Debrancher une cable ###
  On ping la machine 1 a partir machine 3, quand on debrache la cable de la machine 1, on voit a la machine 3 la connexion est interrompu, apres quelques instants on a une message suivante *Destination Host Unreachable*, c-a-d que la machine n'est joinable, une fois on a rebranche la cable la communication avec la machine 1 est etablie.

## Configuration des noms symboliques ##

Avant atribuer les noms à nos machines  le fichier host est suivant:

127.0.0.1       localhost

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
127.0.0.1 a
127.0.0.1 m1

après la modification, on obtient :

192.168.1.2 m2 machine2
192.168.1.3 m3 machine3

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
127.0.0.1 a
127.0.0.1 m1

On applique la même demarche pour chaque machine
Dans la machine 2, on ajoute:
192.168.1.1 m1 machine1
192.168.1.3 m3 machine3

Dans la machine 3, on ajoute:
192.168.1.1 m1 machine1
192.168.1.2 m2 machine2

Testons nos modifications effectuer en utilisant l'option -c de la commande *ping* :
à patir la machine 1 
vers la machine 2:
ping -c 2 m2 donne :

PING m2 (192.168.1.2) 56(84) bytes of data.
64 bytes from m2 (192.168.1.2): icmp_seq=1 ttl=64 time=0.524 ms
64 bytes from m2 (192.168.1.2): icmp_seq=2 ttl=64 time=1.45 ms

--- m2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 0.524/0.987/1.451/0.464 ms

vers la machine 3:
PING m3 (192.168.1.3) 56(84) bytes of data.
64 bytes from m3 (192.168.1.3): icmp_seq=1 ttl=64 time=1.31 ms
64 bytes from m3 (192.168.1.3): icmp_seq=2 ttl=64 time=1.06 ms

--- m3 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 1.068/1.190/1.313/0.127 ms

à partir la machine 2
vers la machine m1:
ping -c 2 m1
PING m1 (192.168.1.1) 56(84) bytes of data.
64 bytes from m1 (192.168.1.1): icmp_seq=1 ttl=64 time=21.2 ms
64 bytes from m1 (192.168.1.1): icmp_seq=2 ttl=64 time=0.603 ms

--- m1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1007ms
rtt min/avg/max/mdev = 0.603/10.926/21.249/10.323 ms

vers la machine 3:
ping -c 2 m3
PING m3 (192.168.1.3) 56(84) bytes of data.
64 bytes from m3 (192.168.1.3): icmp_seq=1 ttl=64 time=21.2 ms
64 bytes from m3 (192.168.1.3): icmp_seq=2 ttl=64 time=1.55 ms

--- m3 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1016ms
rtt min/avg/max/mdev = 1.550/11.393/21.237/9.844 ms

à partir de la machine m3
vers la machine m1:
ping -c 2  m1
PING m1 (192.168.1.1) 56(84) bytes of data.
64 bytes from m1 (192.168.1.1): icmp_seq=1 ttl=64 time=22.1 ms
64 bytes from m1 (192.168.1.1): icmp_seq=2 ttl=64 time=0.700 ms

--- m1 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1017ms
rtt min/avg/max/mdev = 0.700/11.415/22.131/10.716 ms

vers la machine m2 :
ping -c 2  m2
PING m2 (192.168.1.2) 56(84) bytes of data.
64 bytes from m2 (192.168.1.2): icmp_seq=1 ttl=64 time=1.65 ms
64 bytes from m2 (192.168.1.2): icmp_seq=2 ttl=64 time=1.14 ms

--- m2 ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 999ms
rtt min/avg/max/mdev = 1.146/1.402/1.658/0.256 ms

On voit bien que la modification on apporté fonctionne car a chaque fois on ping vers une machine avec son nom, ping  affiche leur adresse IP respective.
L'option -c nbRequete de la ping permet definir le nombre data qu'on va envoyer vers la machine.