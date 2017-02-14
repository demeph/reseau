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

$m6 rightarrow m1$ (sur LAN1)
```
# 
```

$m6 rightarrow m5$ (sur LAN3)
```
# 
```

$m1 rightarrow m2$ (respectivement sur LAN1 et LAN2)
```
# 
```

On constate que les deux premiers pings sont un succès tandis que le dernier ping ne fonctionne pas. La raison derrière ce comportement est que les machines m1 et m2 ne sont pas sur le même réseau et qu'aucune passerelle entre ces réseaux n'est configurée.

## Polarité MDI/MDI-X
