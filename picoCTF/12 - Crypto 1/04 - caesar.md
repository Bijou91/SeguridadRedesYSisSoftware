# caesar

## Descripción
Decrypt this message.
Message: [message](https://challenge-files.picoctf.net/c_fickle_tempest/6c40a1814a02fcc4bb567552d918c53b4b15a1b81518ec0ef7447fbfb73a3ce9/data.enc)
## Solución
Al abrir el archivo que nos entregan, tenemos esta cadena
`picoCTF{rgdhhxcviwtgjqxrdcbxpotman}`

Como vemos, es nuestra bandera, pero el texto dentro de las llaves está encriptado. Para desencriptarlo, usaremos el cifrado cesar de la página dcode.fr, obteniendo esta salida
`crossingtherubiconmiazexly`

Al sustituirlo en la cadena original, obtenemos nuestra bandera.

picoCTF{crossingtherubiconmiazexly}
## Notas
- https://www.dcode.fr/cifrado-cesar