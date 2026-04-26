# Vigenere

## Descripción
Can you decrypt this message?
Decrypt this [message](https://artifacts.picoctf.net/c/160/cipher.txt) using this key "CYLAB".
## Solución
Para resolver este reto, usaremos este código
```python
import string
instr="rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}"
key="CYLAB"
outstr=""
offset_lower=ord('a')
offset_upper=ord('A')
lower=string.ascii_lowercase
upper=string.ascii_uppercase


dicts_l={}
for k in key:
    key_loc=ord(k)-offset_upper
    dicts_l[k]={}
    for l in lower:
        cipher=chr((ord(l)-offset_lower+key_loc)%26+offset_lower)
        dicts_l[k][cipher]=l #dicts_l[key][cipher]=[plain]


dicts_u = {}
for k in key:
    key_loc = ord(k) - offset_upper
    dicts_u[k] = {}
    for u in upper:
        dicts_u[k][chr((ord(u) - offset_upper + key_loc) % 26 + offset_upper)] = u  # dicts_u[key][cipher]=[plain]

count=0
for c in instr:
    if c.isalpha():
        if c.islower():
            outstr+=dicts_l[key[count%len(key)]][c]
        elif c.isupper():
            outstr+=dicts_u[key[count%len(key)]][c]
        count+=1
    else:
        outstr+=c
print(outstr)
```

El cual contiene el texto que nos proporciona el mensaje, así como la llave CYLAB que nos indica el reto.

Este código es un descifrador del Cifrado de Vigenere. Su objetivo es revertir un texto cifrado (instr) utilizando una palabra clave (key), en este caso "CYLAB", para recuperar el mensaje original (la flag).

Al ejecutar este script, obtenemos la flag
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto/vigenere]
└─$ python3 solve.py 
picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}
```
## Notas
