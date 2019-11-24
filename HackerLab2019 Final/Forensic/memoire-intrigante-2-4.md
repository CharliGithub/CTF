* * *
# Un mémoire intrigante (2/4)
> (Forensic, 200 points )
---
## Challenge :
> Le bjCSIRT a été dépeché pour assiter l'OCRC lors de la perquisition du domicile du bras droit de DJAKPATAGLO. Arrivé sur les lieux, ils ont fait l'inventaire des objets trouvés. Parmi ces objets, un ordinateur allumé. L'équipe a naturellement procédé à l'acquisition de la mémoire vive de cet ordinateur. Lors de la phase d'analyse, ils ont découvert qu'un ficher texte ouvert contenait une information précieuse.

**```NB```**: Le dump de la mémoire vive est téléchargeable sur les clés USB, partagées lors de la phase présentielle de la finale du HackerLab2019. 

Le challenge parle d'un fichier texte ouvert et contenant une information précieuse. D'abord, vérifions si parmi les programmes lancés sur l'ordinateur perquisitioné, figure un programme pouvant éditer du contenu textuel.

```console 
root@Y3HW3_Hack3r:~/HackerLab2019# volatility -f memdump.mem --profile=Win7SP1x64 pslist
Volatility Foundation Volatility Framework 2.6
Offset(V)          Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
------------------ -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0xfffffa80018c9040 System                    4      0     86      559 ------      0 2019-10-25 09:48:51 UTC+0000                                 
0xfffffa8002a44420 smss.exe                276      4      2       29 ------      0 2019-10-25 09:48:51 UTC+0000                                 
0xfffffa800337cb30 csrss.exe               344    336      9      423      0      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa800314f910 wininit.exe             380    336      3       75      0      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa8003395b30 csrss.exe               392    372      9      466      1      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa80033a4060 winlogon.exe            432    372      3      108      1      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa8003366b30 services.exe            476    380      7      200      0      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa8003422b30 lsass.exe               492    380      8      732      0      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa80033dbb30 lsm.exe                 504    380     10      149      0      0 2019-10-25 09:48:52 UTC+0000                                 
0xfffffa80034c1060 svchost.exe             604    476     10      356      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa80034e1540 VBoxService.ex          668    476     11      116      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa80034f5b30 svchost.exe             732    476      7      286      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa8003525460 svchost.exe             816    476     23      608      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa8003590060 svchost.exe             896    476     28      543      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa8003599b30 svchost.exe             920    476     38     1095      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa80035ddb30 svchost.exe             336    476     19      499      0      0 2019-10-25 09:48:53 UTC+0000                                 
0xfffffa800361cb30 svchost.exe            1036    476     18      369      0      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa800364db30 dwm.exe                1168    896      3       71      1      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa800368b490 explorer.exe           1180   1152     31      955      1      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa800367cb30 spoolsv.exe            1240    476     13      289      0      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa80036ee450 taskhost.exe           1284    476      8      211      1      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa80036f6b30 svchost.exe            1308    476     18      311      0      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa800376a3e0 armsvc.exe             1412    476      4       73      0      1 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa80037f1060 VBoxTray.exe           1496   1180     12      156      1      0 2019-10-25 09:48:54 UTC+0000                                 
0xfffffa800387f060 Service_KMS.ex         1764    476      9      595      0      0 2019-10-25 09:48:55 UTC+0000                                 
0xfffffa8003320900 svchost.exe            1992    476      5       97      0      0 2019-10-25 09:48:56 UTC+0000                                 
0xfffffa80039dd6c0 WmiPrvSE.exe           2168    604      7      177      0      0 2019-10-25 09:48:58 UTC+0000                                 
0xfffffa800396bb30 WmiPrvSE.exe           2176    604      6      127      0      0 2019-10-25 09:48:58 UTC+0000                                 
0xfffffa8003a9fb30 SearchIndexer.         2620    476     13      645      0      0 2019-10-25 09:49:01 UTC+0000                                 
0xfffffa8003965060 svchost.exe            1744    476     23 --------      0      0 2019-10-25 09:49:36 UTC+0000                                 
0xfffffa8003a50060 svchost.exe            1984    476     13      317      0      0 2019-10-25 09:51:02 UTC+0000                                 
0xfffffa800380b060 wmpnetwk.exe           1196    476     15      442      0      0 2019-10-25 09:51:02 UTC+0000                                 
0xfffffa80038caaa0 svchost.exe            2248    476      7      342      0      0 2019-10-25 09:56:00 UTC+0000                                 
0xfffffa8001b07670 audiodg.exe            1988    816      4      122      0      0 2019-10-25 12:51:16 UTC+0000                                 
0xfffffa8001a86060 firefox.exe            2788   1912     60      918      1      0 2019-10-25 17:09:41 UTC+0000                                 
0xfffffa8001b62b30 firefox.exe            2480   2788     10      204      1      0 2019-10-25 17:09:41 UTC+0000                                 
0xfffffa800348b410 firefox.exe            2524   2788     25      344      1      0 2019-10-25 17:09:42 UTC+0000                                 
0xfffffa8001e8b530 firefox.exe            1384   2788     21      306      1      0 2019-10-25 17:09:42 UTC+0000                                 
0xfffffa80037af960 firefox.exe            3144   2788      0 --------      1      0 2019-10-25 17:09:42 UTC+0000   2019-10-25 17:09:48 UTC+0000  
0xfffffa80039a0060 firefox.exe            3708   2788     21      302      1      0 2019-10-25 17:09:43 UTC+0000                                 
0xfffffa8001cf0910 firefox.exe            2804   2788      0 --------      1      0 2019-10-25 17:09:44 UTC+0000   2019-10-25 17:10:49 UTC+0000  
0xfffffa8001cf3b30 firefox.exe            2368   2788     19      290      1      0 2019-10-25 17:09:46 UTC+0000                                 
0xfffffa8001c5f060 notepad.exe            4180   1180      1       64      1      0 2019-10-25 17:10:01 UTC+0000                                 
0xfffffa8001e85060 cmd.exe                4228   1180      1       23      1      0 2019-10-25 17:10:13 UTC+0000                                 
0xfffffa800309b6c0 conhost.exe            4236    392      2       57      1      0 2019-10-25 17:10:13 UTC+0000                                 
0xfffffa8001d2c060 telnet.exe             4296   4228      3       54      1      0 2019-10-25 17:10:32 UTC+0000                                 
0xfffffa800197db30 dangerous_malw         2556   1180      7      111      1      1 2019-10-25 17:12:13 UTC+0000                                 
0xfffffa8001cd4390 conhost.exe            4196    392      2       54      1      0 2019-10-25 17:12:14 UTC+0000                                 
0xfffffa8001cbf1f0 FTK Imager.exe         4288   1180     18      385      1      0 2019-10-25 17:12:48 UTC+0000                                 
```
Une analyse rapide de cette sortie, révèle la présence du célèbre programme d'édition de texte qui est **notepad**. La prochaine étape  serait de lister tous les fichiers à extension ```.txt```, se retrouvant sur l'ordinateur perquisitioné. Pour le faire, il faudra exécuter la commande suivante :

