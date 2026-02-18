# Collaborative Development

## Descripción
My team has been working very hard on new features for our flag printing program! I wonder how they'll work together?
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ git branch -a                                                                                                      
  feature/part-1
  feature/part-2
  feature/part-3
* main
                     
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ git checkout feature/part-1
Switched to branch 'feature/part-1'
         
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ git log                    
commit f65544e4f1511fe1d1dfff03c4d65869da039b8e (HEAD -> feature/part-1)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:09:45 2024 +0000

    add part 1

commit 54c7842e34d03976ddc080a9dd76742751024358 (main)
Author: picoCTF <ops@picoctf.com>
Date:   Sat Mar 9 21:09:44 2024 +0000

    init flag printer
                                                                                
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ cat flag.py                                                                               
print("Printing the flag...")
print("picoCTF{t3@mw0rk_", end='')                                                                                    
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ git checkout feature/part-2
Switched to branch 'feature/part-2'
                 
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ cat flag.py                
print("Printing the flag...")

print("m@k3s_th3_dr3@m_", end='')                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ git checkout feature/part-3
Switched to branch 'feature/part-3'
                                                                             
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/07-CollabDev/drop-in]
└─$ cat flag.py                
print("Printing the flag...")

print("w0rk_7ffa0077}")
```

picoCTF{t3@mw0rk_m@k3s_th3_dr3@m_w0rk_7ffa0077}
## Notas
