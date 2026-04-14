# Tapping

## Descripción
Theres tapping coming in from the wires.
What's it saying nc fickle-tempest.picoctf.net 61885.
## Solución
Al conectarnos al servidor, solo nos entregan esta cadena de texto.
```
.--. .. -.-. --- -.-. - ..-. { -- ----- .-. ... ...-- -.-. ----- -.. ...-- .---- ... ..-. ..- -. -.-. ----. .---- ..-. -.... ..--- ----- -.... }
```

Como podemos notar, se trata de código morse, así que usando un traductor, obtenemos el texto plano y junto a ello, también obtenemos nuestra bandera

PICOCTF{M0RS3C0D31SFUNC91F6206}
## Notas
- https://morsecode.world/international/translator.html