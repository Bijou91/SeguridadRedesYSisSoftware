## Python Wrangling
# Descripción
Python scripts are invoked kind of like programs in the Terminal...
Can you run [ende.py](https://challenge-files.picoctf.net/c_wily_courier/d8ab9bfd6822fadbdfa9faffb487dab337afaf8c83d447a1b954373e15bc7d7e/ende.py) using [password.txt](https://challenge-files.picoctf.net/c_wily_courier/d8ab9bfd6822fadbdfa9faffb487dab337afaf8c83d447a1b954373e15bc7d7e/password.txt) to get [flag.txt.en](https://challenge-files.picoctf.net/c_wily_courier/d8ab9bfd6822fadbdfa9faffb487dab337afaf8c83d447a1b954373e15bc7d7e/flag.txt.en)?
# Solución
Comenzaremos con descargar los 3 archivos. Notamos que son 2 archivos **.txt** y 1 archivo **.py**. Con esto podemos asumir que los archivos txt contienen nuestra flag y llave mientras el archivo py es el script de desencriptación.

Al analizar el código de ende.py
```

import sys
import base64
from cryptography.fernet import Fernet



usage_msg = "Usage: "+ sys.argv[0] +" (-e/-d) [file]"
help_msg = usage_msg + "\n" +\
        "Examples:\n" +\
        "  To decrypt a file named 'pole.txt', do: " +\
        "'$ python "+ sys.argv[0] +" -d pole.txt'\n"



if len(sys.argv) < 2 or len(sys.argv) > 4:
    print(usage_msg)
    sys.exit(1)



if sys.argv[1] == "-e":
    if len(sys.argv) < 4:
        sim_sala_bim = input("Please enter the password:")
    else:
        sim_sala_bim = sys.argv[3]

    ssb_b64 = base64.b64encode(sim_sala_bim.encode())
    c = Fernet(ssb_b64)

    with open(sys.argv[2], "rb") as f:
        data = f.read()
        data_c = c.encrypt(data)
        sys.stdout.write(data_c.decode())


elif sys.argv[1] == "-d":
    if len(sys.argv) < 4:
        sim_sala_bim = input("Please enter the password:")
    else:
        sim_sala_bim = sys.argv[3]

    ssb_b64 = base64.b64encode(sim_sala_bim.encode())
    c = Fernet(ssb_b64)

    with open(sys.argv[2], "r") as f:
        data = f.read()
        data_c = c.decrypt(data.encode())
        sys.stdout.buffer.write(data_c)


elif sys.argv[1] == "-h" or sys.argv[1] == "--help":
    print(help_msg)
    sys.exit(1)


else:
    print("Unrecognized first argument: "+ sys.argv[1])
    print("Please use '-e', '-d', or '-h'.")
```

Podemos notar una función con el comentario **To decrypt a file named 'pole.txt'**. Sabiendo esto, renombraremos nuestro archivo flag.txt.en a pole.txt para que el código pueda reconocerlo.
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/examen1/gs/pythonwrangling]
└─$ cp flag.txt.en pole.txt && l
ende.py*  flag.txt.en*  password.txt*  pole.txt*
```

Ya lo que nos queda solo es ejecutar el código de python, pasando como contraseña el contenido de password.txt, el cual para mi caso es `720b6ad346f84cd483c60c7464dd95d4`
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/examen1/gs/pythonwrangling]
└─$ python3 ende.py -d pole.txt 
Please enter the password:720b6ad346f84cd483c60c7464dd95d4
picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
```
picoCTF{4p0110_1n_7h3_h0us3_9c5f9bcf}
# Notas adicionales
- 
# Referencias
- 