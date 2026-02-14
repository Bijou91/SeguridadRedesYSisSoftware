# PW Crack 3

## Descripción
Can you crack the password to get the flag?
Download the password checker and you'll need the encrypted flag in the same directory too.
## Solución
### Solución:
Este es el script original:
```
import hashlib

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

flag_enc = open('level3.flag.txt.enc', 'rb').read()
correct_pw_hash = open('level3.hash.bin', 'rb').read()

def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()

def level_3_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    user_pw_hash = hash_pw(user_pw)
    
    if( user_pw_hash == correct_pw_hash ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")

level_3_pw_check()

# The strings below are 7 possibilities for the correct password. 
#   (Only 1 is correct)
pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
```

Analizando este código, podemos notar que en la lista del final del código, tenemos todas las posibilidades de contraseñas. 

Lo que haremos ahora es modificar el código de la función level_3_pw_check para que automatice la revisión de cada posible contraseña hasta que encuentre la correcta:
```
def level_3_pw_check():
    # The strings below are 7 possibilities for the correct password. 
    #   (Only 1 is correct)
    pos_pw_list = ["6997", "3ac8", "f0ac", "4b17", "ec27", "4e66", "865e"]
    
    for user_pw in pos_pw_list:
        user_pw_hash = hash_pw(user_pw)
        
        if user_pw_hash == correct_pw_hash:
            print("Welcome back... your flag, user:")
            decryption = str_xor(flag_enc.decode(), user_pw)
            print(decryption)
            return
    
    print("That password is incorrect")  
	  
level_3_pw_check()
```

Tras ejecutar el código, obtenemos esta salida
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/03_GeneralSkills3/09-PWCrack3]
└─$ python level3.py
Welcome back... your flag, user:
picoCTF{m45h_fl1ng1ng_2b072a90}
```

picoCTF{m45h_fl1ng1ng_2b072a90}
## Notas
