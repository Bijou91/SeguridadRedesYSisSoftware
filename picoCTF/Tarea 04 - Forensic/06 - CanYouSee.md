# CanYouSee

## Descripción
How about some hide and seek?
Download this file [here](https://artifacts.picoctf.net/c_titan/130/unknown.zip).
## Solución
Lo primero que haremos es descomprimir el archivo para ver qué encontramos dentro
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/canyousee]
└─$ unzip unknown.zip  
Archive:  unknown.zip
  inflating: ukn_reality.jpg
```

Como vemos que es una imagen, entonces vamos a aplicarle un exiftool para ver sus metadatos
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/canyousee]
└─$ exiftool ukn_reality.jpg 
ExifTool Version Number         : 13.36
File Name                       : ukn_reality.jpg
Directory                       : .
File Size                       : 2.3 MB
File Modification Date/Time     : 2024:03:11 20:05:55-04:00
File Access Date/Time           : 2024:03:11 20:05:55-04:00
File Inode Change Date/Time     : 2026:03:28 20:22:30-04:00
File Permissions                : -rwxrwx---
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.01
Resolution Unit                 : inches
X Resolution                    : 72
Y Resolution                    : 72
XMP Toolkit                     : Image::ExifTool 11.88
Attribution URL                 : cGljb0NURntNRTc0RDQ3QV9ISUREM05fNmE5ZjVhYzR9Cg==
Image Width                     : 4308
Image Height                    : 2875
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 4308x2875
Megapixels                      : 12.4
```

Podemos notar la cadena sospechosa `cGljb0NURntNRTc0RDQ3QV9ISUREM05fNmE5ZjVhYzR9Cg==` , que al pasarla por CyberChef, aprendemos que está encriptada en base64

Al desencriptarla, obtenemos nuestra bandera

picoCTF{ME74D47A_HIDD3N_6a9f5ac4}
## Notas
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=Y0dsamIwTlVSbnROUlRjMFJEUTNRVjlJU1VSRU0wNWZObUU1WmpWaFl6UjlDZz09