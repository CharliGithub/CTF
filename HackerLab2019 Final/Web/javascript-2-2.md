* * *
# Javascript 2/2
> (Web, 150 points )
---
## Challenge :
> http://hackerlab.bj:8001/web05/web05_eterfrgtrhtrh.html 

Après un clic sur le lien du challenge, on aperçoit une page vide. Notre premier réflexe a été d'afficher le code source de la page pour voir si on pourrait avoir certains contenus. Dans le code source de la page, on remarque un ```script javascript``` obfusqué.
```
$=~[];$={___:++$,$$$$:(![]+"")[$],__$:++$,$_$_:(![]+"")[$],_$_:++$,$_$$:({}+"")[$],$$_$:($[$]+"")[$],_$$:++$,$$$_:(!""+"")[$],$__:++$,$_$:++$,$$__:({}+"")[$],$$_:++$,$$$:++$,$___:++$,$__$:++$};$.$_=($.$_=$+"")[$.$_$]+($._$=$.$_[$.__$])+($.$$=($.$+"")[$.__$])+((!$)+"")[$._$$]+($.__=$.$_[$.$$_])+($.$=(!""+"")[$.__$])+($._=(!""+"")[$._$_])+$.$_[$.$_$]+$.__+$._$+$.$;$.$$=$.$+(!""+"")[$._$$]+$.__+$._+$.$+$.$$;$.$=($.___)[$.$_][$.$_];$.$($.$($.$$+"\""+"//"+$.$$__+$._$+"\\"+$.__$+$.$_$+$.$$_+"\\"+$.__$+$.$$_+$._$$+$._$+(![]+"")[$._$_]+$.$$$_+"."+(![]+"")[$._$_]+$._$+"\\"+$.__$+$.$__+$.$$$+"(\\\"\\"+$.__$+$.___+$._$$+"\\"+$.__$+$._$_+$.$__+"\\"+$.__$+$.___+$.$$_+"_\\"+$.__$+$.__$+$._$_+$.$_$_+"\\"+$.__$+$.$$_+$.$$_+$.$_$_+"\\"+$.__$+$.$$_+$._$$+$.$$__+"\\"+$.__$+$.$$_+$._$_+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$$_+$.___+$.__+"\\"+$.__$+$.___+$.$_$+"\\"+$.__$+$.$_$+$.$$_+$.$$__+$._$+$.$$_$+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$_$+$.$$_+"\\"+$.__$+$.$__+$.$$$+"\\"+$.__$+$.__$+$.__$+"\\"+$.__$+$.$$_+$._$$+"\\"+$.__$+$.__$+$.$$_+$._$+$.__+"\\"+$.__$+$.$_$+$.___+"\\"+$.__$+$.$_$+$.__$+"\\"+$.__$+$.$_$+$.$$_+"\\"+$.__$+$.$__+$.$$$+"\\"+$.__$+$.___+$.$$_+$._$+"\\"+$.__$+$.$$_+$._$_+"\\"+$.__$+$._$$+$.__$+$._$+$._+"\\\");"+"\"")())();
```
Pour obtenir le contenu en clair du script, il suffit de se rendre à cette adresse https://lelinhtinh.github.io/de4js/ pour déobfusquer le code js. Une fois sur la plateforme, il faudra : 
> Mettre le code obfusqué dans le champ de texte, sélectionner l'option JJencode 

Après cela, le contenu en clair apparaît. 
```
//console.log("CTF_JavascriptEncodingIsNothingForYou");
```
```Flag ```: **CTF_JavascriptEncodingIsNothingForYou**
