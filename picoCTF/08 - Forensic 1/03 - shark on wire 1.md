# shark on wire 1

## Descripción
We found this [packet capture](https://challenge-files.picoctf.net/c_fickle_tempest/134d2a2cf6ec5b7e757effc9b32977af7cc324b8e99a5ddb64737794a14dc18d/capture.pcap). Recover the flag.
## Solución
### Solución:
Al entrar al reto, lo único que nos entregan es un archivo PCAP (Packet Capture), así que dentro de kali, utilizaremos la herramienta windshark, como nos indica la pista

![[picoCTF/08 - Forensic 1/imagenes/03sharkonwire1.png]]

Vemos que la comunicación comenzó en el paquete número 11 comenzó la comunicación, así que nos dedicaremos a seguir su stream

![[picoCTF/08 - Forensic 1/imagenes/03sharkonwire2.png]]

Es en el stream 6 que encontramos la bandera

![[picoCTF/08 - Forensic 1/imagenes/03sharkonwire3.png]]

picoCTF{StaT31355_636f6e6e}
## Notas
