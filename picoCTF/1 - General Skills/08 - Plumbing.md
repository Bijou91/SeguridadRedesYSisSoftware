# Plumbing
# Descripción
Sometimes you need to handle process data outside of a file. Can you find a way to keep the output from this program and search for the flag?

Connect to fickle-tempest.picoctf.net 62260.
## Solución
- Comandos de Linux
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01_GeneralSkills/ObedientCat]
└─$ netcat fickle-tempest.picoctf.net 62260
I don't think this is a flag either
I don't think this is a flag either
Not a flag either
Not a flag either
This is defintely not a flag
This is defintely not a flag
Again, I really don't think this is a flag
Again, I really don't think this is a flag
Not a flag either
Again, I really don't think this is a flag
Not a flag either
This is defintely not a flag
This is defintely not a flag
Not a flag either
I don't think this is a flag either
Not a flag either
This is defintely not a flag
...
...
...
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01_GeneralSkills/ObedientCat]
└─$ netcat fickle-tempest.picoctf.net 62260 | grep "pico"
picoCTF{digital_plumb3r_A01Bc3eC}
```

picoCTF{digital_plumb3r_A01Bc3eC}
## Notas
