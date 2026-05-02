# Picker IV

# Descripción 
Can you figure out how this program works to get the flag?
Connect to the program with netcat:
`$ nc saturn.picoctf.net 54391`
The program's source code can be downloaded [here](https://artifacts.picoctf.net/c/528/picker-IV.c). 
The binary can be downloaded [here](https://artifacts.picoctf.net/c/528/picker-IV).
## Solución
Lo que debemos hacer para resolver este reto es que una vez tengamos tanto el código fuente como el binario, usaremos la herramienta objdump para acceder a la ubicación de la función `win`
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/Reversing02/p4]
└─$ objdump -M intel -d  picker-IV | grep "win"
000000000040129e <win>:
  4012d2:       75 16                   jne    4012ea <win+0x4c>
  4012f9:       eb 1a                   jmp    401315 <win+0x77>
  401319:       75 e0                   jne    4012fb <win+0x5d>
```

Ahora nos conectamos al servidor y le pasamos la ubicación de esta función
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/Reversing02/p4]
└─$ nc saturn.picoctf.net 54391
Enter the address in hex to jump to, excluding '0x': 000000000040129e
You input 0x40129e
You won!
picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_14bc5444}
```

picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_14bc5444}
## Notas
- 