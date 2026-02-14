# Bases
## Descripción
What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

## Solución
### Solución 1:
- Usando CyberChef:
https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true,false)&input=YkROaGNtNWZkR2d6WDNJd2NETTE

### Solución 2:
- Usando Webshell
```
Bijou91-picoctf@webshell:~$ echo "bDNhcm5fdGgzX3IwcDM1" | base64 -d
l3arn_th3_r0p35Bijou91-picoctf@webshell:~$ 
```

picoCTF{l3arn_th3_r0p35}
## Notas
