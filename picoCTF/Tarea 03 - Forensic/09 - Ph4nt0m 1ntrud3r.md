# Ph4nt0m 1ntrud3r

## Descripción
A digital ghost has breached my defenses, and my sensitive data has been stolen! 😱💻 Your mission is to uncover how this phantom intruder infiltrated my system and retrieve the hidden flag.
To solve this challenge, you'll need to analyze the provided PCAP file and track down the attack method. The attacker has cleverly concealed his moves in well timely manner. Dive into the network traffic, apply the right filters and show off your forensic prowess and unmask the digital intruder!
Find the PCAP file here [Network Traffic PCAP file](https://challenge-files.picoctf.net/c_verbal_sleep/a681faccaaa199ce75c3abeef9525f813b6451644a8d8d27cc097e4b1ccb741a/myNetworkTraffic.pcap) and try to get the flag.
## Solución
Para este reto usaremos tshark, que es como wireshark pero en versión para la consola.

Comenzaremos recuperando toda la información de los paquetes TCP con este comando
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/phantom]
└─$ tshark -r myNetworkTraffic.pcap -Y "tcp" -T fields -e tcp.segment_data | xxd -p -r | base64 -d

{1t_w4s#����F׸_�Q;�5��B��8�picoCTF)a!�4`        �D��\bh_4r_�1ߎ<f����,���nt_th4t1065384ĂOmh_34sy_t�8��?�e���}I9�y�
```
Si obtuvimos toda la información pero no se muestra correctamente dado a que no necesitamos toda la información.

Ahora solo recuperaremos la información de los paquetes cuyo tamaño sea de 12
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/phantom]
└─$ tshark -r myNetworkTraffic.pcap -Y "tcp.len==12" -T fields -e tcp.segment_data | xxd -p -r | base64 -d
{1t_w4spicoCTFbh_4r_dnt_th4t1065384_34sy_t
```

Como podemos notar, nos han dado la bandera pero está desordenada, por lo que usaremos un último comando para ordenarla
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Forensic/phantom]
└─$ tshark -r myNetworkTraffic.pcap -Y "tcp.len==12 || tcp.len==4" -T fields -e frame.time -e tcp.segment_data | sort -k4 | awk '{print $NF}' | tr -d '\n' | xxd -p -r | base64 -d
picoCTF{1t_w4snt_th4t_34sy_tbh_4r_d1065384}
```

picoCTF{1t_w4snt_th4t_34sy_tbh_4r_d1065384}
## Notas
- 