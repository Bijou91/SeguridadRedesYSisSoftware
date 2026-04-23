# basic-mod1

## Descripción
We found this weird message being passed around on the servers, we think we have a working decryption scheme.
Download the message [here](https://artifacts.picoctf.net/c/129/message.txt).
Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.
Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)
## Solución
Como nos indica la descripción, debemos desencriptar message.txt, que en mi caso contiene esto:
```
350 63 353 198 114 369 346 184 202 322 94 235 114 110 185 188 225 212 366 374 261 213 
```

El primer objetivo es aplicar el módulo 37 a cada número. Para hacer esto, elegí usar un script de Python. Esto significa que quería colocar los números en un arreglo.

Este es el script de Python que usé para completar este desafío
```python
arr = [350, 63, 353, 198, 114, 369, 346, 184, 202, 322, 94, 235, 114, 110, 185, 188, 225, 212, 366, 374, 261, 213]
characterSet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_"
flag = "picoCTF{"

for i in range(len(arr)):
        arr[i] = arr[i] % 37
        flag += characterSet[arr[i]]

flag += "}"
print(flag)

```

Esta es la flag que obtenemos al final:
picoCTF{R0UND_N_R0UND_ADD17EC2}
## Notas
- 