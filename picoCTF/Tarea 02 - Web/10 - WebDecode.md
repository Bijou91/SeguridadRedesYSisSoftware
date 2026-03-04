# WebDecode

## Descripción
Do you know how to use the web inspector?
## Solución
### Solución:
Al entrar a la página que nos dan, vemos esta pantalla, que nos dice que ya tenemos la flag, pero no podemos verla
![[10WebDecode01.png]]

En la página de 'About' en la página, nos dan la pista de revisar el código fuente de la página
![[10WebDecode02.png]]

Ahí, encontramos esta línea
```
<section class="about" notify_true="cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMWY4MzI2MTV9">
```

Como vemos, hay una cadena de texto bastante extraña, que parece estar encriptada en base64
```
cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfMWY4MzI2MTV9 ---> picoCTF{web_succ3ssfully_d3c0ded_1f832615}
```

picoCTF{web_succ3ssfully_d3c0ded_1f832615}
## Notas
