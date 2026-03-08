# What Lies Within

## Descripción
There's something in the building.
![building](https://challenge-files.picoctf.net/c_fickle_tempest/c0eec6af0f04316e2bdc4a9f095afd0e2d0121f5e543dbc4a65bb0038d72a993/buildings.png)
Can you retrieve the flag?
## Solución
### Solución:
Al entrar al reto, lo único que nos entregan es un archivo de imagen PNG.

La pista nos dice esto:
"There is data encoded somewhere... there might be an online decoder." -> "Hay algunos datos codificados en alguna parte... quizá haya un decodificador online"

Como tenemos información codificada dentro de un archivo PNG, lo más seguro es que se trate de estenografía.

Entonces, con un decodificador online y pasándole la imagen, obtenemos nuestra flag
picoCTF{h1d1ng_1n_th3_b1t5}
## Notas
Decodificador usado:
https://stylesuxx.github.io/steganography/