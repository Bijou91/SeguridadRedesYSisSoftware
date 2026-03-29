# Redaction gone wrong

## Descripción
Now you DON’T see me.
This [report](https://artifacts.picoctf.net/c/84/Financial_Report_for_ABC_Labs.pdf) has some critical data in it, some of which have been redacted correctly, while some were not. 
Can you find an important key that was not redacted properly?
## Solución
Para este reto nos entregan un reporte de finanzas en pdf. Como podemos ver, hay un montón de recuadros negros que no nos permiten ver toda la información.
![report](https://miro.medium.com/v2/resize:fit:640/format:webp/1*__giu9FQBrajkFADgF27bw.png)

Para solucionar este reto, solo hay que copiar y pegar el texto (incluyendo los recuadros negros) fuera del pdf
```
Financial Report for ABC Labs, Kigali, Rwanda for the year 2021.
Breakdown - Just painted over in MS word.

Cost Benefit Analysis
Credit Debit
This is not the flag, keep looking
Expenses from the
picoCTF{C4n_Y0u_S33_m3_fully}
Redacted document.
```

picoCTF{C4n_Y0u_S33_m3_fully}
## Notas
- 