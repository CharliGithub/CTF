* * *
# Un mémoire intrigante (1/4)
> (Forensic, 200 points )
---
## Challenge :
> Le bjCSIRT a été dépeché pour assiter l'OCRC lors de la perquisition du domicile du bras droit de DJAKPATAGLO. Arrivé sur les lieux, ils ont fait l'inventaire des objets trouvés. Parmi ces objets, un ordinateur allumé. L'équipe a naturellement procédé à l'acquisition de la mémoire vive de cet ordinateur. Lors de la phase d'analyse, ils ont découvert une connexion étrange. Suivez la !


**```NB```**: Le dump de la mémoire vive est téléchargeable sur les clés USB, partagées lors de la phase présentielle de la finale du HackerLab2019. L'objectif du challenge, est d'arriver à retrouver une connexion étrange ayant eu lieu sur l'ordinateur allumé perquisitionné au domicile du bras droit de **DJAKPATAGLO**. Pour mener à bien notre investigation, nous utiliserons un célèbre outil du nom de **Volatility** (https://github.com/volatilityfoundation/volatility) . Commencons d'abord par réccupérer le **profil** du dump, c'est-à-dire l'architecture du système d'exploitation .

```console 
root@Y3HW3_Hack3r:~/HackerLab2019# volatility -f memdump.mem imageinfo
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
         Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_24000, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_24000, Win7SP1x64_23418
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/Y3HW3_Hack3r/HackerLab2019/memdump.mem)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf8000284d0a0L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff8000284ed00L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2019-10-25 17:13:20 UTC+0000
     Image local date and time : 2019-10-25 18:13:20 +0100

```
Après ceci, examinons toutes les connexions ayant été effectuées depuis la machine.

