# logon

## Descripción
The factory is hiding things from all of its users.
Can you login as Joe and find what they've been looking at?
## Solución
### Solución:
Al abrir la página web, vemos que hay un login
![[03logon01.png]]

usando 'admin' como username y 'helloworld' como contraseña, nos deja entrar pero
![[03logon02.png]]

Usando un editor de cookies, lo que debemos hacer es alterar el login del admin, pasando su valor de ``False`` a ``True``
![[03logon03.png]]

Tras editar y guardar la cookie, ahora recargamos la página para encontrar la flag
![[03logon04.png]]
#### Flag
picoCTF{th3_c0nsp1r4cy_l1v3s_4d184b0d}
## Notas
