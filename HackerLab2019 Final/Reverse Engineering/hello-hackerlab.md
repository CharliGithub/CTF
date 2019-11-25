* * *
# Hello HackerLab
> (Reverse Engineering, 300 points )
---
## Challenge :
>  [ [hello-hackerlab.crx](File/hello-hackerlab.crx ) ]

Une fois le fichier du challenge téléchargé, on remarque qu'il porte l'extension ```.crx```. Les fichiers avec l’extension ```CRX``` sont des plugins associés au navigateur ```Google Chrome```. Pour comprendre le fonctionnement du plugin, il serait intéressant d'avoir son code source. Pour l'obtenir, nous utiliserons une plateforme web qui se chargera de nous extraire le code source de l'extension. Cette fameuse plateforme est accessible à cette adresse https://crxextractor.com/ .  
> Uploader le fichier à extension ```.crx```, puis télécharger le code source 

Après l'avoir fait, vous obtiendrez un fichier zip contenant le code source du plugin ```hello hackerlab```. (<a href="File/hello-hackerlab.zip">hello-hackerlab.zip</a>)

Concernant les plugins pour navigateur, le code décrivant la logique de fonctionnement du plugin se retrouve dans le fichier ```main.js```. Essayons donc de voir le contenu de ce fichier.

```js
chrome.app.runtime.onLaunched.addListener(function() {
  // Center window on screen.
  var screenWidth = screen.availWidth;
  var screenHeight = screen.availHeight;
  var width = 500;
  var height = 300;
  //console.log("43,54,46,5f,59,6f,75,57,69,6e,54,68,65,43,68,72,6f,6d,65,41,70,70,52,65,76,65,72,73,65,42,65,67,69,6e,6e,65,72,42,61,64,67,65");

  chrome.app.window.create('index.html', {
    id: "helloWorldID",
    outerBounds: {
      width: width,
      height: height,
      left: Math.round((screenWidth-width)/2),
      top: Math.round((screenHeight-height)/2)
    }
  });
});

```
On remarque dans le code ```js```, un commentaire assez suspect. En effet, une suite de code ```hexadécimal``` est passée en argument à la fonction ```console.log()```. Cherchons donc le correspondant ```ascii``` de ce code. 

```console
root@Y3HW3_Hack3r:~/HackerLab2019# python
Python 2.7.16 (default, Apr  6 2019, 01:42:57) 
[GCC 8.3.0] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> a = "43,54,46,5f,59,6f,75,57,69,6e,54,68,65,43,68,72,6f,6d,65,41,70,70,52,65,76,65,72,73,65,42,65,67,69,6e,6e,65,72,42,61,64,67,65".replace(",","")
>>> a.decode('hex')
'CTF_YouWinTheChromeAppReverseBeginnerBadge'
>>> 
```


```Flag ```: **CTF_YouWinTheChromeAppReverseBeginnerBadge**
