# Operation Oni

## Descripción
Download this disk image, find the key and log into the remote machine.
Note: if you are using the webshell, download and extract the disk image into /tmp not your home directory.
## Solución
Lo primero, obviamente, es bajar la imagen a nuestra máquina local, luego la descomprimimos para poder trabajar con ella
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ wget https://artifacts.picoctf.net/c/71/disk.img.gz 
--2026-03-20 19:09:24--  https://artifacts.picoctf.net/c/71/disk.img.gz
Resolving artifacts.picoctf.net (artifacts.picoctf.net)... 3.161.55.100, 3.161.55.64, 3.161.55.61, ...
Connecting to artifacts.picoctf.net (artifacts.picoctf.net)|3.161.55.100|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 48132743 (46M) [application/octet-stream]
Saving to: ‘disk.img.gz’

disk.img.gz                               100%[===================================================================================>]  45.90M  2.38MB/s    in 20s     z

2026-03-20 19:09:44 (2.29 MB/s) - ‘disk.img.gz’ saved [48132743/48132743]

                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ gzip -d disk.img.gz
```

Para poder analizar las particiones del disco, utilizaremos la herramienta **'mmls'**
```                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ mmls disk.img     
DOS Partition Table
Offset Sector: 0
Units are in 512-byte sectors

      Slot      Start        End          Length       Description
000:  Meta      0000000000   0000000000   0000000001   Primary Table (#0)
001:  -------   0000000000   0000002047   0000002048   Unallocated
002:  000:000   0000002048   0000206847   0000204800   Linux (0x83)
003:  000:001   0000206848   0000471039   0000264192   Linux (0x83)
```

Ahora utilizaremos una herramienta más: **fls**. Esta herramienta se utiliza para listar archivos y directorios en una imagen de disco. La usaremos para navegar hasta encontrar la llave privada que necesitaremos
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ fls -o 206848 disk.img                      
d/d 458:        home
d/d 11: lost+found
d/d 12: boot
d/d 13: etc
d/d 79: proc
d/d 80: dev
d/d 81: tmp
d/d 82: lib
d/d 85: var
d/d 94: usr
d/d 104:        bin
d/d 118:        sbin
d/d 464:        media
d/d 468:        mnt
d/d 469:        opt
d/d 470:        root
d/d 471:        run
d/d 473:        srv
d/d 474:        sys
V/V 33049:      $OrphanFiles
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ fls -o 206848 disk.img 470
r/r 2344:       .ash_history
d/d 3916:       .ssh
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ fls -o 206848 disk.img 3916
r/r 2345:       id_ed25519
r/r 2346:       id_ed25519.pub
```

El siguiente paso será guardar esa llave
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ icat -o 206848 disk.img 2345
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAAAMwAAAAtzc2gtZW
QyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLAAAAJgxpYKDMaWC
gwAAAAtzc2gtZWQyNTUxOQAAACBgrXe4bKNhOzkCLWOmk4zDMimW9RVZngX51Y8h3BmKLA
AAAECItu0F8DIjWxTp+KeMDvX1lQwYtUvP2SfSVOfMOChxYGCtd7hso2E7OQItY6aTjMMy
KZb1FVmeBfnVjyHcGYosAAAADnJvb3RAbG9jYWxob3N0AQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ icat -o 206848 disk.img 2345 > key_file
```

Y con ese archivo, nos conectamos al servidor para validar los datos y obtener nuestra bandera:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/OperationOni]
└─$ ssh -i key_file -p 52834 ctf-player@saturn.picoctf.net
The authenticity of host '[saturn.picoctf.net]:52834 ([13.59.203.175]:52834)' can't be established.
ED25519 key fingerprint is: SHA256:XBSvB1lk28EctsAVdKJtsl0A7C5bonqPrvHCYH8aEy4
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[saturn.picoctf.net]:52834' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
Welcome to Ubuntu 20.04.5 LTS (GNU/Linux 6.8.0-1047-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

ctf-player@challenge:~$ ls
flag.txt
ctf-player@challenge:~$ cat flag.txt 
picoCTF{k3y_5l3u7h_af277f77}ctf-player@challenge:~$
```

picoCTF{k3y_5l3u7h_af277f77}
## Notas
