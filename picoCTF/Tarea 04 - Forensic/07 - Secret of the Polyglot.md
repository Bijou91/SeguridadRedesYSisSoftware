# Secret of the Polyglot

## Descripción
The Network Operations Center (NOC) of your local institution picked up a suspicious file, they're getting conflicting information on what type of file it is. They've brought you in as an external expert to examine the file. Can you extract all the information from this strange file?
Download the suspicious file [here](https://artifacts.picoctf.net/c_titan/8/flag2of2-final.pdf).
## Solución
Para este reto lo primero que haremos es abrir el pdf que nos entregan, obteniendo directamente una parte de la bandera
![2half](https://miro.medium.com/v2/resize:fit:720/format:webp/1*bXkldXNyIhaCfTwVRuJSeQ.png)
```

```

Obviamente, conmigo el número cambia
```
1n_pn9_&_pdf_249d05c0}
```

Ahora usaremos un hexdump para revisar si nuestro archivo PDF es verdaderamente PDF, y al usar el comando hexdump podemos notar que en realidad se trata de un PNG
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/secret]
└─$ hexdump -C flag2of2-final.pdf 
00000000  89 50 4e 47 0d 0a 1a 0a  00 00 00 0d 49 48 44 52  |.PNG........IHDR|
00000010  00 00 00 32 00 00 00 32  08 06 00 00 00 1e 3f 88  |...2...2......?.|
00000020  b1 00 00 01 85 69 43 43  50 49 43 43 20 70 72 6f  |.....iCCPICC pro|
00000030  66 69 6c 65 00 00 28 91  7d 91 3d 48 c3 40 1c c5  |file..(.}.=H.@..|
00000040  5f 53 a5 a2 15 11 3b 88  08 66 a8 0e 62 41 54 c4  |_S....;..f..bAT.|
00000050  51 ab 50 84 0a a1 56 68  d5 c1 e4 d2 2f 68 d2 90  |Q.P...Vh..../h..|
```

Si lo renombramos a png y abrimos la imagen, obtenemos la primer parte de nuestra bandera
![1half](https://miro.medium.com/v2/resize:fit:100/format:webp/1*gh8q2eHXGfZ8q-oKGUWfpA.png)
```
picoCTF{f1u3n7_
```

Al unir las 2 partes de la bandera, obtenemos la bandera

``picoCTF{f1u3n7_1n_pn9_&_pdf_249d05c0}
## Notas
- 