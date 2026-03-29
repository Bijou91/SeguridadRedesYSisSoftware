# Scan Surprise

## Descripción
I've gotten bored of handing out flags as text. Wouldn't it be cool if they were an image instead?You can download the challenge files here:
- [challenge.zip](https://artifacts.picoctf.net/c_atlas/15/challenge.zip)
## Solución
Para este reto lo único que haremos es conectarnos al servidor que nos proporcionan, lo cual directamente nos muestra una imagen de un código QR
![QR](https://miro.medium.com/v2/resize:fit:720/format:webp/1*sn1FJ7KUop6oCdlxvra5jg.png)

Para escanearlo usaremos el comando zbarimg, que nos proporciona la bandera
```
ctf-player@challenge:~/drop-in$ zbarimg flag.png
Connection Error (Failed to connect to socket /var/run/dbus/system_bus_socket: No such file or directory)
Connection Null
QR-Code:picoCTF{p33k_@_b00_19eccd10}
```

``picoCTF{p33k_@_b00_19eccd10}``
## Notas
- Imagen del QR tomada de aquí: https://iritt.medium.com/picoctf-scan-surprise-challenge-walkthrough-026b20a3b2a3