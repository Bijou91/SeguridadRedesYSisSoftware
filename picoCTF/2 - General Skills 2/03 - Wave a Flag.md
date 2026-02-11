# Wave a Flag

## Descripción
Can you invoke help flags for a tool or binary? This program has extraordinarily helpful information... warm
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/03-WaveAFlag]
└─$ file warm   
warm: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=9e46ec8729d2f2aa8ffc4b1cdc058081bddcfe67, for GNU/Linux 3.2.0, with debug_info, not stripped
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/03-WaveAFlag]
└─$ chmod +x warm 

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/03-WaveAFlag]
└─$ ./warm
Hello user! Pass me a -h to learn what I can do!
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/03-WaveAFlag]
└─$ ./warm -h
Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
```

picoCTF{b1scu1ts_4nd_gr4vy_ac5832c}
## Notas
