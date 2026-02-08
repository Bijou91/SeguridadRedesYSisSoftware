# Glitch Cat
# Descripción
Our flag printing service has started glitching!
```
$ nc saturn.picoctf.net 50094
```

## Solución
- Comandos de Linux
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01_GeneralSkills/ObedientCat]
└─$ nc saturn.picoctf.net 50094                          
'picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32) + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01_GeneralSkills/ObedientCat]
└─$ python3
Python 3.13.9 (main, Oct 15 2025, 14:56:22) [GCC 15.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 'picoCTF{gl17ch_m3_n07_' + chr(0x39) + chr(0x63) + chr(0x34) + chr(0x32)\
 + chr(0x61) + chr(0x34) + chr(0x35) + chr(0x64) + '}'
'picoCTF{gl17ch_m3_n07_9c42a45d}'
>>> exit
```

picoCTF{gl17ch_m3_n07_9c42a45d}
## Notas
