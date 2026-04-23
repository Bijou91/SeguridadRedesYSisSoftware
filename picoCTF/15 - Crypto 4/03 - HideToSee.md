# HideToSee

## Descripción
How about some hide and seek heh?
Look at this image [here](https://artifacts.picoctf.net/c/239/atbash.jpg).
## Solución
Comenzamos con descargar la imagen que nos dan, que es esta:
![img](https://artifacts.picoctf.net/c/239/atbash.jpg)

Dado que la pista sugería extraer algo de la imagen, vamos a utilizar stegseek en el archivo de la imagen
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/Crypto4/HideToSee]
└─$ stegseek atbash.jpg                            
StegSeek 0.6 - https://github.com/RickdeJager/StegSeek

[i] Found passphrase: ""
[i] Original filename: "encrypted.txt".
[i] Extracting to "atbash.jpg.out".
```

Como vemos, si que había algo escondido en la imagen, un texto que ha sido extraído al archivo atbash.jpg.out, al cual si le aplicamos un cat, nos muestra la flag
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/Crypto4/HideToSee]
└─$ cat atbash.jpg.out
krxlXGU{zgyzhs_xizxp_1u84w779}
```

Como podemos notar, sigue encriptada, así que usando CyberChef la desencriptamos con Atbash, ahora si obteniendo nuestra flag real
picoCTF{atbash_crack_1f84d779}
## Notas
- https://gchq.github.io/CyberChef/#recipe=Atbash_Cipher()&input=a3J4bFhHVXt6Z3l6aHNfeGl6eHBfMXU4NHc3Nzl9&ieol=CRLF&oeol=CRLF