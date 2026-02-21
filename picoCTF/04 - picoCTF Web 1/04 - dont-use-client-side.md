# dont-use-client-side

## Descripción
Can you break into this super secure portal?
## Solución
### Solución:
Al abrir la página web, vemos que hay un login, donde nos pide las credenciales válidas
![[04NoClient01.png]]
Vemos que la forma en que revisa si la contraseña es correcta es por partes, indicando las posiciones de las "partes" como si de un arreglo se tratase, pero están desordenadas
![[04NoClient02.png]]
Así que tenemos que rearmar la contraseña:
pico + CTF{ + no_c + lien + ts_p + lz_2 + eb02 + b45}
picoCTF{no_clients_plz_2eb02b45}

Y vemos que es la correcta
![[04NoClient03.png]]

Al tener formato de bandera, sabemos que esta es nuestra flag
#### Flag
picoCTF{no_clients_plz_2eb02b45}
## Notas
