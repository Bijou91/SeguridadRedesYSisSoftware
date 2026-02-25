# Scavenger Hunt

## Descripción
There is some interesting information hidden around this site. Can you find it?
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan, como en un reto anterior, vemos lo que utilizó el creador para hacerla
![[03Scav01.png]]

Estas son las herramientas que utilizó
![[03Scav02.png]]

Analizamos el primero, el HTML de la página, donde encontramos la primer parte de la flag
![[03Scav03.png]]
picoCTF{t

El segundo, la hoja de estilos CSS
![[03Scav04.png]]
h4ts_4_l0

Y el último, el archivo de JavaScript pero hubo un problema, no hay parte de la flag
![[03Scav05.png]]

Así que haremos uso del robots.txt que aprendimos antes, pero solo nos entrega una parte
![[03Scav06.png]]
t_0f_pl4c

Al ser un servidor apache, nos implica que podemos acceder al archivo .htaccess
![[03Scav07.png]]
3s_2_lO0k

Y por último, vamos al .DS_Store, gracias a la pista de la máquina Mac
![[03Scav08.png]]
__9588550}

picoCTF{th4ts_4_l0t_0f_pl4c3s_2_lO0k_9588550}
## Notas
