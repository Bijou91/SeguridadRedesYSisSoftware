# Local Authority

## Descripción
Can you get the flag?
## Solución
### Solución:
Al entrar a la página que nos dan, vemos esta pantalla
![[04LocalAuth01.png]]

al ingresar, obviamente no nos permiten loguearnos.

Ahora, analizaremos el código fuente de la página, donde encontramos un script llamado 'secure.js'
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="style.css">
    <title>Login Page</title>
  </head>
  <body>
    <script src="secure.js"></script>
    
    <p id='msg'></p>
... ... ...
... ... ...
```

Al analizar este archivo, encontramos las credenciales válidas
```
function checkPassword(username, password)
{
  if( username === 'admin' && password === 'strongPassword098765' )
  {
    return true;
  }
  else
  {
    return false;
  }
}
```

Al usar esas credenciales, nos permiten loguearnos y nos entregan la bandera
picoCTF{j5_15_7r4n5p4r3n7_a8788e61}
## Notas
