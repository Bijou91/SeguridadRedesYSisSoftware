# Sleuthkit Intro

## Descripción
Download the disk image and use `mmls` on it to find the size of the Linux partition. Connect to the remote checker service to check your answer and get the flag.
Note: if you are using the webshell, download and extract the disk image into `/tmp` not your home directory.
[Download disk image](https://artifacts.picoctf.net/c/164/disk.img.gz)
## Solución
Lo primero, obviamente, es bajar la imagen a nuestra máquina local, luego la descomprimimos para poder trabajar con ella
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthkitintro]
└─$ wget https://artifacts.picoctf.net/c/164/disk.img.gz      
--2026-03-20 18:44:57--  https://artifacts.picoctf.net/c/164/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.100, 3.161.55.26, 3.161.55.61, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29714372 (28M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                               100%[===================================================================================>]  28.34M  2.40MB/s    in 12s     

2026-03-20 18:45:09 (2.46 MB/s) - ‘disk.img.gz’ saved [29714372/29714372]

                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthkitintro]
└─$ gzip -d disk.img.gz
```

Para poder analizar las particiones del disco, utilizaremos la herramienta **'mmls'**, que es una herramienta utilizada para mostrar la tabla de particiones y la estructura de volúmenes de una imagen de disco.
```                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthkitintro]
└─$ mmls disk.img       
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000204799   0000202752   Linux (0x83)
```

Ahora con esta información, nos conectamos al servidor que nos indica el reto para validar esta información y obtener nuestra bandera
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/sleuthkitintro]
└─$ nc saturn.picoctf.net 49458
What is the size of the Linux partition in the given disk image?
Length in sectors: 202752
202752
Great work!
picoCTF{mm15_f7w!}
```

picoCTF{mm15_f7w!}
## Notas
