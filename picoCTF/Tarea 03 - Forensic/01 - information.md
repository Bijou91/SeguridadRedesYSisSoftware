# information

## Descripción
Files can always be changed in a secret way. Can you find the flag?
[cat.jpg](https://challenge-files.picoctf.net/c_wily_courier/76e95e3e6ee69b4f82b3cea25051f5a9a5918b57809a1f90b29b06b776c73bc7/cat.jpg)
## Solución
Lo primero que haremos es revisar si el archivo es realmente un jpg o algún otro tipo con la extensión modificada
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/info]
└─$ hexdump -C cat.jpg | head
00000000  ff d8 ff e0 00 10 4a 46  49 46 00 01 02 00 00 01  |......JFIF......|
00000010  00 01 00 00 ff ed 00 30  50 68 6f 74 6f 73 68 6f  |.......0Photosho|
00000020  70 20 33 2e 30 00 38 42  49 4d 04 04 00 00 00 00  |p 3.0.8BIM......|
00000030  00 13 1c 02 74 00 07 50  69 63 6f 43 54 46 1c 02  |....t..PicoCTF..|
00000040  00 00 02 00 04 00 ff e1  0b f9 68 74 74 70 3a 2f  |..........http:/|
00000050  2f 6e 73 2e 61 64 6f 62  65 2e 63 6f 6d 2f 78 61  |/ns.adobe.com/xa|
00000060  70 2f 31 2e 30 2f 00 3c  3f 78 70 61 63 6b 65 74  |p/1.0/.<?xpacket|
00000070  20 62 65 67 69 6e 3d 27  ef bb bf 27 20 69 64 3d  | begin='...' id=|
00000080  27 57 35 4d 30 4d 70 43  65 68 69 48 7a 72 65 53  |'W5M0MpCehiHzreS|
00000090  7a 4e 54 63 7a 6b 63 39  64 27 3f 3e 0a 3c 78 3a  |zNTczkc9d'?>.<x:|
```

Como vemos que es una imagen, entonces vamos a aplicarle un exiftool para ver sus metadatos
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/info]
└─$ exiftool cat.jpg        
ExifTool Version Number         : 13.36
File Name                       : cat.jpg
Directory                       : .
File Size                       : 878 kB
File Modification Date/Time     : 2025:12:12 14:21:14-05:00
File Access Date/Time           : 2026:03:28 20:37:59-04:00
File Inode Change Date/Time     : 2026:03:28 20:37:59-04:00
File Permissions                : -rwxrwx---
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
JFIF Version                    : 1.02
Resolution Unit                 : None
X Resolution                    : 1
Y Resolution                    : 1
Current IPTC Digest             : 7a78f3d9cfb1ce42ab5a3aa30573d617
Copyright Notice                : PicoCTF
Application Record Version      : 4
XMP Toolkit                     : Image::ExifTool 10.80
License                         : cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9
Rights                          : PicoCTF
Image Width                     : 2560
Image Height                    : 1598
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2560x1598
Megapixels                      : 4.1
```

Podemos notar la cadena sospechosa `cGljb0NURnt0aGVfbTN0YWRhdGFfMXNfbW9kaWZpZWR9` , que al pasarla por CyberChef, aprendemos que está encriptada en base64

Al desencriptarla, obtenemos nuestra bandera

picoCTF{the_m3tadata_1s_modified}
## Notas
- https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=Y0dsamIwTlVSbnQwYUdWZmJUTjBZV1JoZEdGZk1YTmZiVzlrYVdacFpXUjk