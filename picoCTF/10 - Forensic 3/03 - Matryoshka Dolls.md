# Matryoshka Dolls

## Descripción
Matryoshka dolls are a set of wooden dolls of decreasing size placed one inside another. What's the final one?
Image: [dolls.jpg](https://challenge-files.picoctf.net/c_wily_courier/f1f4181c217358672b720e801df28731166311181fd73b364baa4479f8500044/dolls.jpg)
## Solución
Al analizar los metadatos de la imagen, vemos que tiene un zip 'dentro' (sin dejar de ser una imagen)

Así que para esto utilizaremos la herramienta binwalk para extraer estos archivos 'ocultos'. Yo tuve que agregar cosas extra al comando pues no funcionaba simplemente poner `binwalk -e dolls.jpg`
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/15_Forensic3/M_dolls]
└─$ binwalk -e --matryoshka dolls.jpg

Scan Time:     2026-03-15 22:45:09
Target File:   /media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/dolls.jpg
MD5 Checksum:  563f82d420f407f582d6cce327617ea2
Signatures:    436

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
272492        0x4286C         Zip archive data, at least v2.0 to extract, compressed size: 378933, uncompressed size: 383920, name: base_images/2_c.jpg

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented


Scan Time:     2026-03-15 22:45:09
Target File:   /media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/_dolls.jpg.extracted/base_images/2_c.jpg
MD5 Checksum:  e3fa93b59d62b25117c563f028cdf8ed
Signatures:    436

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
187707        0x2DD3B         Zip archive data, at least v2.0 to extract, compressed size: 196025, uncompressed size: 201427, name: base_images/3_c.jpg

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented


Scan Time:     2026-03-15 22:45:09
Target File:   /media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/3_c.jpg
MD5 Checksum:  fdbf99dfe0b7d1597c3eb005cbefccab
Signatures:    436

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
123606        0x1E2D6         Zip archive data, at least v2.0 to extract, compressed size: 77633, uncompressed size: 79786, name: base_images/4_c.jpg

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented


Scan Time:     2026-03-15 22:45:10
Target File:   /media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/4_c.jpg
MD5 Checksum:  dbc103a52d4ea7741386f2b409fe0c68
Signatures:    436

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
79578         0x136DA         Zip archive data, at least v1.0 to extract, compressed size: 42, uncompressed size: 42, name: flag.txt

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented


Scan Time:     2026-03-15 22:45:10
Target File:   /media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted/flag.txt
MD5 Checksum:  c8974fd9d4f96521b3fe75e817437d77
Signatures:    436

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
```

Como vemos en esa última extracción
```
/media/sf_almacenamientoCompartido/15_Forensic3/M_dolls/_dolls.jpg.extracted/base_images/_2_c.jpg.extracted/base_images/_3_c.jpg.extracted/base_images/_4_c.jpg.extracted/flag.txt
```
tenemos un archivo flag.txt, que al abrirlo descubrimos nuestra flag.

picoCTF{LL9lb1dR4QbGe4l4iWCvGq9pdtwt7392}
## Notas
