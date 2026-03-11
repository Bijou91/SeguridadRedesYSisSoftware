# c0rrupt

## Descripción
We found this [file](https://challenge-files.picoctf.net/c_fickle_tempest/87bdc8ce30b177d033b3d68bca4647950bb07304032861baa912ebe08701d355/mystery). Recover the flag.
## Solución
Lo primero que haremos es aplicarle un file para ver qué tipo de archivo es
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ file mystery 
mystery: data
```
Solo nos dice que es data, esto pasa cuando el archivo se corrompe y linux no sabe como interpretarlo.

Entonces, revisaremos los magic bytes para ver con qué tipo de archivo vamos a trabajar
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ xxd -g 1 mystery | head
00000000: 89 65 4e 34 0d 0a b0 aa 00 00 00 0d 43 22 44 52  .eN4........C"DR
00000010: 00 00 06 6a 00 00 04 47 08 02 00 00 00 7c 8b ab  ...j...G.....|..
00000020: 78 00 00 00 01 73 52 47 42 00 ae ce 1c e9 00 00  x....sRGB.......
00000030: 00 04 67 41 4d 41 00 00 b1 8f 0b fc 61 05 00 00  ..gAMA......a...
00000040: 00 09 70 48 59 73 aa 00 16 25 00 00 16 25 01 49  ..pHYs...%...%.I
00000050: 52 24 f0 aa aa ff a5 ab 44 45 54 78 5e ec bd 3f  R$......DETx^..?
00000060: 8e 64 cd 71 bd 2d 8b 20 20 80 90 41 83 02 08 d0  .d.q.-.  ..A....
00000070: f9 ed 40 a0 f3 6e 40 7b 90 23 8f 1e d7 20 8b 3e  ..@..n@{.#... .>
00000080: b7 c1 0d 70 03 74 b5 03 ae 41 6b f8 be a8 fb dc  ...p.t...Ak.....
00000090: 3e 7d 2a 22 33 6f de 5b 55 dd 3d 3d f9 20 91 88  >}*"3o.[U.==. ..
```

Podemos notar cosas como 'gAMA' o 'pHYs', que son usualmente usados en archivos png, así que para manipularlo, crearemos una copia de nuestro archivo con extensión .png
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ cp mystery fixed.png
```

Ahora, arreglaremos los magic bytes para que se reconozca como un archivo png
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ printf '\x89\x50\x4E\x47\x0D\x0A\x1A\x0A' | dd of=fixed.png bs=1 seek=0 count=8 conv=notrunc
8+0 records in
8+0 records out
8 bytes copied, 0.00248742 s, 3.2 kB/s
```

Ahora usaremos la herramienta pngcheck para revisar si sigue teniendo problemas
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ pngcheck -v fixed1.png
File: fixed1.png (202940 bytes)
  invalid chunk name "C"DR" (43 22 44 52)
ERRORS DETECTED in fixed1.png
```

Vemos que hay un problema con el chunk, así que usamos este código para corregirlo, además de revisar si es que ya se reconoce como archivo png
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ printf '\x00\x00\x00\x0D\x49\x48\x44\x52' | dd of=fixed.png bs=1 seek=8 count=8 conv=notrunc
8+0 records in
8+0 records out
8 bytes copied, 0.00171048 s, 4.7 kB/s

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ file fixed1.png                                                                              
fixed1.png: PNG image data, 1642 x 1095, 8-bit/color RGB, non-interlaced
```

Si bien ya se reconoce como png, no podemos abrir el archivo en el explorador, así que ahora toca usar la herramienta pngcheck para revisar si hay errores adicionales
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ pngcheck -v fixed.png 
File: fixed.png (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 2852132389x5669 pixels/meter
  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERRORS DETECTED in fixed.png
```

Ahora para arreglar el error del CRC, usaremos este código:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ printf '\x38\xD8\x2C\x82' | dd of=fixed.png bs=1 seek=79 count=4 conv=notrunc
4+0 records in
4+0 records out
4 bytes copied, 0.00221939 s, 1.8 kB/s
```

Sin embargo, ahora nos dice que el Chunk es muy largo, por lo que debemos utilizar dos códigos para arreglarlo
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ printf '\x49\x44\x41\x54' | dd of=fixed.png bs=1 seek=87 count=4 conv=notrunc
4+0 records in
4+0 records out
4 bytes copied, 0.00140041 s, 2.9 kB/s
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ printf '\x00\x00' | dd of=fixed.png bs=1 seek=83 count=2 conv=notrunc        
2+0 records in
2+0 records out
2 bytes copied, 0.000820923 s, 2.4 kB/s
```

El primero es para corregir el error del tamaño, el segundo es para reemplazar los valores incorrectos para que se ajusten al tamaño del chunk.

Finalmente, revisamos con pngcheck para ver si ya hemos terminado
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/c0rrupt]
└─$ pngcheck -c -v fixed.png 2>/dev/null                                         
File: fixed.png (202940 bytes)
  chunk IHDR at offset 0x0000c, length 13
    1642 x 1095 image, 24-bit RGB, non-interlaced
  chunk sRGB at offset 0x00025, length 1
    rendering intent = perceptual
  chunk gAMA at offset 0x00032, length 4: 0.45455
  chunk pHYs at offset 0x00042, length 9: 2852132389x5669 pixels/meter
  chunk IDAT at offset 0x00057, length 65445
    zlib: deflated, 32K window, fast compression
  chunk IDAT at offset 0x10008, length 65524
  chunk IDAT at offset 0x20008, length 65524
  chunk IDAT at offset 0x30008, length 6304
  chunk IEND at offset 0x318b4, length 0
No errors detected in fixed.png (9 chunks, 96.3% compression).
```

picoCTF{c0rrupt10n_1847995}
## Notas
