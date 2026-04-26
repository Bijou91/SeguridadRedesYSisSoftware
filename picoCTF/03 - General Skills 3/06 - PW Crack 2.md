# PW Crack 2

## Descripción
Can you crack the password to get the flag?
Download the password checker and you'll need the encrypted flag in the same directory too.
## Solución
### Solución:
Este es el script original:
```python
### THIS FUNCTION WILL NOT HELP YOU FIND THE FLAG --LT ########################
def str_xor(secret, key):
    #extend key to secret length
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c,new_key_c) in zip(secret,new_key)])
###############################################################################

flag_enc = open('level2.flag.txt.enc', 'rb').read()

def level_2_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65) ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

level_2_pw_check()
```

Analizando este código, podemos notar que en el if cerca del final, se nos pone cuál es la contraseña, esta vez en formato ascii
### Python:
Para obtener el valor de la contraseña, utilizamos python para convertir```
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/03_GeneralSkills3/06-PWCrack2]
└─$ python          
Python 3.13.9 (main, Oct 15 2025, 14:56:22) [GCC 15.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> print(chr(0x33) + chr(0x39) + chr(0x63) + chr(0x65))
39ce
```

Tras ejecutar el código, obtenemos esta salida
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/03_GeneralSkills3/06-PWCrack2]
└─$ python level2.py
Please enter correct password for flag: 39ce
Welcome back... your flag, user:
picoCTF{tr45h_51ng1ng_502ec42e}
```

picoCTF{tr45h_51ng1ng_502ec42e}
## Notas
