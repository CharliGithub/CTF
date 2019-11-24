* * *
# Photo de famille
> (Steganography, 100 points )
---
## Challenge :
> Un souvenir inoubliable!  [ [amazones.jpg](File/amazones.jpg ) ]

L'objectif du challenge est d'arriver à retrouver un certain ```flag``` derrière cette image. Pour commencer, exécutons la commande ```strings``` , pour voir si on pourrait avoir une information intéressante.
```console
root@Y3HW3_Hack3r:~/HackerLab2019# strings -n 10 amazones.jpg
%&'()*456789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
&'()*56789:CDEFGHIJSTUVWXYZcdefghijstuvwxyz
>|)qiug,bk
```
Aucune information pouvant aider n'est retrouvée. De même, les outils tels que ```binwalk```, ```foremost```, ```exiftool``` n'ont rien révélé de suspect. Il a fallu utiliser l'outil ```steghide``` pour obtenir le ```flag```.

```console
root@Y3HW3_Hack3r:~/HackerLab2019# steghide extract -sf amazones.jpg
Entrez la passphrase: 
Ecriture des données extraites dans "flag.txt".
```
```Flag : ``` **CTF_YOUROCKTAKEYOURFLAG**