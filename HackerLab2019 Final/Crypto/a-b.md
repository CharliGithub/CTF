* * *
# a^b
> (Crypto, 300 points )
---
## Challenge :
> 4354465f4f6e6542797465586f724973426164617307

Pour ce challenge, nous avons un texte en **hexadecimal**. Essayons de le **convertir** donc en **ascii**.
Pour le faire, on utilisera ```python```.

```console
root@Y3HW3_H4CK3R:~/HackerLab2019# python
>>> "4354465f4f6e6542797465586f724973426164617307".decode("hex")
'CTF_OneByteXorIsBadas\x07'
```
Ici, nous remarquons qu’il manque un caractère pour valider le flag. Du coup, on se tourne vers les autocollants distribués puis nous voyons sur l'un ```I am a bada$$ r3verse ENGIN33R.``` 

On remplace donc notre dernier caractère par ```s```, puis nous retrouvons le ```flag```.

```Flag ```: **CTF_OneByteXorIsBadass**
