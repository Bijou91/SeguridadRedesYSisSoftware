# Serpentine

## Descripción
Find the flag in the Python script!
## Solución
### Solución:
Primero ejecutamos el código para obtener pistas:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/03_GeneralSkills3/10-Serpentine]
└─$ python serpentine.py 
/media/sf_almacenamientoCompartido/03_GeneralSkills3/10-Serpentine/serpentine.py:41: SyntaxWarning: invalid escape sequence '\ '
  /     \      .- ~ ~ -.

    Y
  .-^-.
 /     \      .- ~ ~ -.
()     ()    /   _ _   `.                     _ _ _
 \_   _/    /  /     \   \                . ~  _ _  ~ .
   | |     /  /       \   \             .' .~       ~-. `.
   | |    /  /         )   )           /  /             `.`.
   \ \_ _/  /         /   /           /  /                `'
    \_ _ _.'         /   /           (  (
                    /   /             \  \
                   /   /               \  \
                  /   /                 )  )
                 (   (                 /  /
                  `.  `.             .'  /
                    `.   ~ - - - - ~   .'
                       ~ . _ _ _ _ . ~

Welcome to the serpentine encourager!


a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) b

Oops! I must have misplaced the print_flag function! Check my source code!
```

Nos pide consultar el código fuente, donde está esta línea:
```
while True:
    print('a) Print encouragement')
    print('b) Print flag')
    print('c) Quit\n')
    choice = input('What would you like to do? (a/b/c) ')
    
    if choice == 'a':
      print_encouragement()
      
    elif choice == 'b':
      print('\nOops! I must have misplaced the print_flag function! Check my source code!\n\n')
      
    elif choice == 'c':
      sys.exit(0)
      
    else:
      print('\nI did not understand "' + choice + '", input only "a", "b" or "c"\n\n')
```

Ahora vamos a modificarlo para que la opción 'b' imprima la verdadera flag, dando como resultado:
```
Welcome to the serpentine encourager!


a) Print encouragement
b) Print flag
c) Quit

What would you like to do? (a/b/c) b
picoCTF{7h3_r04d_l355_7r4v3l3d_ae0b80bd}
```

picoCTF{7h3_r04d_l355_7r4v3l3d_ae0b80bd}
## Notas
