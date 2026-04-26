# credstuff

## Descripción
We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it?
Download the leak [here](https://artifacts.picoctf.net/c/151/leak.tar).
The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.
## Solución
Lo que haremos primero es extraer el archivo tar, notando que contiene 2 archivos, usernames y passwords
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto/credstuff]
└─$ tar -xf leak.tar 
                                                                                                                                                                      
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto/credstuff]
└─$ tree            
.
├── leak
│   ├── passwords.txt
│   └── usernames.txt
└── leak.tar
```

La descripción nos pide encontrar la contraseña de cultiris, si buscamos este archivo en el archivo usernames, está en la línea 378
```
... ... ...
affectedruby
femininebouquet
cultiris
satisfieddecide
snowboardcompany
... ... ...
```

Si nos vamos a la misma línea en el archivo de contraseñas, nos encontramos un formato familiar
```
ARKadGaCZBc3ue4BfB7Vjwx83
CSYbRFVpJZNQJ4Jz3GmDsAa9Q
cvpbPGS{P7e1S_54I35_71Z3}
wTL8rTRNCkSyGP5AFsG5qK52y
9jyG4W6PnsAVuyx8MJkHKYtXV
```

Parece ser una flag encriptada, para la que usaremos este código
```python
from string import ascii_lowercase, ascii_uppercase

enc_flag = 'cvpbPGS{P7e1S_54I35_71Z3}'

for shift in range(26):
    flag = ''

    for c in enc_flag:
        if c in ascii_lowercase:
            flag += ascii_lowercase[(ascii_lowercase.index(c) + shift) % 26]
        elif c in ascii_uppercase:
            flag += ascii_uppercase[(ascii_uppercase.index(c) + shift) % 26]
        else:
            flag += c

    print(flag)
```

Y del cual obtenemos varios output, donde se encuentra nuestra flag
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto/credstuff]
└─$ python3 solve.py 
cvpbPGS{P7e1S_54I35_71Z3}
dwqcQHT{Q7f1T_54J35_71A3}
exrdRIU{R7g1U_54K35_71B3}
fyseSJV{S7h1V_54L35_71C3}
gztfTKW{T7i1W_54M35_71D3}
haugULX{U7j1X_54N35_71E3}
ibvhVMY{V7k1Y_54O35_71F3}
jcwiWNZ{W7l1Z_54P35_71G3}
kdxjXOA{X7m1A_54Q35_71H3}
leykYPB{Y7n1B_54R35_71I3}
mfzlZQC{Z7o1C_54S35_71J3}
ngamARD{A7p1D_54T35_71K3}
ohbnBSE{B7q1E_54U35_71L3}
picoCTF{C7r1F_54V35_71M3}
qjdpDUG{D7s1G_54W35_71N3}
rkeqEVH{E7t1H_54X35_71O3}
slfrFWI{F7u1I_54Y35_71P3}
tmgsGXJ{G7v1J_54Z35_71Q3}
unhtHYK{H7w1K_54A35_71R3}
voiuIZL{I7x1L_54B35_71S3}
wpjvJAM{J7y1M_54C35_71T3}
xqkwKBN{K7z1N_54D35_71U3}
yrlxLCO{L7a1O_54E35_71V3}
zsmyMDP{M7b1P_54F35_71W3}
atnzNEQ{N7c1Q_54G35_71X3}
buoaOFR{O7d1R_54H35_71Y3}
```
## Notas
