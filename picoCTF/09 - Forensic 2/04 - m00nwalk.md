# m00nwalk

## Descripción
Decode this [message](https://challenge-files.picoctf.net/c_fickle_tempest/c9834b19f74a20802d7c53dc42fe1ccd8a69da4cf5c38fa5b6aab8ec472efdd3/message.wav) from the moon.
## Solución
Para descodificar el archivo .wav, usaremos la herramienta sstv, y a posterior, lo abrimos
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/moonwalk]
└─$ sstv -d message.wav -o result.png
Searching for calibration header... Found!    
Detected SSTV mode Scottie 1
Decoding image...                                    [####################################################################################################] 100%
Drawing image data...
...Done!

┌──(kali㉿kali)-[~/sstv_work]
└─$ open result.png
```

![[space.png]]

picoCTF{beep_boop_im_in_space}
## Notas
