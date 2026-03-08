# Extensions

## Descripción
This is a really weird text file. Can you find the flag?
Get the flag from [TXT](https://challenge-files.picoctf.net/c_fickle_tempest/31fe772e6a4c71e867af0b2a93818e06d8f8ebf8af2a9615495d00356ff576da/flag.txt).
## Solución
### Solución:
Al entrar al reto, lo único que nos entregan es un archivo txt de una texto, pero al inspeccionarlo con linux, vemos que en realidad se trata de una imagen png
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/13_Forensic1]
└─$ file flag.txt  
flag.txt: PNG image data, 1697 x 608, 8-bit/color RGB, non-interlaced
```

Lo que debemos de hacer es renombrar el archivo para corregir el fallo y ponerle la extensión correspondiente
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/13_Forensic1]
└─$ mv flag.txt flag.png
```

Y al abrirlo, descubrimos nuestra flag
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/13_Forensic1]
└─$ open flag.png
```

![[picoCTF/08 - Forensic 1/imagenes/02Extensions.png]]

picoCTF{now_you_know_about_extensions}
## Notas
