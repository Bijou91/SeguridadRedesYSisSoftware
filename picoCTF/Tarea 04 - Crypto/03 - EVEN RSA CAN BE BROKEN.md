# EVEN RSA CAN BE BROKEN???

## Descripción
This service provides you an encrypted flag. Can you decrypt it with just N & e?
Connect to the program with netcat:
`$ nc verbal-sleep.picoctf.net 62028`
The program's source code can be downloaded [here](https://challenge-files.picoctf.net/c_verbal_sleep/32d7f9da267fbc80629d78138372a9bdf1b8e574080294e184f95878950065d2/encrypt.py).
## Solución
Lo primero que haremos en este código es conectarnos múltiples veces al servidor que nos entregan para intentar un patrón
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ nc verbal-sleep.picoctf.net 49937                                                                                                  
N: 18814048263310562050507922096585494644363272988599658605824239932559950721508775809053279403741479818683263567665318355302316379675562890788113799766640822
e: 65537
cyphertext: 12480642106252489574633357505601358517995595362424562011253316477750372052067400027136291324596471228583114102835609273471551606664194716089110964993741125

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ nc verbal-sleep.picoctf.net 62250
N: 22504314002987805372715497361433241775461565489499982052234536807121276825253224316044872432638369992009171680087400094491538458615010651910338386765643402
e: 65537
cyphertext: 20198647898163381915656188330208924169057320486968457868321239947182576954205165050706493086139521341457200061092805524247937256120391918751164053137494185
     
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ nc verbal-sleep.picoctf.net 62250
N: 19306668395506183373950058889108091631358229608832284127968043571690260266305347814563063405637161402415452793288826376907175897668746176506306088537228494
e: 65537
cyphertext: 8965817781767449388039946762134892771220460486818095747553770086507467841638415698712003598916930263249310776926223666818675277752944641274705468538074177

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ nc verbal-sleep.picoctf.net 62250
N: 17074751258844578812939544513990806347712427838345990406417718613798209752059863951194710402533947461927661242572624887050003299994814758823751219743327822
e: 65537
cyphertext: 11920347397325483980013252952030012255122687852563235828529832295023984138058405287443682283160071528971844016640386287491836091249274347373437600263079383

┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ nc verbal-sleep.picoctf.net 62250
N: 15761367205023588147458607304405238840907365954044039982696401405801138040584179671546358336533050857520055175007335744397881798866637869532791979125223242
e: 65537
cyphertext: 1991629497040573941799314089522214623411760500509405904842478254278559193306848683640248870867971176482151607037048231153898397814537252148168375500047203
```

Podemos notar que todos los valores de N son par. Así que, para resolver este reto, simplemente podemos hacer ingeniería inversa a la codificación que hace el código original.

Código original:
```python
from sys import exit
from Crypto.Util.number import bytes_to_long, inverse
from setup import get_primes

e = 65537

def gen_key(k):
    """
    Generates RSA key with k bits
    """
    p,q = get_primes(k//2)
    N = p*q
    d = inverse(e, (p-1)*(q-1))

    return ((N,e), d)

def encrypt(pubkey, m):
    N,e = pubkey
    return pow(bytes_to_long(m.encode('utf-8')), e, N)

def main(flag):
    pubkey, _privkey = gen_key(1024)
    encrypted = encrypt(pubkey, flag) 
    return (pubkey[0], encrypted)

if __name__ == "__main__":
    flag = open('flag.txt', 'r').read()
    flag = flag.strip()
    N, cypher  = main(flag)
    print("N:", N)
    print("e:", e)
    print("cyphertext:", cypher)
    exit()
```

Código a usar para obtener la flag:
```python
from Crypto.Util.number import long_to_bytes, inverse

# valores
N = 18814048263310562050507922096585494644363272988599658605824239932559950721508775809053279403741479818683263567665318355302316379675562890788113799766640822
e = 65537
c = 12480642106252489574633357505601358517995595362424562011253316477750372052067400027136291324596471228583114102835609273471551606664194716089110964993741125

# Como N es par, p es 2
p = 2
# q es N dividido por 2 (usamos // para división entera)
q = N // 2

# Calculamos Phi
phi = (p - 1) * (q - 1)

# Calculamos el exponente privado
d = inverse(e, phi)

# Desciframos el mensaje
m = pow(c, d, N)

# Convertimos el número resultante a bytes para leer la flag
try:
    flag = long_to_bytes(m).decode()
    print(f"La flag es: {flag}")
except Exception as e:
    # A veces el decode falla si hay caracteres no ASCII, imprimimos el raw por si acaso
    print(f"Error al decodificar: {e}")
    print(f"Resultado en bytes: {long_to_bytes(m)}")
```

Ese código lo usaremos con los valores del inicio
`N = 18814048263310562050507922096585494644363272988599658605824239932559950721508775809053279403741479818683263567665318355302316379675562890788113799766640822`
`e = 65537`
`c = 12480642106252489574633357505601358517995595362424562011253316477750372052067400027136291324596471228583114102835609273471551606664194716089110964993741125`

Y así obtenemos la flag:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto]
└─$ python3 decrypt.py
La flag es: picoCTF{tw0_1$_pr!m3de643ad5}
```
## Notas
