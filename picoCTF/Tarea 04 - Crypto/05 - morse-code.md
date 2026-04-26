# morse-code

## Descripción
Morse code is well known. Can you decrypt this?
Download the file [here](https://artifacts.picoctf.net/c/79/morse_chal.wav).
Wrap your answer with picoCTF{}, put underscores in place of pauses, and use all lowercase.
## Solución
Para esto lo que único que haremos es subir el archivo .wav a un decodificador de código morse, y este nos entregará el código decodificado

**WH47 H47H 90D W20U9H7**

El cual, como nos indica el reto, le agregamos el picoctf{} y guiones bajos para sustituir los espacios

picoCTF{WH47_H47H_90D_W20U9H7}
## Notas
- https://morsecode.world/international/decoder/audio-decoder-adaptive.html