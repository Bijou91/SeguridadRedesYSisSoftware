# Nice netcat
# Descripción
There is a nice program that you can talk to by using this command in a shell:$ nc wily-courier.picoctf.net 56588, but it doesn't speak English...

## Solución
- Comandos de Linux
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/01_GeneralSkills/ObedientCat]
└─$ nc wily-courier.picoctf.net 56588
112 
105 
99 
111 
67 
84 
70 
123 
103 
48 
48 
100 
95 
107 
49 
116 
116 
121 
33 
95 
110 
49 
99 
51 
95 
107 
49 
116 
116 
121 
33 
95 
100 
57 
52 
55 
54 
125 
10
```

Ahora usamos un convertidor para pasar de ASCII a texto (https://www.duplichecker.com/ascii-to-text.php) y obtenemos este resultado:
```picoCTF{g00d_k1tty!_n1c3_k1tty!_d9476}```
## Notas
