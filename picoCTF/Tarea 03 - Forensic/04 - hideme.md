# hideme

## Descripción
Every file gets a flag.
The SOC analyst saw one image been sent back and forth between two people. They decided to investigate and found out that there was more than what meets the eye [here](https://artifacts.picoctf.net/c/259/flag.png).
## Solución
Para este reto lo único que haremos es aplicarle un xxd para ver los bytes del archivo, y podemos ver una referencia a una carpeta ``secret``, así que podemos intuir que hay un zip escondido en la imagen
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/hideme]
└─$ xxd flag.png| tail     
0000a720: 1000 ed41 0000 0000 7365 6372 6574 2f55  ...A....secret/U
0000a730: 5405 0003 8f78 1264 7578 0b00 0104 0000  T....x.dux......
0000a740: 0000 0400 0000 0050 4b01 021e 0314 0000  .......PK.......
0000a750: 0008 003a 1070 5667 4523 b535 0b00 00d0  ...:.pVgE#.5....
0000a760: 0b00 000f 0018 0000 0000 0000 0000 00a4  ................
0000a770: 8141 0000 0073 6563 7265 742f 666c 6167  .A...secret/flag
0000a780: 2e70 6e67 5554 0500 038f 7812 6475 780b  .pngUT....x.dux.
0000a790: 0001 0400 0000 0004 0000 0000 504b 0506  ............PK..
0000a7a0: 0000 0000 0200 0200 a200 0000 bf0b 0000  ................
0000a7b0: 0000
```

Sabiendo esto, le aplicaremos un binwalk para extraer estos archivos ocultos
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/hideme]
└─$ binwalk -e flag.png              

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
41            0x29            Zlib compressed data, compressed
39739         0x9B3B          Zip archive data, at least v1.0 to extract, name: secret/
39804         0x9B7C          Zip archive data, at least v2.0 to extract, compressed size: 2869, uncompressed size: 3024, name: secret/flag.png

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented
```

Ahora solo cambiamos de carpeta y abrimos el archivo
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/hideme]
└─$ cd _flag.png.extracted                                                                   
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/hideme/_flag.png.extracted]
└─$ tree
.
├── 29
├── 29.zlib
├── 9B3B.zip
└── secret
    └── flag.png

2 directories, 4 files
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/hideme/_flag.png.extracted]
└─$ open secret/flag.png
```

Ahí encontraremos la bandera
![flag](https://miro.medium.com/v2/resize:fit:640/format:webp/1*1NBAWnzbN58F6wXZO8JjcA.png)

picoCTF{Hiddinng_An_imag3_within_@n_ima9e_cda72af0}
## Notas
- Imagen tomada de aquí: https://0xodinx.medium.com/picoctf-hideme-writeup-5bc0a6289141