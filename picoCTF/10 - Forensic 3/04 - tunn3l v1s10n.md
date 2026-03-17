# tunn3l v1s10n

## Descripción
We found this file. Recover the flag.
[tunn3l_v1s10n](https://challenge-files.picoctf.net/c_wily_courier/626df9feed926c1e1280804f5d87fde5576e266ff250a819a5528b0471b0f3f7/tunn3l_v1s10n)
## Solución
Primero, utilizaremos un editor hexadecimal para revisar qué tipo de archivo es pues no tiene una extensión
```
00000000  42 4D 8E 26  2C 00 00 00   00 00 BA D0  00 00 BA D0                                                                                         BM.&,...........
00000010  00 00 6E 04  00 00 32 01   00 00 01 00  18 00 00 00                                                                                         ..n...2.........
00000020  00 00 58 26  2C 00 25 16   00 00 25 16  00 00 00 00                                                                                         ..X&,.%...%.....
00000030  00 00 00 00  00 00 23 1A   17 27 1E 1B  29 20 1D 2A                                                                                         ......#..'..) .*
00000040  21 1E 26 1D  1A 31 28 25   35 2C 29 33  2A 27 38 2F                                                                                         !.&..1(%5,)3*'8/
00000050  2C 2F 26 23  33 2A 26 2D   24 20 3B 32  2E 32 29 25                                                                                         ,/&#3*&-$ ;2.2)%
00000060  30 27 23 33  2A 26 38 2C   28 36 2B 27  39 2D 2B 2F                                                                                         0'#3*&8,(6+'9-+/
00000070  26 23 1D 12  0E 23 17 11   29 16 0E 55  3D 31 97 76                                                                                         &#...#..)..U=1.v
00000080  66 8B 66 52  99 6D 56 9E   70 58 9E 6F  54 9C 6F 54                                                                                         f.fR.mV.pX.oT.oT
00000090  AB 7E 63 BA  8C 6D BD 8A   69 C8 97 71  C1 93 71 C1                                                                                         .~c..m..i..q..q.
000000A0  97 74 C1 94  73 C0 93 72   C0 8F 6F BD  8E 6E BA 8D                                                                                         .t..s..r..o..n..
000000B0  6B B7 8D 6A  B0 85 64 A0   74 55 A3 77  5A 98 6F 56                                                                                         k..j..d.tU.wZ.oV
000000C0  76 52 3A 71  52 3D 6C 4F   40 6D 52 44  6E 53 49 77                                                                                         vR:qR=lO@mRDnSIw
000000D0  5E 54 53 39  33 70 58 52   76 61 59 73  5F 54 7E 6B                                                                                         ^TS93pXRvaYs_T~k
```

Vemos que es un bmp, o bitmap. Pero su encabezado no es correcto y por eso, como nos indica la pista, no muestra nada al abrirlo.

Así que usaremos el hexeditor para modificar los valores de necesitamos
- offset 0x0e
	- Aquí editamos el BA D0 para que pase a ser 28 00
- offset 0x0a
	- Aquí volvemos a editar el BA D0 para que pase a ser 28 00

Con estas correcciones, intentamos abrir la imagen pero no hay bandera
![[04_tunnel01.png]]

Buscando en los metadatos del archivo, podemos notar que la altura de la imagen no es completamente concordante con el tamaño que tiene el archivo.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/15_Forensic3/tunnel_vision]
└─$ exiftool tunn3l_v1s10n 
ExifTool Version Number         : 13.36
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2026:03:17 19:24:11-04:00
File Access Date/Time           : 2026:03:17 19:24:11-04:00
File Inode Change Date/Time     : 2026:03:17 19:24:11-04:00
File Permissions                : -rwxrwx---
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Windows V3
Image Width                     : 1134
Image Height                    : 306
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Image Size                      : 1134x306
Megapixels                      : 0.347
```

Así que regresamos al hexeditor, en el offset 16, que es quién controla la altura de la imagen.

Tras realizar la edición, volvemos a revisar los metadatos, y vemos que si aumentó la altura de la imagen.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/15_Forensic3/tunnel_vision]
└─$ hexeditor tunn3l_v1s10n
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/15_Forensic3/tunnel_vision]
└─$ exiftool tunn3l_v1s10n 
ExifTool Version Number         : 13.36
File Name                       : tunn3l_v1s10n
Directory                       : .
File Size                       : 2.9 MB
File Modification Date/Time     : 2026:03:17 19:30:13-04:00
File Access Date/Time           : 2026:03:17 19:30:13-04:00
File Inode Change Date/Time     : 2026:03:17 19:30:13-04:00
File Permissions                : -rwxrwx---
File Type                       : BMP
File Type Extension             : bmp
MIME Type                       : image/bmp
BMP Version                     : Windows V3
Image Width                     : 1134
Image Height                    : 1088
Planes                          : 1
Bit Depth                       : 24
Compression                     : None
Image Length                    : 2893400
Pixels Per Meter X              : 5669
Pixels Per Meter Y              : 5669
Num Colors                      : Use BitDepth
Num Important Colors            : All
Image Size                      : 1134x1088
Megapixels                      : 1.2
```

Ahora sí, nuestra flag es visible
![[04_tunnel02.png]]

picoCTF{qu1t3_a_v13w_2020}
## Notas
