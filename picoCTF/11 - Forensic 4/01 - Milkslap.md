# Milkslap

## Descripción
🥛
## Solución
Cuando arrancamos el reto, solo nos entregan esta [página web](http://wily-courier.picoctf.net:51124/). Donde hay un gif que actúa según el movimiento de nuestro cursor.

Así que revisaremos el código fuente de la página:
```html
<!doctype html>

<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=400" />
  <title>🥛</title>
  <link rel="stylesheet" href="style.css" />

</head>
<body>
  <div id="image" class="center"></div>
  <div id="foot" class="center">
    <h1>MilkSlap!</h1>
    Inspired by <a href="http://eelslap.com">http://eelslap.com</a> <br>
    Credit to: <a href="https://github.com/boxmein">boxmein</a> for code inspiration.
  </div>
  <script src="script.js">


</script>
</body>
</html>
```

Para continuar, nos fijaremos dentro de la hoja de estilos
```css
/* source: milkslap-milkslap.scss */
body {
  margin: 0;
  padding: 0;
  overflow: hidden; }

a {
  color: inherit; }

.center {
  width: 1080px;
  height: 720px;
  margin: 0 auto; }

#image {
  height: 720px;
  margin-top: 5%;
  margin-bottom: 20px;
  background-image: url(concat_v.png);
  background-position: 0 0; }

#foot {
  margin-bottom: 5px;
  color: #999999; }
  #foot h1 {
    font-family: serif;
    font-weight: normal;
    font-size: 1rem;
    text-align: center; }
```

Vemos que se hace referencia a un archivo **.png**, así que lo manipularemos de manera local utilizando zsteg, que es una herramienta utilizada para detectar datos ocultos mediante esteganografía en archivos PNG y BMP.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/milkslap]
└─$ wget http://wily-courier.picoctf.net:51124/concat_v.png
--2026-03-20 19:34:41--  http://wily-courier.picoctf.net:51124/concat_v.png
Resolving wily-courier.picoctf.net (wily-courier.picoctf.net)... 18.189.99.27
Connecting to wily-courier.picoctf.net (wily-courier.picoctf.net)|18.189.99.27|:51124... connected.
HTTP request sent, awaiting response... 200 OK
Length: 18095920 (17M) [image/png]
Saving to: ‘concat_v.png’

concat_v.png                              100%[===================================================================================>]  17.26M   818KB/s    in 25s     

2026-03-20 19:35:07 (698 KB/s) - ‘concat_v.png’ saved [18095920/18095920]

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/16_Forensic4/milkslap]
└─$ RUBY_THREAD_VM_STACK_SIZE=500000000 zsteg concat_v.png

imagedata           .. text: "\n\n\n\n\n\n\t\t"
chunk:0:IHDR        .. file: Adobe Photoshop Color swatch, version 0, 1280 colors; 1st RGB space (0), w 0xb9a0, x 0x802, y 0, z 0; 2nd HSB space (1), w 0, x 0, y 0, z 0                                                                                                                                                                    
b1,b,lsb,xy         .. text: "picoCTF{imag3_m4n1pul4t10n_sl4p5}\n"
b1,bgr,lsb,xy       .. <wbStego size=0x941a5b ext=nil data="\xB6\xAD\xB6}\xDB\xB2lR\x7F\xDF\x86\xB7c\xFC\xFF\xBF\x02Zr\x8E\xE2Z\x12\xD8q\xE5&MJ-X:\xB5\xBF\xF7\x7F\xDB\xDFI\bm\xDB\xDB\x80m\x00\x00\x00\xB6m\xDB\xDB\xB6\x00\x00\x00\xB6\xB6\x00m\xDB\x12\x12m\xDB\xDB\x00\x00\x00\x00\x00\xB6m\xDB\x00\xB6\x00\x00\x00\xDB\xB6mm\xDB\xB6\xB6\x00\x00\x00\x00\x00m\xDB" even=true hdr=nil enc=nil mix=true controlbyte="[">                                                                                       
b2,r,lsb,xy         .. text: ["U" repeated 8 times]
b2,r,msb,xy         .. file: VISX image file
b2,g,lsb,xy         .. file: VISX image file
b2,g,msb,xy         .. file: SoftQuad DESC or font file binary - version 15722
b2,b,msb,xy         .. text: "UfUUUU@UUU"
b4,r,lsb,xy         .. text: "\"\"\"\"\"#4D"
b4,r,msb,xy         .. text: "wwww3333"
b4,g,lsb,xy         .. text: "wewwwwvUS"
b4,g,msb,xy         .. text: "\"\"\"\"DDDD"
b4,b,lsb,xy         .. text: "vdUeVwweDFw"
b4,b,msb,xy         .. text: "UUYYUUUUUUUU"
```

picoCTF{imag3_m4n1pul4t10n_sl4p5}
## Notas
