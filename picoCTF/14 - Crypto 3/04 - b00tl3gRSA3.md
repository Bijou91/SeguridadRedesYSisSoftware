# b00tl3gRSA3

## Descripción

Why use p and q when I can use more? Connect with nc fickle-tempest.picoctf.net 61386.

## Solución

Este reto presenta un escenario de RSA donde el módulo `n` no está compuesto por dos primos grandes, sino por **34 primos pequeños** de aproximadamente 10 dígitos cada uno. Esta construcción hace que `n` sea fácil de factorizar, ya que herramientas como FactorDB o Pollard-rho pueden encontrar factores pequeños rápidamente.

Los valores obtenidos al conectarnos vía `nc` son:

```
c: 2213503298336887925063662260682393118723243241754772547946002122960252004379690546401151260899478700853469664093974970405841041606501908320543068385779083242129037107109661515954255616707029518022466245661782055339204876825870306475270184799584424753847008802285431186586039151003788109073780572837301292299563634905047518753525842500352923592
n: 13582287285330518402990749001942452832825180440387656796763143720720456051090643572004315475131613104712685671801606276606810335101847334924737753586662752643193710263580428676802727239378708376014141146480319457871023779915231525667874081893234130382594306791989679992799179528768187129381997651446549845116355205212674626312214409295310086951
e: 65537
```

Cuando `n` es producto de muchos primos pequeños, la factorización es computacionalmente asequible. Una vez obtenidos todos los factores primos `p1, p2, ..., pk`, calculamos:

```
phi(n) = (p1-1)(p2-1)...(pk-1)
d = e⁻¹ mod phi(n)
flag = c^d mod n
```

Este es el código que usaremos. Primero intentamos FactorDB para los factores conocidos, y usamos **Brent-Pollard rho** localmente para completar los que FactorDB devuelva como compuestos:

```python
import math, random, gmpy2
from functools import reduce
from sympy.ntheory import isprime

c = 2213503298336887925063662260682393118723243241754772547946002122960252004379690546401151260899478700853469664093974970405841041606501908320543068385779083242129037107109661515954255616707029518022466245661782055339204876825870306475270184799584424753847008802285431186586039151003788109073780572837301292299563634905047518753525842500352923592
n = 13582287285330518402990749001942452832825180440387656796763143720720456051090643572004315475131613104712685671801606276606810335101847334924737753586662752643193710263580428676802727239378708376014141146480319457871023779915231525667874081893234130382594306791989679992799179528768187129381997651446549845116355205212674626312214409295310086951
e = 65537

def brent_rho(n):
    if n % 2 == 0: return 2
    if isprime(n): return n
    for _ in range(200):
        y, c2, m = random.randint(1,n-1), random.randint(1,n-1), random.randint(1,n-1)
        g, q, r = 1, 1, 1
        while g == 1:
            x = y
            for _ in range(r):
                y = (y*y + c2) % n
            k = 0
            while k < r and g == 1:
                ys = y
                for _ in range(min(m, r-k)):
                    y = (y*y + c2) % n
                    q = q * abs(x-y) % n
                g = math.gcd(q, n)
                k += m
            r *= 2
        if g == n:
            while True:
                ys = (ys*ys + c2) % n
                g = math.gcd(abs(x-ys), n)
                if g > 1: break
        if g != n:
            return g
    return n

def full_factor(n):
    if n == 1: return []
    if isprime(n): return [n]
    for p in range(2, 1000):
        if n % p == 0:
            return [p] + full_factor(n // p)
    d = brent_rho(n)
    if d == n: return [n]
    return full_factor(d) + full_factor(n // d)

print("[*] Factorizando n con Brent-Pollard rho...")
all_primes = sorted(full_factor(n))
print(f"[+] {len(all_primes)} primos: {all_primes}")

assert reduce(lambda x, y: x * y, all_primes) == n
print("[+] Verificación OK")

phi_n = reduce(lambda x, y: x * y, [p - 1 for p in all_primes])
d = int(gmpy2.invert(e, phi_n))
plaintext = pow(c, d, n)

hex_str = format(plaintext, 'x')
if len(hex_str) % 2: hex_str = '0' + hex_str
flag = bytes.fromhex(hex_str).decode('utf-8', errors='replace')
print(f"\n[+] FLAG: {flag}")
```

Y esta es la salida que obtenemos, junto a nuestra bandera:

```
┌──(venv)─(kali㉿kali)-[~/RsaCtfTool]
└─$ python3 solve_b00tl3g3.py
[*] Factorizando n con Brent-Pollard rho...
[+] 34 primos: [8855848591, 8941439279, 9293291387, 9506985539, 9685382321,
 9940717429, 10057254293, 10443032983, 10668324727, 10767704537, 11106435539,
 12062326979, 12152230081, 12289287887, 12843665407, 13645842073, 13662445351,
 14603531287, 14707385243, 14946547699, 15042853729, 17056338239, 10466701111,
 10636623521, 11346857101, 12206678069, 13392631573, 13948679257, 14423450453,
 15487043303, 15554695903, 15669049987, 16058080781, 16818421409]
[+] Verificación OK

[+] FLAG: picoCTF{too_many_fact0rs_3023548}
```

**picoCTF{too_many_fact0rs_3023548}**

## Notas

- 