# More SQLi

## Descripción
Can you find the flag on this website.
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan, vemos que tenemos un login, el cual intentaremos con al típico admin-admin, que falla, claramente
![[02MoreSQLi01.png]]

Para poder ingresar, repetiremos la inyección del reto pasado `' or 1 = 1;`, que al ingresar, nos topamos con esta tabla de direcciones
![[02MoreSQLi02.png]]

Continuaremos con la inyección de sql, primero lo haremos para conocer la versión de SQL
![[02MoreSQLi03.png]]

Ahora con esta sentencia, vamos a recuperar las estructuras de las tablas presentes, como podemos ver, la tabla `more_table` contiene una columna llamada 'flag'
![[02MoreSQLi04.png]]

Ahora usamos esta consulta para recuperar los datos de esta `more table`, la cual contiene nuestra flag
![[02MoreSQLi05.png]]
picoCTF{G3tting_5QL_1nJ3c7I0N_l1k3_y0u_sh0ulD_78d0583a}
## Notas
