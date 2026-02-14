# Bases
## Descripción
Can you find the flag in the file? This would be really tedious to look through manually, something tells me there is a better way.

## Solución
- Comandos de Linux
```
(kali㉿kali)-[/media/sf_almacenamientoCompartido/01 - General Skills]
└─$ cat file | grep ctf      
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01 - General Skills]
└─$ cat file | grep flag
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01 - General Skills]
└─$ cat file | grep pico
Aquí se muestra todo el archivo file pero con la palabra pico (la que se le indica al grep) resaltada en color rojo, si hubiese usado "pico", mostraría solo la cadena de texto que contiene la palabra pico
```

picoCTF{grep_is_good_to_find_things_beD770f5}
## Notas