```console 
root@Y3HW3_Hack3r:~/HackerLab2019# volatility -f memdump.mem --profile=Win7SP1x64 netscan
Volatility Foundation Volatility Framework 2.6
Offset(P)          Proto    Local Address                  Foreign Address      State            Pid      Owner          Created
0x7dc5b4a0         UDPv4    0.0.0.0:5355                   *:*                                   1036     svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7dc70700         UDPv4    0.0.0.0:0                      *:*                                   668      VBoxService.ex 2019-10-25 17:13:27 UTC+0000
0x7dc73a70         UDPv4    0.0.0.0:3702                   *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7dc73a70         UDPv6    :::3702                        *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7dc76c70         UDPv4    0.0.0.0:60798                  *:*                                   1744     svchost.exe    2019-10-25 09:55:59 UTC+0000
0x7dc76c70         UDPv6    :::60798                       *:*                                   1744     svchost.exe    2019-10-25 09:55:59 UTC+0000
0x7de1f5f0         UDPv4    0.0.0.0:5355                   *:*                                   1036     svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7de1f5f0         UDPv6    :::5355                        *:*                                   1036     svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7de927f0         UDPv4    0.0.0.0:4500                   *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7de927f0         UDPv6    :::4500                        *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7de9dc20         UDPv4    0.0.0.0:500                    *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7de9dc20         UDPv6    :::500                         *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7de9f200         UDPv4    0.0.0.0:4500                   *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7de9f7a0         UDPv4    0.0.0.0:500                    *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7dea0c40         UDPv4    0.0.0.0:0                      *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7deae3b0         UDPv4    0.0.0.0:0                      *:*                                   1992     svchost.exe    2019-10-25 09:48:57 UTC+0000
0x7deae3b0         UDPv6    :::0                           *:*                                   1992     svchost.exe    2019-10-25 09:48:57 UTC+0000
0x7df93e00         UDPv4    0.0.0.0:0                      *:*                                   2248     svchost.exe    2019-10-25 09:56:00 UTC+0000
0x7df93e00         UDPv6    :::0                           *:*                                   2248     svchost.exe    2019-10-25 09:56:00 UTC+0000
0x7dfe8120         UDPv4    0.0.0.0:5004                   *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7dffe010         UDPv4    0.0.0.0:3702                   *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7dffe010         UDPv6    :::3702                        *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7e0deb60         UDPv4    0.0.0.0:123                    *:*                                   336      svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7e130090         UDPv6    fe80::34ad:187e:cad1:15d2:546  *:*                                   816      svchost.exe    2019-10-25 17:11:26 UTC+0000
0x7e17e3a0         UDPv4    0.0.0.0:0                      *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7e17e3a0         UDPv6    :::0                           *:*                                   920      svchost.exe    2019-10-25 09:48:55 UTC+0000
0x7e1b2010         UDPv4    0.0.0.0:0                      *:*                                   1992     svchost.exe    2019-10-25 09:48:57 UTC+0000
0x7e1ba5f0         UDPv4    127.0.0.1:61018                *:*                                   1744     svchost.exe    2019-10-25 17:11:31 UTC+0000
0x7e2661c0         UDPv6    ::1:61016                      *:*                                   1744     svchost.exe    2019-10-25 17:11:31 UTC+0000
0x7e2772c0         UDPv4    127.0.0.1:1900                 *:*                                   1744     svchost.exe    2019-10-25 17:11:27 UTC+0000
0x7e2891c0         UDPv6    fe80::34ad:187e:cad1:15d2:1900 *:*                                   1744     svchost.exe    2019-10-25 17:11:27 UTC+0000
0x7e385e00         UDPv4    0.0.0.0:5005                   *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7e385e00         UDPv6    :::5005                        *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7dc78ef0         TCPv4    10.0.2.15:139                  0.0.0.0:0            LISTENING        4        System         
0x7dd46d00         TCPv4    0.0.0.0:49159                  0.0.0.0:0            LISTENING        492      lsass.exe      
0x7de38ad0         TCPv4    0.0.0.0:49155                  0.0.0.0:0            LISTENING        476      services.exe   
0x7deae1f0         TCPv4    0.0.0.0:49156                  0.0.0.0:0            LISTENING        1992     svchost.exe    
0x7deae1f0         TCPv6    :::49156                       :::0                 LISTENING        1992     svchost.exe    
0x7debd7d0         TCPv4    0.0.0.0:2869                   0.0.0.0:0            LISTENING        4        System         
0x7debd7d0         TCPv6    :::2869                        :::0                 LISTENING        4        System         
0x7ded7970         TCPv4    0.0.0.0:554                    0.0.0.0:0            LISTENING        1196     wmpnetwk.exe   
0x7df73ef0         TCPv4    10.0.2.15:139                  0.0.0.0:0            LISTENING        4        System         
0x7df965d0         TCPv4    0.0.0.0:5357                   0.0.0.0:0            LISTENING        4        System         
0x7df965d0         TCPv6    :::5357                        :::0                 LISTENING        4        System         
0x7e0c0710         TCPv4    0.0.0.0:49154                  0.0.0.0:0            LISTENING        920      svchost.exe    
0x7e0c1980         TCPv4    0.0.0.0:49154                  0.0.0.0:0            LISTENING        920      svchost.exe    
0x7e0c1980         TCPv6    :::49154                       :::0                 LISTENING        920      svchost.exe    
0x7e19a260         TCPv4    0.0.0.0:49156                  0.0.0.0:0            LISTENING        1992     svchost.exe    
0x7e20a8b0         TCPv4    0.0.0.0:49159                  0.0.0.0:0            LISTENING        492      lsass.exe      
0x7e20a8b0         TCPv6    :::49159                       :::0                 LISTENING        492      lsass.exe      
0x7e2b3890         TCPv4    0.0.0.0:49153                  0.0.0.0:0            LISTENING        816      svchost.exe    
0x7e2b3890         TCPv6    :::49153                       :::0                 LISTENING        816      svchost.exe    
0x7e30a920         TCPv4    0.0.0.0:135                    0.0.0.0:0            LISTENING        732      svchost.exe    
0x7e30a920         TCPv6    :::135                         :::0                 LISTENING        732      svchost.exe    
0x7e30c1d0         TCPv4    0.0.0.0:135                    0.0.0.0:0            LISTENING        732      svchost.exe    
0x7e314450         TCPv4    0.0.0.0:49152                  0.0.0.0:0            LISTENING        380      wininit.exe    
0x7e314450         TCPv6    :::49152                       :::0                 LISTENING        380      wininit.exe    
0x7e362a90         TCPv4    0.0.0.0:3587                   0.0.0.0:0            LISTENING        2248     svchost.exe    
0x7e362a90         TCPv6    :::3587                        :::0                 LISTENING        2248     svchost.exe    
0x7e37e770         TCPv4    0.0.0.0:445                    0.0.0.0:0            LISTENING        4        System         
0x7e37e770         TCPv6    :::445                         :::0                 LISTENING        4        System         
0x7e3867e0         TCPv4    0.0.0.0:49153                  0.0.0.0:0            LISTENING        816      svchost.exe    
0x7dc84a90         TCPv4    -:0                            104.176.128.3:0      CLOSED           1764     Service_KMS.ex 
0x7dc88730         TCPv6    -:0                            68f0:8703:80fa:ffff:68f0:8703:80fa:ffff:0 CLOSED           1764     Service_KMS.ex 
0x7de8e5c0         TCPv4    10.0.2.15:49381                88.221.134.155:80    ESTABLISHED      2788     firefox.exe    
0x7dfb9800         TCPv4    10.0.2.15:0                    216.58.198.195:0     LISTENING        -1                      
0x7e07c7c0         TCPv6    -:0                            389b:5903:80fa:ffff:389b:5903:80fa:ffff:0 CLOSED           1        @y????       
0x7e0d0890         TCPv4    10.0.2.15:49372                92.123.180.89:80     ESTABLISHED      2788     firefox.exe    
0x7e0e7780         TCPv4    127.0.0.1:49378                127.0.0.1:2869       ESTABLISHED      1196     wmpnetwk.exe   
0x7e106cf0         TCPv4    -:49384                        196.49.8.205:443     CLOSED           2788     firefox.exe    
0x7e16c7f0         TCPv6    -:0                            4890:8c01:80fa:ffff:4890:8c01:80fa:ffff:0 CLOSED           1196     wmpnetwk.exe   
0x7e1f9cf0         TCPv6    -:0                            68f0:8703:80fa:ffff:68f0:8703:80fa:ffff:0 CLOSED           1764     Service_KMS.ex 
0x7e236850         TCPv4    10.0.2.15:49363                51.83.76.195:42000   ESTABLISHED      4296     telnet.exe     
0x7e2882e0         TCPv4    127.0.0.1:49324                127.0.0.1:49323      ESTABLISHED      2524     firefox.exe    
0x7e3037b0         TCPv4    127.0.0.1:49334                127.0.0.1:49333      ESTABLISHED      3708     firefox.exe    
0x7e30aab0         TCPv4    -:0                            56.91.79.3:0         CLOSED           1        @y????       
0x7e310cf0         TCPv4    -:0                            56.91.79.3:0         CLOSED           1        @y????       
0x7e38a2a0         TCPv4    -:49337                        -:80                 CLOSED           2788     firefox.exe    
0x7e550c00         UDPv4    0.0.0.0:5005                   *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7e5c5010         UDPv4    10.0.2.15:138                  *:*                                   4        System         2019-10-25 17:11:29 UTC+0000
0x7e6d9ec0         UDPv6    ::1:1900                       *:*                                   1744     svchost.exe    2019-10-25 17:11:27 UTC+0000
0x7e58f100         TCPv4    0.0.0.0:49155                  0.0.0.0:0            LISTENING        476      services.exe   
0x7e58f100         TCPv6    :::49155                       :::0                 LISTENING        476      services.exe   
0x7e7293d0         TCPv4    0.0.0.0:49152                  0.0.0.0:0            LISTENING        380      wininit.exe    
0x7e776480         TCPv4    0.0.0.0:10243                  0.0.0.0:0            LISTENING        4        System         
0x7e776480         TCPv6    :::10243                       :::0                 LISTENING        4        System         
0x7ec399d0         TCPv4    127.0.0.1:49333                127.0.0.1:49334      ESTABLISHED      3708     firefox.exe    
0x7ee68bb0         UDPv4    0.0.0.0:0                      *:*                                   2248     svchost.exe    2019-10-25 09:56:11 UTC+0000
0x7ee68bb0         UDPv6    :::0                           *:*                                   2248     svchost.exe    2019-10-25 09:56:11 UTC+0000
0x7eefcec0         UDPv4    0.0.0.0:60797                  *:*                                   1744     svchost.exe    2019-10-25 09:55:59 UTC+0000
0x7ef21590         UDPv4    0.0.0.0:123                    *:*                                   336      svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7ef21590         UDPv6    :::123                         *:*                                   336      svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7f1f9310         UDPv4    0.0.0.0:5004                   *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7f1f9310         UDPv6    :::5004                        *:*                                   1196     wmpnetwk.exe   2019-10-25 09:51:02 UTC+0000
0x7effb4e0         TCPv4    0.0.0.0:554                    0.0.0.0:0            LISTENING        1196     wmpnetwk.exe   
0x7effb4e0         TCPv6    :::554                         :::0                 LISTENING        1196     wmpnetwk.exe   
0x7ef17510         TCPv4    10.0.2.15:49380                52.222.237.163:443   ESTABLISHED      2788     firefox.exe    
0x7f8831d0         UDPv4    0.0.0.0:0                      *:*                                   336      svchost.exe    2019-10-25 09:59:00 UTC+0000
0x7f8831d0         UDPv6    :::0                           *:*                                   336      svchost.exe    2019-10-25 09:59:00 UTC+0000
0x7f89d9c0         UDPv4    0.0.0.0:0                      *:*                                   336      svchost.exe    2019-10-25 09:59:00 UTC+0000
0x7fa06b40         UDPv4    0.0.0.0:3702                   *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fa06b40         UDPv6    :::3702                        *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fa0bd60         UDPv4    0.0.0.0:3702                   *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fa84230         UDPv4    0.0.0.0:53500                  *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fb37010         UDPv4    0.0.0.0:3702                   *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7fb3bb80         UDPv4    10.0.2.15:137                  *:*                                   4        System         2019-10-25 17:11:29 UTC+0000
0x7fb5f660         UDPv4    0.0.0.0:0                      *:*                                   2248     svchost.exe    2019-10-25 09:56:00 UTC+0000
0x7fb5f660         UDPv6    :::0                           *:*                                   2248     svchost.exe    2019-10-25 09:56:00 UTC+0000
0x7fb61420         UDPv4    0.0.0.0:3702                   *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fb61420         UDPv6    :::3702                        *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fc774e0         UDPv4    0.0.0.0:3702                   *:*                                   1744     svchost.exe    2019-10-25 17:11:32 UTC+0000
0x7fc80be0         UDPv4    0.0.0.0:0                      *:*                                   1036     svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7fc80be0         UDPv6    :::0                           *:*                                   1036     svchost.exe    2019-10-25 17:11:29 UTC+0000
0x7fcba010         UDPv4    0.0.0.0:3702                   *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fd25560         UDPv4    0.0.0.0:49239                  *:*                                   336      svchost.exe    2019-10-25 17:09:21 UTC+0000
0x7fd2d010         UDPv4    10.0.2.15:1900                 *:*                                   1744     svchost.exe    2019-10-25 17:11:27 UTC+0000
0x7fd42a00         UDPv4    0.0.0.0:53501                  *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fd42a00         UDPv6    :::53501                       *:*                                   336      svchost.exe    2019-10-25 17:11:33 UTC+0000
0x7fd68a60         UDPv6    fe80::34ad:187e:cad1:15d2:61015 *:*                                   1744     svchost.exe    2019-10-25 17:11:31 UTC+0000
0x7fdc96c0         UDPv4    0.0.0.0:3540                   *:*                                   2248     svchost.exe    2019-10-25 09:56:11 UTC+0000
0x7fdc96c0         UDPv6    :::3540                        *:*                                   2248     svchost.exe    2019-10-25 09:56:11 UTC+0000
0x7ffab3a0         UDPv4    10.0.2.15:61017                *:*                                   1744     svchost.exe    2019-10-25 17:11:31 UTC+0000
0x7fa8a7f0         TCPv4    127.0.0.1:49348                127.0.0.1:49349      ESTABLISHED      2368     firefox.exe    
0x7fb02cf0         TCPv4    127.0.0.1:49322                127.0.0.1:49321      ESTABLISHED      2788     firefox.exe    
0x7fb14010         TCPv4    -:49364                        52.43.139.170:443    CLOSED           2788     firefox.exe    
0x7fb75ac0         TCPv4    10.0.2.15:49382                216.58.201.238:443   ESTABLISHED      2788     firefox.exe    
0x7fb83cf0         TCPv4    10.0.2.15:49383                216.58.198.195:80    ESTABLISHED      2788     firefox.exe    
0x7fc1a7a0         TCPv4    10.0.2.15:49375                54.148.100.30:443    ESTABLISHED      2788     firefox.exe    
0x7fc82480         TCPv4    127.0.0.1:49325                127.0.0.1:49326      ESTABLISHED      1384     firefox.exe    
0x7fcd88b0         TCPv4    127.0.0.1:49326                127.0.0.1:49325      ESTABLISHED      1384     firefox.exe    
0x7fd30cf0         TCPv4    -:49356                        -:443                CLOSED           2788     firefox.exe    
0x7fd5dcf0         TCPv4    10.0.2.15:49336                216.58.198.195:80    CLOSED           2788     firefox.exe    
0x7fd6b010         TCPv4    127.0.0.1:49321                127.0.0.1:49322      ESTABLISHED      2788     firefox.exe    
0x7fd706b0         TCPv4    127.0.0.1:49323                127.0.0.1:49324      ESTABLISHED      2524     firefox.exe    
0x7fe877f0         TCPv4    127.0.0.1:49349                127.0.0.1:49348      ESTABLISHED      2368     firefox.exe    
0x7feaa5d0         TCPv4    127.0.0.1:2869                 127.0.0.1:49378      ESTABLISHED      4        System         
0x7fee9310         TCPv4    10.0.2.15:49371                92.123.180.89:80     ESTABLISHED      2788     firefox.exe    

```
En examinant minitieusement la sortie du ```netscan```, on fini par retrouver une connexion étrange vers cette adresse ip **51.83.76.195** au port **42000** par l'utilitaire **telnet.exe**. 

Pour obtenir le flag, il a suffit joindre l'hôte **51.83.76.195** au port **42000** avec **telnet** .
```
telnet 51.83.76.195 42000
```
<!-- 

Essayons aussi de joindre cette adresse au port **42000**  avec l'utitaire ```telnet``` pour examiner la sortie .
```
root@Y3HW3_Hack3r:~/HackerLab2019# telnet 51.83.76.195 42000
``` -->
<!-- ```Flag ```: **** -->
