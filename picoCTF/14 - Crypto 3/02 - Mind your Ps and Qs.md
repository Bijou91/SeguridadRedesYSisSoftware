# Mind your Ps and Qs

## Descripción
In RSA, a small e value can be problematic, but what about N? Can you decrypt this?
[values](https://challenge-files.picoctf.net/c_wily_courier/f5f0388785f1835df56b6c50fcbe25d88004d2c3184fe7191b852514bf04941a/values)
## Solución
Como el nombre del reto nos indica, nuevamente nos topamos con una encriptación RSA. El archivo que nos entregan contiene esto:
```
Decrypt my super sick RSA:
c: 15341890103764929939105506004034128738090325640037083301857608662849501626260517
n: 948406957756830799684818171639547165784816468744946013083947881743680617123566349
e: 65537
```

El archivo que nos entregan solo tiene c, n y e, pero no p y q. Necesitamos factorizar n primero.

Esto lo hacemos con una página web (https://factordb.com/), donde le pasamos el valor de nuestra n, y estos son los valores que recibimos
```
	9484069577...49<81> = 1891771437429478964908181306574287207137<40> · 501332739776173570344039681219489434626477<42>
```

Ahora que tenemos nuestros valores de p y q, usamos este script
```python
from Crypto.Util.number import inverse, long_to_bytes

n = 948406957756830799684818171639547165784816468744946013083947881743680617123566349
c = 15341890103764929939105506004034128738090325640037083301857608662849501626260517
e = 65537

p = 1891771437429478964908181306574287207137
q = 501332739776173570344039681219489434626477

phi = (p - 1) * (q - 1)
d = inverse(e, phi)
m = pow(c, d, n)
print(long_to_bytes(m))
```

En esta ocasión, me imprimió la bandera al revés: `}19ea7cd1_do0g_0n_N_11ams{FTCocip`

Usando [text reverse](https://www.textreverse.com/) esta es la flag:
picoCTF{sma11_N_n0_g0od_1dc7ae91}
## Notas
- 