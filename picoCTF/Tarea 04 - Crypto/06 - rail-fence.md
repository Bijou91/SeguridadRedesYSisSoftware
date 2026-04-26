# rail-fence

## Descripción
A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it?
Download the message [here](https://artifacts.picoctf.net/c/190/message.txt).
Put the decoded message in the picoCTF flag format, `picoCTF{decoded_message}`.
## Solución
Lo que vemos al aplicarle un cat al message.txt es esto:
```
┌──(kali㉿kali)-[/media/sf_almacenamientoCompartido/T04_Crypto/rail-fence]
└─$ cat message.txt 
Ta _7N6DDDhlg:W3D_H3C31N__0D3ef sHR053F38N43D0F i33___NA 
```

Ese código lo debemos pasar a un decodificador.

El resultado es este:
`The flag is: WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D00AFDD3`

Así que solo agregamos esa solución en el formato picoCTF{}
picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D00AFDD3}
## Notas
- https://www.boxentriq.com/ciphers/rail-fence-cipher