# RED

## Descripción
RED, RED, RED, RED
Download the image: [red.png](https://challenge-files.picoctf.net/c_verbal_sleep/831307718b34193b288dde31e557484876fb84978b5818e2627e453a54aa9ba6/red.png)
## Solución
Para este reto nos entregan una imagen, así que le aplicaremos un zsteg para obtener cualquier información potencialmente oculta, al zsteg le agregaré un grep con "_=_="  para de una vez encontrar cualquier cadena posiblemente encriptada
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/RED]
└─$ zsteg -a red.png | grep "=="                             
b1,rgba,lsb,xy      .. text: "cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ=="
b1,abgr,msb,XY      .. text: "==QffVTNz4GZ0UzXyBjZfNjc1N2XzQHNtFDdsV3XzgGdfNXMfR2MytnRUN0bjlGc==QffVTNz4GZ0UzXyBjZfNjc1N2XzQHNtFDdsV3XzgGdfNXMfR2MytnRUN0bjlGc==QffVTNz4GZ0UzXyBjZfNjc1N2XzQHNtFDdsV3XzgGdfNXMfR2MytnRUN0bjlGc==QffVTNz4GZ0UzXyBjZfNjc1N2XzQHNtFDdsV3XzgGdfNXMfR2MytnRUN0bjlGc"
```

Notamos que una empieza con "_=_=", mientras que la otra termina con los doble iguales, así que podemos identificar como cadena encriptada a la que **termina** con los iguales.

Al tomar esa cadena `(cGljb0NURntyM2RfMXNfdGgzX3VsdDFtNHQzX2N1cjNfZjByXzU0ZG4zNTVffQ==)` y pasarla por cyberchef, obtenemos nuestra bandera.

picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}
## Notas
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=Y0dsamIwTlVSbnR5TTJSZk1YTmZkR2d6WDNWc2RERnROSFF6WDJOMWNqTmZaakJ5WHpVMFpHNHpOVFZmZlE9PQ