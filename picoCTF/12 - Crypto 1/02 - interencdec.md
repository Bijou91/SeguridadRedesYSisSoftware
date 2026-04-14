# interencdec

## Descripción
Can you get the real meaning from this file.
Download the file [here](https://artifacts.picoctf.net/c_titan/2/enc_flag).
## Solución
En el archivo que nos entregan hay una cadena de texto
```
YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6YzRNalV3YUcxcWZRPT0nCg==
```

Con los dos '`=`' del final podemos intuir que se ha codificado con base64. Obteniendo esta salida
```
b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzc4MjUwaG1qfQ=='
```

Si volvemos a desencriptar pero solo lo que está entre las apóstrofes, obtenemos esta nueva salida
```
wpjvJAM{jhlzhy_k3jy9wa3k_78250hmj}
```

Ahora esta última salida la desencriptaremos con [Caesar](https://www.dcode.fr/caesar-cipher) y obtendremos nuestra bandera

picoCTF{caesar_d3cr9pt3d_78250afc}
## Notas
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=WWlka00wSnhaR3R3UWxSWWRIRmhSM2cyWVVoc1ptRjZUbkZsVkd3eldWUk9jbGg2WXpSTmFsVjNZVWN4Y1daUlBUMG5DZz09
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=ZDNCcWRrcEJUWHRxYUd4NmFIbGZhek5xZVRsM1lUTnJYemM0TWpVd2FHMXFmUT09