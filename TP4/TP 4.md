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
  Chaque machine a son unique adresse MAC
- le nom du source port.
- le checksum de la partie UDP
- transaction ID de la partie DNS
- le temps de la requête (Time)

Les autres champs sont identiques.



## Étude du protocole TCP

### Question 1

```
No.     Time        Source                Destination           Protocol Info
  1 0.000000    192.168.1.1           192.168.1.2           TCP      4083 > http [SYN] Seq=0 Win=5840 Len=0 MSS=1460 TSV=4294963568 TSER=0 WS=1
  2 0.000343    192.168.1.2           192.168.1.1           TCP      http > 4083 [SYN, ACK] Seq=0 Ack=1 Win=5792 Len=0 MSS=1460 TSV=4294963407 TSER=4294963568 WS=1
  3 0.000287    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=1 Ack=1 Win=5840 Len=0 TSV=4294963568 TSER=4294963407
  4 0.020884    192.168.1.1           192.168.1.2           HTTP     GET / HTTP/1.0
  5 0.020911    192.168.1.2           192.168.1.1           TCP      http > 4083 [ACK] Seq=1 Ack=216 Win=6864 Len=0 TSV=4294963410 TSER=4294963570
  6 0.068318    192.168.1.2           192.168.1.1           HTTP     HTTP/1.1 200 OK (text/html)
  7 0.068594    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=216 Ack=297 Win=6912 Len=0 TSV=4294963574 TSER=4294963413
  8 0.069314    192.168.1.2           192.168.1.1           TCP      http > 4083 [FIN, ACK] Seq=297 Ack=216 Win=6864 Len=0 TSV=4294963413 TSER=4294963574
  9 0.113180    192.168.1.1           192.168.1.2           TCP      4083 > http [ACK] Seq=216 Ack=298 Win=6912 Len=0 TSV=4294963578 TSER=4294963413
  10 0.113182    192.168.1.1           192.168.1.2           TCP      4083 > http [FIN, ACK] Seq=216 Ack=298 Win=6912 Len=0 TSV=4294963579 TSER=4294963413
  11 0.113213    192.168.1.2           192.168.1.1           TCP      http > 4083 [ACK] Seq=298 Ack=217 Win=6864 Len=0 TSV=4294963418 TSER=4294963579
```

- L'ordres de trames c'est exactement pareil
- ​