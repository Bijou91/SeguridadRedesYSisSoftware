# Safe opener 2

# Descripción 
What can you do with this file?
I forgot the key to my safe but this [file](https://artifacts.picoctf.net/c/292/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?
## Solución
Esta ocasión nos entregan el archivo de la clase compilada, no del código fuente.

Por lo que para encontrar la flag de forma más rápida, usaremos la herramienta strings y grep:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/Reversing02]
└─$ strings -t x SafeOpener.class | grep picoCTF
    31d ,picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_0e57c117}
```

Y la flag es esta
picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_0e57c117}
## Notas
- 