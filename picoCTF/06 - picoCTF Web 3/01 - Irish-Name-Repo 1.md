# Irish-Name-Repo 1

## Descripción
Do you think you can log us in? Try to see if you can login!
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan, vemos que efectivamente, es una página de gente irlandesa
![[01Irish01.png]]

En el submenú de la izquierda hay 3 opciones, intentaremos loguearnos
![[01Irish02.png]]

Intentamos con un básico 'admin' de username y 'password' como contraseña
![[01Irish03.png]]

Falla el login, así que investigaremos un poco el HTML de la página del login
![[01Irish04.png]]

Aquí activaremos el debug para ver como es que se realiza la validación
![[01Irish05.png]]

Vuelve a fallar, pero ahora sabemos como funciona la sentencia de SQL que verifica el login
![[01Irish06.png]]

Así que ahora haremos algo de SQL Injection, colocando esta parte de una sentencia en la contraseña (el username sigue siendo admin)
![[01Irish07.png]]

Y listo, ya nos hemos logueado
![[01Irish08.png]]
picoCTF{s0m3_SQL_85832275}
## Notas
