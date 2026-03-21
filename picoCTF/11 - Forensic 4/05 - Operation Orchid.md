# Operation Orchid

## Descripción
Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/214/disk.flag.img.gz)
## Solución
Lo primero que vamos a hacer es aplicarle un mmls para conocer sus particiones
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ mmls disk.flag.img 
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000411647   0000204800   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000411648   0000819199   0000407552   Linux (0x83)
```

Ahora aplicaremos el fls para leer los archivos internos en la imagen.
```                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ fls -o 411648 disk.flag.img 
d/d 460:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 81: proc
d/d 82: dev
d/d 83: tmp
d/d 84: lib
d/d 87: var
d/d 96: usr
d/d 106:        bin
d/d 120:        sbin
d/d 466:        media
d/d 470:        mnt
d/d 471:        opt
d/d 472:        root
d/d 473:        run
d/d 475:        srv
d/d 476:        sys
d/d 2041:       swap
V/V 51001:      $OrphanFiles
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ fls -o 411648 disk.flag.img 472
r/r 1875:       .ash_history
r/r * 1876(realloc):    flag.txt
r/r 1782:       flag.txt.enc
```

Al intentar leer esto, muestra un error. Pero nos da una pista: Está encriptado con OpenSSL AES-256.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ icat -o 411648 disk.flag.img 1782
Salted__S�+%���+�O��k�ђ(A����c��
                                @]ԣ
L�ޢȤ7� ���؎$�'%
```

Ahora aplicamos un string y un grep y ahí podemos notar una posible contraseña para desencriptar el archivo anterior, así que lo guardamos en un archivo para usarlo.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ strings -t d disk.flag.img | grep flag.txt
218985524 flag.txt
218985540 flag.txt.enc
219964416 touch flag.txt
219964431 nano flag.txt 
219964483 nano flag.txt 
219964506 openssl aes256 -salt -in flag.txt -out flag.txt.enc -k unbreakablepassword1234567
219964588 shred -u flag.txt
303193140 flag.txt
303317044 flag.txt
303317060 flag.txt.enc
303328308 flag.txt
303328324 flag.txt.enc
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ icat -o 411648 disk.flag.img 1782 > flag.txt.enc
```

Ahora usamos la llave de desencriptación y guardamos la bandera en un archivo de texto, y al leerlo
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ openssl aes256 -d -salt -in flag.txt.enc -out flag.txt -k unbreakablepassword1234567

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/opOrchid]
└─$ cat flag.txt                                               
picoCTF{h4un71ng_p457_1d02081e}
```

picoCTF{h4un71ng_p457_1d02081e}
## Notas
