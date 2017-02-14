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
ifconfig eth0:lan3 10.10.10.5/24
```

même chose pour m6 :
```
ifconfig eth0:lan3 10.10.10.6/24
```
