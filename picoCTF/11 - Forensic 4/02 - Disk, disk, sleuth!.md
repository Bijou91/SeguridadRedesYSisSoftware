# Disk, disk, sleuth!

## Descripción
Use `srch_strings` from the sleuthkit and some terminal-fu to find a flag in this disk image.
[dds1-alpine.flag.img.gz](https://challenge-files.picoctf.net/c_wily_courier/a7895bbce833fd95502d3a661fa54735e90d9bec9346d711ff05cbd40b5f3c8e/dds1-alpine.flag.img.gz)
## Solución
Lo primero que haremos obviamente es bajarlo para manipular el archivo
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/disk1]
└─$ wget https://challenge-files.picoctf.net/c_wily_courier/a7895bbce833fd95502d3a661fa54735e90d9bec9346d711ff05cbd40b5f3c8e/dds1-alpine.flag.img.gz
--2026-03-20 20:05:48--  https://challenge-files.picoctf.net/c_wily_courier/a7895bbce833fd95502d3a661fa54735e90d9bec9346d711ff05cbd40b5f3c8e/dds1-alpine.flag.img.gz
Resolving challenge-files.picoctf.net (challenge-files.picoctf.net)... 3.161.44.103, 3.161.44.22, 3.161.44.84, ...
Connecting to challenge-files.picoctf.net (challenge-files.picoctf.net)|3.161.44.103|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 29768911 (28M) [application/octet-stream]
Saving to: ‘dds1-alpine.flag.img.gz’

dds1-alpine.flag.img.gz                   100%[===================================================================================>]  28.39M  2.36MB/s    in 12s     

2026-03-20 20:06:00 (2.45 MB/s) - ‘dds1-alpine.flag.img.gz’ saved [29768911/29768911]

                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/disk1]
└─$ gzip -d dds1-alpine.flag.img.gz
```

Es un reto bastante directo, pues solo hay que usar la herramienta srch_strings, a la que agregaremos un grep para solo obtener la bandera
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/disk1]
└─$ srch_strings -a dds1-alpine.flag.img| grep picoCTF
  SAY picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
```
picoCTF{f0r3ns1c4t0r_n30phyt3_5e56e786}
## Notas
