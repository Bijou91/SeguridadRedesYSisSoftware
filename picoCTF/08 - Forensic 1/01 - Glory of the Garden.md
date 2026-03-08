# Glory of the Garden

## Descripción
This file contains more than it seems.
Get the flag from garden.jpg 
![garden.jpg](https://challenge-files.picoctf.net/c_fickle_tempest/6013221da747114c37db29c554381dbe4bb4e746cf6bd880f9c3b5d0b495a823/garden.jpg).
## Solución
### Solución:
Al entrar al reto, lo único que nos entregan es un archivo jpg de una imagen
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/13_Forensic1]
└─$ file garden.jpg 
garden.jpg: JPEG image data, JFIF standard 1.01, resolution (DPI), density 72x72, segment length 16, baseline, precision 8, 2999x2249, components 3
```

La pista del reto nos habla de un reto, así que usaremos esta herramienta
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/13_Forensic1]
└─$ hexeditor garden.jpg
```

Dentro del editor, tenemos la opción de buscar por texto así que buscamos la palabra pico, que lleva al final del archivo, donde se encuentra la bandera junto a sus valores hexadecimales
```
pi
00230570  63 6F 43 54  46 7B 6D 6F   72 65 5F 74  68 61 6E 5F                                                                                          coCTF{more_than_
00230580  6D 33 33 74  73 5F 74 68   65 5F 33 79  33 33 39 31                                                                                          m33ts_the_3y3391
00230590  34 30 31 32  39 7D 0A                                                                                                                        40129}
```

picoCTF{more_than_m33ts_the_3y339140129}
## Notas
