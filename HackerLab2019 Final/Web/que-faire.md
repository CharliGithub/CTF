* * *
# Que faire ?
> (Web, 100 points )
---
## Challenge :
> Pour défendre notre cyber-contrée, les cyber-amazones devaient choisir la bonne méthode. http://hackerlab.bj:8001/web01/web01_sqfrs35_quefaire.php

Concernant ce challenge, le lien affiche une page vide. Pareil quand on tente d'afficher le code source. Si on fait attention au texte de présentation du challenge, on remarque qu’il parle de bonne ```méthode``` à choisir. Nous avions donc poussé notre réflexion vers les ```méthodes HTTP```. Une liste des méthodes ```HTTP``` se retrouve sur cette page https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol . L'objectif sera donc d'examiner les ```réponses``` qu'on aura du serveur quand on tentera d'accéder au lien avec une méthode ```HTTP``` spécifique. Pour le faire, exécutons la commande ci-dessous :
```console
root@Y3HW3_Hack3r:~/HackerLab2019# for i in {"GET","HEAD","POST","PUT","DELETE","CONNECT","OPTIONS","TRACE","PATCH"}; do curl -X $i http://hackerlab.bj:8001/web01/web01_sqfrs35_quefaire.php ; done
Warning: Setting custom HTTP method to HEAD with -X/--request may not work the 
Warning: way you want. Consider using -I/--head instead.
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>400 Bad Request</title>
</head><body>
<h1>Bad Request</h1>
<p>Your browser sent a request that this server could not understand.<br />
</p>
<hr>
<address>Apache/2.4.38 (Debian) Server at 172.24.0.2 Port 80</address>
</body></html>
CTF_34GFGLFRFE343432323R2
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>405 Method Not Allowed</title>
</head><body>
<h1>Method Not Allowed</h1>
<p>The requested method TRACE is not allowed for the URL /web01/web01_sqfrs35_quefaire.php.</p>
<hr>
<address>Apache/2.4.38 (Debian) Server at hackerlab.bj Port 8001</address>
</body></html>
```
En regardant minitieusement la sortie obtenue, on aperçoit notre flag **CTF_34GFGLFRFE343432323R2**.

```Flag ```: **CTF_34GFGLFRFE343432323R2**
