# flags

## Descripción
What do the [flags](https://challenge-files.picoctf.net/c_fickle_tempest/214c9d918be75903d4183c35fa4b94ef60dba05fc4df37c97cf0868087067372/flag.png) mean?
## Solución
Cuando vemos la imagen, observamos una secuencia de cuadrados decorados.
![flag](https://challenge-files.picoctf.net/c_fickle_tempest/214c9d918be75903d4183c35fa4b94ef60dba05fc4df37c97cf0868087067372/flag.png)

Sabemos que esto hace referencia a el Código Internacional de Señales. Estas señales son un tipo común de criptografía mediante banderas marítimas. Ahora, simplemente decodificamos las señales a sus respectivos caracteres en mayúscula y obtenemos la flag.

Para esto usaremos esta referencia:
![decode](https://github.com/kevinjycui/picoCTF-2019-writeup/raw/master/Cryptography/Flags/screenshot.JPG)

Flag:
PICOCTF{F1AG5AND5TUFF}
## Notas
- 