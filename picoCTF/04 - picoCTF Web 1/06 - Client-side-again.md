# Client-side-again

## Descripción
Can you break into this super secure portal?
## Solución
### Solución:
Al abrir la página web, vemos que hay un nuevo login, donde nos pide las credenciales válidas
![[06ClientSide01.png]]

Como podemos ver, al ver el código fuente, a diferencia de la versión anterior, el código no es tan legible y no nos da la flag de forma tan sencilla
![[06ClientSide02.png]]

Al usar la página jsnice.org para desofuscar el código y que sea algo más legible, no obtenemos mucho, pero obtenemos el arreglo `_0x5a46`, que podemos notar partes de la flag
![[06ClientSide03.png]]

Usando la consola, creamos una 'suma' con las distintas posiciones para restaurar la flag
![[06ClientSide04.png]]
#### Flag
picoCTF{not_this_again_4daf93}
## Notas
