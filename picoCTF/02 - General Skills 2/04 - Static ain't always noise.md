# Static ain't always noise

## Descripción
Can you look at the data in this binary? The bash script might help!
static, ltdis.sh
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/04-StaticAintAlwaysNoise]
└─$ ./ltdis.sh static
Attempting disassembly of static ...
Disassembly successful! Available at: static.ltdis.x86_64.txt
Ripping strings from binary with file offsets...
Any strings found in static have been written to static.ltdis.strings.txt with file offset

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/04-StaticAintAlwaysNoise]
└─$ cat static.ltdis.strings.txt | grep pico
   3020 picoCTF{d15a5m_t34s3r_20335e41}

```

picoCTF{d15a5m_t34s3r_20335e41}
## Notas