```console 
root@Y3HW3_Hack3r:~/HackerLab2019# volatility -f memdump.mem --profile=Win7SP1x64 filescan | grep .txt
Volatility Foundation Volatility Framework 2.6
0x000000007dc3dc00     16      0 R--rw- \Device\HarddiskVolume2\Users\cuckoo1\Desktop\flag.txt
0x000000007dec3700      1      1 -W-rw- \Device\HarddiskVolume2\Users\cuckoo1\AppData\Local\Temp\FXSAPIDebugLogFile.txt
0x000000007e0dd470     16      0 -W-rw- \Device\HarddiskVolume2\Users\cuckoo1\AppData\Roaming\Mozilla\Firefox\Profiles\rebrfz5b.default-release\SiteSecurityServiceState.txt
0x000000007e271b00     16      0 -W-rwd \Device\HarddiskVolume2\Users\cuckoo1\AppData\Roaming\Mozilla\Firefox\Profiles\rebrfz5b.default-release\gmp-widevinecdm\4.10.1440.19\LICENSE.txt.tmp
0x000000007e5c07d0      3      0 -W-rw- \Device\HarddiskVolume2\Users\cuckoo1\AppData\Roaming\Mozilla\Firefox\Profiles\rebrfz5b.default-release\cert_override.txt
0x000000007f496950     16      0 R--rw- \Device\HarddiskVolume2\Users\cuckoo1\AppData\Roaming\Mozilla\Firefox\Profiles\REBRFZ~1.DEF\pkcs11.txt
0x000000007fb9f700      3      0 -W-rw- \Device\HarddiskVolume2\Users\cuckoo1\AppData\Roaming\Mozilla\Firefox\Profiles\rebrfz5b.default-release\enumerate_devices.txt
```

