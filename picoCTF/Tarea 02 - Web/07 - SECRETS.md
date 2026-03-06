# SECRETS

## Descripción
We have several pages hidden. Can you find the one with the flag?
## Solución
### Solución:
Al entrar a la página que nos dan, vemos esta pantalla
![[07Secrets.png]]

Al inspeccionar el código fuente de la página, descubrimos que existe una carpeta 'secret'
```
<link href="secret/assets/index.css" rel="stylesheet" />
  </head>
  <body>
    <!-- ***** Header Area Start ***** -->
    <div class="topnav">
      <a class="active" href="#home">Home</a>
      <a href="about.html">About</a>
      <a href="contact.html">Contact</a>
    </div>

    <div class="imgcontainer">
      <img
        src="secret/assets/DX1KYM.jpg"
```

Dentro de esta carpeta, al ver el código fuente de la página que hay ahí, descubrimos otra carpeta
```
<link rel="stylesheet" href="hidden/file.css" />
```

Nuevamente, en el código fuente de la página en la carpeta hidden descubrimos otra carpeta más
```
<link href="superhidden/login.css" rel="stylesheet" />
```

Finalmente, en el código fuente de esta nueva página, está la bandera
```
<!DOCTYPE html>
<html>
  <head>
    <title></title>
    <link rel="stylesheet" href="mycss.css" />
  </head>

  <body>
    <h1>Finally. You found me. But can you see me</h1>
    <h3 class="flag">picoCTF{succ3ss_@h3n1c@10n_39849bcf}</h3>
  </body>
</html>
```

picoCTF{succ3ss_@h3n1c@10n_39849bcf}
## Notas
