* * *
# Bad practice 
> (Miscellaneous, 100 points )
---
## Challenge :
> En respectant les règles d'hygienes informatique, on ne devrait pas être amenés à faire ca
9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5
Précédez la réponse de CTF_

Dans cette épreuve, nous sommes amenés à retrouver la chaîne de caractères ayant pour ```hash``` 9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5. Pour aller rapidement, on fera usage du célèbre logiciel ```buster``` (https://github.com/s0md3v/Hash-Buster), réputé pour le bruteforce des ```hash```.

```console
root@Y3HW3_H4CK3R:~/HackerLab2019# buster -s 9ed6c336c58699768ee0ff4782532203a06f541aec022015d8fa4b23813a36d5
_  _ ____ ____ _  _    ___  _  _ ____ ___ ____ ____
|__| |__| [__  |__|    |__] |  | [__   |  |___ |__/
|  | |  | ___] |  |    |__] |__| ___]  |  |___ |  \  v3.0

[!] Hash function : SHA-256
rasdzv3
```

```Flag : ``` **CTF_rasdzv3**