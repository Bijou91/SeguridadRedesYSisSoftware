## findme
# Descripción
Help us test the form by submiting the username as `test` and password as `test!`
The website running [here](http://saturn.picoctf.net:60562/).
# Solución
Al entrar a la página que nos entregan, nos topamos con esto
![[picoCTF/Examen 1er. Parcial/Web/imagenes/05findme.png]]

Si ingresamos los datos que nos piden ingresar test:test! e inspeccionamos la sección 'Network' con las herramientas de desarrollador, podemos notar varias solicitudes
![[05findme 1.png]]

Inmediatamente destacan las dos request con 'id', y el hecho que una tenga al final un `==` nos da una pista que se trata de un string codificado en base64.

Si las juntamos en CyberChef, obtenemos nuestra flag.

picoCTF{proxies_all_the_way_25bbae9a}
# Notas adicionales
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=Y0dsamIwTlVSbnR3Y205NGFXVnpYMkZzYkY5MGFHVmZkMkY1WHpJMVltSmhaVGxoZlE9PQ&ieol=CRLF&oeol=CRLF
# Referencias
- 