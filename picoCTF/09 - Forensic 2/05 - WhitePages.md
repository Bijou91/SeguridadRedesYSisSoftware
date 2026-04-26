# WhitePages

## Descripción
I stopped using YellowPages and moved onto WhitePages... but [the page they gave me](https://challenge-files.picoctf.net/c_fickle_tempest/f35d2be8de731d412d3dbd8c79e6c5b32c62efbb124cf319f54ebddf76ea0ffe/whitepages.txt) is all blank!
## Solución
Primero, analizamos un poco el archivo, podemos notar que tiene un patrón recurrente con un '20' apareciendo aquí y allá
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/WhitePages]
└─$ xxd -g 1 whitepages.txt
00000000: e2 80 83 e2 80 83 e2 80 83 e2 80 83 20 e2 80 83  ............ ...
00000010: 20 e2 80 83 e2 80 83 20 20 20 e2 80 83 e2 80 83   ......   ......
00000020: e2 80 83 e2 80 83 e2 80 83 20 20 e2 80 83 20 e2  .........  ... .
00000030: 80 83 e2 80 83 20 e2 80 83 20 20 e2 80 83 e2 80  ..... ...  .....
00000040: 83 e2 80 83 20 20 e2 80 83 20 20 e2 80 83 20 20  ....  ...  ...  
00000050: 20 20 e2 80 83 20 e2 80 83 e2 80 83 e2 80 83 e2    ... ..........
00000060: 80 83 20 20 e2 80 83 20 e2 80 83 20 e2 80 83 20  ..  ... ... ... 
00000070: e2 80 83 e2 80 83 e2 80 83 20 e2 80 83 e2 80 83  ......... ......
00000080: e2 80 83 20 20 e2 80 83 e2 80 83 e2 80 83 e2 80  ...  ...........
00000090: 83 e2 80 83 20 e2 80 83 20 e2 80 83 e2 80 83 e2  .... ... .......
000000a0: 80 83 e2 80 83 e2 80 83 20 e2 80 83 20 e2 80 83  ........ ... ...
000000b0: e2 80 83 20 e2 80 83 20 e2 80 83 e2 80 83 20 20  ... ... ......  
000000c0: e2 80 83 20 e2 80 83 e2 80 83 e2 80 83 20 e2 80  ... ......... ..
000000d0: 83 20 e2 80 83 20 e2 80 83 e2 80 83 e2 80 83 20  . ... ......... 
... ... ... ... ... ... ... ... ... ... ... ... ... ... ... ... ... ... ... ... 

```

Al examinar la secuencia que se repite, podemos notar que son valores hexadecimales pertenecientes al **UNICODE EM SPACE**. Mientras que el 20 representa un espacio en blanco en ASCII
![unicode](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*fv1Obtotuv28BxurdFkngw.jpeg)

Entonces para procesar este archivo, usaremos este código:
```python
def convertSpacesToBinary():
    with open('whitepages.txt', 'rb') as f:
        result = f.read()
    result = result.replace(b'\xe2\x80\x83', b'0')  # Unicode EM SPACE -> 0
    result = result.replace(b'\x20', b'1')  # ASCII Space -> 1
    result = result.decode()
    return result

def convertFromBinaryToASCII(binaryValues):
    binary_int = int(binaryValues, 2)
    byte_number = (binary_int.bit_length() + 7) // 8
    binary_array = binary_int.to_bytes(byte_number, "big")
    ascii_text = binary_array.decode('ascii')
    print(ascii_text)

convertFromBinaryToASCII(convertSpacesToBinary())
```

La función convertSpacesToBinary primero lee el archivo como bytes puros, asegurando que todos los caracteres (incluyendo los no visibles) se capturen con precisión. Después, reemplaza las ocurrencias del espacio UNICODE EM SPACE (e2 80 83) con 0 y reemplaza el espacio ASCII (20) con 1, convirtiendo efectivamente el patrón oculto en una secuencia binaria.

La función convertFromBinaryToASCII toma esta secuencia binaria y la procesa más a fondo. Primero, convierte la cadena binaria en un número entero y luego transforma ese entero en una matriz de bytes (byte array). Finalmente, decodifica dicha matriz de bytes en una cadena ASCII, revelando el mensaje oculto que estaba incrustado en el archivo.

```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/WhitePages]
└─$ python script.py        

picoCTF

SEE PUBLIC RECORDS & BACKGROUND REPORT
5000 Forbes Ave, Pittsburgh, PA 15213
picoCTF{not_all_spaces_are_created_equal_f6166971531e3ad3b35138611330bba8}
```

picoCTF{not_all_spaces_are_created_equal_f6166971531e3ad3b35138611330bba8}
## Notas
Fuente del código:
https://medium.com/@sobatistacyber/picoctf-writeup-whitepages-4d13300b3566