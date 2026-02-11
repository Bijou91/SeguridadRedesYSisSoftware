# strings it

## Descripción
Can you find the flag in file without running it?
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/02 - StringsIt]
└─$ strings strings
/lib64/ld-linux-x86-64.so.2
~u)f
libc.so.6
puts
stdout
__cxa_finalize
setvbuf
__libc_start_main
GLIBC_2.2.5
__gmon_start__
_ITM_deregisterTMCloneTable
_ITM_registerTMCloneTable
u+UH
[]A\A]A^A_
Maybe try the 'strings' function? Take a look at the man page
:*3$"
XMdasaWpAXqIHqvFBYTt
32VO1kKGW7st50mkv
B2WqFg3mFhCfUyvG3sNEs9Ep3FYP2gEkUePqFgUVN30MAZtV
zc2qhtc8wESHxGya1S9WpEXLgKo4D8ZrKODtQ4
YkHTxIzcJIJkLASXl1wr3EJ2IfoAKQskB7CYl54MqTnFhKd4
8s0TgxgiH9CL890ND9xWiSa2Y3iH8UeyjDfcLjougfE8
Ltd2AGC5UT2165K4WnvoNBbi0oauIrvQDTzBTWPQqp3PVlj
pp6DsuJVD5M8STb8BSUZD2WSVewAXSjZYjyumV
NJhIzdIKzLkeSDE5xAGul7rbxbsgThIyLL8sMDfFxcc
7uZYDkCYS7X7PCpioV
Z3IqcPbmAvXaUHJ0k8gdMvS7oWUds0qXme3sT
n6DXS8V5ckI69aW1HWpBQJqWtLP7
...
...
...
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/02_GeneralSkills2/02 - StringsIt]
└─$ strings strings | grep "pico"
picoCTF{5tRIng5_1T_47948C73}
```

picoCTF{5tRIng5_1T_47948C73}
## Notas
