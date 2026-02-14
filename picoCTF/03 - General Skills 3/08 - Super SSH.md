# Super SSH

## Descripción
Using a Secure Shell (SSH) is going to be pretty important.
Can you ssh as ctf-player to titan.picoctf.net at port 53428 to get the flag?
You'll also need the password 83dcefb7. If asked, accept the fingerprint with yes.
## Solución
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/03_GeneralSkills3/07-runme]
└─$ ssh ctf-player@titan.picoctf.net -p 54347       
The authenticity of host '[titan.picoctf.net]:54347 ([3.139.174.234]:54347)' can't be established.
ED25519 key fingerprint is: SHA256:4S9EbTSSRZm32I+cdM5TyzthpQryv5kudRP9PIKT7XQ
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[titan.picoctf.net]:54347' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
ctf-player@titan.picoctf.net's password: 
Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_8969f7d3}
Connection to titan.picoctf.net closed.
```

picoCTF{s3cur3_c0nn3ct10n_8969f7d3}
## Notas
