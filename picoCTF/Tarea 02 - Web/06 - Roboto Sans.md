# Roboto Sans

## Descripción
The flag is somewhere on this web application not necessarily on the website. Find it.
## Solución
### Solución:
Al entrar a la página que nos dan, vemos esta pantalla
![[06RobotoSans.png]]

El nombre del reto nos recuerda a los robots.txt, así que investigamos en este archivo
```
User-agent *
Disallow: /cgi-bin/
Think you have seen your flag or want to keep looking.

ZmxhZzEudHh0;anMvbXlmaW
anMvbXlmaWxlLnR4dA==
svssshjweuiwl;oiho.bsvdaslejg
Disallow: /wp-admin/
```

Nos entregan unas líneas, las cuales están encriptadas y debemos desencriptadas con base64
```
ZmxhZzEudHh0;anMvbXlmaW = flag1.txtjs/myfi
anMvbXlmaWxlLnR4dA== = js/myfile.txt
```

Al investigar en ese archivo dentro del servidor de la página, encontramos la flag

picoCTF{Who_D03sN7_L1k5_90B0T5_032f1c2b}
## Notas