On remarque de cette nouvelle sortie, la présence d'un fameux fichier ```flag.txt``` se trouvant dans le répertoire ```Desktop``` de l'utilisateur ```cuckoo1```. Conclusion évidente, notre ```flag``` se retrouve dans ce fichier. L'objectif serait maintenant de chercher à extraire le contenu de ce fichier. Pour cela, on utilisera le plugin ```mftparser```, que nous offre notre logiciel d'investigation numérique **Volatility**. La commande à exécuter est la suivante :

```console 
root@Y3HW3_Hack3r:~/HackerLab2019# volatility -f memdump.mem --profile=Win7SP1x64 mftparser > mft_output.txt
Volatility Foundation Volatility Framework 2.6
root@Y3HW3_Hack3r:~/HackerLab2019# grep -A 10 "flag.txt" mft_output.txt
2019-10-25 09:56:56 UTC+0000 2019-10-25 09:56:56 UTC+0000   2019-10-25 09:56:56 UTC+0000   2019-10-25 09:56:56 UTC+0000   Users\cuckoo1\Desktop\flag.txt

$OBJECT_ID
Object ID: 3839cfa5-0cf7-e911-a1d4-080027c1199a
Birth Volume ID: 80000000-3800-0000-0000-180000000100
Birth Object ID: 1b000000-1800-0000-4354-465f596f7552
Birth Domain ID: 65616c6c-7944-6573-6572-766541487567

$DATA
0000000000: 43 54 46 5f 59 6f 75 52 65 61 6c 6c 79 44 65 73   CTF_YouReallyDes
0000000010: 65 72 76 65 41 48 75 67 4d 61 6e                  erveAHugMan
--
0000000110: 6b 74 6f 70 5c 66 6c 61 67 2e 74 78 74 00 1f 00   ktop\flag.txt...
0000000120: 2e 00 2e 00 5c 00 2e 00 2e 00 5c 00 2e 00 2e 00   ....\.....\.....
0000000130: 5c 00 2e 00 2e 00 5c 00 2e 00 2e 00 5c 00 44 00   \.....\.....\.D.
0000000140: 65 00 73 00 6b 00 74 00 6f 00 70 00 5c 00 66 00   e.s.k.t.o.p.\.f.
0000000150: 6c 00 61 00 67 00 2e 00 74 00 78 00 74 00 18 00   l.a.g...t.x.t...
0000000160: 43 00 3a 00 5c 00 55 00 73 00 65 00 72 00 73 00   C.:.\.U.s.e.r.s.
0000000170: 5c 00 63 00 75 00 63 00 6b 00 6f 00 6f 00 31 00   \.c.u.c.k.o.o.1.
0000000180: 5c 00 44 00 65 00 73 00 6b 00 74 00 6f 00 70 00   \.D.e.s.k.t.o.p.
0000000190: 28 00 00 00 09 00 00 a0 1c 00 00 00 31 53 50 53   (...........1SPS
00000001a0: e2 8a 58 46 bc 4c 38 43 bb fc 13 93 26 98 6d ce   ..XF.L8C....&.m.
00000001b0: 00 00 00 00 00 00 00 00 60 00 00 00 03 00 00 a0   ........`.......
```
Dans le résultat de la commande précédente, on peut voir afficher notre ```flag```. 


```Flag ```: **CTF_YouReallyDeserveAHugMan**
