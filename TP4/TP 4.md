 *JAMET Félix - PHALAVANDISHVILI Demetre*

# TP 4#

## Etude du protocole UDP##

```
No.     Time        Source                Destination           Protocol Info
      1 0.000000    192.168.1.1           192.168.1.2           DNS      Standard query A www.google.fr

Frame 1 (73 bytes on wire, 73 bytes captured)
Ethernet II, Src: BbnInter_bf:bf:bb (02:04:06:bf:bf:bb), Dst: BbnInter_e3:c4:48 (02:04:06:e3:c4:48)
    ...
    Type: IP (0x0800)
Internet Protocol, Src: 192.168.1.1 (192.168.1.1), Dst: 192.168.1.2 (192.168.1.2)
    Version: 4
    Header length: 20 bytes
    ...
    Total Length: 59
    ...
    Time to live: 64
    Protocol: UDP (0x11)
    Header checksum: 0xb75e [correct]
        [Good: True]
        [Bad : False]
    Source: 192.168.1.1 (192.168.1.1)
    Destination: 192.168.1.2 (192.168.1.2)
User Datagram Protocol, Src Port: shilp (2049), Dst Port: domain (53)
    Source port: shilp (2049)
    Destination port: domain (53)
    Length: 39
    Checksum: 0x7028 [correct]
        [Good Checksum: True]
        [Bad Checksum: False]
Domain Name System (query)
    Transaction ID: 0xdd46
    Flags: 0x0100 (Standard query)
    ...
    Questions: 1
    ...
    Queries
        www.google.fr: type A, class IN
            Name: www.google.fr
            Type: A (Host address)
            Class: IN (0x0001)

No.     Time        Source                Destination           Protocol Info
      2 0.000377    192.168.1.2           192.168.1.1           ICMP     Destination unreachable (Port unreachable)
```

​	Les champs différents sont les suivants : 

- les adresses MAC

  ​	Chaque machine a son unique adresse MAC;

- le nom du source port

  ​	Le numero port c'est le même. la dfference de nom on peux expliquer comme la nom du service du protocole *UDP* utilisant *2049*;

- le checksum de la partie UDP

  ​	checksum(contrôle de somme) permet de s'assurer de l'intégrité du paquet reçu quand elle est différente de zéro. Elle est calculée sur l'ensemble de l'en-tête UDP et des données, mais aussi sur un pseudo en-tête;

- transaction ID de la partie DNS

  ​	L'ID de transaction est créée par l'expéditeur du message(dans notre cas m1) et est copié par le répondeur(machine m2) dans son message de réponse. À l'aide de l'ID de transaction, le client DNS peut correspondre à des réponses à ses demandes;

- le temps de la requête (Time)

Les autres champs sont identiques.



## Étude du protocole TCP

### Question 1

```
No.     Time        Source                Destination           Protocol Info
  1 0.000000    192.168.1.1           192.168.1.2           TCP      4083 > http [SYN] Seq=0 Win=5840
  2 0.000343    192.168.1.2           192.168.1.1           TCP      http > 4083 [SYN, ACK] Seq=0 Ack=1 Win=5792
  3 0.000287    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=1 Ack=1 Win=5840 
  4 0.020884    192.168.1.1           192.168.1.2           HTTP     GET / HTTP/1.0
  5 0.020911    192.168.1.2           192.168.1.1           TCP      http > 4083 [ACK] Seq=1 Ack=216 Win=6864
  6 0.068318    192.168.1.2           192.168.1.1           HTTP     HTTP/1.1 200 OK (text/html)
  7 0.068594    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=216 Ack=297 Win=6912
  8 0.069314    192.168.1.2           192.168.1.1           TCP      http > 4083 [FIN, ACK] Seq=297 Ack=216 Win=6864
  9 0.113180    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=216 Ack=298 Win=6912
  10 0.113182    192.168.1.1           192.168.1.2           TCP      4083 > http [FIN, ACK] Seq=216 Ack=298 Win=6912
  11 0.113213    192.168.1.2           192.168.1.1           TCP      http > 4083 [ACK] Seq=298 Ack=217 Win=6864
```

-  	L'ordres de trames c'est exactement même, les numeros des sequences et des accusés reception sont exactement même que dans la feuille de TP. Une seule difference qu'on peut observer c'est le difference nom de machine, au lieu de m1 on a 4083.
- ​        Les trois 1er trames corresponda à l'ouverture d'une connexion *TCP* entre les machine m1 et m2. La machine m1 est client et la machine m2 est un serveur. Toute 1ere trame signifie que le client demande à une serveur d'ouvrir une connexion en envoyant indicateur SYN. Le serveur(m2) alloue un socket et l'associe au socket client(m1). Après le serveur repond à la demande de connexion SYN en envoyant un accusé de reception ACK (ACK= seqInitial +1= 0 + 1 = 1) avec son propr requête  de synchronisation (SYN). Puis le client reçoit le message du serveur et repond par une accusé de reception. A partir de là la connexion TCP est completement ouvert entre le client et serveur.	

