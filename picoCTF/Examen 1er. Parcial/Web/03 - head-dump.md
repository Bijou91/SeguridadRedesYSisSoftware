## head-dump
# Descripción
Welcome to the challenge! In this challenge, you will explore a web application and find an endpoint that exposes a file containing a hidden flag.
The application is a simple blog website where you can read articles about various topics, including an article about API Documentation. Your goal is to explore the application and find the endpoint that generates files holding the server’s memory, where a secret flag is hidden.
The website is running [picoCTF News](http://verbal-sleep.picoctf.net:50657/).
# Solución
Al entrar a la página que nos entregan, nos topamos con esto
![inicioHD](https://blog.qz.sg/content/images/2025/03/head-dump-site.webp)

Notamos una página llamada "API Documentation", y al entrar nos topamos con esto
![swagger](https://blog.qz.sg/content/images/size/w1000/2025/03/head-dump-apidocs.webp)

En la parte más del fondo hay una sección "diagnosing", donde podemos interactuar y en retorno nos entregarán un archivo
![diagnosis](https://blog.qz.sg/content/images/2025/03/head-dump-headdump.webp)

Ahora que hemos descargado el archivo, le aplicaremos un grep para obtener nuestra bandera
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/examen1/web/head-dump]
└─$ grep -E "picoCTF{.*}" heapdump-1774404312560.heapsnapshot 
picoCTF{Pat!3nt_15_Th3_K3y_a485f162}
```

picoCTF{Pat!3nt_15_Th3_K3y_a485f162}
# Notas adicionales
- 
# Referencias
- Imágenes tomadas de aquí: https://blog.qz.sg/picoctf-2025-web-exploitation-writeups/