* * *
# Fichier corrompu
> (Steganography, 150 points )
---
## Challenge :
> Les agents de DJAKPATAGLO ont trouvé une nouvelle astuce: corrompre des fichiers pour exfiltrer des données. L'astuce a été encore une fois découverte par le bjCSIRT qui sollicite votre expertixe pour lire le contenu de ce fichier.  [ [chal.png](File/chal.png ) ]

L'objectif de ce challenge est d'arriver à lire le contenu d'un fichier corrompu.
Le fichier téléchargé porte une extension ```.png```, donc évidemment une image. Or, lorsqu'on exécute la commande ```file``` sur ce dernier ```chal.png```, on constate qu'il n'en est pas un. 
```console
root@Y3HW3_Hack3r:~/HackerLab2019# file chal.png
chal.png: data
```

Utilisons l'outil ```xxd``` pour vérifier le ```header``` du fichier.
```console
root@Y3HW3_Hack3r:~/HackerLab2019# xxd -l 16 chal.png
00000000: 9051 4e47 0d0a 1a0a 0000 000d 4948 4452  .QNG........IHDR
```
On remarque très rapidement que le ```header``` du fichier a subit une légère modification. Normalement, un fichier ```.PNG``` est censé avoir cette signature (**magic bytes**) ```8950 4e47 0d0a 1a0a```.  
Le défi consistera donc à ajuster le header du fichier corrompu. Pour cela, il faudra exécuter la commande ci-dessous :
```console
root@Y3HW3_Hack3r:~/HackerLab2019# printf '\x89\x50' | dd of=chal.png bs=1 seek=0 conv=notrunc
2+0 enregistrements lus
2+0 enregistrements écrits
2 octets copiés, 0,000136671 s, 14,6 kB/s
```
<b>Image obtenue en sortie</b> : <a href="File/chal_2.png" target="_blank">chal.png</a>  
Une fois l'opération terminée, on remarque que le fichier ```chal.png``` est maintenant lisible. Une fois ouvert, nous voyons le ```flag``` du challenge apparaître sur l'image.  
```Flag : ``` **CTF_Amazone_Slayer**