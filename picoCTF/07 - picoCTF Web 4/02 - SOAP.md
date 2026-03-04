# SOAP

## Descripción
The web project was rushed and no security assessment was done. Can you read the /etc/passwd file?
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan son 3 posibles "universidades" para aplicar
![[02SOAP01.png]]

Utilizando la herramienta burp, interceptamos las señales de los botones de aplicar para cada universidad
![[02SOAP02.png]]

Ahora usando el repeater con una de las señales, vemos que hay un método de entrada, y aquí inyectamos un poco de código para como dice la descripción del reto: "Leer el archivo passwd en la carpeta etc".

Ahí, vemos que hasta la parte de hasta bajo, viene nuestra bandera
![[02SOAP03.png]]
picoCTF{XML_3xtern@l_3nt1t1ty_e79a75d4}
## Notas
