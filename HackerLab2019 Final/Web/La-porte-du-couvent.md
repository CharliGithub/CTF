* * *
# La porte du couvent
> (Web, 400 points )
---
## Challenge :
> Dans leur élan pour secourir les dernières victimes du célèbre Gayeman DJAKPATAGLO, les cyber-amazones font face à la porte d'un couvent impénétrable. http://hackerlab.bj:8001/web03/web03_frjofjzefzf.html

En accédant au lien du challenge, on se voit présenter un formulaire.

<img src="Images/porte-couvent-1.png">

On remarque que, peu importe ce qu'on entre dans le champ  ```username``` et ```password```, on est redirigé sur une **URL** nous présentant une chaîne encodée en base64: **dm91cyBuJ8OqdGVzIHBsdXMgbG9pbiBkdSBsb2dpbjogZTc3OTFlY2U5ZGE1YTZlM2YwYWE2YmE3NzUzNmZiYzZiNzc4MDg5NQ==** . Pour décoder cette chaîne, il suffira d'exécuter la commande ci-dessous :
```console 
root@Y3HW3_Hack3r:~/HackerLab2019# base64 -d <<< "dm91cyBuJ8OqdGVzIHBsdXMgbG9pbiBkdSBsb2dpbjogZTc3OTFlY2U5ZGE1YTZlM2YwYWE2YmE3NzUzNmZiYzZiNzc4MDg5NQ=="
vous n'êtes plus loin du login: e7791ece9da5a6e3f0aa6ba77536fbc6b7780895
```
La chaîne décodée est : **vous n'êtes plus loin du login: e7791ece9da5a6e3f0aa6ba77536fbc6b7780895**. Ce message nous présente à la fin un hash. L'objectif serait maintenant de chercher à avoir le contenu du hash. Pour le faire, nous utiliserons un célèbre outil ```buster``` (https://github.com/s0md3v/Hash-Buster) , qui pourra nous aider à obtenir le contenu du ```hash```. 
```console 
root@Y3HW3_Hack3r:~/HackerLab2019# buster -s "e7791ece9da5a6e3f0aa6ba77536fbc6b7780895"
_  _ ____ ____ _  _    ___  _  _ ____ ___ ____ ____
|__| |__| [__  |__|    |__] |  | [__   |  |___ |__/
|  | |  | ___] |  |    |__] |__| ___]  |  |___ |  \  v3.0

[!] Hash function : SHA1
amazone

```
En un rien de temps, nous obtenons la chaîne se retrouvant derrière le ```hash``` : **amazone**.  
Cette chaîne obtenue représente donc notre ```login``` pour le formulaire de la page http://hackerlab.bj:8001/web03/web03_frjofjzefzf.html. L'objectif suivant serait maintenant de retrouver le ```mot de passe``` qui va avec ce ```login```. Pour l'obtenir, nous avions testé un **bruteforce** par **"POST"** sur le formulaire avec le célèbre outil ```hydra```, mais sans succès. Nous avions aussi essayé une **injection SQL** pour bypasser l'authenfication, mais sans succès aussi. En fin de compte, nous avions donc cherché à avoir un coup de main en cliquant sur le ```hint``` du challenge. L'indice dévoilé est en effet : **php type struggle**. Des recherches effectuées à partir de cet indice nous amène sur cette page https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Type%20Juggling. Cette page parle du **PHP Juggling type and magic hashes**. Méthode pouvant permettre de ```bypasser des comparaisons en php```. En fouillant un peu la page, on retrouve quelques extraits de **chaînes de caractères magiques** pouvant bypasser des comparaisons php utilisant ```==```.

| Hash | “Magic” Number / String    | Magic Hash                                    | Found By      |
| ---- | -------------------------- |:---------------------------------------------:| -------------:|
| MD5  | 240610708                  | 0e462097431906509019562988736854              | [@spazef0rze](https://twitter.com/spazef0rze/status/439352552443084800) |
| SHA1 | 10932435112                | 0e07766915004133176347055865026311692244      | Independently found by Michael A. Cleverly & Michele Spagnuolo & Rogdham |
| SHA-224 | 10885164793773          | 0e281250946775200129471613219196999537878926740638594636 | [@TihanyiNorbert](https://twitter.com/TihanyiNorbert/status/1138075224010833921) |
| SHA-256 | 34250003024812          | 0e46289032038065916139621039085883773413820991920706299695051332 | [@TihanyiNorbert](https://twitter.com/TihanyiNorbert/status/1148586399207178241) |
| SHA-256 | TyNOQHUS                | 0e66298694359207596086558843543959518835691168370379069085300385 | [@Chick3nman512](https://twitter.com/Chick3nman512/status/1150137800324526083)


Nous allons donc essayer ses différents **“Magic” Number / String** comme ```password``` pour voir le résultat.
```console 
root@Y3HW3_Hack3r:~/HackerLab2019# curl -X POST http://hackerlab.bj:8001/web03/loginform.php --data "username=amazone&password=240610708"
Flag: CTF_NOMDEHACKERCEQUETUESFORT
```
En testant le premier **“Magic” Number / String** ( **240610708** ) comme ```password```, on obtient notre ```flag```.

```Flag ```: **CTF_NOMDEHACKERCEQUETUESFORT**
