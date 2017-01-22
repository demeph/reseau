# TP 1 - Reseaux 

Les  7 couches OSSI (plus haut niveau $\rightarrow $ bas niveau)

- Application 
- Presentation
- Session
- Transport qui ransporte les données et se charge que c'est bien reçu
- Reseau IP
- Liaison
- Physique

Tous ces couches  ça trouve sur une autre ordi qu'on est connecté

Chaque couche ajoute son informationn a l'entête de suite octets



Protocole TCP/IP

- Application
- TCP
- IP
- Physique

Les deux reseaux sont connectés via le routeur(IP IP) qui lui a aussi couche OSSI, et cette configuration on appelle Passerelle, il a deux sorties physique ( voir l'image de la feuille de TP)





Deux notions adresses : IP et MAC

### IP### 

-  adresse logique, deux machines connectées sur la meme reseau ont mem debut ip
-  met mask  23 bits après le 23eme bit on met les 0 pour avoir adresse reseau
-  223.157.9.254; qd on met que des 1 dans la partie de machine,ça signifie adresse de broadcast
-  255.255.255.0 on peut configurer que de 4 machine

#### 5 classes IP

##### A

1 bit diff + 7  bit de resaux : 246 machines

  $\rightarrow$ $2^7 $ reseaux = 1.0.0.0 $\rightarrow $ 127.0.0.0

  $\rightarrow  2^24$ 16 millions de machine

##### B

2 bits + 14 b reseaux + 16 b machines
 $2^16 machines 64000$ 128.0.0.0 $\rightarrow$ 191.255.0.0

##### C

3 bits + 21b reseau + 8b reseaux

 256 machines 192.0.0.0 -> 223.255.255.0

##### D

##### E



@phy = @mac 

​	= xx:xx:xx:xx:xx:xx

trois premiere block c'est pour le numero fabriquant OUI

et la reste c'est pour le numero de carte reseau don 2^24 cartes ethernet



ifconfig pour reconfigurer reseaux 

ifconfig eth0 @IP network @MASS

route

route add_net @res netmask @Mask gw @passerelle $\leftarrow$ pour communiquer avec une autre machine

ping @ip pour testela connexion

- 127.0.0.0 adresse fictive qui permet appertenir a la machine : LOCALHOST
- @Prive adresse prive, pas connecté au reseau mondiale
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0 /16
- On peut utiliser ce reseau sans aucun autorisation
- on a une adresse public qui permet de communquer avec le reseau mondiale











