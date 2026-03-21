# Sleuthkit Apprentice

## Descripción
Download this disk image and find the flag.
Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.

- [Download compressed disk image](https://artifacts.picoctf.net/c/137/disk.flag.img.gz)
## Solución
Lo primero, obviamente, es bajar la imagen a nuestra máquina local, luego la descomprimimos para poder trabajar con ella
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ wget https://artifacts.picoctf.net/c/137/disk.flag.img.gz                                                                                       
--2026-03-20 20:25:21--  https://artifacts.picoctf.net/c/137/disk.flag.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.61, 3.161.55.64, 3.161.55.26, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.61|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 47534568 (45M) [application/octet-stream]
Saving to: ‘disk.flag.img.gz’

disk.flag.img.gz                          100%[===================================================================================>]  45.33M  2.38MB/s    in 20s     

2026-03-20 20:25:42 (2.28 MB/s) - ‘disk.flag.img.gz’ saved [47534568/47534568]

                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ gzip -d disk.flag.img.gz
```

Para poder analizar las particiones del disco, utilizaremos la herramienta **'mmls'**.
```                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ mmls disk.flag.img    
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000360447   0000153600   Linux Swap / Solaris x86 (0x82)
004:  000:002   0000360448   0000614399   0000253952   Linux (0x83)
```

Ahora utilizaremos el comando **fsstat** para saber con qué tipo de sistema de archivos fue usado en la imagen, como vemos, es Ext4
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ fsstat -o 2048 disk.flag.img
FILE SYSTEM INFORMATION
--------------------------------------------
File System Type: Ext4
Volume Name: 
Volume ID: 8e023955b4e7dab7e04b7643076ccf0f

Last Written at: 2021-09-29 14:10:02 (EDT)
Last Checked at: 2021-09-29 11:57:16 (EDT)
```

Ahora utilizaremos fls para mostrar los archivos del disco, al cual le aplicaremos un grep para solo mostrar archivos con posibles flags
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ fls -i raw -f ext4 -o 2048 -r disk.flag.img
d/d 11: lost+found
r/r 12: ldlinux.sys
r/r 13: ldlinux.c32
r/r 15: config-virt
r/r 16: vmlinuz-virt
r/r 17: initramfs-virt
l/l 18: boot
r/r 20: libutil.c32
r/r 19: extlinux.conf
r/r 21: libcom32.c32
r/r 22: mboot.c32
r/r 23: menu.c32
r/r 14: System.map-virt
r/r 24: vesamenu.c32
V/V 25585:      $OrphanFiles
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ fls -i raw -f ext4 -o 360448 -r disk.flag.img | grep flag
++ r/r * 2082(realloc): flag.txt
++ r/r 2371:    flag.uni.txt
```

Y posteriormente mostramos el contenido en terminal para obtener la flag:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthApprentice]
└─$ icat -i raw -f ext4 -o 360448 disk.flag.img 2371
picoCTF{by73_5urf3r_adac6cb4}
```

picoCTF{by73_5urf3r_adac6cb4}
## Notas
