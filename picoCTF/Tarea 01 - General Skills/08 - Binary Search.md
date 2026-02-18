# Binary Search

## Descripción
Want to play a game? As you use more of the shell, you might be interested in how they work! Binary search is a classic algorithm used to quickly find an item in a sorted list. Can you find the flag? You'll have 1000 possibilities and only 10 guesses.
Cyber security often has a huge amount of data to look through - from logs, vulnerability reports, and forensics. Practicing the fundamentals manually might help you in the future when you have to write your own tools!
## Solución
La solución es seguir el algoritmo de búsqueda binaria: Sumar extremo más extremo y dividir entre 2 para encontrar el centro del rango
### Solución:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T01_GeneralSkills1/08-BinarySearch/home]
└─$ ssh -p 54698 ctf-player@atlas.picoctf.net
The authenticity of host '[atlas.picoctf.net]:54698 ([18.217.83.136]:54698)' can't be established.
ED25519 key fingerprint is: SHA256:M8hXanE8l/Yzfs8iuxNsuFL4vCzCKEIlM/3hpO13tfQ
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[atlas.picoctf.net]:54698' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
ctf-player@atlas.picoctf.net's password: 
Welcome to the Binary Search Game!
I'm thinking of a number between 1 and 1000.
Enter your guess: 500
Lower! Try again.
Enter your guess: 250
Lower! Try again.
Enter your guess: 125
Higher! Try again.
Enter your guess: 188
Higher! Try again.
Enter your guess: 219
Higher! Try again.
Enter your guess: 235
Higher! Try again.
Enter your guess: 242
Lower! Try again.
Enter your guess: 238
Lower! Try again.
Enter your guess: 237
Congratulations! You guessed the correct number: 237
Here's your flag: picoCTF{g00d_gu355_de9570b0}
Connection to atlas.picoctf.net closed.
```

picoCTF{g00d_gu355_de9570b0}
## Notas
