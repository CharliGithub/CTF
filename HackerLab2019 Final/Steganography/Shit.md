* * *
# Shit! 
> (Steganography, 300 points )
---
## Challenge :
> [ [file](File/file ) ]

Pour ce challenge, le fichier à analyser est compressé. En faisant l'extraction, on constate que ce fichier contient des repertoires comme **```xl, _rels, docProps```**, et un fichier **```xml```**. Notre premier réflexe a donc été de revoir le ```format``` du fichier compressé.
```console
root@Y3HW3_H4CK3R:~/HackerLab2019# file file
file: Microsoft Excel 2007+
``` 
On remarque donc que le fichier compressé était à l'origine un fichier **excel**. Pour alors obtenir le fichier excel de départ, il a fallu exécuter la commande ci-dessous : 
```console
root@Y3HW3_H4CK3R:~/HackerLab2019# unzip -p file > file.csv
root@Y3HW3_H4CK3R:~/HackerLab2019# cat file.csv | grep CTF
 <sst xmlns="http://schemas.openxmlformats.org/spreadsheetml/2006/main" count="1" uniqueCount="1"><si><t xml:space="preserve">CTF_thaiq0H_ze8Hoow </t></si></sst><?xml version="1.0" encoding="UTF-8" standalone="yes"?>
``` 

```Flag : ``` **CTF_thaiq0H_ze8Hoow**