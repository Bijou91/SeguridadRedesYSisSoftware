## Specialer
# Descripción
Reception of Special has been cool to say the least. That's why we made an exclusive version of Special, called Secure Comprehensive Interface for Affecting Linux Empirically Rad, or just 'Specialer'. With Specialer, we really tried to remove the distractions from using a shell. Yes, we took out spell checker because of everybody's complaining. But we think you will be excited about our new, reduced feature set for keeping you focused on what needs it the most. Please start an instance to test your very own copy of Specialer.
`ssh -p 61980 ctf-player@saturn.picoctf.net`. The password is `af86add3`
# Solución
Este, al igual que el reto anterior, es un reto que impide usar todos los caracteres, así que usaremos un doble tab para ver qué comandos tenemos disponibles.
```
Specialer$ 
!          alias      caller     compopt    do         esac       fc         hash       kill       printf     return     suspend    true       unset      
./         bash       case       continue   done       eval       fg         help       let        pushd      select     test       type       until      
:          bg         cd         coproc     echo       exec       fi         history    local      pwd        set        then       typeset    wait       
[          bind       command    declare    elif       exit       for        if         logout     read       shift      time       ulimit     while      
[[         break      compgen    dirs       else       export     function   in         mapfile    readarray  shopt      times      umask      {          
]]         builtin    complete   disown     enable     false      getopts    jobs       popd       readonly   source     trap       unalias    } 
```

Al usar un doble tab para revisar qué carpetas hay, notamos la carpeta home:
```
Specialer$ cd ../../
bin/   home/  lib/   lib64/
```

Dentro de esta carpeta hay una más relacionada a pico, llamada `ctf-player`, y dentro de esta, se encuentran más:
```
Specialer$ cd  ../../home/ctf-player/
.hushlogin  .profile    abra/       ala/        sim/
```

Intentaremos imprimir la información de todo `ctf-player` 
```
Specialer$ cd abra
Specialer$ pwd
/home/ctf-player/abra
Specialer$ echo $(<cadabra.txt)
Nothing up my sleeve!
Specialer$ echo $(<cadaniel.txt)
Yes, I did it! I really did it! I'm a true wizard!
```

Ahora, como estamos en 'abra' y hemos probado con 'cadabra', nos pasaremos a la carpeta que vimos antes 'ala', haciendo un echo al archivo 'kazam.txt'
```
Specialer$ cd ../ala
Specialer$ echo $(<kazam.txt)
return 0 picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_a8567b6f}
```
picoCTF{y0u_d0n7_4ppr3c1473_wh47_w3r3_d01ng_h3r3_a8567b6f}
# Notas adicionales
- 
# Referencias
- 