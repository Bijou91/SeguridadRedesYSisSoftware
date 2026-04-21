# Mini RSA

# Descripción 
What happens if you have a small exponent? There is a twist though, we padded the plaintext so that (M ** e) is just barely larger than N. Let's decrypt this.
- **Pista:** pico is in the flag, but not at the beginning
## Solución

El archivo entregado contiene estos parámetros RSA:

```
N: 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401...
e: 3
c: 5709720175026317841944505166332182779419760031115432215563425901875620052791608163398...
```

Con `e = 3` y el mensaje paddeado para que `M³` sea apenas mayor que `N`, la reducción modular apenas ocurre. Esto significa:

```
M³ = c + k·N   (donde k es un entero pequeño: 0, 1, 2, ...)
```

Si encontramos `k` tal que `(c + k·N)` sea un cubo perfecto, entonces `M = ∛(c + k·N)`.

En este caso se observó que `c > N`, lo que indica que `c` ya es directamente `M³` sin reducción modular (k = 0). Basta con calcular la raíz cúbica exacta de `c`.

Se usó el siguiente script:

```python
def icbrt(n):
    # Raíz cúbica entera (método de Newton en aritmética entera)
    if n == 0: return 0
    x = n
    y = (2*x + n // (x*x)) // 3
    while y < x:
        x = y
        y = (2*x + n // (x*x)) // 3
    return x

N = 1615765684321463054078226051959887884233678317734892901740763321135213636796075462401...
e = 3
c = 5709720175026317841944505166332182779419760031115432215563425901875620052791608163398...

for k in range(0, 1000):
    candidate = c + k * N
    root = icbrt(candidate)
    if root**3 == candidate:
        m_bytes = root.to_bytes((root.bit_length() + 7) // 8, 'big')
        print(f'Flag: {m_bytes.decode("utf-8", errors="replace")}')
        break
```

Con `k = 0` se encontró el cubo perfecto directamente, y la salida fue:

```
Flag:                                         picoCTF{e_sh0u1d_b3_lArg3r_92f4d5a5}
```

Los espacios al inicio son el padding añadido al mensaje para inflar `M` y asegurar que `M³ > N`.

Flag: `picoCTF{e_sh0u1d_b3_lArg3r_92f4d5a5}`

## Notas
- 