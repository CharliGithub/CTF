* * *
# Damn Url shortener
> (Forensic, 300 points )
---
## Challenge :
> L'unité Forensic a collecté beaucoup d'urls raccourcies et ne sait pas laquelle est la bonne. Elle sait néamoins que Djakpataglo utilisait l'une de ces urls raccourcies pour des attaques de phishing contre les membres du gouvernement. [ [url_list.tar.xz](File/url_list.tar.xz ) ]

Après extraction du fichier du challenge, on obtient un fichier [ [url_list](File/url_list) ] contenant une gande liste d'une url raccourcies. Essayons de voir le nombre exact d'URL contenu dans ce fichier.
```console
root@Y3HW3_Hack3r:~/HackerLab2019# wc -l url_list
27849 url_list
```

Il serait carrément fastidieux pour nous, de tester la sortie de toutes les URLs contenues dans ce fichier. Le premier réflèxe a été de ressortir les URLs non dupliquées du fichier, c'est-à-dire ceux qui apparaissent une et une seule fois. Pour le faire, exécutons la commande ci-dessous :

```console
root@Y3HW3_Hack3r:~/HackerLab2019# sort url_list | uniq -u
https://bit.ly/2oQSSN6
https://bit.ly/VhhKEvd
https://bit.ly/VhhKEvf
https://bit.ly/VhhKEvg
```

En testant la sortie de la première URL raccourcie , on est redirigé sur ce domaine : **http://dev2608.hackerlab.bj:8001/for_2/** . 
En retirant le sous-domaine **dev2608** de l'URL, on fini par retrouver le ```flag``` sur ce domaine http://hackerlab.bj:8001/for_2/ . 


```Flag ```: **CTF_HackerLabBestForensicSearcherIsYOU**
