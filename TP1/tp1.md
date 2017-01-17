Resultatde la commande **ifconfig** avant la configuration



```
lo       Link encap:Boucle locale
          inetadr:127.0.0.1  Masque:255.0.0.0 
          adrinet6: ::1/128 Scope:Hôte 
          UPLOOPBACK RUNNING  MTU:16436  Metric:1 
          RXpackets:192 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:192 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:0lg file transmission:0 
          RXbytes:52605 (20.3 KiB)  TX bytes:52605 (20.3 KiB) 
```



```
if config eth0 192.168.0.2 netmask 255.255.255.0
```

​	cette commande permet de mettre en place le reseau local, en attribuantl’adresse logique IP, c’est-à-dire affectel'adresse 192.168.0.2 à la première interface physique

Resultatde la commande **ifconfig** aprés la configuration:

```
eth0     Link encap:Ethernet  HWaddr 00:23:ae:a6:7f:f6  
          inetadr:192.168.0.2  Bcast:192.168.0.255  Masque:255.255.255.0 
          adrinet6: fe80::223:aeff:fea6:7ff6/64 Scope:Lien 
          UPBROADCAST MULTICAST  MTU:1500  Metric:1 
          RXpackets:247 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:123 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:10lg file transmission:1000 
          RXbytes:37369 (36.4 KiB)  TX bytes:16466 (16.0 KiB) 
          Interruption:16
          
lo       Link encap:Boucle locale  
          inetadr:127.0.0.1  Masque:255.0.0.0 
          adrinet6: ::1/128 Scope:Hôte 
          UPLOOPBACK RUNNING  MTU:16436  Metric:1 
          RXpackets:192 errors:0 dropped:0 overruns:0 frame:0 
          TXpackets:192 errors:0 dropped:0 overruns:0 carrier:0 
          collisions:0lg file transmission:0 
          RXbytes:52605 (51.3 KiB)  TX bytes:52605 (51.3 KiB) 
```

- Pour avoir le table de routage IP,  on utilise la commande Unix **route** et on obient

```
Table de routage IP du noyau 

Destination    Passerelle      Genmask         Indic Metric Ref    Use  Iface 
192.168.0.0    *               255.255.255.0   U     0      0        0  eth0 

```