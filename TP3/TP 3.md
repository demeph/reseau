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
ifconfig eth1 10.1O.0.254 netmask 255.255.255.0 sur h2
```

- machine m4

```
ifconfig eth0 10.10.0.4 netmask 255.255.255.0
```



## Configuration d'un connexion avec la passerelle pour chaque machine

​	Pour établir une connexion avec les machines qui sont connecté au hub h2, on doit configurer la passerelle sur la machine 3 car c'est une seule machine qui est relié a la fois à h1 et h2.

​	On utilise la commande *route* pour etablir la connexion avec les machines connectées au h1 et h2.

- sur la machine  1 et 2 , on tape la commande suivante:

````
route add -net 10.10.0.0 netmask 255.255.255.0 gw 192.168.1.254
````

- sur la machine 3, on n'a pas besoin cette commande, car par default elle est deja connectés à 2 hubs, mais on autorise de faire la passerelle en tapant la commande suivante :

```
echo 1 > /proc/sys/net/ipv4/ip_forward
```

- sur la machine 4 on tape la commande 

````
route add -net 192.168.1.0 netmask 255.255.255.0 gw 10.10.0.254
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







