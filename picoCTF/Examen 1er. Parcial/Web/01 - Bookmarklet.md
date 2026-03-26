## Bookmarklet
# Descripción
Why search for the flag when I can make a bookmarklet to print it for me?
Browse [here](http://titan.picoctf.net:50570/), and find the flag!
# Solución
Al entrar a la página que nos entregan, nos topamos con esto
![introflag](https://blog.qz.sg/content/images/2024/03/bookmarklet-site.webp)

Dentro de esta página, notamos que nos entregan un código en javascript
```
        javascript:(function() {
            var encryptedFlag = "àÒÆÞ¦È¬ëÙ£ÖÓÚåÛÑ¢ÕÓÓÇ¡¥Ìí";
            var key = "picoctf";
            var decryptedFlag = "";
            for (var i = 0; i < encryptedFlag.length; i++) {
                decryptedFlag += String.fromCharCode((encryptedFlag.charCodeAt(i) - key.charCodeAt(i % key.length) + 256) % 256);
            }
            alert(decryptedFlag);
        })();
    
```

Para hacer útil este código, lo vamos a ejecutar, pero esta vez lo haremos dentro de la consola de las herramientas de desarrollador de nuestro navegador.

Al ejecutarlo, nos saldrá un pop-up con la bandera
![[01book02.png]]
picoCTF{p@g3_turn3r_0c0d211f}
# Notas adicionales
- 
# Referencias
- Imagen tomada de aquí: https://blog.qz.sg/picoctf-2024-web-exploitation-writeups/