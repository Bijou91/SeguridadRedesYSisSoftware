# shark on wire 2

## Descripción
We found this [packet capture](https://challenge-files.picoctf.net/c_fickle_tempest/07bf5ee832c595a6de406476b6c07f164d2951fbcfcf9cf3739c25dea26e5f0b/capture.pcap). Recover the flag.
## Solución
A diferencia del resto de paquetes, el paquete #1104 tiene una fuente y puerto de destino diferentes.
![[sharkwire2.png]]

Entonces, con este pequeño código extraeremos los puertos de destino
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/sharkonwire2]
└─$ tcpdump -nr capture.pcap "udp and port 22" |awk {'print $3'} |cut -d . -f 5 |tr '\n' ' '
reading from file capture.pcap, link-type EN10MB (Ethernet), snapshot length 262144
5000 5112 5105 5099 5111 5067 5084 5070 5123 5112 5049 5076 5076 5102 5051 5114 5051 5100 5095 5100 5097 5116 5097 5095 5118 5049 5097 5095 5115 5116 5051 5103 5048 5125 5000
```

Podemos notar que empieza y termina con el número 5000, lo que nos puede indicar un mensaje oculto, así que ahora aplicaremos el mismo código, pero ahora extrayendo un 5 y un 0
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/14_Forensic2/sharkonwire2]
└─$ tcpdump -nr capture.pcap "udp and port 22" |awk {'print $3'} |cut -d . -f 5 |sed 's/^5//g' |sed 's/^0//g' |tr '\n' ' '
reading from file capture.pcap, link-type EN10MB (Ethernet), snapshot length 262144
00 112 105 99 111 67 84 70 123 112 49 76 76 102 51 114 51 100 95 100 97 116 97 95 118 49 97 95 115 116 51 103 48 125 00
```

Esto nos deja con estos caracteres que podemos decodificar con [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Charcode('Space',10)&input=MDAgMTEyIDEwNSA5OSAxMTEgNjcgODQgNzAgMTIzIDExMiA0OSA3NiA3NiAxMDIgNTEgMTE0IDUxIDEwMCA5NSAxMDAgOTcgMTE2IDk3IDk1IDExOCA0OSA5NyA5NSAxMTUgMTE2IDUxIDEwMyA0OCAxMjUgMDA&oeol=NEL), que nos entrega nuestra bandera.

picoCTF{p1LLf3r3d_data_v1a_st3g0}
## Notas
Reto realizado con esta [guía](https://dmfrsecurity.com/2021/09/05/picoctf-2019-shark-on-wire-2-writeup/).