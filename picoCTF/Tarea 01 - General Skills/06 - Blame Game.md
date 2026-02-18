# Blame Game

## Descripción
Someone's commits seems to be preventing the program from working. Who is it?
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/06-BlameGame]
└─$ cd drop-in                                                                                       
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/06-BlameGame/drop-in]
└─$ git init
Reinitialized existing Git repository in /media/sf_almacenamientoCompartido/T01_GeneralSkills1/06-BlameGame/drop-in/.git/
                                                                                  
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/06-BlameGame/drop-in]
└─$ ls      
message.py
         
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/06-BlameGame/drop-in]
└─$ git log message.py 
commit 9ae3e1bc67ad0143c611c5f65399b79850d20983
Author: picoCTF{@sk_th3_1nt3rn_b64c4705} <ops@picoctf.com>
Date:   Sat Mar 9 21:09:01 2024 +0000

    optimize file size of prod code

commit f3cec26cf7f80f91b5c3d1972f14dd4e9f97ec83
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:09:01 2024 +0000

    create top secret project
```

picoCTF{@sk_th3_1nt3rn_b64c4705}
## Notas
